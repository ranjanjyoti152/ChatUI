# Chat UI

<p align="center">
  <img src="static/static/logo.png" alt="Chat UI Logo" width="200">
</p>

A powerful, self-hosted AI chat interface with support for multiple LLM providers including OpenAI, Ollama, Google Gemini, Anthropic Claude, and image generation via ComfyUI.

## ✨ Features

- 🤖 **Multi-Provider Support**: Connect to OpenAI, Ollama, Gemini, Anthropic, and more
- 🎨 **Image Generation**: Built-in support for ComfyUI, Automatic1111, and OpenAI DALL-E with real-time progress tracking
- 🔍 **Web Search**: Integrated web search capabilities
- 📁 **File Upload**: Upload and analyze documents, images, and code files
- 💬 **Multi-Model Chat**: Chat with multiple models simultaneously
- 🎙️ **Voice Input**: Speech-to-text for hands-free chatting
- 📝 **Markdown Support**: Rich text formatting with code highlighting
- 🔒 **Self-Hosted**: Complete privacy control - your data stays on your server

---

## 🐳 Docker Deployment (Recommended)

### Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/chat-ui.git
cd chat-ui

# Copy environment file and configure
cp env.chat-ui.example .env
# Edit .env and set WEBUI_SECRET_KEY

# Build and start
docker-compose -f docker-compose.chat-ui.yaml up -d --build
```

🎉 **Access Chat UI at** `http://localhost:3000`

### Services

| Service | Description | Port |
|---------|-------------|------|
| `chat-ui` | Main application | 3000 → 8080 |
| `ollama` | Local LLM service | 11434 (internal) |

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `CHAT_UI_PORT` | External port | `3000` |
| `WEBUI_SECRET_KEY` | JWT secret key (change this!) | - |
| `OLLAMA_DOCKER_TAG` | Ollama image version | `latest` |
| `CORS_ALLOW_ORIGIN` | CORS origin (set domain for production) | `*` |

> **📝 Note**: API keys for LLM providers (OpenAI, Gemini, Anthropic) and image generation (ComfyUI) can be configured in the UI:
> - **Settings → Connections** (for LLM providers)
> - **Admin Panel → Settings → Images** (for image generation)

### GPU Support (NVIDIA)

Uncomment the GPU section in `docker-compose.chat-ui.yaml`:

```yaml
ollama:
  deploy:
    resources:
      reservations:
        devices:
          - driver: nvidia
            count: all
            capabilities: [gpu]
```

### Docker Commands

```bash
# Start services
docker-compose -f docker-compose.chat-ui.yaml up -d

# View logs
docker logs chat-ui -f

# Stop services
docker-compose -f docker-compose.chat-ui.yaml down

# Rebuild after changes
docker-compose -f docker-compose.chat-ui.yaml up -d --build
```

---

## 💻 Local Development

### Prerequisites

- **Python 3.11+**
- **Node.js 18.x - 22.x**
- **npm**

### Backend Setup

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
.\venv\Scripts\activate

# Activate (Linux/macOS)
source venv/bin/activate

# Install dependencies
cd backend
pip install -r requirements.txt

# Start backend
.\start_windows.bat  # Windows
./start.sh           # Linux/macOS
```

### Frontend Development

```bash
# Install dependencies
npm install --legacy-peer-deps

# Development server (hot reload)
npm run dev

# Production build
npm run build
```

---

## 🔧 Configuration

### Adding LLM Providers

1. Go to **Settings** → **Connections**
2. Add your API keys for:
   - OpenAI
   - Ollama (local)
   - Google Gemini
   - Anthropic Claude

### Image Generation Setup

1. Go to **Admin Panel** → **Settings** → **Images**
2. Enable image generation
3. Select your engine:
   - **ComfyUI**: Local Stable Diffusion with real-time progress
   - **Automatic1111**: Alternative Stable Diffusion interface
   - **OpenAI**: DALL-E models
   - **Gemini**: Google's Imagen

---

## 📁 Project Structure

```
chat-ui/
├── backend/                     # Python backend (FastAPI)
│   ├── open_webui/
│   │   ├── routers/            # API endpoints
│   │   ├── utils/              # Utilities & middleware
│   │   └── main.py             # Entry point
│   └── requirements.txt
├── src/                         # Svelte frontend
│   ├── lib/
│   │   ├── components/         # UI components
│   │   ├── apis/               # API clients
│   │   └── stores/             # State management
│   └── app.html
├── static/                      # Static assets (logos, icons)
├── docker-compose.chat-ui.yaml  # Docker deployment
├── env.chat-ui.example          # Environment template
└── Dockerfile
```

---

## 🔐 Security Best Practices

| Recommendation | Description |
|---------------|-------------|
| **Secret Key** | Always set a strong `WEBUI_SECRET_KEY` |
| **CORS** | Set `CORS_ALLOW_ORIGIN` to your domain in production |
| **HTTPS** | Use a reverse proxy (nginx, Traefik) for SSL |
| **Network** | Restrict access with firewall rules |

---

## 📄 License

This project is licensed under the MIT License.
