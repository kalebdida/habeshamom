# Habesha Mom AI

**Confess. Get judged. Eat something.**

> LLMs speak like Silicon Valley. Habesha Mom AI is a culturally grounded persona that code-switches between Amharic and English, proving local culture can live inside AI, one guilt trip at a time.

## The problem

Most AI assistants sound the same: polite, neutral, and culturally from nowhere in particular. African and Ethiopian voices are rare in mainstream models, and so is the way millions of people really talk, switching between Amharic and English inside a single sentence. If AI is going to be part of daily life in Addis Ababa, it should be able to sound like someone from there.

## The solution

Habesha Mom AI gives an LLM a persona every Ethiopian recognizes instantly: the loving, dramatic mother. You confess something about your life. She responds with guilt, worry, a comparison to the neighbor's son who is a doctor, and finally the only question that matters: *"Have you eaten?"*

It is a comedy app, and it is also a small demonstration that persona design, code-switching, and safety rules can make a general model feel local.

### Features

- **Confession box** with six one-tap preset confessions for fast live demos
- **Chat display** with mom's replies in Amharic-English code-switching (Amharic written in Latin letters so any audience can follow)
- **Disappointment Meter**: an animated 0-100% bar, from "Proud mom 🥹" to "SLIPPER INCOMING 🩴"
- **Flying slipper**: a spinning 🩴 crosses the screen with a screen shake for truly outrageous confessions
- **Real Amharic voice**: mom's reply is spoken in Amharic by an Ethiopian-built voice model (Addis AI), with the Amharic text shown under the English. Falls back to browser text-to-speech, with an auto-speak toggle for stage demos
- **Son / daughter switch** so mom uses the right Amharic forms (ante / anchi)
- **Live 3D background** (three.js) that reacts to the mouse and spins faster as mom gets angrier
- **Structured AI output**: the model returns JSON (`reply`, `reply_am`, `disappointment`, `slipper`) that drives the whole UI
- **Offline mom 📴**: 20+ hand-written replies matched by keyword. If the API key is missing, the network fails, or the model takes longer than 8 seconds, the app switches over automatically and the demo never breaks

## Demo examples

**Confession:** "I failed my math exam"

> **Mom:** Wey gud! You failed?! Tsehay's son is a doctor at Tikur Anbessa and he never failed even a blood test. I sold my gold for your school fees, yene lij. Come, sit, eat something, then we study until morning.
> *Disappointment: 88% (Calling your father 📞)*

**Confession:** "I want to be a TikToker"

> **Mom:** TikToker?! Ere tew! I carried you for nine months so you can dance for strangers on a phone? Only doctor, engineer, or pilot, yene lij. Choose one and then come eat.
> *Disappointment: 95% (SLIPPER INCOMING 🩴)*

**Confession:** "I didn't eat breakfast"

> **Mom:** Ere bakih! No breakfast? Do you want to disappear? I woke up at five to make firfir and you walked past it like a stranger. Come. Eat. Then eat again.
> *Disappointment: 68% (Calling your father 📞)*

## Tech stack

- **One file**: `index.html` with inline CSS and vanilla JavaScript. No frameworks, no build step, no backend
- **AI**: Google Gemini API (`generateContent`) called directly from the browser, with a system instruction for the persona and `responseMimeType: "application/json"` for structured output
- **Voice**: Addis AI text-to-speech (Amharic, `voice/generations` API) with the browser's Web Speech API as fallback
- **3D**: three.js from a CDN
- **Design**: pure CSS, including the tibeb-style woven border and all animations
- **Hosting**: any static host (Netlify drag and drop)

The model name is a single constant (`MODEL`) at the top of the script.

## Responsible design

- **Roasts choices, never identity.** The system prompt forbids jokes about body, looks, ethnicity, region, or religion, and bans profanity and cruelty. The humor comes from love.
- **Serious confessions get a serious answer.** If a confession sounds like self-harm, abuse, or a crisis, mom drops the comedy completely, responds with warmth, encourages the person to talk to someone they trust, and sets disappointment to 0. The offline mode has the same safeguard.
- **No API keys in the code.** The Gemini and Addis AI keys are pasted into a settings field and stored only in that browser's localStorage. For a production version the keys would move behind a small server proxy. Nothing is committed to the repository.
- **Offline fallback.** The app degrades gracefully and labels offline replies with a visible badge, so users know when they are not talking to the live model.
- **No data collection.** No backend, no analytics, no stored conversations.

## Future work

- Amharic versions of the offline replies, so the Amharic voice works with no connection to the LLM
- Afaan Oromoo and Tigrinya moms
- A Telegram bot version, where Ethiopia's group chats already live
- "Habesha Dad AI", who only says "ishi" and keeps watching the news

## Run it

Open `index.html` in a browser. Paste a Gemini API key in Settings for live mom, or skip it and talk to offline mom.
