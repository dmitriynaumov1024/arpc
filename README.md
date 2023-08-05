# arpc

Advanced Remote Procedure Call 

(C) 2023 Dmitriy Naumov


## Master's qualifying paper

Implementation of a remote procedure call protocol (51)

Реалізація протоколу віддаленого виклику процедур (50)


## Motivation

Nowadays there is a lot of distributed applications and websites which rely 
on protocols of network communication such as HTTP(S) and TCP. There are 
numerous ways to implement communication of website backend and frontend. 
It can be: 1) a simple server-side rendered application with no requests
between page reloads; 2) a thick client (built with or without any frontend 
framework) communicating with REST API server; 3) a thick client communicating 
with server via WebSocket or any other two-way communication. 

So, the motivation to define and implement own remote procedure call protocol
is: 1) to create a flexible, protocol-format-agnostic communication protocol 
(though JSON over HTTP is prioritized); 2) to get rid of deprecated, scuffy HTTP
and its methods and statuses; 3) to provide a bridge between client and server;
4) to create a server-driven communication protocol; 5) to make communication 
more safe by using various programming language constructs.


## Analogs

1) SAFE stack
2) gRPC
3) SignalR
4) Runtime.Remoting (.NET Framework only)


## Description of the ARPC protocol 

Considerations: 
1) There is a fixed public URL of ARPC action set definition. 
2) JSON serialization and HTTP transport are used under the hood.

Sequence: 
1) Client performs a GET ${definitionURL}, server always responds with 
HTTP 200 OK and JSON body if action set definition exists there, otherwise 
HTTP 404 Not Found.
2) Client code calls some method of ARPC adapter, adapter performs 
a POST ${endpointURL} request. 


## Implementation proposal

For a proper implementation, there should be a server adapter and a client adapter.

Implementation proposals:
1) .NET / ASP.NET Core 6+ server adapter plugin
2) Node.js / Express.js server adapter plugin
3) .NET client adapter
4) Javascript client adapter

Serialization proposals:
1) JSON (plain, old)
2) Array Buffers

Transport proposals:
1) HTTP (almost-sync calls)
2) WebSocket (async calls)
3) Socket.io (js-only async calls)

