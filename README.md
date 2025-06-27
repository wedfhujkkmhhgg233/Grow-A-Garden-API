# 🌱 Grow A GARDEN API

This is the README file for the **Grow A GARDEN API**, designed to help you integrate live plant stock data and events via HTTP REST or WebSocket.

---

## Table of Contents

- [Overview](#overview)  
- [Base URLs](#base-urls)  
- [Endpoints](#endpoints)  
  - [GET /stock](#get-stock)  
  - [WebSocket Stream](#websocket-stream)  
- [Authentication](#authentication)  
- [Usage Examples](#usage-examples)  
  - [HTTP Example (cURL)](#http-example-curl)  
  - [JavaScript (Fetch)](#javascript-fetch)  
  - [WebSocket Example (Node.js)](#websocket-example-nodejs)  
- [Error Handling](#error-handling)  
- [Rate Limiting & Best Practices](#rate-limiting--best-practices)  
- [Contributing](#contributing)  
- [License](#license)

---

## Overview

Grow A GARDEN API provides real-time data about garden stocks (e.g., seeds, plants, supplies).  
You can:

- Retrieve current stock levels via REST  
- Listen for live updates via WebSocket  

---

## Base URLs

- **HTTP REST**: `https://gagapi-production.up.railway.app/stock`  
- **WebSocket**: `wss://gagapi-production.up.railway.app/`  

---

## Endpoints

### GET /stock

Fetch the latest inventory.

**Request:**  
```http
GET /stock
Host: gagapi-production.up.railway.app

Response (JSON):

[
  {
    "itemId": "seed-001",
    "name": "Tomato Seeds",
    "quantity": 150,
    "unit": "packets",
    "updatedAt": "2025-06-27T12:34:56Z"
  }
]


---

WebSocket Stream

Connect for real-time stock updates.

URL:

wss://gagapi-production.up.railway.app/

Message Format (Server → Client):

{
  "event": "stockUpdate",
  "data": {
    "itemId": "plant-023",
    "name": "Rose Bush",
    "quantity": 42,
    "unit": "pots",
    "updatedAt": "2025-06-27T12:35:10Z"
  }
}


---

Authentication

🔐 Currently, no authentication is required.
(If auth is added later, this section will be updated.)


---

Usage Examples

HTTP Example (cURL)

curl https://gagapi-production.up.railway.app/stock

JavaScript (Fetch)

fetch('https://gagapi-production.up.railway.app/stock')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))

WebSocket Example (Node.js)

const WebSocket = require('ws')
const ws = new WebSocket('wss://gagapi-production.up.railway.app/')

ws.on('open', () => console.log('Connected to Grow A GARDEN stream'))
ws.on('message', msg => {
  const { event, data } = JSON.parse(msg)
  if (event === 'stockUpdate') {
    console.log('Update:', data)
  }
})
ws.on('error', console.error)
ws.on('close', () => console.log('Connection closed'))


---

Error Handling

REST: Uses standard HTTP status codes (4xx for client errors, 5xx for server errors).

WebSocket: Errors are sent as:

{
  "event": "error",
  "message": "Description of the error"
}



---

Rate Limiting & Best Practices

Prefer WebSocket over frequent REST polling for real-time applications.

Implement reconnect logic for WebSocket to ensure reliability.

Respect any rate limits communicated by the service.



---

Contributing

Found a bug or want a feature?
Feel free to open an issue or PR.
Please follow the style guidelines in CONTRIBUTING.md.


---

License

This project is licensed under the MIT License – see LICENSE for details.


---

Happy planting! 🌼



