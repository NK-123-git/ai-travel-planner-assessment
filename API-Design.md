# API Design

## Overview

The backend exposes REST APIs for authentication, trip management, itinerary generation, and trip updates.

Base URL:

```
/api
```

---

# Authentication APIs

## Register User

### Endpoint

```http
POST /api/auth/register
```

### Request

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

### Response

```json
{
  "message": "User registered successfully"
}
```

---

## Login User

### Endpoint

```http
POST /api/auth/login
```

### Request

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

### Response

```json
{
  "token": "jwt_token"
}
```

---

# Trip APIs

## Create Trip

### Endpoint

```http
POST /api/trips
```

### Request

```json
{
  "destination": "Tokyo",
  "durationDays": 5,
  "budgetTier": "Medium",
  "interests": ["Food", "Culture"]
}
```

### Response

```json
{
  "message": "Trip created successfully"
}
```

---

## Get User Trips

### Endpoint

```http
GET /api/trips
```

### Response

```json
[
  {
    "_id": "tripId",
    "destination": "Tokyo"
  }
]
```

---

## Get Single Trip

### Endpoint

```http
GET /api/trips/:id
```

---

## Update Trip

### Endpoint

```http
PUT /api/trips/:id
```

---

## Delete Trip

### Endpoint

```http
DELETE /api/trips/:id
```

---

# AI APIs

## Generate Itinerary

### Endpoint

```http
POST /api/trips/generate
```

### Purpose

Generates:

- Day-by-day itinerary
- Budget estimation
- Hotel recommendations

### Response Example

```json
{
  "itinerary": [
    {
      "day": 1,
      "activities": [
        "Visit Senso-ji Temple",
        "Explore Asakusa"
      ]
    }
  ],
  "budget": {
    "total": 950
  }
}
```

---

## Regenerate Day

### Endpoint

```http
POST /api/trips/:id/regenerate-day
```

### Example Request

```json
{
  "day": 3,
  "instruction": "More outdoor activities"
}
```

---

# Security

Protected routes require:

```http
Authorization: Bearer <jwt_token>
```

JWT middleware validates access before processing requests.

---

# Error Handling

Example:

```json
{
  "success": false,
  "message": "Unauthorized access"
}
```

---

# Future Enhancements

- Flight APIs
- Hotel APIs
- Google Maps Integration
- Multi-user trip collaboration