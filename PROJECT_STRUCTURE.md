# Project Structure Documentation

## Overview

This document outlines the complete structure of the Trading Simulator project, explaining the purpose and relationships between different components.

## Directory Structure

```
src/
├── components/       # React components
├── hooks/           # Custom React hooks
├── pages/           # Page components
├── providers/       # Context providers
├── services/        # API and services
├── store/           # State management
├── types/           # TypeScript types
└── utils/           # Utility functions
```

## Components

### Authentication Components (`src/components/auth/`)
- `LoginForm.tsx` - User login form with email/password
- `RegisterForm.tsx` - New user registration
- `AuthRoute.tsx` - Protected route wrapper
- `AdminRoute.tsx` - Admin-only route protection

### Admin Components (`src/components/admin/`)
- `AdminDashboard.tsx` - Main admin interface
- `UserManagement.tsx` - User CRUD operations
- `SystemConfiguration.tsx` - System settings
- `ActivityMonitor.tsx` - User activity tracking
- `ContentManager.tsx` - Educational content management

### Trading Components (`src/components/trading/`)
- `TradingApp.tsx` - Main trading interface
- `StockChart.tsx` - Interactive price charts
- `TradeForm.tsx` - Order execution form
- `PositionDetails.tsx` - Current position info
- `TradeHistory.tsx` - Past trades list

### Dashboard Components (`src/components/dashboard/`)
- `AccountSummary.tsx` - User account overview
- `QuickTrade.tsx` - Simplified trading interface
- `MarketOverview.tsx` - Market statistics
- `RecentTrades.tsx` - Latest transactions

### UI Components (`src/components/ui/`)
- `Button.tsx` - Reusable button component
- `Table.tsx` - Data table component
- `Toggle.tsx` - Toggle switch component
- `SearchInput.tsx` - Search input field

### Layout Components (`src/components/layout/`)
- `DashboardLayout.tsx` - Main application layout
- `Navbar.tsx` - Navigation header
- `AdminLayout.tsx` - Admin panel layout

## Pages

### Main Pages (`src/pages/`)
- `HomePage.tsx` - Landing/login page
- `DashboardPage.tsx` - User dashboard
- `SettingsPage.tsx` - User preferences
- `AuthPage.tsx` - Authentication page

## Hooks

### Custom Hooks (`src/hooks/`)
- `useAuth.tsx` - Authentication logic
- `useStockPrices.ts` - Real-time price data
- `useTrading.ts` - Trading operations
- `useStockData.ts` - Stock information
- `useAdminAuth.ts` - Admin authentication
- `useAuditLog.ts` - Activity logging

## Services

### API Services (`src/services/`)
- `polygon.ts` - Polygon.io API integration
- `auth/` - Authentication services
  - `validation.ts` - Input validation
  - `security.ts` - Security utilities
  - `storage.ts` - Local storage management

## Store

### State Management (`src/store/`)
- `auth.ts` - Authentication state
- `admin.ts` - Admin state
- `atoms.ts` - Jotai atoms

## Types

### Type Definitions (`src/types/`)
- `index.ts` - Common types
- `admin.ts` - Admin-related types

## Utils

### Utility Functions (`src/utils/`)
- `cn.ts` - Class name utilities
- `validation.ts` - Input validation
- `chartUtils.ts` - Chart helpers
- `errorHandling.ts` - Error handlers

## Routing Structure

```
/                   # Home/Login page
├── /dashboard      # User dashboard
├── /trading       # Trading platform
├── /profile       # User profile
├── /settings      # User settings
└── /admin         # Admin panel
    ├── /users     # User management
    ├── /system    # System settings
    ├── /activity  # Activity monitoring
    └── /content   # Content management
```

## Data Flow

### Authentication Flow
1. User enters credentials (`LoginForm.tsx`)
2. Authentication check (`useAuth.ts`)
3. Route protection (`AuthRoute.tsx`)
4. State management (`auth.ts`)

### Trading Flow
1. Stock selection (`StockList.tsx`)
2. Price monitoring (`useStockPrices.ts`)
3. Order placement (`TradeForm.tsx`)
4. Position tracking (`PositionDetails.tsx`)

### Admin Flow
1. Admin authentication (`AdminRoute.tsx`)
2. User management (`UserManagement.tsx`)
3. System monitoring (`ActivityMonitor.tsx`)
4. Settings control (`SystemConfiguration.tsx`)

## State Management

### Jotai Atoms
- `userAtom` - Current user data
- `adminUserAtom` - Admin user data
- `systemSettingsAtom` - System settings

### React Query
- Stock price caching
- User data caching
- Trading history

## Security Implementation

### Route Protection
- Public routes
- Protected user routes
- Admin-only routes

### Data Validation
- Form validation with Zod
- API request validation
- Input sanitization

## API Integration

### Polygon.io
- Real-time quotes
- Historical data
- Company information

## Component Communication

### Parent-Child
- Props passing
- Event handlers
- Render props

### Global State
- Jotai atoms
- React Query cache
- Context providers

## Error Handling

### Error Boundaries
- Component error catching
- Fallback UI
- Error reporting

### Form Validation
- Input validation
- Error messages
- Field highlighting

## Performance Optimization

### Code Splitting
- Lazy loading
- Route-based splitting
- Component chunking

### Caching
- API response caching
- State persistence
- Local storage

## Development Guidelines

### Component Creation
1. Create component file
2. Define TypeScript interfaces
3. Implement component logic
4. Add styling
5. Write documentation

### State Management
1. Identify state scope
2. Choose appropriate store
3. Implement actions/updates
4. Handle side effects

### Error Handling
1. Define error types
2. Implement error boundaries
3. Add error messages
4. Provide recovery options