# Speech UI

Browser-based test interface for the homelab Speech Node — Whisper STT and CoquiTTS TTS APIs.

Deployed on Delivery VM via Dokploy (Nixpacks). Calls APIs on Speech LXC (192.168.1.202).

## Access

```
http://speech-test.traefik.me                  (current)
http://delivery.lan:3000                       (local)
https://speech-ui.hlab.codepilot.cl            (via NPM, once configured)
```

## Speech API Endpoints (Speech LXC)

```
http://speech.lan:8000   Whisper STT
http://speech.lan:5002   CoquiTTS TTS
```

## Deploy

### 1. Dokploy — connect repo (one-time)

1. Dokploy UI → **New Application** → **Git Provider**
2. Repo: `esgabo/speech-ui`
3. Build type: **Nixpacks**
4. Port: `3000`
5. Enable **Auto-deploy on push**
6. Deploy

### 2. Configure NPM

Add a proxy host in NPM:
- **Domain:** `speech-ui.hlab.codepilot.cl`
- **Forward to:** Delivery VM (192.168.x.101), port `3000`
- **SSL:** Let's Encrypt (wildcard)

### 3. Future updates

Push to `main` → Dokploy auto-redeploys.

## Tech Stack

- Nixpacks (Node.js auto-detected)
- `serve` — lightweight static file server
- Static HTML/JS (no build step)
- Calls Whisper and CoquiTTS REST APIs on Speech LXC

## See Also

- [Speech LXC Setup](../homelab/docs/nodes/speech-lxc102.md)
- [AI Services Docs](../homelab/docs/services/ai/)
