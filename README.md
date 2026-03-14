# Speech UI

Browser-based test interface for the homelab Speech Node — Whisper STT and CoquiTTS TTS APIs.

Deployed on Delivery VM via Dokploy. Calls APIs on Speech LXC (192.168.1.202).

## Access

```
http://delivery.lan:8888/speech-test.html      (local)
https://speech-ui.hlab.codepilot.cl            (via NPM, once configured)
```

## Speech API Endpoints (Speech LXC)

```
http://192.168.1.202:8000   Whisper STT
http://192.168.1.202:5002   CoquiTTS TTS
```

## Setup

### 1. Add speech-test.html

Copy the HTML file from the Speech LXC and update the default API URLs:

```bash
scp root@192.168.1.202:/opt/whisper-tts/speech-test.html .
```

Then open `speech-test.html` and update the default API URL values to point to the Speech node:

```
WHISPER_API_URL = http://192.168.1.202:8000
TTS_API_URL     = http://192.168.1.202:5002
```

### 2. Push to GitHub

```bash
git init
git remote add origin git@github.com:esgabo/speech-ui.git
git add .
git commit -m "Initial speech UI deployment"
git push -u origin main
```

### 3. Deploy via Dokploy

1. In Dokploy UI → **New Application** → **Git Provider**
2. Connect repo `esgabo/speech-ui`
3. Build type: **Dockerfile**
4. Port: `8888`
5. Deploy

### 4. Configure NPM

Add a proxy host in NPM:
- **Domain:** `speech-ui.hlab.codepilot.cl`
- **Forward to:** `delivery.lan` (or `192.168.x.101`), port `8888`
- **SSL:** Let's Encrypt (wildcard)

## Tech Stack

- nginx:alpine
- Static HTML/JS (no build step)
- Calls Whisper and CoquiTTS REST APIs on Speech LXC

## See Also

- [Speech LXC Setup](../homelab/docs/nodes/speech-lxc102.md)
- [AI Services Docs](../homelab/docs/services/ai/)
