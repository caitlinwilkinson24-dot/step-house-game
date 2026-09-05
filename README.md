# Step House Game 🏠👣

A gamified fitness app that transforms your daily steps into in-game currency to customize your virtual Animal Crossing-style house.

## Features

- 📍 **GPS Tracking**: Real-time location tracking for step validation
- 👣 **Step Counter**: Integrates with device step sensors
- 🏠 **Virtual House**: Customize your house with decorations, cosmetics, and virtual pets
- 💰 **In-Game Currency**: Convert steps into coins to purchase items
- 🌤️ **Dynamic Weather**: Your in-game weather mimics your local weather
- 📱 **Cross-Platform**: iOS and Android via React Native
- 🔐 **User Accounts**: Secure authentication and data persistence

## Project Structure

```
step-house-game/
├── mobile/           # React Native Expo app
├── backend/          # Node.js/Express server
├── docs/             # Documentation
└── README.md
```

## Tech Stack

### Mobile
- **React Native** (Expo)
- **TypeScript**
- React Navigation
- Expo Location & Pedometer APIs

### Backend
- **Node.js** with Express
- **PostgreSQL** for data persistence
- **JWT** for authentication
- **OpenWeather API** for weather data

## Getting Started

### Prerequisites
- Node.js 16+
- npm or yarn
- Expo CLI (`npm install -g expo-cli`)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/caitlinwilkinson24-dot/step-house-game.git
cd step-house-game
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp backend/.env.example backend/.env
# Edit backend/.env with your configuration
```

4. Start development:
```bash
npm run dev
```

## API Documentation

See [docs/API.md](docs/API.md) for backend API endpoints.

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

MIT License - see [LICENSE](LICENSE) for details.
