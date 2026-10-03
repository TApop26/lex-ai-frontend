# LexAI: legal research assistant (frontend)

> **3rd place at PoliHack v19** (April 2026). A 4-person hackathon team project.
> This is my fork of [MirceaGodiac/lex-ai-frontend](https://github.com/MirceaGodiac/lex-ai-frontend). **Live demo:** https://lex-ai-frontend-five.vercel.app

LexAI helps people research legal questions. You ask a question in plain language, and LexAI answers with **citations and supporting evidence**. It also shows **the network of laws, articles and concepts** behind the answer, so it can be checked instead of trusted blindly.

## My contribution

The features were split across the four of us. I worked mainly on the **frontend** and on the **final presentation**.

- **Knowledge-graph explorer.** I built the app's first interactive visualisation of the legal knowledge graph: the explorer page (`src/pages/GraphPage.tsx`) and a WebGL renderer (`src/components/explore/SigmaGraphRenderer.tsx`).
  - It renders with Sigma.js in WebGL on graphology data, using a ForceAtlas2 force-directed layout and graph controls.
  - Hovering or clicking a node highlights its neighbourhood and dims the rest of the graph.
  - Later in the hackathon the team merged graph visualisation into the product page (`/graph` now redirects to `/product`). The explorer code is still in this repo, but it isn't routed in the final build.
- **Presentation:** I worked on the final presentation shown to the jury.

Teammates: [Mircea Godiac](https://github.com/MirceaGodiac), [David Sabau](https://github.com/Zabau11) and Andrei-Anton Iancu. They built the landing page, the product page with its chat, canvas and force-graph view, the assistant view (citations, evidence and verifier panels), and the API integration.

## What's in this repository

| Route / folder | Description |
|---|---|
| `/` | Landing page |
| `/assistant` | Question → answer with citations, evidence, verifier and debug panels |
| `/product` | Chat plus a force-directed graph of the legal units used in the answer |
| `/canvas`, `/library` | Canvas workspace and saved-items library |
| `src/pages/GraphPage.tsx`, `src/components/explore/` | My graph-explorer prototype (not routed in the final build) |
| `backend/` | Small FastAPI **mock** of the LexAI API (placeholder answers) for local frontend development |

**Tech stack:** TypeScript · React 19 · Vite · React Router 7 · Tailwind CSS 4 · Sigma.js + graphology (ForceAtlas2) · react-force-graph · Framer Motion · Zustand · Zod · deployed on Vercel

`npm ci` and `npm run build` were tested on Windows 11 with Node 24 and pass.

---

*The original setup notes from the upstream repository follow, unchanged.*

## Stack

- Vite
- React
- TypeScript
- React Router
- Tailwind

## Local setup

```bash
npm install
cp .env.example .env.local
npm run dev
```

## Environment

```bash
VITE_API_BASE_URL=http://127.0.0.1:8010
```

Important:

- `VITE_API_BASE_URL` must be the backend origin only.
- It should not include `/api`.
- Example local value: `http://127.0.0.1:8010`
- Example production value: `https://your-backend.example.com`

## Scripts

```bash
npm run dev
npm run build
npm run preview
npm run lint
```

## Vercel deploy

- Framework preset: Vite
- Build command: `npm run build`
- Output directory: `dist`
- Required environment variable: `VITE_API_BASE_URL`
- Backend must allow CORS from the deployed Vercel domain.
- `vercel.json` rewrites all routes to `/index.html` because this is a BrowserRouter SPA.
