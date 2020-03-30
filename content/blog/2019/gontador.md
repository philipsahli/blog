---
title: Gontador
date: 2019-01-06T12:17:01+02:00
categories: [tutorial]
tags: [kubernetes,golang]
language: en
slug: gontador
draft: true
---
Gontador

An einem I2 Standortmeeting hat Laurent Bovet eindrücklich aufgezeigt, wie ein einfacher Service in NodeJs implementiert und für den Betrieb auf Openshift “fit” gemacht wird.

https://github.com/lbovet/contador

Contador ist ein Service, der bei jedem HTTP GET-Request in Redis einen Counter um 1 erhöht und der neue Wert in der HTTP-Response dem Client überträgt. Laurent hat verschiedene notwendige Aspekte in Commits implementiert.

* Logging mit TraceId https://github.com/lbovet/contador/commit/e7c4b282aa416ac9528ab324d810698354a9a3b1
* Applikation muss auf ein SIGHUP reagieren und ein “graceful shutdown” machen. Während einer bestimmten Zeit werden die offenen Requests noch fertig bearbeitet und beantwortet. https://github.com/lbovet/contador/commit/0aa8c7c741481d837d20e5f58bf7a96daef00138
* Behandeln von “Readiness” und “Liveness” Anfragen https://github.com/lbovet/contador/commit/5db408f07f6f36745c8586c4c61aaa4809dc8d67  Readiness dient dazu, dass Kubernetes den Pod erst mit Requests bedient, wenn er ready ist. Liveness um nicht funktionierende Pod’s nicht zu bedienen und zu ersetzen.
* Senden von Metriken an Telegraf, welcher die Daten an Grafana weiterleitet.

Contador ist mit NodeJs implementiert und verwendet das Web-Framework “Express”.

Beim Durcharbeiten einiger Abschnitte des Kurses "Go: The Complete Developer's Guide (Golang)" hatte ich den Drang zu praktischer Arbeit mit Go gespürt und bin auf die Idee gekommen, Laurent's Contador in Go zu implementieren. Daraus wurde meine persönliche Challenge:

Meine Challenge

* Bin ich nach einem Udemy-Kurs in der Lage, einen (sehr einfachen) Service in Go zu implementieren?
* Existieren Libraries für die in Contador verwendeten Funktionalitäten?
* Kann die Post-Toolchain auch für Go eingesetzt werden?

Was ist Go

Go eignet sich für:
* Microservices, z.b. aufgrund der Effizienz und des kleinen RAM-Fussabdrucks. (siehe https://medium.com/@craigchilds94/go-for-php-developer-getting-started-14e817eb82de)
* Command Line Interfaces, z.b. wegen der Portabilität (`go build` erzeugt eine ausführbare Datei pro Zielplattform). Auf der Zielplattform muss keine Laufzeitumgebung, keine Pakete oder Bibliotheken installiert werden.

Bei der Implementierung bin ich über folgende Libraries und Lösungen gestossen:

* Mux als Web-Framework
* Logging Konfiguration
* Type-safe Redis client for Golang https://github.com/go-redis/redis 
* Dependency Management mittels go-dep https://github.com/golang/dep In Go werden abhängige Pakete von ihrer Source aus einem Repository heruntergeladen (z.b. go get -u github.com/gorilla/mux). Zur Buildzeit werden alle verwendeten Pakete gebuildet und gecached. Somit können geforkte Repositories ohne grossen Zusatzaufwand verwendet werden. Wollen wir etwas am Paket gorilla/mux ändern, klont man das Repo gorilla/mux nach philipsahli/mux und macht die gewünschten Änderungen. Damit der dann auch wirklich diesen Fork verwendet, müssen wir ein Constraint in Gopkg.toml eintragen:

    [[constraint]]
       name = "github.com/gorilla/mux”
       branch = “master”
       source = "github.com/philipsahli/mux”

* Build Prozess mittels “Multi-stage builds” https://github.com/philipsahli/gontador/blob/go-implementation/Dockerfile  In einem Dockerfile werden mehrere Base-Images verwendet (Pro stage eine `FROM` Instruktion), von Stage zu einem anderen Stages können z.b. Artefakte kopiert werden. In unserem Fall wird im golang-Dockerimage das Programm gebuildet und dann in ein schlankes alpine-Image kopiert, was zu einem sehr schlanken Dockerimage führt und wir uns nicht um Aufräumarbeiten (Entfernen von Compiler, Source etc.) kümmern müssen.

https://github.com/philipsahli/gontador

Fazit

In Go zu programmieren macht Spass und scheint einfach zu sein. Vorallem der rasche Einstieg erstaunt mich und motiviert mich, den Gontador zu erweitern. 

Was kommt als nächstes:

- Gonsumidor Gonsumidor kommuniziert über gRPC mit Gontador

- Goperador Mehrere Kubernetes-integrierte Counters: Operator Pattern mit Operator SDK https://github.com/operator-framework/operator-sdk 

