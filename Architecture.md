# System Architecture

## Overview

The AI Travel Planner is a full-stack web application that generates personalized travel itineraries using an AI model.

The system follows a client-server architecture.

## High-Level Architecture

```text
+-------------------+
|   Next.js Frontend |
+---------+---------+
          |
          | HTTPS Requests
          v
+-------------------+
| Express Backend   |
+---------+---------+
          |
          |
          +----------------+
          |                |
          v                v
+----------------+   +----------------+
| MongoDB Atlas  |   | Gemini API     |
+----------------+   +----------------+
```

## Application Flow

1. User registers or logs in.
2. JWT token is generated.
3. User submits trip preferences.
4. Backend validates the request.
5. Backend sends a prompt to Gemini.
6. Gemini generates:
   - Day-by-day itinerary
   - Budget estimation
   - Hotel recommendations
7. Data is stored in MongoDB.
8. User can modify or regenerate itinerary sections.

## Authentication Flow

1. User logs in.
2. Password is verified using bcrypt.
3. JWT token is issued.
4. Token is attached to protected requests.
5. Middleware validates token before access.

## Data Isolation

Every trip document contains a userId.

Example:

Trip → userId → User

Users can only access trips that belong to their own account.

## Scalability Considerations

- REST API architecture
- Modular route structure
- Reusable frontend components
- Database indexing
- Stateless authentication using JWT