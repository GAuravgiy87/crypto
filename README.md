
# CryptoTracker - Cryptocurrency Dashboard with Regular Updates

A responsive React application that displays cryptocurrency data with regular price updates every 2-3 seconds, filtering, and sorting capabilities.

![CryptoTracker Dashboard]
![Screenshot 2025-04-24 071509](https://github.com/user-attachments/assets/8dd8e84d-3a92-40a2-9dac-ef9cd7c99ff1)


## How It Works - Visualization

The application fetches real cryptocurrency market data from CoinGecko API and then simulates price movements every 1-2 seconds:



## Features

- **Regular Price Updates**: Cryptocurrency price updates every 2-3 seconds through WebSocket
- **Real Market Data**: Initial data fetched from CoinGecko API with simulated price movements
- **Interactive UI**: Sort by market cap, price, or 24h change
- **Filtering**: Filter by all, favorites, gainers, or losers
- **Search Functionality**: Search for specific cryptocurrencies by name or symbol
- **Responsive Design**: Works on mobile, tablet, and desktop
- **Dark/Light Theme**: Toggle between dark and light modes
- **Favorites**: Save your favorite cryptocurrencies for quick access

## Tech Stack

- **Frontend**:
  - React 18
  - TypeScript
  - Redux Toolkit for state management
  - Tailwind CSS with shadcn/ui components
  - WebSockets for real-time updates

- **Backend**:
  - Express server
  - WebSocket server for real-time data streaming
  - CoinGecko API integration for market data

## Redux Toolkit Implementation

The application uses Redux Toolkit for efficient state management:

```typescript
// Store setup (app/store.ts)
import { configureStore } from '@reduxjs/toolkit';
import cryptoReducer from '@/features/crypto/cryptoSlice';

export const store = configureStore({
  reducer: {
    crypto: cryptoReducer,
  },
});

// Cryptocurrency slice (features/crypto/cryptoSlice.ts)
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

// Async thunk for fetching cryptocurrency data
export const fetchCryptoData = createAsyncThunk(
  'crypto/fetchCryptoData',
  async () => {
    const response = await fetch('/api/crypto');
    return await response.json();
  }
);

export const cryptoSlice = createSlice({
  name: 'crypto',
  initialState,
  reducers: {
    updateCryptoPrice: (state, action) => {
      // Handle real-time price updates
    },
    toggleFavorite: (state, action) => {
      // Toggle favorite status
    },
    // More actions...
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchCryptoData.fulfilled, (state, action) => {
        // Handle successful data fetch
      });
      // More cases...
  }
});
```

## Architecture

```
┌─────────────────┐       ┌───────────────────┐       ┌─────────────────┐
│                 │       │                   │       │                 │
│  React Frontend │◄─────►│  Express Backend  │◄─────►│  CoinGecko API  │
│                 │  WebSocket              REST      │                 │
└─────────────────┘       └───────────────────┘       └─────────────────┘
```

- **Data Flow**:
  1. Initial cryptocurrency data is fetched from CoinGecko API via our backend REST endpoint
  2. Real-time price updates are pushed to the frontend via WebSocket connection
  3. User interactions (filtering, sorting, favorites) are handled locally in Redux

## Setup Instructions

### Prerequisites

- Node.js (v16+)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/crypto-tracker.git
   cd crypto-tracker
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to [http://localhost:5000](http://localhost:5000)

### Building for Production

1. Build the application:
   ```bash
   npm run build
   ```

2. Start the production server:
   ```bash
   npm start
   ```

## How It Works

- **Regular Price Updates**: The application establishes a WebSocket connection to our server, which simulates cryptocurrency price updates every 2-3 seconds.
- **Data Source**: We fetch initial cryptocurrency data from the CoinGecko API to ensure accurate starting points, then apply small simulated price movements.
- **State Management**: Redux Toolkit manages the global state, with dedicated actions for price updates, filtering, and favoriting.
- **UI Components**: The interface is built with shadcn/ui components and styled with Tailwind CSS for a responsive and modern design.
- **Visual Feedback**: Price changes are highlighted with animations (green for increases, red for decreases) to provide visual feedback to users.

## Project Structure

```
/
├── client/                  # Frontend React application
│   ├── src/
│   │   ├── app/             # Redux store setup
│   │   ├── components/      # React components
│   │   ├── features/        # Redux slices
│   │   ├── hooks/           # Custom React hooks
│   │   ├── services/        # API and WebSocket services
│   │   ├── types/           # TypeScript type definitions
│   │   └── utils/           # Utility functions
├── server/                  # Express backend
│   ├── routes.ts            # API routes and WebSocket setup
│   └── index.ts             # Express server initialization
└── shared/                  # Shared code between frontend and backend
    └── schema.ts            # Database schema definitions
```

