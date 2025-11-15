---
label: UpPing
icon: rocket
order: 95
---

# UpPing Documentation

> A fast, modern website uptime and performance monitoring tool built with React, TypeScript, and Cloudflare Workers.

[![Deploy Status](https://img.shields.io/badge/deploy-cloudflare-orange)](https://upping.vxcloud.workers.dev/)
[![Frontend](https://img.shields.io/badge/frontend-react-blue)](https://reactjs.org/)
[![API](https://img.shields.io/badge/api-cloudflare%20workers-orange)](https://workers.cloudflare.com/)
[![TypeScript](https://img.shields.io/badge/typescript-ready-blue)](https://www.typescriptlang.com/)

---

## Overview

UpPing is a comprehensive website monitoring solution that provides real-time uptime checks, performance metrics, SSL validation, and detailed error diagnostics. Built with modern web technologies and powered by Cloudflare's edge network for lightning-fast global performance.

### Key Features

+++ Real-time Monitoring
Check any website's uptime and performance instantly with sub-second response times powered by Cloudflare Workers edge computing.
+++ Performance Metrics
Get detailed insights including:
- Response Time
- Time to First Byte (TTFB)
- SSL Certificate Status
- Health Score (0-100)
- Content Type Detection
+++ Smart Classification
Automatic categorization of issues:
- DNS Resolution Problems
- SSL/TLS Certificate Issues
- Server Errors (5xx)
- Client Errors (4xx)
- Network Timeouts
- Invalid Domains
+++ Redirect Tracking
Full redirect chain analysis with hop-by-hop information showing the complete path from requested URL to final destination.
+++

---

## Architecture

```
┌─────────────────┐    HTTP/HTTPS    ┌─────────────────┐
│                 │    ────────►     │                 │
│   Frontend      │                  │   Cloudflare    │
│   (React/Vite)  │    ◄────────     │   Workers API   │
│                 │      JSON        │                 │
└─────────────────┘                  └─────────────────┘
```

### Technology Stack

=== Frontend
- **React 18** - Modern UI library with hooks
- **TypeScript** - Type-safe development
- **Vite** - Lightning-fast build tool
- **Tailwind CSS** - Utility-first styling
- **Axios** - HTTP client
- **Lucide React** - Icon library
=== API
- **Cloudflare Workers** - Edge computing platform
- **Wrangler** - CLI and development tool
- **Vitest** - Testing framework
===

---

## Getting Started

### Prerequisites

!!! warning System Requirements
- Node.js v18 or higher
- npm or yarn package manager
- Wrangler CLI (for API deployment)
!!!

### Installation

#### 1. Clone Repository

```bash
git clone https://github.com/vxrachit/UpPing.git
cd UpPing
```

#### 2. Frontend Setup

```bash
cd frontend
npm install
```

Create `.env` file:

```env
VITE_API_BASE_URL=https://your-worker-domain.workers.dev/
```

Start development server:

```bash
npm run dev
```

Frontend available at: `http://localhost:5173`

#### 3. API Setup

```bash
cd api
npm install
```

Start local development:

```bash
npm run dev
```

API available at: `http://localhost:8787`

---

## Project Structure

```
UpPing/
├── frontend/              # React frontend application
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   │   ├── Header.tsx          # Navigation header
│   │   │   ├── Footer.tsx          # Footer with links
│   │   │   ├── ResultCard.tsx      # Results display
│   │   │   └── RecentChecks.tsx    # Recent checks list
│   │   ├── hooks/         # Custom React hooks
│   │   │   ├── useTheme.ts         # Dark/light mode
│   │   │   ├── useLocalStorage.ts  # Local storage hook
│   │   │   └── useScrollAnimation.ts # Scroll animations
│   │   ├── lib/           # Utilities and API client
│   │   │   └── api.ts              # API integration
│   │   ├── pages/         # Page components
│   │   │   ├── Home.tsx            # Main monitoring page
│   │   │   ├── Health.tsx          # Backend health check
│   │   │   └── About.tsx           # About page
│   │   ├── App.tsx        # Root component
│   │   ├── main.tsx       # Entry point
│   │   └── index.css      # Global styles
│   ├── package.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── tsconfig.json
├── api/                   # Cloudflare Workers API
│   ├── src/
│   │   └── index.js       # Main worker script
│   ├── package.json
│   └── wrangler.jsonc     # Cloudflare config
└── README.md
```

## API Documentation

### Endpoints

#### Health Check

Check API status and version.

+++ Request
```http
GET /api/health
```
+++ Response
```json
{
  "ok": true,
  "version": "1.0",
  "timestamp": "2025-11-15T10:30:00.000Z"
}
```
+++

#### Website Check

Perform comprehensive website health check.

+++ Request
```http
GET /api/check?url={website}
```

**Query Parameters:**
- `url` (required) - Website URL to check (with or without protocol)

**Examples:**
```
/api/check?url=google.com
/api/check?url=https://example.com
/api/check?url=github.com
```
+++ Success Response
```json
{
  "requestedUrl": "https://google.com",
  "finalUrl": "https://www.google.com/",
  "redirected": true,
  "redirectCount": 1,
  "redirectChain": [
    {
      "from": "https://google.com",
      "to": "https://www.google.com/",
      "code": 301
    }
  ],
  "statusCode": 200,
  "responseTime": 245,
  "ttfb": 180,
  "sslStatus": "valid",
  "contentType": "text/html; charset=utf-8",
  "responseSize": 12345,
  "classification": "Success",
  "reason": "ok",
  "error": null,
  "advice": null,
  "healthScore": 95,
  "cached": false,
  "checkedAt": "2025-11-15T10:30:00.000Z"
}
```
+++ Error Response
```json
{
  "requestedUrl": "https://invalid-domain-xyz.com",
  "finalUrl": "https://invalid-domain-xyz.com",
  "redirected": false,
  "redirectCount": 0,
  "redirectChain": [],
  "statusCode": null,
  "responseTime": 5234,
  "ttfb": 0,
  "sslStatus": "unknown",
  "contentType": null,
  "responseSize": 0,
  "classification": "invalid_domain",
  "reason": "invalid_domain",
  "error": "Domain does not exist or cannot be resolved",
  "advice": "This is not a valid website address. Please check the spelling.",
  "healthScore": 0,
  "cached": false,
  "checkedAt": "2025-11-15T10:30:00.000Z"
}
```
+++

### Status Classifications

The API automatically classifies website status into the following categories:

| Classification | HTTP Codes | Description |
|---------------|------------|-------------|
| **Success** | 200-299 | Website is healthy and responding normally |
| **client_error** | 400-499 | Client-side errors (403, 404, etc.) |
| **server_error** | 500-599 | Server-side errors |
| **timeout** | - | Request exceeded timeout limit |
| **invalid_domain** | - | DNS resolution failed or invalid domain |
| **dns_error** | - | DNS lookup issues |
| **ssl_error** | - | SSL/TLS certificate problems |
| **network_error** | - | Network connectivity issues |
| **cloudflare_internal_error** | - | Cloudflare edge connection issues |
| **unknown_error** | - | Unclassified errors |


### Caching Strategy

The API implements intelligent caching:

- **Cache Duration**: 60 seconds
- **Cache Key**: Full URL
- **Cache Storage**: Cloudflare edge cache
- **Cache Indicator**: `cached: true/false` in response

### Error Handling

The API provides detailed error classification and advice:

**Example Error Classifications:**

!!!success Valid Domain - Slow Response
```json
{
  "classification": "Success",
  "healthScore": 60,
  "advice": null,
  "responseTime": 2500
}
```
!!!

!!!warning Timeout
```json
{
  "classification": "timeout",
  "reason": "timeout",
  "advice": "The site took too long to respond. Possibly under heavy load.",
  "healthScore": 25
}
```
!!!

!!!danger Invalid Domain
```json
{
  "classification": "invalid_domain",
  "reason": "invalid_domain",
  "advice": "This is not a valid website address. Please check the spelling.",
  "healthScore": 0
}
```
!!!

### Performance Features

#### Request Strategy

The API uses a multi-stage request strategy:

1. **HEAD Request** - Initial attempt with minimal data transfer
2. **Fallback GET Request** - With Range header (0-1023 bytes) if HEAD fails
3. **Redirect Following** - Manual handling up to 10 redirects
4. **Browser Headers** - Mimics real browser behavior

#### Timeout Configuration

- Default timeout: 10 seconds
- Configurable per request
- AbortController for proper cancellation


---

## Development

### Available Scripts

#### Frontend Scripts

```bash
npm run dev          # Start development server (localhost:5173)
npm run build        # Build for production
npm run preview      # Preview production build
npm run lint         # Run ESLint
npm run typecheck    # TypeScript type checking
```

#### API Scripts

```bash
npm run dev          # Start local development (localhost:8787)
npm run deploy       # Deploy to Cloudflare Workers
npm run start        # Alias for dev
npm test            # Run Vitest tests
```

### Environment Configuration

#### Frontend (.env)

```env
VITE_API_BASE_URL=https://your-api-domain.workers.dev/
```


### Development Workflow

1. **Local Development**
   ```bash
   # Terminal 1 - Start API
   cd api
   npm run dev
   
   # Terminal 2 - Start Frontend
   cd frontend
   npm run dev
   ```

2. **Testing Changes**
   - Frontend: Hot reload at `http://localhost:5173`
   - API: Available at `http://localhost:8787`

3. **Type Checking**
   ```bash
   cd frontend
   npm run typecheck
   ```

4. **Linting**
   ```bash
   cd frontend
   npm run lint
   ```
---

## Deployment

### Frontend Deployment

#### Build for Production

```bash
cd frontend
npm run build
```

Output: `dist/` folder

#### Deployment Options

=== Cloudflare Pages
1. Connect GitHub repository
2. Set build command: `npm run build`
3. Set build output: `dist`
=== GitHub Pages
Use GitHub Actions workflow
===

### API Deployment

#### Deploy to Cloudflare Workers

```bash
cd api

# Login (first time only)
wrangler login

# Deploy
npm run deploy
```

#### Post-Deployment

1. Note the worker URL: `https://your-worker.workers.dev`
2. Update frontend `.env` with worker URL
3. Rebuild and redeploy frontend

---

## Testing

### Frontend Testing

Current setup uses TypeScript type checking:

```bash
npm run typecheck
```

### API Testing

Using Vitest with Cloudflare Workers pool:

```bash
cd api
npm test
```


## Troubleshooting

### Common Issues

!!!warning Frontend Not Connecting to API
**Solution:**
1. Check `.env` file has correct `VITE_API_BASE_URL`
2. Ensure API is running
3. Check browser console for CORS errors
4. Verify API URL format (include trailing slash)
!!!

!!!warning API Deployment Fails
**Solution:**
1. Run `wrangler login` to authenticate
2. Check `wrangler.jsonc` configuration
3. Verify account has Workers enabled
4. Check deployment logs: `wrangler tail`
!!!

!!!warning Build Errors
**Solution:**
1. Delete `node_modules` and reinstall
2. Clear build cache: `rm -rf dist .vite`
3. Update dependencies: `npm update`
4. Check Node.js version (v18+)
!!!

---

## Security

### Frontend Security

- **Input Validation** - URL validation before API calls
- **XSS Prevention** - React automatic escaping
- **HTTPS Only** - Force secure connections
- **Environment Variables** - Sensitive data in `.env`

### API Security

- **CORS Configuration** - Controlled cross-origin access
- **Rate Limiting** - Cloudflare automatic protection
- **Input Sanitization** - URL validation and parsing
- **Error Handling** - No sensitive data in errors
- **Timeout Protection** - Prevent long-running requests

### Best Practices

!!!danger Never Commit
- `.env` files
- API keys
- Wrangler credentials
- Production URLs
!!!

---

---

## Contributing

!!!
If you find UpPing useful, please consider:
- ⭐ **Starring** the [GitHub repository](https://github.com/vxrachit/UpPing)
- 🍴 **Forking** to create your own version
- 📢 **Sharing** with others who might benefit
!!!

### Development Setup

1. **Fork the repository** on GitHub
2. **Clone your fork** locally
   ```bash
   git clone https://github.com/YOUR_USERNAME/UpPing.git
   cd UpPing
   ```
3. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Install dependencies**
   ```bash
   # Frontend
   cd frontend && npm install
   
   # API
   cd ../api && npm install
   ```
5. **Make your changes** and test thoroughly
6. **Submit a pull request** with clear description

### Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Focus on the code, not the person
- Help others learn and grow

---

## Support & Contact

### Get Help

- **Email**: [mail@vxrachit.is-a.dev](mailto:mail@vxrachit.is-a.dev)
- **Issues**: [GitHub Issues](https://github.com/vxrachit/UpPing/issues)


### Links

- **Live Demo**: [https://upping.vxrachit.is-a.dev](https://upping.vxrachit.is-a.dev)
- **Repository**: [https://github.com/vxrachit/UpPing](https://github.com/vxrachit/UpPing)

---

## Changelog

### Version 1.0.0 (Current)

- ✨ Initial release
- ✅ Real-time website monitoring
- ✅ Performance metrics (Response Time, TTFB)
- ✅ SSL validation
- ✅ Health scoring algorithm
- ✅ Redirect chain tracking
- ✅ Recent checks history
- ✅ Cloudflare Workers API
- ✅ Comprehensive error handling

---


<p align="center">
  Made with ❤️ by <a href="https://github.com/vxrachit">vxRachit</a>
</p>

<p align="center">
  <a href="https://upping.vxrachit.is-a.dev/">🌐 Live Demo</a> •
  <a href="https://github.com/vxrachit/UpPing/issues">🐛 Report Bug</a> •
</p>
