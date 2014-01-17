<a name="hosted-services"></a>
## Hosted Realtime Services

<a name="hosted-client"></a>
### General Messaging & PubSub

#### [Tambur.io](https://tambur.io)

* [Docs](https://www.tambur.io/documentation)
* [Pricing](https://www.tambur.io/pricing)
* [Libraries](https://github.com/tamburio/)

> Tambur.io provides your business with a simple messaging API to build scalable realtime web and mobile apps.

* Realtime messaging
* HTTP/REST
* SSL
* Websockets
* Comet
* Streams
* Modes
* Broadcast
* Unicast
* Authcast
* Presence
* Direct Messaging
* PHP
* Ruby
* Java
* .Net
* Erlang
* JavaScript


##### Subscribe

###### JavaScript (client)

    var connection = new tambur.Connection("API_KEY", "APP_ID");
    var stream = connection.get_stream("my_stream");
    stream.onmessage = function(msg){
        // handle message
    };    
    
##### Publish

###### Python (client)

    tambur = Tambur(api_key='API_KEY', app_id='APP_ID', secret='SECRET')
    tambur.publish('my_stream', 'some message')

##### Modes

Streams can operate in one or several modes. As an example a stream can enable the 'Authentication' mode and therefore receive messages that target an authenticated receiver. Besides the 'Authentication' mode Tambur.io supports a 'Direct Messaging' mode that allows the subscribers of a stream to communicate directly among each other, as well as a 'Presence' mode that automatically publishes presence status of all the stream subscribers.

###### Authentication Mode (JavaScript)

    stream.enable_auth("AuthToken");
    stream.onauth = function(msg) {
        // handle authenticated message
    };

###### Direct Messaging Mode (JavaScript)

    stream.enable_direct("MyUserName", "DirectToken");
    stream.ondirect = function(msg) {
        var sender = msg[0];
        var content = msg[1];
        /* reply back */
        stream.direct_msg(sender, "thanks for the message!");
    };

###### Presence Mode (JavaScript)

    stream.enable_presence("MyUserName", "PresenceToken");
    stream.onpresence = function(notification) {
        var user = notification[0];
        var status = notification[1];
        if (status === "up") {
            // subscriber has joined the stream 
        } else {
            // subscriber has left the stream  
        }
    };


#### [Hydna](https://www.hydna.com/)

* [Docs](https://www.hydna.com/documentation/)
* [Pricing](https://www.hydna.com/plans-and-pricing/)

> Hydna is a hosted backend into which you can send data and have it instantly appear on other devices.

* Real-Time messaging
* Binary
* WebSockets
* Comet
* Flash
* HTTP/REST
* Behaviors
* Routing
* Authentication
* Room partitioning
* Presence
* .NET
* Erlang
* Java
* Node.js
* Objective-C
* PHP
* Python
* Ruby
* Multiplexing


##### Subscribe

###### JavaScript (client)

    var channel = new HydnaChannel('public.hydna.net/my-channel', 'r');
    
    channel.onmessage = function(event) {
      // handle update
    };
    
##### Publish

###### JavaScript (client)

    var channel = new HydnaChannel('public.hydna.net/my-channel', 'w');

    channel.onopen = function(event) {
      channel.send('Hello world');
    };


##### Authentication

Developers can deploy `Behaviors` (small snippets of code) to Hydna.
Behaviors instruct Hydna how to behave when certain actions take place
(when a channel is opened for example). This is useful when you want
to keep state, authenticate users, connect with external services etc.

The following example describes how authentication can be added to a channel.

###### Behavior (Hydna BeMachine)

    // Create rules for channel "/admin" 
    behavior('/admin', {
      open: function (event) {
        if (event.token == 'password) {
          event.allow();
        } else {
          event.deny('Incorrect password');
        }
      }
    });

###### JavaScript (client)

    var channel = new HydnaChannel('public.hydna.net/admin?password', 'w');

    channel.onopen = function (event) {
      // Granted to open channel, handle update
    };

    channel.onclose = function (event) {
      if (event.wasDenied && event.data == 'Incorrect password') {
        // Incorrect password
      }
    };

#### [PubNub](http://pubnub.com)

* [Libraries](http://www.pubnub.com/developers)
* [Pricing](http://www.pubnub.com/pricing)

> Pubnub is the fastest cloud-hosted realtime messaging system for web and mobile apps.

* BOSH
* Fallback-support
* Real-Time Client Push
* Real-Time messaging
* Real-Time data
* Coldfusion
* .NET
* Erlang
* Google App Engine (GAE)
* Java
* JavaScript
* Lua-Corona
* node.js
* Objective-C
* Perl
* PHP
* Python
* Ruby
* Silverlight
* Titaniumf
* REST API
* PubSub

##### Subscribe

###### JavaScript (client)

    var pubnub = PUBNUB.init({
      subscribe_key: 'demo'
    });
    
    pubnub.subscribe({
      channel: 'my_channel',
      message: function( msg )  {
        // handle update
      }
    });
    
##### Publish

###### JavaScript (client)

    var pubnub = PUBNUB.init({
      publish_key: 'demo'
    });

    pubnub.publish( {
      channel: 'my_channel',        
      message: 'hello!'
    } );

###### PHP

    $pubnub = new Pubnub(
      "demo",  ## PUBLISH_KEY
      "demo",  ## SUBSCRIBE_KEY
      "",      ## SECRET_KEY
      false    ## SSL_ON?
    );
    
    $info = $pubnub->publish( array(
      'channel' => 'hello_world',
      'message' => 'Hey World!'
    ) );    

#### [Pusher](http://pusher.com)

* [Docs](http://pusher.com/docs)
* [Libraries](http://pusher.com/docs/libraries)
* [Pricing](http://pusher.com/pricing)

> Pusher is a hosted API for quickly, easily and securely adding scalable realtime functionality to web and mobile apps.

* WebSockets
* HTTP fallback
* Flash socket fallback
* Real-Time Client Push
* Real-Time messaging
* Real-Time Data
* in-built security
* HTML5
* JavaScript
* Objective-C
* Ruby
* PHP
* node.js
* .NET
* Silverlight
* ActionScript
* Google App Engine (GAE)
* Erlang
* Perl
* Coldfusion
* Python
* Groovy
* Java
* REST API
* Presence
* PubSub

##### Subscribe

###### JavaScript (client)

    var pusher = new Pusher( 'APP_KEY', options );
    var channel = pusher.subscribe( 'my-channel' );
    channel.bind( 'my-event', function( eventData ) {
      // handle event
    } );

##### Publish

###### Node.js

    var pusher = new Pusher( { appId: 'APP_ID', key: 'APP_KEY', secret: 'APP_KEY' } );
    pusher.trigger( 'my-channel', 'my-event', { "some": "data" } );
    
###### PHP

    $pusher = new Pusher( 'APP_KEY', 'APP_SECRET', 'APP_ID' );
    $pusher->trigger( 'my-channel', 'my_event', array( 'some' => 'data' );

#### [Realtime.co](http://framework.realtime.co)

* [Docs](http://messaging-public.realtime.co/documentation/starting-guide/overview.html)
* [Libraries](http://framework.realtime.co/messaging/#documentation)
* [Pricing](http://framework.realtime.co/messaging/#pricing)

> The Realtime Messaging Framework is a cloud-hosted messaging system for websites and mobile apps that require constant content updates in just a few milliseconds, enabling any application to interact with millions of connected users in a fast and secure way.

* Websockets
* Fallback-support (streaming and polling)
* Real-Time Client Push
* Real-Time messaging
* Real-Time data
* Mobile Push Notifications for iOS and Android (APNS and GCM)
* .NET
* Java / Android
* JavaScript
* Lua
* iOS
* Titanium Appcelerator
* Windows Phone
* node.js
* Objective-C
* PHP
* Python
* C/C++
* Ruby
* Silverlight
* ActionScript
* REST API
* Pub/Sub
* Presence
* built-in security (authentication and authorization)
* multiplexing (through the use of channels)
* HTML5 real-time enabled templating engine (xRTML)

##### Subscribe

###### JavaScript (client)

	var RealtimeClient = RealtimeFactory.createClient();
	RealtimeClient.connect('[YOUR_APPLICATION_KEY]', '[USER_TOKEN]');
	
	RealtimeClient.onConnected = function (theClient) {               
    	theClient.subscribe('my-channel', true,
        	function (theClient, channel, msg) {
          		console.log("Received message:", msg);
        	});                                
    };    

##### Publish

###### JavaScript (client)

	var RealtimeClient = RealtimeFactory.createClient();
    RealtimeClient.connect('[YOUR_APPLICATION_KEY]', '[USER_TOKEN]');
	
	RealtimeClient.onConnected = function (theClient) {               
    	theClient.send('my-channel', 'Hello World');                                
    };
    
###### PHP

    $URL = 'http://ortc-developers.realtime.co/server/2.1';
	$AK = '[YOUR_APPLICATION_KEY]';
	$PK = '[YOUR_APPLICATION_PRIVATE_KEY]';
	$TK = '[USER_TOKEN]'; // not necessary if private key is used

	$rt = new Realtime( $URL, $AK, $PK, $TK );
	$result = $rt->send("my-channel", "Hello World", $response);

#### [WebSync on-demand (by FrozenMountain)](http://www.frozenmountain.com)

* Comet
* Real-Time Client Push
* Real-Time messaging
* Real-Time data

#### [OpenPush](http://openpush.im) - **No activity since 2011**


#### [spire.io](http://spire.io) - **Down. Status unknown**

> Build serverless applications with our secure, scalable web APIs for web and mobile development.

#### x-stream.ly - **Service defunct**

* JavaScript
* REST API
* Presence
* Real-Time Client Push

#### Kwwika - **Service defunct**

* JavaScript
* .NET
* REST API
* Real-Time Client Push
* HTTP Streaming
* Comet

<a name="hosted-data-sync"></a>
### Data Synchronisation, Persistence, Full Stack

#### [Firebase](http://firebase.com)

> A scalable real-time backend for your web app. Build apps really fast without the hassle of managing servers

* iOS
* Java / Android
* JavaScript
* WebSockets
* BaaS (Backend as a Service)

##### JavaScript (client)

    var dataRef = new Firebase( 'https://my-app.firebaseio.com/' );

    dataRef.push( { name: '@leggetter', text: 'Yo from FOWA!' } );

    dataRef.on( 'child_added', function(snapshot) {
      // Add the data
    } );

    dataRef.on( 'child_changed', function(snapshot) {
      // Update the data
    } );

    dataRef.on( 'child_removed', function(snapshot) {
      // Remove the data
    } );

#### [Google Drive Realtime API](https://developers.google.com/drive/realtime/)

> Add Realtime collaboration to your app
Give your users the power of Google Docs–style collaboration.
All JavaScript. No server. No sweat.

#### [Meteor](http://meteor.com)

> Meteor is a set of new technologies for building top-quality web apps in a fraction of the time, whether you're an expert developer or just getting started.

* Node.js
* fullstack
* HTTP Streaming
* HTTP Long-polling
* WebSockets

*Not to be confused with the original Meteor Comet server*

#### [Realtime.co Cloud Storage](http://framework.realtime.co/storage)

* [Docs](http://storage-public.realtime.co/documentation/starting-guide/1.0.0/overview.html)
* [Libraries](http://framework.realtime.co/storage/#documentation)
* [Pricing](http://framework.realtime.co/storage/#pricing)

> The Realtime.co Cloud Storage is a highly-scalable backend-as-a-service based on Amazon DynamoDB. Built-in real-time notifications keep data synchronized between users (web and mobile).

* BaaS (Backend-as-a-Service)
* Real-time data sync
* JavaScript
* iOS
* Android (Java)
* Node.js
* NoSQL
* DynamoDB
* HTTP Streaming
* HTTP Long-polling
* WebSockets
* Mobile Push Notifications for iOS and Android (APNS and GCM)

##### JavaScript (client)

	var credentials = {
        applicationKey: "[YOUR_APPLICATION_KEY]",
        authenticationToken: "[USER_TOKEN]"
    }

    var storageRef = Realtime.Storage.create(credentials);
	var tableRef = storageRef.table("chat-messages");

	var chat-msg = {
    	chatid : "My chat room",
    	timestamp : +new Date(),
    	text : "Hello World",
    	nickname : "Beavis"
    };
       
    tableRef.push(chat-msg, function() {
    	// item successfully committed to database    
    });

 	tableRef.on("put", function(item) {
        // item was added to the database table
    });

	tableRef.on("update", function(item) {
        // item was updated at the database table
    });

	tableRef.on("delete", function(item) {
        // item was removed from the database table
    });


#### [simperium](https://simperium.com/)

> Simperium is a service for developers to move data everywhere it's needed, instantly and automatically.

<a name="hosted-servers"></a>
### Messaging: with focus on delivery to servers

#### [Superfeedr](http://superfeedr.com/)
* RSS
* PubSubHubbub

#### [DataSift](http://datasift.com)

* Social Media data
* RSS
* HTTP Streaming

### Other

### [Echo](http://aboutecho.com)

<a name="self-hosted"></a>
## Self Hosted Realtime Services

### [Prosody](http://prosody.im/)

> Prosody is a modern flexible communications server for Jabber/XMPP written in Lua. It aims to be easy to set up and configure, and light on resources. For developers it aims to be easy to extend and give a flexible system on which to rapidly develop added functionality, or prototype new protocols.

* Jabber
* XMPP
* Lua
* BOSH

### [Centrifuge](https://github.com/FZambia/centrifuge)

> Simple platform for real-time message broadcasting in web applications.

* WebSockets
* SockJS
* HTTP-fallback
* Presence
* Event/Message history
* JavaScript
* PubSub

### [Spike-Engine](http://www.spike-engine.com)

> Spike-Engine allows quick and painless creation of real-time web services in .NET. Spike-Engine focuses on latency, bandwith and perfomance and has been designed and proven to be robust and reliable. The technology has been tested in production environment with thousands of simultaneous connections and used to build reliable game and application servers.

* RPC
* Automatic Client Stub Generation
* WebSockets
* Fallback Support
* Cross-Domain Support
* Comet
* Long-Polling
* PubSub
* HTTP
* .NET
* Flash
* FlashSockets
* SPML / SECP
* HTTP Tunneling
* Security
* Cross-Platform
* Monitoring


### [SignalR](https://github.com/SignalR/SignalR)

* WebSockets
* Long-polling
* ASP.NET
* IIS
* PubSub
* RMI

### [Mojolicious](http://mojolicio.us/)

> A modern Perl web framework built from the ground-up as a nonblocking web server, including built-in support for web sockets.

* Full nonblocking web server
* WebSockets
* Perl

### [Alchemy Websockets](http://alchemywebsockets.net/)

> An extremely efficient C# WebSocket server for .NET projects.

* WebSockets
* .NET
* C#

### [SockJS](https://github.com/sockjs/sockjs-client)

> SockJS is a browser JavaScript library that provides a WebSocket-like object. SockJS gives you a coherent, cross-browser, Javascript API which creates a low latency, full duplex, cross-domain communication channel between the browser and the web server.

* WebSockets
* Fallback-support
* HTTP Streaming
* HTTP Polling
* JSONP Polling
* Cross Domain support
* EventSource

### [socket.io](http://socket.io)

> Socket.IO aims to make realtime apps possible in every browser and mobile device, blurring the differences between the different transport mechanisms. It's care-free realtime 100% in JavaScript.

* WebSockets
* Fallback-support
* Flash Socket
* HTTP Long-Polling
* node.js
* Cross Domain Support

### [Firehose.io](http://firehose.io)

> Firehose is a minimally invasive way of building realtime web apps without complex protocols or rewriting your app from scratch. Its a dirt simple pub/sub server that keeps client-side Javascript models in synch with the server code via WebSockets or HTTP long polling.

* WebSockets
* HTTP Long-Polling
* Ruby

### [Thunder Push](https://github.com/thunderpush/thunderpush)

> Thunderpush is a Tornado and SockJS based push service. It provides a Beaconpush (beaconpush.com) inspired HTTP API and client.

* SockJS
* Python

### [Cramp](http://cramp.in/)

* WebSockets
* Server Sent Events
* EventSource
* Ruby
 
### [phpDaemon](http://daemon.io/)

> Asynchronous server-side framework for Web and network applications implemented in PHP using libevent. phpDaemon can handle thousands of simultaneous connections

* PHP

### [http://nugget.codeplex.com/](Nugget)

> A web socket server implemented in c#.
> 
> The goal of the projects is to create an easy way to start using HTML5 web sockets in .NET web applications.

* C#
* .NET

### [SuperWebSocket, a .NET WebSocket server](http://superwebsocket.codeplex.com/)

* WebSockets,
* .NET

### [webbit](http://webbitserver.org/)

> An event-based WebSocket and HTTP server in Java

* Java

### [Fleck](https://github.com/statianzo/Fleck)

> Fleck is a WebSocket server implementation in C#. Fleck requires no inheritance, container, or additional references.</p>

* WebSockets
* .NET

### [Persevere](http://www.persvr.org/)

* Comet
* PubSub

### [Migratory](http://migratory.ro/)

* Comet
* WebSockets

### [Meteor](http://meteorserver.org/)

* Comet
* Perl

### [Beacon Push](http://beaconpush.com)

* WebSockets
* Comet
* Fallback-support
* Real-Time Client Push
* Real-time messaging
* Real-Time Data
* Python
* Ruby
* PHP
* node.js
* REST API

### [LightStreamer](http://lightstreamer.com/)

* Comet
* WebSockets

### [Jetty](http://jetty.codehaus.org/jetty/)

* WebSockets
* HTTP Streaming

### [Ratchet](https://github.com/cboden/Ratchet)

> A PHP 5.3 (PSR-0 compliant) component library for serving/consuming sockets and building socket based applications. Build up your application (like Lego!) through simple interfaces using the decorator and command patterns. Re-use your application without changing any of its code just by wrapping it in a different protocol.

* PHP
* WebSockets

### [WebSockets and Joomla](https://github.com/eddieajau/joomla-platform-examples/tree/sockets/web/socket)

* PHP
* WebSockets
* Joomla

### [Atmosphere](https://github.com/Atmosphere/atmosphere)

* Comet
* WebSockets
* Scala
* Groovy
* Java

### [erlycomet](http://code.google.com/p/erlycomet/)

* Comet

### [cometD](http://cometdproject.dojotoolkit.org/)

* Comet

### [Pokein](http://pokein.com/)

* Comet
* ASP.NET
* Mono

### [APE Project](http://www.ape-project.org/)

* WebSockets
* Comet

### [StreamHub](http://www.stream-hub.com/)

### [Caplin System's Liberator](http://www.freeliberator.com/index.php)

* Comet
* WebSockets
* Fallback-support
* PubSub

### [ICEfaces](http://www.icefaces.org/main/home/)

### [Kaazing](http://kaazing.com/)

* WebSockets
* Fallback-support

### [FAYE](http://faye.jcoglan.com/)

* Real-Time messaging
* Bayeux
* node.js
* Ruby

### [XSockets](http://xsockets.net/)

* WebSockets
* .NET
* Fallback-support
* 
### [Tornado](http://www.tornadoweb.org/en/stable/)

> Tornado is a Python web framework and asynchronous networking library, originally developed at FriendFeed. By using non-blocking network I/O, Tornado can scale to tens of thousands of open connections, making it ideal for long polling, WebSockets, and other applications that require a long-lived connection to each user.

Represents a core building block of many other realtime web servers.

### [misultin](https://github.com/ostinelli/misultin)

* WebSockets
* Erlang

### [Cowboy](https://github.com/extend/cowboy)

* WebSockets
* Erlang

### [YAWS (Yet Another Web Server)](http://yaws.hyber.org/)

* WebSockets
* HTTP Long-Polling
* HTTP Streaming
* Erlang

### [juggernaut](https://github.com/maccman/juggernaut) *[deprecated](http://blog.alexmaccaw.com/killing-a-library)*

* WebSockets
* Comet
* Fallback-support
* node.js

### [PHP WebSocket](http://code.google.com/p/phpwebsocket/)

* PHP
* WebSockets

### [apache-websocket](https://github.com/disconnect/apache-websocket)

> WebSocket module for Apache

* PHP
* WebSockets
* Apache

### [jwebsocket](http://code.google.com/p/jwebsocket/)

* Java
* WebSockets

### [Goliath](http://goliath.io)

* Ruby
* Asynchronous
* non-blocking
* HTTP Streaming

### [ws4py](https://github.com/Lawouach/WebSocket-for-Python/tree/master/ws4py/server)

* Python
* WebSockets
* Server
* Client

### [SocketTornad.IO](https://github.com/SocketTornadIO/SocketTornad.IO)

> Implementation of the Socket.IO Websocket emulation protocol in Python on top of the non-blocking Tornado Web Framework.

* Python
* WebSockets
* Server
* Client

### [erlang_websocket](https://github.com/MiCHiLU/erlang_websocket)

* Erlang
* WebSockets
* Server

### [Slanger](https://github.com/stevegraham/slanger)

> Slanger is an open source server implementation of the Pusher protocol written in Ruby.</p>

* Ruby
* WebSockets
* Server

### [em-websocket](https://github.com/igrigorik/em-websocket)

> EventMachine based, async, Ruby WebSocket server.

* Ruby
* WebSockets
* Server

### [Java-WebSocket](http://java-websocket.org/)

> This repository contains a barebones WebSocket server and client implementation written in 100% Java. The underlying classes are implemented using the Java ServerSocketChannel and SocketChannel classes, which allows for a non-blocking event-driven model (similar to the WebSocket API for web browsers).

* Java
* WebSockets
* Server
* Client

### [Autobahn WebSocket](http://autobahn.ws/)

> Autobahn provides Open-Source client and server implementations of WebSocket and WAMP.

* WebSockets
* Java
* Android

### [libwebsockets](http://git.warmcat.com/cgi-bin/cgit/libwebsockets/)

> C Websockets Server Library

* C
* WebSockets
* Server

### [ArduinoWebsocketServer](https://github.com/ejeklint/ArduinoWebsocketServer)

> This library implements a Websocket server running on an Arduino

* WebSockets
* Server
* Arduino

### [nowjs](https://github.com/Flotype/now)

* node.js

*Doesn't appear to be actively maintained any more and the website is down.*

<a name="websocket-client-libraries"></a>
## WebSocket Client Libraries

### JavaScript - Flash Socket Fallback</dt>

* [web-socket-js](https://github.com/gimite/web-socket-js)

### ActionScript

* [AS3 WebSocket](https://github.com/Worlize/AS3WebSocket)

### .NET
* [Microsoft .NET 4.5 namespace and classes](http://msdn.microsoft.com/en-us/library/hh159285.aspx)
* [Anaida - WebSocket Client/Adapter](http://anaida.codeplex.com/)
* [Microsoft Windows Store app MessageWebSocket class](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.sockets.messagewebsocket.aspx)
* [WebSocket Sharp](https://github.com/sta/websocket-sharp)
* [WebSocket4Net](http://websocket4net.codeplex.com/) - originated from the SuperWebSocket codebase

### Silverlight
[Silverlight WebSocket client](http://html5labs.interoperabilitybridges.com/prototypes/websockets/websockets/info) - prototype

### Java

* [Java WebSocket Client](http://code.google.com/p/weberknecht/)
* [UnittWebSocket](http://code.google.com/p/unitt/wiki/UnittWebSocket)
* [Java-WebSocket](http://java-websocket.org/)

### C++
* [Arduino C++ WebSocket client](https://github.com/krohling/ArduinoWebsocketClient)

### Ruby
* [web-socket-ruby"](https://github.com/gimite/web-socket-ruby)
* [em-websocket-client](https://github.com/mwylde/em-websocket-client)

### Python

* [ws4py](https://github.com/Lawouach/WebSocket-for-Python/tree/master/ws4py/client)
* [websocket-client](http://pypi.python.org/pypi/websocket-client/)

### Objective-C

* [ZTWebSocket](https://github.com/esad/zimt/blob/master/src/ZTWebSocket.m)
* [SocketRocket](https://github.com/square/SocketRocket) - Objective-C WebSocket Client (beta)
