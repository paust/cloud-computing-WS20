# KV: Special Topics - Cloud Computing from an Engineering Perspective

Repository for the lecture **921CSPTST1K13**

## Team members:

| Name                | Matrikulation Number |
| ------------------- | :------------------- |
| Radic  Nikola       | k01555465            |
| Ratzenböck  Michael | k01606472            |

## Introduction

The entire proposal can be found in [proposal.md](proposal.md). 

The main idea of this project is to split up an already existing monolith into microservices. The monolith consists, provides,roughly speaking three services:

1) A frontend application which is written in Angular.
2) A traffic service, that scrapes traffic data from [ö3](oe3.orf.at) and provides it via an REST API to the frontend
3) A weather service, that gets weather data from [openweathermap](www.openweathermap.org) and also provides it via an REST API to the frontend.

These services should then be split up into _microservices_ and those microservices should be running inside Docker-containers. Moreover, both backend microservices should be managed by Kubernetes.

By splitting the monolith up into microservices it is also easier to set up continuous integration and deployment. For this Github-Actions and Dockerhub should be used.

## The Monolith

The original architecture of the monolith looks something like this:
![Monolith - Architecture](./documentation/figs/monolith-architecture.svg)
This depicts the the functionality of the application a bit better. 

Currently, everything gets compiled into a single jar which gets deployed on a local Tomcat Webserver (This is Spring-stuff). The architecture is roughly split into the frontend (Angular) and backend (Java - SpringBoot).

The frontend currently contains two components. First, there is the _Traffic Component_ which is responsible for displaying the traffic information and second, the _Weather Component_ which is responsible for displaying the weather information. Each of the components uses an _Angular Service_ which is used to request the data from the backend. This means, that the frontend makes _localhost_ HTTP calls. 

The backend is a Spring Boot application that currently consists of two _Spring RestControllers_. First, there is the _TrafficController_ which listens for incoming HTTP GET requests on _/traffic_. Second, there is the _WeatherController_ which listens for incoming HTTP GET requests on _/weather_ and _/weatherForecast_. Both of these Controllers use a _Spring Service_ which actually gets the data. This means for example the _TrafficService_ queries data via HTTP from [oe3.orf.at](oe3.orf.at).

## Microservices to the rescue

## Introducing Kubernetes with Minikube 