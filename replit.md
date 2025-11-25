# Jessepunk Spin - Farcaster Mini App

## Overview
A mobile-first spin-to-earn game built as a Farcaster Mini App. Users pay a daily GM fee ($0.01 USD worth of ETH on Base) to unlock 10 daily spins, or purchase premium access (0.0005 ETH) for unlimited spins. Players earn points with each spin and compete on the leaderboard, then redeem points for rewards on the marketplace.

## Current State
**Status**: PostgreSQL + Features Complete ✅
**Last Updated**: November 25, 2025

### Implemented Features
- ✅ Farcaster Mini App integration with social sign-in
- ✅ Animated spin wheel with 12 prize segments (5-200 points)
- ✅ Daily GM payment system (0.01 ETH on Base = 10 spins)
- ✅ Premium tier (0.0005 ETH on Base = unlimited spins)
- ✅ Points system with real-time leaderboard
- ✅ Base network wallet integration via wagmi
- ✅ Mobile-first responsive design with animations
- ✅ PostgreSQL persistent storage (migrated from in-memory)
- ✅ Points redemption marketplace - Redeem points for items/rewards
- ✅ Social sharing to Farcaster - Share spin wins on Farcaster feed
- ✅ Confetti celebrations on wins
- ✅ Beautiful loading and error states

## Project Architecture

### Tech Stack
- **Frontend**: React, TypeScript, Tailwind CSS, Framer Motion
- **Backend**: Express.js, Node.js
- **Database**: PostgreSQL with Drizzle ORM (persistent data)
- **Blockchain**: Wagmi (Base network), Viem
- **Social**: @farcaster/frame-sdk
- **State Management**: TanStack Query v5

### Key Files

#### Frontend
- `client/src/pages/game.tsx` - Main game page with all user interactions
- `client/src/components/SpinWheel.tsx` - Animated spin wheel component
- `client/src/components/DailyGMPaymentModal.tsx` - GM fee payment modal
- `client/src/components/PremiumUpgradeCard.tsx` - Premium purchase card
- `client/src/components/RewardsMarketplace.tsx` - Points redemption marketplace
- `client/src/components/ShareWinModal.tsx` - Farcaster share modal for wins
- `client/src/components/Leaderboard.tsx` - Points leaderboard display
- `client/src/components/BalanceStats.tsx` - User statistics dashboard
- `client/src/components/AppHeader.tsx` - Sticky header with user info
- `client/src/components/FarcasterProvider.tsx` - Farcaster context provider
- `client/src/components/WalletProvider.tsx` - Web3 wallet provider

#### Backend
- `server/routes.ts` - API endpoints for spins, payments, leaderboard, rewards, redemptions
- `server/storage.ts` - PostgreSQL storage implementation with Drizzle ORM
- `server/db.ts` - Drizzle database instance
- `shared/schema.ts` - TypeScript types, Zod schemas, and Drizzle tables

### Database Schema

**Tables**:
- `users` - User profiles with points, spins, premium status
- `spins` - Spin history with points awarded
- `payments` - Payment records (GM fees, premium purchases)
- `rewards` - Available rewards/items in marketplace
- `redemptions` - User redemption history

### API Endpoints

**User & Game**
- `GET /api/user/me` - Get or create user by Farcaster FID
- `GET /api/leaderboard` - Get top players by points (limit: default 100)
- `GET /api/user/today-spins` - Get user's spin count for today
- `POST /api/spin` - Execute a spin and award points

**Payments**
- `POST /api/payment/gm` - Process daily GM fee payment (grants 10 spins)
- `POST /api/payment/premium` - Process premium purchase (unlimited spins)

**Rewards & Redemptions**
- `GET /api/rewards` - Get all available rewards
- `POST /api/redeem` - Redeem points for a reward (deducts points from user)
- `GET /api/user/redemptions` - Get user's redemption history

## Business Logic

### Daily Spins System
- New users start with 0 spins
- Paying GM fee ($0.01 USD = 0.000005 ETH on Base) grants 10 spins for the day
- GM fee must be paid daily to get new spins
- Spins reset to 0 at midnight if no payment made

### Premium System
- One-time purchase of 0.0005 ETH
- Grants unlimited spins forever
- Premium users don't need to pay daily GM fee
- Premium status persists across sessions

### Points & Leaderboard
- Each spin awards random points (5-200)
- Points accumulate over time
- Leaderboard shows top 100 players by total points
- User's current rank displayed in stats

### Rewards Marketplace
- Users redeem accumulated points for items/rewards
- Each reward has a point cost
- Redemption deducts points from user balance
- Redemption history tracked in database

### Social Sharing
- After each win, users see share modal with points won
- One-click share to Farcaster feed with win details
- Uses @farcaster/frame-sdk to open Warpcast composer

## Design System

### Colors
- Primary: Purple (`hsl(262 83% 58%)`)
- Chart colors: Purple, Pink, Blue, Cyan, Orange variations
- Background: White (light) / Dark gray (dark mode)
- Card: Subtle elevated backgrounds

### Typography
- Headings: Poppins (600, 700, 800)
- Body: Inter (400, 500, 600, 700)
- Mobile-optimized sizing

### Animations
- Spin wheel: 4s cubic-bezier easing
- Confetti on wins: 5s duration
- Bounce-in for modals
- Count-up for point increments
- Pulse glow for premium badges

## Development

### Running the App
```bash
npm run dev
