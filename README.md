# AuraLive

Real-time emotive AI avatar platform powered by Gemini. Talk to animated male and female avatars that react with dynamic facial expressions, stream bidirectional voice through the Gemini Live API, and translate conversations across languages.

## Features

- **Live voice conversations** — bidirectional audio streaming with Gemini Live over WebSockets
- **Emotive avatars** — 2D and 3D avatars plus an audio-reactive orb, with expressions driven by detected sentiment
- **Voice cloning studio** — analyze a voice sample and map it to a matching voice profile
- **Multilingual subtitles** — live translation of the conversation transcript
- **Offline resilience** — fallback engine when the network or API is unavailable
- **Kiosk / peripheral mode** — full-screen display mode with peripheral telemetry
- **Ambient soundscapes** and an emotion telemetry radar

## Tech stack

- **Frontend:** React 19, Vite, Tailwind CSS 4, Three.js, Motion
- **Backend:** Express + `ws` (`server.ts`), run with `tsx`
- **AI:** `@google/genai` (Gemini Live, TTS, and chat models)

## Getting started

**Prerequisites:** Node.js 20+ (or Bun) and a [Gemini API key](https://aistudio.google.com/apikey).

1. Install dependencies:
   ```sh
   npm install    # or: bun install
   ```
2. Create a `.env` file in the project root:
   ```sh
   GEMINI_API_KEY=your-gemini-api-key
   # Optional
   PORT=3000
   APP_URL=http://localhost:3000
   ```
3. Start the dev server:
   ```sh
   npm run dev
   ```
4. Open http://localhost:3000 and allow camera and microphone access when prompted.

## Environment variables

| Variable         | Required | Description                                                  |
| ---------------- | -------- | ------------------------------------------------------------ |
| `GEMINI_API_KEY` | Yes      | Gemini API key used by the server for all AI calls           |
| `PORT`           | No       | Server port (default `3000`)                                 |
| `APP_URL`        | No       | Public URL where the app is hosted                           |
| `NODE_ENV`       | No       | Set to `production` to serve the built `dist/` bundle        |
| `DISABLE_HMR`    | No       | Set to `true` to disable Vite HMR and file watching          |

`.env*` files are git-ignored — never commit your API key.

## Scripts

| Command           | Description                                        |
| ----------------- | -------------------------------------------------- |
| `npm run dev`     | Start the Express server with Vite middleware      |
| `npm run build`   | Build the frontend into `dist/`                    |
| `npm start`       | Start the server (set `NODE_ENV=production` to serve `dist/`) |
| `npm run preview` | Preview the built frontend with Vite               |
| `npm run lint`    | Type-check with `tsc --noEmit`                     |
| `npm run clean`   | Remove build output                                |

### Production

```sh
npm run build
NODE_ENV=production npm start
```

## API

| Method | Path                         | Description                                   |
| ------ | ---------------------------- | --------------------------------------------- |
| `WS`   | `/live`                      | Gemini Live bidirectional voice session       |
| `GET`  | `/api/health`                | Server status, API key presence, model info   |
| `POST` | `/api/gemini/chat`           | Text chat with sentiment / emotion detection  |
| `POST` | `/api/gemini/tts`            | Text-to-speech                                |
| `POST` | `/api/voice-clone/analyze`   | Analyze a voice sample                        |
| `POST` | `/api/translate`             | Translate text                                |
| `POST` | `/api/peripherals/telemetry` | Peripheral / kiosk telemetry                  |

## Project structure

```
server.ts              Express + WebSocket server, Gemini API routes
index.html             App entry HTML
src/
  App.tsx              Main application
  components/          Avatars, orb, voice controller, studio, kiosk, etc.
  utils/               Audio processing helpers
  types/               Shared TypeScript types
  assets/              Avatar images
```
