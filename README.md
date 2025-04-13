# Neighb0urhood

**Neighb0urhood** is a decentralized marketplace that connects local service providers (e.g., plumbers, tutors, gardeners) with customers, leveraging the Ethereum blockchain to eliminate intermediaries, reduce fees, and ensure trust through transparent, tamper-proof transactions. Providers can list services with descriptions and prices, customers can book them by sending cryptocurrency, and payments are securely held in escrow until the job is completed, then released automatically. The platform combines blockchain’s decentralization with modern web technologies to deliver a scalable, user-friendly experience for communities worldwide.

This project is designed for developers interested in Web3, local economies, or decentralized applications (dApps). Whether you’re a contributor, a service provider, or a customer, Neighb0urhood offers a new way to engage in local services with fairness and efficiency.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Smart Contract Deployment](#smart-contract-deployment)
  - [Running the Application](#running-the-application)
- [Usage](#usage)
- [Security Considerations](#security-considerations)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Project Overview

Neighb0urhood addresses the challenges of traditional service platforms, such as high fees, lack of transparency, and reliance on centralized authorities. By using Ethereum smart contracts, it ensures that every transaction—listing a service, booking it, or completing it—is recorded immutably, building trust between providers and customers. The platform’s hybrid architecture combines blockchain for critical operations with off-chain storage for performance, making it both decentralized and efficient.

For example:
- A gardener lists “Lawn mowing for 0.01 ETH.”
- A customer books it, sending 0.01 ETH to a smart contract.
- After the job, the customer confirms completion, and the ETH is released to the gardener.

This process is automated, secure, and transparent, empowering local communities to exchange services without intermediaries.

## Features

Neighb0urhood offers a robust set of features to facilitate local service transactions:

- **Service Listing**:
  - Providers create listings with a description (e.g., “Dog walking”) and price in cryptocurrency (ETH or equivalent).
  - Listings are stored on the Ethereum blockchain, ensuring immutability and transparency.

- **Secure Booking**:
  - Customers browse available services and book one by sending the exact price.
  - Payments are locked in a smart contract (escrow) until the service is completed, preventing fraud.

- **Automatic Payment Release**:
  - Upon customer confirmation, the smart contract releases the payment to the provider.
  - No manual intervention is needed, ensuring efficiency and trust.

- **Dual Authentication**:
  - Blockchain interactions use wallet-based authentication via MetaMask.
  - Optional email/password authentication (for non-blockchain features) enhances accessibility for non-crypto users.

- **Responsive Interface**:
  - A modern, mobile-friendly UI ensures seamless access across devices.
  - Intuitive forms and buttons simplify listing, booking, and completing services.

- **Scalable Storage**:
  - Off-chain data (e.g., user profiles, cached service metadata) is stored in a cloud database for faster performance.
  - Reduces blockchain queries, lowering costs and improving speed.

- **Security Measures**:
  - Rate limiting and bot protection prevent spam and abuse.
  - Smart contract checks ensure only authorized actions are performed.

- **Fiat Payment Support**:
  - Optional fiat payments for premium features (e.g., promoted listings or subscriptions) cater to diverse users.

## Tech Stack

Neighb0urhood is built with a carefully selected stack to balance decentralization, performance, and usability:

| **Technology**          | **Purpose**                                                                 | **Role in Neighb0urhood**                                                                 |
|-------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **Web3 with Solidity**  | Blockchain logic and smart contracts                                        | Handles service listings, bookings, and escrow payments on Ethereum.                      |
| **Next.js**             | Front-end and back-end framework                                            | Powers the UI and server-side logic for a fast, SEO-friendly experience.                  |
| **Tailwind with Shadcn**| Styling and UI components                                                   | Delivers a polished, responsive design with reusable components.                          |
| **Better Auth**         | Authentication for non-blockchain features                                  | Provides optional email/password login for user profiles and preferences.                 |
| **Neondb with Postgres**| Scalable cloud database                                                     | Stores off-chain data (e.g., user profiles, metadata) for performance.                    |
| **Prisma**              | Object-Relational Mapping (ORM)                                             | Simplifies database interactions with type-safe queries.                                  |
| **Arc Jet**             | Security and rate limiting                                                  | Protects against spam, bots, and abuse for platform reliability.                          |
| **Vercel**              | Hosting and deployment                                                      | Hosts the Next.js app with automatic scaling and CI/CD.                                  |
| **Stripe/Razorpay**     | Fiat payment processing                                                     | Processes non-blockchain payments for premium features.                                   |

## Architecture

Neighb0urhood’s architecture integrates decentralized and centralized components for a balanced, efficient system:

### Blockchain Layer
- **Smart Contract** (Solidity):
  - Deployed on Ethereum (Sepolia testnet for development, Polygon for production).
  - Stores service details (ID, provider address, description, price, status).
  - Manages escrow: locks customer payments during booking and releases them upon completion.
  - Emits events (e.g., `ServiceListed`, `ServiceBooked`) for front-end updates.
- **Web3 Integration**:
  - Web3.js connects the Next.js front-end to the blockchain.
  - MetaMask authenticates users and signs transactions (e.g., listing a service).

### Front-End Layer
- **Next.js**:
  - Renders a dynamic UI with client-side (for Web3 interactions) and server-side (for SEO) rendering.
  - Displays service listings, forms for providers, and booking/completion buttons.
- **Tailwind with Shadcn**:
  - Utility-first CSS (Tailwind) styles the app (e.g., `flex`, `p-4`).
  - Shadcn provides accessible components (e.g., modals, buttons) for a consistent design.

### Back-End Layer
- **Neondb with Postgres**:
  - Stores non-critical data, such as user profiles (e.g., display name) and cached service metadata.
  - Reduces blockchain queries for faster load times.
- **Prisma**:
  - Maps database tables to JavaScript objects (e.g., `prisma.service.findMany()`).
  - Ensures type-safe, secure queries.
- **Better Auth**:
  - Manages email/password login for optional features (e.g., saving favorite services).
  - Stores user credentials securely in Neondb.

### Security Layer
- **Arc Jet**:
  - Applies rate limiting to API routes (e.g., max 10 bookings per minute per IP).
  - Detects and blocks bots, preserving server resources.
- **Smart Contract**:
  - Uses `require` checks (e.g., only customers can complete services) to enforce rules.

### Payment Layer
- **Web3 with Solidity**:
  - Handles cryptocurrency payments (ETH) for service bookings.
  - Escrow ensures funds are secure until completion.
- **Stripe/Razorpay**:
  - Processes fiat payments for premium features (e.g., $5 for a featured listing).
  - Integrates with Next.js API routes for secure checkout.

### Hosting
- **Vercel**:
  - Deploys the Next.js app with a global CDN for low latency.
  - Provides CI/CD for automatic updates on code pushes.
  - Manages custom domains (e.g., `neighb0urhood.com`).

## Getting Started

Follow these steps to set up Neighb0urhood locally or deploy it.

### Prerequisites

Ensure you have the following installed or set up:

- **Node.js** (>=18.x): Download from [nodejs.org](https://nodejs.org/).
- **MetaMask**: Install the browser extension from [metamask.io](https://metamask.io/) for wallet interactions.
- **Neondb Account**: Sign up for a free Postgres database at [neon.tech](https://neon.tech/).
- **Vercel Account**: Create an account at [vercel.com](https://vercel.com/) for deployment.
- **Stripe/Razorpay Keys** (Optional): Obtain API keys from [stripe.com](https://stripe.com/) or [razorpay.com](https://razorpay.com/) for fiat payments.
- **Ethereum Testnet ETH**: Get free test ETH for Sepolia from a faucet like [sepolia-faucet.pk910.de](https://sepolia-faucet.pk910.de/).

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/neighb0urhood.git
   cd neighb0urhood
