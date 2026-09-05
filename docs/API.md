# API Documentation

## Base URL
```
http://localhost:3000/api
```

## Authentication
All endpoints (except auth) require JWT token in Authorization header:
```
Authorization: Bearer <token>
```

## Endpoints

### Authentication

#### POST /auth/register
Create a new user account.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "username": "playerName"
}
```

**Response:**
```json
{
  "token": "eyJhbGc...",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "username": "playerName",
    "currency": 0
  }
}
```

#### POST /auth/login
Login to existing account.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "token": "eyJhbGc...",
  "user": { ... }
}
```

### Steps

#### POST /steps/log
Log step data from device.

**Request:**
```json
{
  "steps": 150,
  "latitude": 37.7749,
  "longitude": -122.4194,
  "timestamp": "2024-01-15T10:30:00Z"
}
```

**Response:**
```json
{
  "currencyEarned": 15,
  "totalCurrency": 245,
  "message": "150 steps logged successfully!"
}
```

#### GET /steps/daily
Get today's step count.

**Response:**
```json
{
  "date": "2024-01-15",
  "steps": 5230,
  "currency": 523
}
```

### Weather

#### GET /weather?latitude=37.7749&longitude=-122.4194
Get current weather for given coordinates.

**Response:**
```json
{
  "condition": "rain",
  "temperature": 62,
  "humidity": 80,
  "windSpeed": 12,
  "description": "Light rain",
  "icon": "10d"
}
```

### Shop

#### GET /shop/items
Get all available shop items.

**Response:**
```json
{
  "items": [
    {
      "id": "item-001",
      "name": "Wooden Chair",
      "category": "decoration",
      "price": 50,
      "description": "A cozy wooden chair",
      "image": "https://..."
    },
    {
      "id": "pet-001",
      "name": "Cat",
      "category": "pet",
      "price": 200,
      "description": "Adorable virtual cat",
      "image": "https://..."
    }
  ]
}
```

#### POST /shop/purchase
Purchase an item from the shop.

**Request:**
```json
{
  "itemId": "item-001"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Purchase successful!",
  "remainingCurrency": 195,
  "item": { ... }
}
```

### House/Inventory

#### GET /house
Get user's house and all items in it.

**Response:**
```json
{
  "house": {
    "id": "house-uuid",
    "userId": "user-uuid",
    "weatherCondition": "rain",
    "items": [
      {
        "id": "inv-001",
        "itemId": "item-001",
        "name": "Wooden Chair",
        "position": { "x": 100, "y": 200 },
        "rotation": 0
      }
    ]
  }
}
```

#### POST /house/item/place
Place an item in the house.

**Request:**
```json
{
  "itemId": "item-001",
  "position": { "x": 150, "y": 250 },
  "rotation": 45
}
```

**Response:**
```json
{
  "success": true,
  "item": { ... }
}
```

#### POST /house/item/move
Move an item's position in the house.

**Request:**
```json
{
  "inventoryId": "inv-001",
  "position": { "x": 200, "y": 300 },
  "rotation": 90
}
```

**Response:**
```json
{
  "success": true,
  "item": { ... }
}
```

## Error Responses

### 400 Bad Request
```json
{
  "error": "Invalid request parameters",
  "details": "latitude must be between -90 and 90"
}
```

### 401 Unauthorized
```json
{
  "error": "Unauthorized",
  "message": "Invalid or missing authentication token"
}
```

### 404 Not Found
```json
{
  "error": "Resource not found",
  "message": "Item with id 'invalid-id' not found"
}
```

### 500 Internal Server Error
```json
{
  "error": "Internal server error",
  "message": "An unexpected error occurred"
}
```
