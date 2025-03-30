# AI Sync

A collaborative drawing application powered by Google's Gemini 2.0

## 🎨 Project Overview

AI Sync is a collaborative drawing application that leverages Google's Gemini 2.0 API for real-time image generation. Draw with friends and let AI enhance your creations based on text prompts, making artistic collaboration more accessible and creative than ever before.

### Key Features

- **Collaborative Canvas** - Real-time drawing with multiple participants on the same canvas
- **Gemini 2.0 AI** - AI image generation and enhancement powered by Google's latest API
- **Customization** - Adjustable brushes, colors, and styles for your artistic vision
- **AI Enhancements** - Use text prompts to guide AI in improving your drawings

**Tags:** `AI Art` `Collaboration` `Google Gemini` `Next.js`

## 🚀 Try It Out

Experience AI Sync live in your browser through our hosted versions:

- [GitHub Pages](https://b-aragu.github.io/ArtSync/)
- [Hugging Face Space](https://huggingface.co/spaces/Trudy/gemini-codrawing)

## 🔧 Getting Started

### Prerequisites
- Node.js 14+
- npm or yarn
- Google API key for Gemini 2.0

### Installation

```bash
git clone git@hf.co:spaces/Trudy/gemini-codrawing
```

### Quick Start

```bash
# Clone the repository
git clone git@hf.co:spaces/Trudy/gemini-codrawing
cd gemini-codrawing

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Run the development server
npm run dev
```

### Environment Setup

```
# Required environment variables
NEXT_PUBLIC_GEMINI_API_KEY=your_api_key_here
NEXT_PUBLIC_BASE_URL=http://localhost:3000

# Optional variables for advanced configuration
NEXT_PUBLIC_COLLAB_SERVER=wss://your-socket-server
NEXT_PUBLIC_MAX_USERS=10
NEXT_PUBLIC_DEFAULT_PROMPT="Make this drawing more realistic"
```

### Running Locally

```bash
# After installation

# Development mode (hot reload)
npm run dev

# Production build
npm run build

# Start production server
npm run start

# Or run via PM2
pm2 start npm --name "ai-sync" -- start
```

## ⚙️ Technology Stack

- **Next.js** - Frontend framework
- **Gemini 2.0** - AI Image API
- **React** - UI Components
- **Node.js** - Backend Runtime

### Project Structure

```
ai-sync/
├── public/            # Static assets
├── src/
│   ├── components/    # React components
│   ├── pages/         # Next.js pages
│   ├── lib/           # Utility functions
│   ├── hooks/         # Custom React hooks
│   ├── styles/        # Global styles
│   └── store/         # State management
├── .env.example       # Environment template
├── next.config.js     # Next.js configuration
└── package.json       # Dependencies
```

## 🤝 Contributing

We welcome contributions from the community! Here's how you can help improve AI Sync:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Suggested Improvements

- Add more brush types and drawing tools
- Implement better user presence indicators
- Add AI prompt suggestions
- Improve mobile responsiveness

---

Created by [b-aragu](https://github.com/b-aragu)

- [GitHub Repository](https://github.com/b-aragu/ArtSync)
- [Hugging Face Space](https://huggingface.co/spaces/Trudy/gemini-codrawing)
- [Live Demo](https://b-aragu.github.io/ArtSync/)
