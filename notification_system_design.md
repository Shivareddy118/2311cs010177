# Stage 1

# Notification System REST API Design

## Overview

This document defines the REST API contract for a Notification System that allows users to receive, view, manage, and update notifications after logging into the application.

---

# Base URL

```
http://4.224.186.213/evaluation-service/logs
```

---

# Authentication

All endpoints require JWT authentication.

### Request Headers

```
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json
Accept: application/json
```

---

# Notification Model

```json
{
    "email": "2311cs010177@mallareddyuniversity.ac.in",
    "name": "duvuru shiva reddy",
    "mobileNo": "6304944458",
    "rollNo": "2311cs010177",
    "accessCode": "xpQddd",
}

```

---

# API Endpoints

---

## 1. Get All Notifications

### Endpoint

```
GET /notifications
```

### Headers

```
Authorization: Bearer <JWT_TOKEN>
```

### Success Response

```json
{
    "email": "2311cs010177@mallareddyuniversity.ac.in",
    "name": "duvuru shiva reddy",
    "rollNo": "2311cs010177",
    "accessCode": "xpQddd",
    "clientID": "4dc5f609-7c83-4ebe-8f1a-4c86325368c2",
    "clientSecret": "nXFfrNEcshbZEGXy"
}

```

---

## 2. Get Notification By ID

### Endpoint

```
GET /notifications/{id}
```

### Response

```json
{
  "success": true,
  "notification": {
    "id": "1",
    "title": "Welcome",
    "message": "Welcome to the Notification System",
    "type": "info",
    "priority": "low",
    "isRead": false
  }
}
```

---




---

# HTTP Status Codes

| Status Code | Description |
|-------------|-------------|
|200|Success|
|201|Created|
|400|Bad Request|
|401|Unauthorized|
|404|Not Found|
|500|Internal Server Error|

---

# Real-Time Notification Mechanism

The application uses **WebSocket (Socket.IO)** to send real-time notifications.

## Connection

```
http://4.224.186.213/evaluation-service/vehicles
```

## Events

### Client Connected

```
connect
```

### New Notification

```json
 {
            "TaskID": "e8a6375e-508e-42d0-b786-b9dbc66c8a3f",
            "Duration": 4,
            "Impact": 3
        },
        {
            "TaskID": "cd3af32d-e6e4-4ff8-a96d-89fb03c717fe",
            "Duration": 1,
            "Impact": 8
        },
        {
            "TaskID": "4b8398ee-29d9-4fa7-9651-66774fbc3776",
            "Duration": 1,
            "Impact": 6
        },
        {
            "TaskID": "33da6f0a-6d35-431a-9f9b-b4f0edf02eca",
            "Duration": 5,
            "Impact": 9
        },
        {
            "TaskID": "7e45ccc3-810b-4fd1-9897-517b5ebe8278",
            "Duration": 2,
            "Impact": 2
        },
        {
            "TaskID": "1f99fce1-2622-4d85-b3fc-61630fc905fe",
            "Duration": 8,
            "Impact": 1
        },
        {
            "TaskID": "20c3f4c3-ac38-4ad4-b443-1af3ebfac84a",
            "Duration": 8,
            "Impact": 6
        },
        {
            "TaskID": "d2e91716-906b-4622-9819-008f06013ea5",
            "Duration": 3,
            "Impact": 6
        },
        {
            "TaskID": "0182b555-8178-48a7-b944-47934f3e9119",
            "Duration": 6,
            "Impact": 8
        }


```

---

# API Summary

| Method | Endpoint | Description |
|--------|----------|-------------|
|GET|/notifications|Retrieve all notifications|
|GET|/notifications/{id}|Retrieve notification by ID|
|POST|/notifications|Create a notification|
|PUT|/notifications/{id}|Update a notification|
|PATCH|/notifications/{id}/read|Mark a notification as read|
|PATCH|/notifications/read-all|Mark all notifications as read|
|GET|/notifications/unread|Retrieve unread notifications|
|DELETE|/notifications/{id}|Delete a notification|
|DELETE|/notifications|Delete all notifications|

---

# Design Principles

- RESTful API naming conventions.
- JWT-based authentication.
- JSON request and response format.
- Consistent HTTP status codes.
- Predictable endpoint naming.
- Secure communication using HTTPS in production.
- Real-time updates using WebSocket (Socket.IO).
- Scalable and maintainable API structure.