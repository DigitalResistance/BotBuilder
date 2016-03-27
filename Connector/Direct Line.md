---
layout: page
title:  Direct Line
permalink: /connector/direct-line/
weight: 212
parent1: Bot Connector
parent2: Channels
---


The Direct Line API is a simple REST API for connecting directly to a single bot. This API is intended for developers
writing their own client applications, web chat controls, or mobile apps that will talk to their bot.

Credentials for the Direct Line API may be obtained from the Bot Framework developer portal, and will only allow the
caller to connect to the bot they were generated for. The you are writing a server-to-server application,
the Direct Line secret may be used directly against the API. If instead you are writing an application where a client
connects directly (and possibly insecurely) to the Direct Line API, you may exchange the secret for a token that will
work only for a single conversation and only for a limited amount of time. Tokens expire by default after 30 minutes
although they may be renewed up until their expiration.

The secret or token (depending on the authorization model) are supplied as basic auth with the "BotConnector" scheme
and no further encoding.

Each conversation on the Direct Line channel must be explicitly started using a POST to the /api/conversations endpoint.
If the call was authorized with a token, the conversation ID is the conversation ID in the scoped token. If a
secret was used to start the conversation, the conversation will be started with a new, random ID.

The client may send messages to the bot by calling POST on /api/messages/conversationId.

The client may retrieve messages sent by the bot by calling GET on /api/messages/conversationId. The JSON structure
returned contains a watermark that can be sent on subsequent requests to skip old messages.

The Direct Line API does not store messages indefinitely. Your client application must pick them up quickly before
they are deleted.

See the Direct Line REST API reference [here](/sdkreference/restapi-directline/)