# Notes

A collection of technical notes.

## 🚀 React Fiber Architecture
A concise explanation of how React Fiber works, including reconciliation, scheduling, and incremental rendering.  
👉 [Read the full note](./React%20Fiber%20Architecture.md)


## 🚀 Rendering Strategies in Next.js

Before deploying a Next.js app, it’s important to understand **how your pages are rendered**, because it directly affects:
- Server load
- Performance
- Caching behavior
- Nginx + PM2 setup expectations

This note covers all core rendering strategies used in Next.js:
- **CSR (Client-Side Rendering)**
- **SSR (Server-Side Rendering)**
- **SSG (Static Site Generation)**
- **ISR (Incremental Static Regeneration)**

👉 **Read the full explanation here:**  
[Rendering Strategies in Next.js](./Rendering%20Strategies%20in%20Next.js.md)


## 🚀 Deployment Guide (Ubuntu VPS)

This step-by-step guide explains how to deploy a **Next.js application on an Ubuntu VPS** using:
- Node.js (LTS)
- PM2 for process management
- Nginx as a reverse proxy

It focuses on **real-world deployment**, explaining not just *what to run*, but *why it’s needed*.

👉 **Read the full deployment guide:**  
[Deploying a Next.js App on Ubuntu VPS](./Deploying%20a%20Next.js%20App%20on%20Ubuntu%20VPS.md)
