# Libraries and Tools Documentation

## Core Libraries

### React and TypeScript
- **React**: v18.2.0 - Core UI library
- **React DOM**: v18.2.0 - React rendering for web
- **TypeScript**: v5.2.2 - Static typing and modern JavaScript features
- **Vite**: v5.1.4 - Build tool and development server

### State Management
- **Jotai**: v2.6.5
  - Atomic state management
  - Used for user authentication state
  - Manages application-wide settings

### Data Fetching
- **@tanstack/react-query**: v5.24.1
  - Data fetching and caching
  - Real-time stock data management
  - Automatic background updates

### Routing
- **react-router-dom**: v6.22.2
  - Application routing
  - Protected routes
  - Navigation management

## UI Components and Styling

### Styling
- **TailwindCSS**: v3.4.1
  - Utility-first CSS framework
  - Responsive design
  - Custom theme configuration

### UI Utilities
- **clsx**: v2.1.0
  - Conditional class name construction
- **tailwind-merge**: v2.1.0
  - Efficient Tailwind class merging

### Icons and Charts
- **lucide-react**: v0.344.0
  - Modern icon library
  - SVG-based icons
- **lightweight-charts**: v4.1.3
  - Trading charts
  - Technical analysis tools

## Form Handling and Validation

### Form Management
- **react-hook-form**: v7.50.1
  - Form state management
  - Form validation
  - Performance optimization

### Validation
- **@hookform/resolvers**: v3.3.4
  - Form validation resolvers
- **zod**: v3.22.4
  - Schema validation
  - Type inference

## Date and Time
- **date-fns**: v3.3.1
  - Date manipulation
  - Formatting
  - Time zone handling

## Security

### Authentication
- **bcryptjs**: v2.4.3
  - Password hashing
  - Salt generation
- **jwt-decode**: v4.0.0
  - JWT token handling
  - Token validation

## Development Tools

### ESLint Configuration
- **eslint**: v8.56.0
- **@typescript-eslint/eslint-plugin**: v7.0.2
- **@typescript-eslint/parser**: v7.0.2
- **eslint-plugin-react-hooks**: v4.6.0
- **eslint-plugin-react-refresh**: v0.4.5

### Build Tools
- **autoprefixer**: v10.4.18
- **postcss**: v8.4.35
- **@vitejs/plugin-react**: v4.2.1

## External APIs

### Market Data
- **Polygon.io**
  - API Key: `baaf81ba-1174-42dc-b155-74b96c5de680`
  - Real-time stock quotes
  - Historical data
  - Company information

## Environment Configuration

### Development
```env
VITE_POLYGON_API_KEY=baaf81ba-1174-42dc-b155-74b96c5de680
```

## Type Definitions

### React Types
- **@types/react**: v18.2.56
- **@types/react-dom**: v18.2.19
- **@types/bcryptjs**: v2.4.6

## Library Usage Examples

### State Management with Jotai
```typescript
import { atom, useAtom } from 'jotai';

// Define atom
const userAtom = atom<User | null>(null);

// Use in components
const [user, setUser] = useAtom(userAtom);
```

### Data Fetching with React Query
```typescript
import { useQuery } from '@tanstack/react-query';

export function useStockPrices() {
  return useQuery({
    queryKey: ['stocks'],
    queryFn: fetchStocks,
    refetchInterval: 10000,
  });
}
```

### Form Handling with React Hook Form
```typescript
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';

const { register, handleSubmit } = useForm({
  resolver: zodResolver(schema)
});
```

### Styling with Tailwind and clsx
```typescript
import { cn } from '../utils/cn';

export function Button({ className, ...props }) {
  return (
    <button
      className={cn(
        "px-4 py-2 rounded-md",
        className
      )}
      {...props}
    />
  );
}
```

## Performance Considerations

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

### Code Splitting
- React.lazy for component loading
- Dynamic imports for routes
- Chunk optimization in Vite

## Security Implementation

### Password Hashing
```typescript
import bcrypt from 'bcryptjs';

const hashPassword = async (password: string) => {
  const salt = await bcrypt.genSalt(10);
  return bcrypt.hash(password, salt);
};
```

### JWT Handling
```typescript
import { jwtDecode } from 'jwt-decode';

const verifyToken = (token: string) => {
  try {
    const decoded = jwtDecode(token);
    return decoded;
  } catch {
    return null;
  }
};
```

## Development Setup

### Installation
```bash
npm install
```

### Development Server
```bash
npm run dev
```

### Production Build
```bash
npm run build
```