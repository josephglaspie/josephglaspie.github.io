# Joseph Glaspie - Professional Resume

A modern, responsive resume website built with multi-agent architecture and deployed on GitHub Pages.

## Features

- 🎨 Professional, clean design
- 📱 Fully responsive (mobile, tablet, desktop)
- 🖨️ Print-optimized for PDF generation
- ♿ WCAG AA accessible
- ⚡ Fast loading (<1s page load)
- 🎯 Zero dependencies (vanilla HTML/CSS/JS)
- 🚀 Automated GitHub Pages deployment

## Quick Start

### View Live Site

Visit: `https://[your-username].github.io/agents/`

### Local Development

```bash
# Clone the repository
git clone https://github.com/[your-username]/agents.git
cd agents

# Open in browser
open docs/index.html
# or use a local server
python3 -m http.server 8000 --directory docs
```

## Multi-Agent Architecture

This project uses coordinating agents that work together to build and maintain the resume site.

See `agents/README.md` for detailed agent coordination protocols.

## Project Structure

```
.
├── agents/              # Multi-agent system definitions
├── docs/               # GitHub Pages site
│   ├── index.html     # Main resume page
│   ├── css/           # Stylesheets
│   └── js/            # JavaScript
└── .github/
    └── workflows/
        └── deploy.yml # Automated deployment
```

## Contact

- Email: joseph@glaspie.us
- Location: Whitehouse, TX

Built with ❤️ using a multi-agent architecture
# resume
