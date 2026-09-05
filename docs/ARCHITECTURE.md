# Architecture Overview

## System Design

```
┌─────────────────────────────────────────────────────────────┐
│                    Mobile App (React Native)                 │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ • GPS Location Tracking                              │   │
│  │ • Step Counter (Pedometer)                           │   │
│  │ • Weather Display                                    │   │
│  │ • House Customization UI                             │   │
│  │ • Shop/Marketplace UI                                │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                            ↕
                    (HTTPS REST API)
                            ↕
┌─────────────────────────────────────────────────────────────┐
│                  Backend (Node.js/Express)                   │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ • Authentication (JWT)                               │   │
│  │ • Step Data Processing                               │   │
│  │ • Currency Conversion                                │   │
│  │ • Weather API Integration (OpenWeather)              │   │
│  │ • Shop/Inventory Management                          │   │
│  │ • User Profile Management                            │   │
│  └──────────────────────────────────────────────────────┘   │
│                            ↕                                  │
│                      (SQL Queries)                            │
│                            ↕                                  │
│  ┌──────────────────────────────────────────────────────┐   │
│  │            PostgreSQL Database                       │   │
│  │  • Users                                             │   │
│  │  • House/Inventory                                   │   │
│  │  • Items/Shop Catalog                                │   │
│  │  • Step History                                      │   │
│  │  • Transactions                                      │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                            ↕
                    (External APIs)
                            ↕
                  OpenWeather API
```

## Data Flow

### Step Tracking Flow
1. Mobile app requests step count from device's pedometer API
2. GPS validates location (to prevent cheating)
3. Step data sent to backend with timestamp and location
4. Backend stores in database and calculates currency
5. User's in-game currency updated

### Weather Integration Flow
1. Mobile app sends user's GPS coordinates to backend
2. Backend queries OpenWeather API for local weather
3. Backend returns weather data and weather state for in-game rendering
4. Mobile app applies weather effects to house rendering (rain, snow, clouds, etc.)

### Shop Transaction Flow
1. User selects item from shop
2. Mobile app sends purchase request to backend
3. Backend validates user has sufficient currency
4. Backend deducts currency and adds item to user's inventory
5. Mobile app updates house UI with new item

## Database Schema

See [docs/DATABASE.md](DATABASE.md) for detailed schema.
