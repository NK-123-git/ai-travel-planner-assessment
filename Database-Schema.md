# Database Schema

## Overview

The application uses MongoDB Atlas as the primary database.

Two main collections are used:

1. Users
2. Trips

---

# User Collection

```json
{
  "_id": "ObjectId",
  "email": "user@example.com",
  "password": "hashedPassword",
  "createdAt": "Date",
  "updatedAt": "Date"
}
```

## Purpose

Stores authentication information and user account details.

---

# Trip Collection

```json
{
  "_id": "ObjectId",
  "userId": "ObjectId",

  "destination": "Tokyo",

  "durationDays": 5,

  "budgetTier": "Medium",

  "interests": [
    "Food",
    "Culture"
  ],

  "itinerary": [
    {
      "day": 1,
      "activities": [
        "Visit Senso-ji Temple",
        "Explore Asakusa Street Food"
      ]
    }
  ],

  "estimatedBudget": {
    "flights": 400,
    "accommodation": 300,
    "food": 150,
    "activities": 100,
    "total": 950
  },

  "hotels": [
    {
      "name": "Hotel Sakura Tokyo",
      "tier": "Budget"
    }
  ],

  "packingList": [
    "Passport",
    "Winter Jacket",
    "Power Adapter"
  ],

  "createdAt": "Date",
  "updatedAt": "Date"
}
```

---

# Relationships

User (1) ------> (Many) Trips

One user can create multiple trips.

Each trip belongs to exactly one user.

---

# Data Isolation Strategy

Every trip document contains a userId.

Example Query:

```javascript
Trip.find({
  userId: req.user.id
});
```

This ensures users can only access their own trips.

---

# Future Database Enhancements

Additional collections could include:

- Hotels
- Saved Destinations
- Reviews
- Shared Trips
- Flight Information