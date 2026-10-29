# Arcade Arena

Five games tracked live by camera and microphone and scored by an on-device judge.

| Game | Tracking | What is judged |
|---|---|---|
| Flamingo Balance | MediaPipe Pose | One-foot hold time (foot lift measured against leg length) and torso sway |
| Keepy-Uppy (football) | MediaPipe Pose | Foot/toe contact with a virtual ball, streaks, alternating feet, drops |
| Hand Catch | MediaPipe Hands | Palm hits on moving targets and catch speed |
| Player Chain | Browser speech recognition | Footballer names, last-letter chain, repeats, timing |
| Country Chain | Browser speech recognition | Country names, last-letter chain, repeats, timing |

## Run

```bash
npm install
npm run dev     # http://localhost:3000
```

Camera and microphone need `localhost` or HTTPS. Use **Chrome or Edge** for voice (the other browsers lack speech recognition; typed answers still work in the word games).

## How judging works

The judge is not a language model. Trained vision models (MediaPipe) and speech recognition measure the real world; `lib/judge.js` converts those measurements into scores, verdicts and coaching text, and the referee speaks results with the browser's speech synthesis. Word-game answers are checked against the lists in `lib/data.js` (extend them freely).

## Word-game rules

+10 per valid answer, +5 if answered within 5 s, +5 for long names, +20 to the last player standing. 12 s per turn. One free retry per turn for misheard or invalid answers, then a strike. Three strikes and a player is out. No repeats.

## Privacy and cost

Everything is free: no API keys, no server, no database. Pose and hand video is processed in your browser and not uploaded. Models load from Google and jsDelivr CDNs on first use. Chrome's speech recognition sends microphone audio to Google for transcription; this is how that browser implements it. Scores are stored in `localStorage` on the device only.

Stand about 2 m from the camera with good lighting for the body games.
