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

## 3. Create Notification

### Endpoint

```
POST /notifications
```

### Request Body

```json
{
  "title": "Server Maintenance",
  "message": "Server maintenance scheduled at 11 PM.",
  "type": "warning",
  "priority": "high"
}
```

### Response

```json
{
  "success": true,
  "message": "Notification created successfully.",
  "notification": {
    "id": "3",
    "title": "Server Maintenance",
    "message": "Server maintenance scheduled at 11 PM.",
    "type": "warning",
    "priority": "high",
    "isRead": false
  }
}
```

---

## 4. Update Notification

### Endpoint

```
PUT /notifications/{id}
```

### Request Body

```json
{
  "title": "Updated Title",
  "message": "Updated notification message.",
  "priority": "medium"
}
```

### Response

```json
{
  "success": true,
  "message": "Notification updated successfully."
}
```

---

## 5. Mark Notification as Read

### Endpoint

```
PATCH /notifications/{id}/read
```

### Response

```json
{
  "success": true,
  "message": "Notification marked as read."
}
```

---

## 6. Mark All Notifications as Read

### Endpoint

```
PATCH /notifications/read-all
```

### Response

```json
{
  "success": true,
  "message": "All notifications marked as read."
}
```

---

## 7. Get Unread Notifications

### Endpoint

```
GET /notifications/unread
```

### Response

```json
{
  "success": true,
  "count": 1,
  "notifications": [
    {
      "id": "5",
      "title": "Offer",
      "message": "Special discount available.",
      "isRead": false
    }
  ]
}
```

---

## 8. Delete Notification

### Endpoint

```
DELETE /notifications/{id}
```

### Response

```json
{
  "success": true,
  "message": "Notification deleted successfully."
}
```

---

## 9. Delete All Notifications

### Endpoint

```
DELETE /notifications
```

### Response

```json
{
  "success": true,
  "message": "All notifications deleted successfully."
}
```

---

# Error Response

```json
{
  "success": false,
  "message": "Notification not found."
}
```

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
ws://localhost:3000
```

## Events

### Client Connected

```
connect
```

### New Notification

```json
{
  "event": "notification:new",
  "data": {
    "id": "10",
    "title": "New Message",
    "message": "You received a new message.",
    "type": "info",
    "priority": "medium"
  }
}
```

### Notification Read

```json
{
  "event": "notification:read",
  "data": {
    "id": "10",
    "isRead": true
  }
}
```

### Notification Deleted

```json
{
  "event": "notification:delete",
  "data": {
    "id": "10"
  }
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