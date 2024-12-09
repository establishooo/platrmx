# Database and API Documentation

## API Keys and Services

### Polygon.io API
- **API Key**: `baaf81ba-1174-42dc-b155-74b96c5de680`
- **Base URL**: `https://api.polygon.io/v2`
- **Endpoints**:
  - `/snapshot/locale/us/markets/stocks/tickers` (Real-time quotes)
  - `/aggs/ticker/{symbol}/range/1/minute/today` (Intraday data)
  - `/reference/tickers` (Stock symbols)

## Data Structure

### User
```typescript
interface User {
  id: string;
  fullName: string;
  email: string;
  passwordHash: string;
  balance: number;
  portfolioValue: number;
  trades: Trade[];
  status: 'ACTIVE' | 'SUSPENDED' | 'INACTIVE';
  createdAt: Date;
  lastLogin: Date;
}
```

### Trade
```typescript
interface Trade {
  id: string;
  userId: string;
  symbol: string;
  type: 'BUY' | 'SELL';
  quantity: number;
  price: number;
  orderType: 'MARKET' | 'LIMIT' | 'STOP_LOSS';
  status: 'PENDING' | 'COMPLETED' | 'CANCELLED';
  timestamp: Date;
}
```

### Stock
```typescript
interface Stock {
  symbol: string;
  name: string;
  price: number;
  change: number;
  changePercent: number;
  volume: number;
  lastUpdated: Date;
}
```

### Admin User
```typescript
interface AdminUser {
  id: string;
  fullName: string;
  email: string;
  role: 'ADMIN' | 'SUPER_ADMIN';
  permissions: Permission[];
  lastLogin: Date;
  createdAt: Date;
  status: 'ACTIVE' | 'SUSPENDED' | 'INACTIVE';
}
```

### Permission
```typescript
interface Permission {
  id: string;
  code: string;
  name: string;
  description: string;
  category: 'USER_MANAGEMENT' | 'TRADING' | 'CONTENT' | 'SYSTEM' | 'REPORTS';
}
```

### System Settings
```typescript
interface SystemSettings {
  tradingEnabled: boolean;
  maintenanceMode: boolean;
  maxTradeValue: number;
  allowedOrderTypes: ('MARKET' | 'LIMIT' | 'STOP_LOSS')[];
  registrationEnabled: boolean;
  defaultInitialBalance: number;
  apiKeys: {
    polygonApi: string;
  };
}
```

## Data Flow

### Authentication Flow
1. User registration
   - Validate input
   - Hash password
   - Create user record
   - Generate JWT token

2. User login
   - Validate credentials
   - Generate JWT token
   - Update last login

### Trading Flow
1. Place order
   - Validate user balance
   - Create trade record
   - Update user balance
   - Update portfolio value

2. Market data
   - Fetch from Polygon.io
   - Cache in React Query
   - Update through WebSocket

### Admin Operations
1. User management
   - CRUD operations
   - Balance adjustments
   - Account status updates

2. System monitoring
   - Trading activity logs
   - Performance metrics
   - Error tracking

## Security Measures

### Password Security
- Bcrypt hashing with salt rounds: 10
- Minimum password length: 8 characters
- Required complexity: letters, numbers, special characters

### JWT Configuration
- Token expiration: 7 days
- Refresh token expiration: 30 days
- Signing algorithm: HS256

### API Security
- Rate limiting: 100 requests per minute
- CORS configuration: Restricted to application domain
- Request validation using Zod schemas

## Local Storage Structure

### Auth Data
```typescript
interface AuthStorage {
  user: User | null;
  adminUser: AdminUser | null;
  token: string | null;
  refreshToken: string | null;
}
```

### Settings
```typescript
interface LocalSettings {
  theme: 'light' | 'dark';
  language: 'ar' | 'en';
  notifications: boolean;
  chartType: 'candlestick' | 'line' | 'area';
}
```

## Cache Strategy

### React Query Configuration
```typescript
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 5000,
      cacheTime: 10 * 60 * 1000,
      retry: 2,
      refetchOnWindowFocus: false,
    },
  },
});
```

### Cached Data
- Stock quotes: 5 seconds stale time
- User data: 1 minute stale time
- Market overview: 10 seconds stale time
- Trade history: 1 minute stale time