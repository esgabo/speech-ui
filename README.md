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

## Deploy

### 1. Dokploy — connect repo (one-time)

1. Dokploy UI → **New Application** → **Git Provider**
2. Repo: `esgabo/speech-ui`
3. Build type: **Dockerfile**
4. Port: `8888`
5. Enable **Auto-deploy on push** (Dokploy watches the repo directly — no Woodpecker needed)
6. Deploy

### 2. Configure NPM

Add a proxy host in NPM:
- **Domain:** `speech-ui.hlab.codepilot.cl`
- **Forward to:** Delivery VM (192.168.x.101), port `8888`
- **SSL:** Let's Encrypt (wildcard)

### 3. Future updates

Push to `main` → Dokploy auto-redeploys.

## Tech Stack

- nginx:alpine
- Static HTML/JS (no build step)
- Calls Whisper and CoquiTTS REST APIs on Speech LXC

## See Also

- [Speech LXC Setup](../homelab/docs/nodes/speech-lxc102.md)
- [AI Services Docs](../homelab/docs/services/ai/)
