<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Stnc - Collaborative Drawing App</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #8b5cf6;
            --secondary: #a78bfa;
            --background: #f8fafc;
            --text: #1e293b;
            --accent: #f59e0b;
            --card: #ffffff;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            --creative: #34d399;
        }

        .dark-theme {
            --primary: #a78bfa;
            --secondary: #7c3aed;
            --background: #1e293b;
            --text: #f8fafc;
            --accent: #fbbf24;
            --card: #334155;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.4);
            --creative: #10b981;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            transition: background-color 0.3s, color 0.3s, transform 0.2s;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--background);
            color: var(--text);
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 2px dashed var(--secondary);
        }

        h1 {
            font-size: 2.5rem;
            color: var(--primary);
            margin-bottom: 10px;
            position: relative;
            display: inline-block;
        }

        h1 span {
            color: var(--creative);
        }

        h1::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--creative), var(--accent));
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 0.3s ease;
        }

        h1:hover::after {
            transform: scaleX(1);
        }

        h2 {
            font-size: 1.8rem;
            color: var(--primary);
            margin: 25px 0 15px;
            padding-bottom: 5px;
            border-bottom: 1px solid var(--secondary);
        }

        h3 {
            font-size: 1.4rem;
            color: var(--accent);
            margin: 20px 0 10px;
        }

        p {
            margin-bottom: 15px;
        }

        a {
            color: var(--primary);
            text-decoration: none;
            font-weight: 500;
        }

        a:hover {
            text-decoration: underline;
            color: var(--secondary);
        }

        .badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            background-color: var(--secondary);
            color: white;
            margin-right: 8px;
            margin-bottom: 8px;
        }

        .badge-creative {
            background-color: var(--creative);
        }

        .theme-toggle {
            background: var(--card);
            border: none;
            color: var(--text);
            padding: 8px 15px;
            border-radius: 25px;
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            box-shadow: var(--shadow);
        }

        .theme-toggle:hover {
            transform: translateY(-2px);
        }

        .theme-toggle i {
            font-size: 1.2rem;
        }

        .card {
            background-color: var(--card);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
            border-left: 4px solid var(--accent);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }

        .feature-item {
            background-color: var(--card);
            padding: 20px;
            border-radius: 8px;
            box-shadow: var(--shadow);
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        .feature-icon {
            font-size: 2rem;
            color: var(--accent);
            margin-bottom: 15px;
        }

        .feature-icon.creative {
            color: var(--creative);
        }

        code {
            background-color: rgba(165, 180, 252, 0.2);
            padding: 2px 6px;
            border-radius: 4px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.9rem;
            color: var(--primary);
        }

        pre {
            background-color: rgba(165, 180, 252, 0.2);
            padding: 15px;
            border-radius: 8px;
            overflow-x: auto;
            margin: 20px 0;
            border-left: 3px solid var(--primary);
        }

        .command {
            background-color: rgba(245, 158, 11, 0.1);
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .command i {
            color: var(--accent);
        }

        .tabs {
            display: flex;
            margin-bottom: -1px;
        }

        .tab {
            padding: 10px 20px;
            background-color: var(--card);
            border: 1px solid var(--secondary);
            border-bottom: none;
            border-radius: 8px 8px 0 0;
            cursor: pointer;
            margin-right: 5px;
        }

        .tab.active {
            background-color: var(--primary);
            color: white;
        }

        .tab-content {
            display: none;
            padding: 20px;
            background-color: var(--card);
            border: 1px solid var(--secondary);
            border-radius: 0 8px 8px 8px;
        }

        .tab-content.active {
            display: block;
        }

        .pill {
            display: inline-flex;
            align-items: center;
            padding: 4px 12px;
            background-color: var(--secondary);
            color: white;
            border-radius: 50px;
            font-size: 0.8rem;
            margin-right: 8px;
            margin-bottom: 8px;
        }

        .pill i {
            margin-right: 5px;
            font-size: 0.7rem;
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px dashed var(--secondary);
            color: var(--secondary);
        }

        .demo-frame {
            width: 100%;
            height: 400px;
            border: 1px solid var(--secondary);
            border-radius: 8px;
            overflow: hidden;
            margin: 20px 0;
        }

        @media (max-width: 768px) {
            .feature-grid {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2rem;
            }
        }

        /* Animation classes */
        .animate-pop {
            animation: pop 0.5s ease;
        }

        @keyframes pop {
            0% { transform: scale(0.95); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .animate-float {
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0); }
        }

        /* Scroll indicator */
        .scroll-indicator {
            position: fixed;
            top: 0;
            left: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--creative), var(--accent));
            z-index: 100;
        }
    </style>
</head>
<body>
    <div class="scroll-indicator" id="scrollIndicator"></div>
    <div class="container">
        <header>
            <div>
                <h1 id="projectTitle" class="animate-float">AI <span>Sync</span></h1>
                <p id="taglineText">A collaborative drawing application powered by Google's Gemini 2.0</p>
            </div>
            <button class="theme-toggle" id="themeToggle">
                <i class="fas fa-moon"></i>
                <span>Dark Mode</span>
            </button>
        </header>

        <div class="card">
            <h2 id="overviewHead">🎨 Project Overview</h2>
            <p id="overviewText">AI Stnc is a collaborative drawing application that leverages Google's Gemini 2.0 API for real-time image generation. Draw with friends and let AI enhance your creations based on text prompts, making artistic collaboration more accessible and creative than ever before.</p>
            
            <div class="feature-grid">
                <div class="feature-item animate-pop">
                    <div class="feature-icon creative">
                        <i class="fas fa-paint-brush"></i>
                    </div>
                    <h3>Collaborative Canvas</h3>
                    <p>Real-time drawing with multiple participants on the same canvas</p>
                </div>
                <div class="feature-item animate-pop" style="animation-delay: 0.1s">
                    <div class="feature-icon">
                        <i class="fas fa-robot"></i>
                    </div>
                    <h3>Gemini 2.0 AI</h3>
                    <p>AI image generation and enhancement powered by Google's latest API</p>
                </div>
                <div class="feature-item animate-pop" style="animation-delay: 0.2s">
                    <div class="feature-icon">
                        <i class="fas fa-sliders-h"></i>
                    </div>
                    <h3>Customization</h3>
                    <p>Adjustable brushes, colors, and styles for your artistic vision</p>
                </div>
                <div class="feature-item animate-pop" style="animation-delay: 0.3s">
                    <div class="feature-icon creative">
                        <i class="fas fa-magic"></i>
                    </div>
                    <h3>AI Enhancements</h3>
                    <p>Use text prompts to guide AI in improving your drawings</p>
                </div>
            </div>

            <div>
                <span class="badge creative">AI Art</span>
                <span class="badge">Collaboration</span>
                <span class="badge">Google Gemini</span>
                <span class="badge">Next.js</span>
            </div>
        </div>

        <div class="card">
            <h2>🚀 Try It Out</h2>
            <p>Experience AI Stnc live in your browser through our hosted versions:</p>
            
            <div style="display: flex; gap: 15px; margin: 20px 0;">
                <a href="https://b-aragu.github.io/ArtSync/" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: var(--primary); color: white; border-radius: 8px; text-decoration: none;">
                    <i class="fas fa-external-link-alt"></i> GitHub Pages
                </a>
                <a href="https://huggingface.co/spaces/Trudy/gemini-codrawing" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: var(--primary); color: white; border-radius: 8px; text-decoration: none;">
                    <i class="fas fa-brain"></i> Hugging Face Space
                </a>
            </div>

            <div class="demo-frame">
                <iframe src="https://b-aragu.github.io/ArtSync/" style="width: 100%; height: 100%; border: none;"></iframe>
            </div>
        </div>

        <div class="card">
            <h2>🔧 Getting Started</h2>
            <h3>Prerequisites</h3>
            <ul style="margin-left: 20px; margin-bottom: 15px;">
                <li>Node.js 14+</li>
                <li>npm or yarn</li>
                <li>Google API key for Gemini 2.0</li>
            </ul>

            <h3>Installation</h3>
            <div class="command">
                <i class="fas fa-terminal"></i>
                <code>git clone git@hf.co:spaces/Trudy/gemini-codrawing</code>
            </div>

            <div class="tabs">
                <div class="tab active" onclick="switchTab(event, 'quickstart')">Quick Start</div>
                <div class="tab" onclick="switchTab(event, 'env')">Environment Setup</div>
                <div class="tab" onclick="switchTab(event, 'run')">Running Locally</div>
            </div>

            <div class="tab-content active" id="quickstart">
                <pre><code># Clone the repository
git clone git@hf.co:spaces/Trudy/gemini-codrawing
cd gemini-codrawing

# Install dependencies
npm install

# Set up environment variables (see next tab)
cp .env.example .env.local

# Run the development server
npm run dev</code></pre>
            </div>

            <div class="tab-content" id="env">
                <pre><code># Required environment variables
NEXT_PUBLIC_GEMINI_API_KEY=your_api_key_here
NEXT_PUBLIC_BASE_URL=http://localhost:3000

# Optional variables for advanced configuration
NEXT_PUBLIC_COLLAB_SERVER=wss://your-socket-server
NEXT_PUBLIC_MAX_USERS=10
NEXT_PUBLIC_DEFAULT_PROMPT="Make this drawing more realistic"</code></pre>
            </div>

            <div class="tab-content" id="run">
                <pre><code># After installation

# Development mode (hot reload)
npm run dev

# Production build
npm run build

# Start production server
npm run start

# Or run via PM2
pm2 start npm --name "ai-stnc" -- start</code></pre>
            </div>
        </div>

        <div class="card">
            <h2>⚙️ Technology Stack</h2>
            <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 15px; margin: 20px 0;">
                <div class="feature-item" style="padding: 15px;">
                    <div>
                        <img src="https://upload.wikimedia.org/wikipedia/commons/8/8e/Nextjs-logo.svg" alt="Next.js" style="height: 30px; margin-bottom: 10px; filter: invert(36%) sepia(71%) saturate(1311%) hue-rotate(227deg) brightness(96%) contrast(93%);">
                    </div>
                    <h4>Next.js</h4>
                    <p style="font-size: 0.8rem;">Frontend framework</p>
                </div>
                <div class="feature-item" style="padding: 15px;">
                    <div>
                        <img src="https://upload.wikimedia.org/wikipedia/commons/d/db/Google_AI_Logo.svg" alt="Google Gemini" style="height: 30px; margin-bottom: 10px;">
                    </div>
                    <h4>Gemini 2.0</h4>
                    <p style="font-size: 0.8rem;">AI Image API</p>
                </div>
                <div class="feature-item" style="padding: 15px;">
                    <div>
                        <i class="fab fa-react" style="font-size: 30px; color: var(--primary); margin-bottom: 10px;"></i>
                    </div>
                    <h4>React</h4>
                    <p style="font-size: 0.8rem;">UI Components</p>
                </div>
                <div class="feature-item" style="padding: 15px;">
                    <div>
                        <i class="fab fa-node-js" style="font-size: 30px; color: var(--creative); margin-bottom: 10px;"></i>
                    </div>
                    <h4>Node.js</h4>
                    <p style="font-size: 0.8rem;">Backend Runtime</p>
                </div>
            </div>

            <h3>Project Structure</h3>
            <pre><code>ai-sync/
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
└── package.json       # Dependencies</code></pre>
        </div>

        <div class="card">
            <h2>📝 Live Preview Editor</h2>
            <p>Customize your README in real-time with this editor:</p>
            
            <div style="margin-bottom: 15px;">
                <label for="liveProjectName">Project Name:</label>
                <input type="text" id="liveProjectName" value="AI Stnc" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--secondary); background: var(--card); color: var(--text); margin-top: 5px;">
            </div>
            
            <div style="margin-bottom: 15px;">
                <label for="liveTagline">Tagline:</label>
                <input type="text" id="liveTagline" value="A collaborative drawing application powered by Google's Gemini 2.0" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--secondary); background: var(--card); color: var(--text); margin-top: 5px;">
            </div>
            
            <div style="margin-bottom: 15px;">
                <label for="liveOverview">Project Overview:</label>
                <textarea id="liveOverview" rows="5" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--secondary); background: var(--card); color: var(--text); margin-top: 5px;">AI Stnc is a collaborative drawing application that leverages Google's Gemini 2.0 API for real-time image generation. Draw with friends and let AI enhance your creations based on text prompts, making artistic collaboration more accessible and creative than ever before.</textarea>
            </div>
            
            <div style="margin-bottom: 15px;">
                <label for="liveFeatures">Key Features (comma separated):</label>
                <input type="text" id="liveFeatures" value="Collaborative Canvas, Gemini 2.0 AI, Customization, AI Enhancements" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--secondary); background: var(--card); color: var(--text); margin-top: 5px;">
            </div>
        </div>

        <div class="card">
            <h2>🤝 Contributing</h2>
            <p>We welcome contributions from the community! Here's how you can help improve AI Stnc:</p>
            
            <div class="command">
                <i class="fas fa-code-branch"></i>
                <code>1. Fork the repository</code>
            </div>
            
            <div class="command">
                <i class="fas fa-code"></i>
                <code>2. Create your feature branch (git checkout -b feature/AmazingFeature)</code>
            </div>
            
            <div class="command">
                <i class="fas fa-save"></i>
                <code>3. Commit your changes (git commit -m 'Add some AmazingFeature')</code>
            </div>
            
            <div class="command">
                <i class="fas fa-cloud-upload-alt"></i>
                <code>4. Push to the branch (git push origin feature/AmazingFeature)</code>
            </div>
            
            <div class="command">
                <i class="fas fa-pull-request"></i>
                <code>5. Open a Pull Request</code>
            </div>

            <h3>Suggested Improvements</h3>
            <ul style="margin-left: 20px; margin-bottom: 15px;">
                <li>Add more brush types and drawing tools</li>
                <li>Implement better user presence indicators</li>
                <li>Add AI prompt suggestions</li>
                <li>Improve mobile responsiveness</li>
            </ul>
        </div>

        <div class="footer">
            <p><i class="fas fa-palette" style="color: var(--creative);"></i> Created by <a href="https://github.com/b-aragu" target="_blank">b-aragu</a></p>
            <p>
                <a href="https://github.com/b-aragu/ArtSync" target="_blank" style="margin: 0 10px;"><i class="fab fa-github"></i> GitHub Repository</a>
                <a href="https://huggingface.co/spaces/Trudy/gemini-codrawing" target="_blank" style="margin: 0 10px;"><i class="fas fa-brain"></i> Hugging Face Space</a>
                <a href="https://b-aragu.github.io/ArtSync/" target="_blank" style="margin: 0 10px;"><i class="fas fa-external-link-alt"></i> Live Demo</a>
            </p>
            <p style="margin-top: 15px; font-size: 0.9rem; color: var(--secondary);">
                License: MIT
            </p>
        </div>
    </div>

    <script>
        // Theme toggle functionality
        const themeToggle = document.getElementById('themeToggle');
        const body = document.body;
        
        themeToggle.addEventListener('click', () => {
            body.classList.toggle('dark-theme');
            
            if (body.classList.contains('dark-theme')) {
                themeToggle.innerHTML = '<i class="fas fa-sun"></i><span>Light Mode</span>';
            } else {
                themeToggle.innerHTML = '<i class="fas fa-moon"></i><span>Dark Mode</span>';
            }
        });

        // Tab switching functionality
        function switchTab(event, tabId) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // Remove active class from all tabs
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Show selected tab content
            document.getElementById(tabId).classList.add('active');
            
            // Add active class to clicked tab
            event.currentTarget.classList.add('active');
        }

        // Live preview functionality
        const liveProjectName = document.getElementById('liveProjectName');
        const liveTagline = document.getElementById('liveTagline');
        const liveOverview = document.getElementById('liveOverview');
        const liveFeatures = document.getElementById('liveFeatures');
        const projectTitle = document.getElementById('projectTitle');
        const taglineText = document.getElementById('taglineText');
        const overviewText = document.getElementById('overviewText');
        
        liveProjectName.addEventListener('input', () => {
            projectTitle.innerHTML = liveProjectName.value.replace('AI', '<span>AI</span>').replace('Stnc', '<span>Stnc</span>');
            projectTitle.classList.add('animate-pop');
            setTimeout(() => {
                projectTitle.classList.remove('animate-pop');
            }, 500);
        });
        
        liveTagline.addEventListener('input', () => {
            taglineText.textContent = liveTagline.value;
        });
        
        liveOverview.addEventListener('input', () => {
            overviewText.textContent = liveOverview.value;
        });

        // Scroll indicator
        window.addEventListener('scroll', () => {
            const scrollable = document.documentElement.scrollHeight - window.innerHeight;
            const scrolled = window.scrollY;
            const scrollPercentage = (scrolled / scrollable) * 100;
            document.getElementById('scrollIndicator').style.width = `${scrollPercentage}%`;
        });

        // Demo iframe interaction
        const demoFrame = document.querySelector('.demo-frame');
        demoFrame.addEventListener('mouseenter', () => {
            demoFrame.style.boxShadow = `0 0 0 2px var(--creative)`;
        });
        demoFrame.addEventListener('mouseleave', () => {
            demoFrame.style.boxShadow = 'none';
        });
    </script>
</body>
</html>
