# VTON — Virtual Try-On with Gemini

See yourself wearing any piece of clothing — instantly, for free, directly in your browser.

No app to install. No account needed (other than a free Google one). Your photos never leave your device.

---

## What it does

Upload a photo of yourself and a photo of any garment. The AI replaces your clothing with the new piece while keeping your face, hair, pose, and background exactly the same.

**Powered by Google's Gemini 3.1 Flash Image model.**

---

## Quick start (3 steps)

### Step 1 — Get a free Google API key

1. Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Sign in with your Google account
3. Click **"Create API key"** → select any project (or create one named "vton")
4. Copy the key that appears — it looks like: `AIzaSy...` or `AQ.Ab8R...`

> **Free tier:** Google AI Studio gives you plenty of free requests per day. You will not be charged for normal use.

---

### Step 2 — Open the app

**Option A — Double-click (simplest, may need Option B on some computers)**

Just open `index.html` in your browser by double-clicking it.

**Option B — Local server (recommended, always works)**

Open your terminal and run:

```bash
cd /path/to/vton-gemini
python3 -m http.server 8080
```

Then open your browser and go to: **http://localhost:8080**

> If you're on Windows and don't have Python, download it from [python.org](https://python.org) — it's free and takes 2 minutes.

---

### Step 3 — Use the app

1. Click the **⚙ API Key** section at the top and paste your key → click **Save**
   - Your key is stored only in your browser. It's never sent to any server other than Google's.
2. Click the left zone and upload **your photo** (full or half body, good lighting)
3. Click the right zone and upload **the garment photo** (ideally on a white background)
4. Click **"Try it on →"**
5. Wait ~10–20 seconds for the result
6. Click **"⬇ Download result"** to save the image

---

## Tips for best results

| Do this | Avoid this |
|---|---|
| Clear, well-lit photo of yourself | Dark or blurry photos |
| Standing straight, facing forward | Extreme angles or poses |
| Garment on a white/neutral background | Garment worn by another person |
| JPEG or PNG images | Very small images (under 300px) |

---

## Changing the AI model

Open `index.html` in a text editor and find this line near the top of the `<script>` block:

```js
const MODEL = "gemini-3.1-flash-image";
```

You can replace it with any of these models available on Google AI Studio:

| Model | Speed | Quality |
|---|---|---|
| `gemini-3.1-flash-image` | Fast | Great (default) |
| `gemini-3-pro-image` | Slower | Best quality |
| `gemini-2.5-flash-image` | Fastest | Good |

---

## How it works (technical)

```
Your browser
    │
    ├─ reads both images as base64 (nothing uploaded to any server)
    │
    └─ sends one HTTPS request to:
         generativelanguage.googleapis.com  (Google's API)
              │
              └─ Gemini 3.1 Flash Image processes both photos
                 and returns the result image
                      │
                      └─ displayed directly in your browser
```

Your photos are sent **only** to Google's API as part of the generation request, and only temporarily. They are not stored. Your API key is stored only in your browser's localStorage.

---

## Privacy

- Your images are sent to Google's Gemini API to generate the result. Review [Google's AI Studio terms](https://ai.google.dev/gemini-api/terms) if you have privacy concerns.
- Your API key is saved in your browser's localStorage. It is never sent anywhere except Google's API endpoint.
- This project has no backend, no analytics, no tracking of any kind.

---

## Troubleshooting

**"Invalid API key" error**
→ Re-copy your key from [aistudio.google.com/apikey](https://aistudio.google.com/apikey). Make sure there are no extra spaces.

**CORS error / Network error**
→ Use Option B (local server). Open your terminal and run `python3 -m http.server 8080`, then go to `http://localhost:8080`.

**"No image returned"**
→ The model may have declined to generate an image due to the content. Try with a clearer photo or a different garment.

**Slow or no response**
→ Check your internet connection. The API call can take 10–25 seconds depending on image size.

---

## License

MIT — free to use, modify, and distribute.
