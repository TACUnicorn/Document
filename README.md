# TACUnicorn

![Java](https://img.shields.io/badge/Java-8-green.svg) ![Maven](https://img.shields.io/badge/Maven-4.0.0-orange.svg)

TACUnicorn is a project under TAC Inc, which aims to provide a microservice system facing business based on Spring Cloud and Spring Boot.

## Requirement

- Java: 8
- Docker Engine: 17.12.0
- Docker Machine: 0.13.0
- MySQL: 14.14
- Spring Boot: 1.5.9
- Spring Cloud: Edgware
- Mybatis: 1.3.1
- Zuul: 1.2.3
- Ribbon: 2.2.4
- Eureka: 1.8.6
- RabbitMQ: 3.7.2
- Angular: 5.2.0
- Vue: 2.5.13

## Technology Stack

- Spring Boot: A framework to build a REST-based microservice, simplify the initial setup and development of Spring applications
- Spring Cloud Config: Centralized configuration server for the MSA solution
- Eureka:  Act as Service registry & discovery component
- Zuul: Edge Server, Reverse proxy server. API gateway or gate keeper for external parties
- Ribbon: Load balancer
- RabbitMQ: Messaging protocols for asynchronous communication
- Redis: Distributed caching mechanisms
- Spring Cloud OAuth2: Security mechanisms which can be integrated with microservices
- Docker: Deployment architectures for our microservices
- Angular: Front-End framework for our outside website(online store)
- Vue: Front-End framework for our inside website(background management system)

## Functionalities

### Scenario

As a integral company project, we focus on both costumer based and enterprise based aspects. Firstly, we develop an online store website to sell our product. Thus, we also provide a internal website to manage in background. By using service-oriented architecture(SOA), we develop many services inside and outside.

### Authentication Service

Contains general employee login and sign up function. Thus, only be certified, can you access ``Management Service``, ``Finance Service``, ``Warehouse`` and ``Factory``.

### Finance Service

It will call the ``Bank Adapter`` which packages some financial services, such as charge in the bank account and deposit. As a result, it will call third-party APIs from ``Bank``.

### Warehouse

We have several warehouses all over the world. So we build a commodity dispatch system as well as a commodity management system. It provides following services:

1. Query inventory in real-time
2. Call ``delivery`` APIs to transport goods
3. Call ``OEM``(Original Equipment Manufacturer) APIs to manufacture some goods
4. Call ``Factory`` APIs to manufacture some goods

### Factory

Our self-employed factory can produce some goods which we have the core technology. It will call third-party ``Components`` APIs to purchase some materials. Thus, it can also call ``Delivery`` APIs to transport goods.

#### Third Party Order Service

This is a service we exposed to third-party sellers like JD, Tmall and Amazon. It provides APIs to place a dealer order and estimate delivery time.

#### Website

We also have an official website, it has all our products and user can place a rerail order online. It will call ``Delivery`` to transport and call the ``Finance Service`` to cut payment.

#### Business Intelligence Service

This is a service which comprises the strategies and technologies used by enterprises for the data analysis of business information. Besides analyzing data on our part, it can also provide external service.

## Architecture

### Project Architecture

As you can see in [GitHub](https://github.com/TACUnicorn), 

### Logical Architecture

![logical_architecture](res/architecture.png)

### Development Architecture

![development_architecture](res/architecture2.png)

In this Business scene, we try to design a microservice architecture.

We ignore the external interface in the figure and focus on the very backend design.

Firstly, all services we implement by ourselves provide Restful APIs and are deployed individually with their own database and data cache, by Redis.

And then, all of our services are registered in the Eureka Server. It is a service discovery and register center.

When a service's instance joins or quits the service group, Eureka Server will know and manage that automatically.

A request from outside firstly arrives the Zuul API gateway. It is just like a smart router and filter. 

Then the security component will check the Authorization and decide whether to receive or redirect it to the Authorization Service.

All request will be dispatched by a load-balanced server to every different service.

For conveniently configuring, we use a Dynamic, centralized configuration management server and a distributed messaging system to publish new configuration controlled by Git or SVN.

There is also a Circuit Breaker. It supports fault tolerance with a monitoring dashboard.

## Project Detail

### OAuth SSO

OAuth 2 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, GitHub, and DigitalOcean. It works by delegating user authentication to the service that hosts the user account, and authorizing third-party applications to access the user account. OAuth 2 provides authorization flows for web and desktop applications, and mobile devices.

![sso](res/sso.png)

### Adapter



## Document

- API Document
- Code Style: [Alibaba Java Coding Guidelines](https://alibaba.github.io/Alibaba-Java-Coding-Guidelines/)

## Schedule

| Time Point   | Schedule                                 |
| ------------ | :--------------------------------------- |
| Nov 16, 2017 | Web & SOA: Proposal submission and Proposal Presentation |
| Dec 14, 2017 | Web & SOA: Middle-term progress Presentation and Demonstration |
| Jan 2, 2018  | Java EE: Presentation and Demonstration  |
| Jan 11, 2018 | Web & SOA: Final Delivery & Presentation and Demonstration |

## Demo

[YouTube](https://youtu.be/_dbgT-g96uU)

## About us

TAC Inc. is a multinational technology company that develops and sells consumer electronics via different ways such as direct retail store, online store and third-party store. We also intergrate the entire industrial chain vertically.

**Board Of Directors**(Contributers)

- 1452669 [Yang LI](https://github.com/zjzsliyang)
- 1453645 [Zhongjin LUO](https://github.com/tjluozhongjin)
- 1552730 [Xuantang CUN](https://github.com/wzes)
- 1552771 [Han LI](https://github.com/lisirrx)

## License

[MIT](https://github.com/TACUnicorn/Document/blob/master/LICENSE) License

Copyright (c) 2018 TAC Inc.