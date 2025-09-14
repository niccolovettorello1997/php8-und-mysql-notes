# Chapter 28 – JavaScript

## Sections
1. Preparation  
2. Connecting JavaScript with PHP  
3. Ajax  
4. WebSockets  

---

## Summary
This chapter explains how **JavaScript** interacts with **PHP** in a web environment.  
It covers basics of integration, asynchronous communication (AJAX), and real-time features with **WebSockets**.  

---

## Key Concepts

### 1. Preparation
- JavaScript runs **in the browser** (client-side), PHP runs **on the server**.  
- Integration is achieved by exchanging data between the two, typically over HTTP.  
- Data formats: **JSON** (most common) and sometimes XML.  

---

### 2. Connecting JavaScript with PHP
- Basic approach: JavaScript sends a request, PHP processes it, and sends back a response.  
- Example (JS calling PHP endpoint):  

```javascript
fetch("server.php")
  .then(response => response.json())
  .then(data => console.log(data));
```

* Example (PHP response):

```php
<?php
header('Content-Type: application/json');
echo json_encode(["status" => "ok", "message" => "Hello from PHP"]);
```

* Connection can be done via `fetch`, `XMLHttpRequest`, or libraries like jQuery/Axios.

---

### 3. Ajax (Asynchronous JavaScript and XML)

* Allows communication with the server **without reloading the page**.
* Steps:

  1. JS sends asynchronous request.
  2. PHP processes input (e.g., query DB).
  3. Response sent back to JS and displayed dynamically.

Example with `XMLHttpRequest`:

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "data.php", true);
xhr.onload = function() {
  if (xhr.status === 200) {
    const result = JSON.parse(xhr.responseText);
    console.log(result);
  }
};
xhr.send();
```

* Ajax is foundational for **dynamic web apps**.

---

### 4. WebSockets

* Unlike HTTP (request/response), WebSockets allow **persistent, bidirectional communication** between client and server.
* Useful for **real-time apps**: chats, notifications, live dashboards.
* In PHP, WebSockets can be implemented with libraries like **Ratchet**.

Example (JavaScript client):

```javascript
const socket = new WebSocket("ws://localhost:8080");

socket.onopen = () => {
  console.log("Connected to server");
  socket.send("Hello server");
};

socket.onmessage = (event) => {
  console.log("Message from server:", event.data);
};
```

Example (PHP with Ratchet – server setup):

```php
use Ratchet\MessageComponentInterface;
use Ratchet\ConnectionInterface;

class Chat implements MessageComponentInterface {
    public function onMessage(ConnectionInterface $from, $msg) {
        $from->send("You said: " . $msg);
    }
}
```

---

## Notes

* **Fetch API** is modern and preferred over `XMLHttpRequest`.
* **Ajax** is still relevant, but often replaced with **fetch** or libraries.
* **WebSockets** provide real-time interaction but require additional infrastructure.
* For practical projects, focus on **fetch + JSON** (bread and butter), and try a **small WebSocket demo** for extra learning.