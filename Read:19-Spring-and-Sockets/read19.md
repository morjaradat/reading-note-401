# WebSocket

- its guild about how to build interactive web applications that send and receive messages between client and the server.
- we use WebSocket  to build interactive web application .
- we will  use STOMP messaging with Spring to create an interactive web application .
- STOMP is a subprotocol operating on top of the lower-level WebSocket.

- we will use STOMP dependencies

```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-websocket'
}
```

- also we need :

```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-websocket'
	implementation 'org.webjars:webjars-locator-core'
	implementation 'org.webjars:sockjs-client:1.0.2'
	implementation 'org.webjars:stomp-websocket:2.3.3'
	implementation 'org.webjars:bootstrap:3.3.7'
	implementation 'org.webjars:jquery:3.1.1-1'
}
```

**I will use react not jQuery then without last dependency**

- STOMP message service : the service will receive messages contain a name in STOMP message whose body is a JSON object .

- we need a model and Message-handling Controller to handle the requests(message).

- we will use @MessageMapping("/hello") -- /hello is the massage that will be handled by STOMP.

- Then @SendTo("/topic/greetings") ; The return value is broadcast to all subscribers -- /topic/greetings
- then we pass the message to our method and use our logic.

## Configure Spring for STOMP messaging

- first create new class with notations @Configuration and @EnableWebSocketMessageBroker then we will implements the class to  WebSocketMessageBrokerConfigurer and implement there methods.

- @EnableWebSocketMessageBroker enables WebSocket message handling, backed by a message broker.

- then it take about create the html and added in the head thees script :

```
 <script src="/webjars/jquery/jquery.min.js"></script>
    <script src="/webjars/sockjs-client/sockjs.min.js"></script>
    <script src="/webjars/stomp-websocket/stomp.min.js"></script>
     <script src="/app.js"></script>
```

- the app.js will have the login that will handle the send request.
- The connect() function uses SockJS and stomp.js to open a connection to /gs-guide-websocket, which is where our SockJS server waits for connections.
- The sendName() function retrieves the name entered by the user and uses the STOMP client to send it to the /app/hello destination.

## Execut the Application

- need to change the main method with :

```
public static void main(String[] args) {
    SpringApplication.run(MessagingStompWebsocketApplication.class, args);
  }
```

