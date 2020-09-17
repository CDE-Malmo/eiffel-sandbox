# eiffel-sandbox

Eiffel msg generation
- https://github.com/Praqma/tracey-protocol-eiffel-cli-generator
- https://github.com/jenkinsci/eiffel-broadcaster-plugin

RabbitMQ
- https://hub.docker.com/_/rabbitmq

JCasC
- https://github.com/Praqma/jcasc-conf

Postgres
- https://hub.docker.com/_/postgres

## Goals

1. Generate Eiffel event using Jenkins (Git commit Event)
2. Send generated Eiffel message with command line tool to Rabbit MQ

## Eiffel Jenkins plugin notes

to enable webview
- rabbitmq-plugins enable rabbitmq_management

In Jenkins config:
- mq uri: amqp://rabbitmq:5672
- exchange: jenkins
- Virtual host: /
- Routing Key: jenkins

In rabbitmq management:
- created exchange: jenkins
- created queue: classic jenkins
- binding: jenkins 2 jenkins


## CDE - Gathering 17.09.2020 - Eiffel


## Why do we want to do Eiffel?

### What is Eiffel?
Eiffel is a message protocol, a way to trace something going through the system via event triggered messaged

Eiffel itself is not enough to provide meaningful functionality, there are additional tools around it

What do we need to make it work?

Sender > Message bus > receiver & DB to store the events


Praqma authored Jenkins plugin: https://github.com/Praqma/tracey-jenkins-trigger-plugin
There are other plugins already available: https://github.com/jenkinsci/eiffel-broadcaster-plugin

The goal of the session:
Learn more and figure out if we can actually come up with a project idea where Eiffel could be used

A comparison with ComplianceDB would be interesting too, in the future

So what are we gonna do today?
Let’s try to set up a simple example, use RabbitMQ and send some some example messages,
e.g. git commit triggers sending event to CI system (to be decided) and when an artifact is created another message is sent
whole setup dockerized, if possible and all the code and docs kept in repo: https://github.com/CDE-Malmo/eiffel-sandbox


How did it go?
In the end jenkins instance with eiffel-broadcaster plugin was created and rabbitMQ was listening for messages from it
it did work

it is a broad subject though, and the lack of familiarity with e.g. rabbitMQ made it bigger challenge that it would be if we had some experience with it

What would we like to do in the future?
generic producer (to be able to send eiffel messages from anything)
generic consumer (to be able to receive any - or a subset of - message)

![whiteboard notes](notes.png)

# What now?

1. We control the RabbitMQ setup. Design proposal for a queue/echange structure with persistant DB consumer included.
1. Extend existing plugin? Try to write a simple consumer with configurable Eiffel event message requirements.
1. Ask a member of the Eiffel technical commitee on how RabbitMQ works
1. Figure out proper use-cases for Eiffel, are we covering some real world use cases with Jenkins plugin?
1. Start to create a toolbox (or gather tools for the toolbox), to make it easier to use.
