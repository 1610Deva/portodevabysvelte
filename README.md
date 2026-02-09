# PortoDeva - Portfolio Website

A modern, responsive portfolio website built with **Svelte** and **SvelteKit**, featuring a sleek dark theme with interactive particle animations.

## ✨ Features

- 🎨 **Modern Design** - Glass-morphism cards with smooth animations
- 📱 **Fully Responsive** - Mobile-first approach with Tailwind CSS
- ✨ **Interactive Animations** - Particle.js background effects
- 🌙 **Dark Theme** - Eye-friendly dark mode by default
- 📊 **Dynamic Content** - Data-driven project and experience sections
- ⚡ **Fast & Optimized** - Built with SvelteKit for optimal performance

## 🚀 Getting Started

### Prerequisites
- Node.js 16+ installed
- npm, pnpm, or yarn package manager

### Installation

```sh
# Clone the repository
git clone <repository-url>
cd portodevadatta-sv

# Install dependencies
npm install
```

### Development Server

Start the development server:

```sh
npm run dev

# or open automatically in browser
npm run dev -- --open
```

The app will be available at `http://localhost:5173`

### Production Build

```sh
npm run build
```

Preview the production build:

```sh
npm run preview
```

## 📁 Project Structure

```
src/
├── routes/
│   ├── +layout.svelte       # Main layout with navbar
│   ├── +page.svelte         # Home page
│   ├── about/
│   │   └── +page.svelte     # About page
│   ├── projects/
│   │   └── +page.svelte     # Projects page
│   └── contact/
│       └── +page.svelte     # Contact page
├── lib/
│   ├── assets/              # Images, icons, favicon
│   └── components/          # Reusable components
└── app.html                 # HTML template

static/
├── data/
│   └── data.json            # Portfolio data
└── particlesjs.json         # Particle.js config
```

## 🛠️ Tech Stack

- **Framework**: [SvelteKit](https://kit.svelte.dev/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **Icons**: [Font Awesome](https://fontawesome.com/)
- **Animations**: [Particles.js](https://particles.js.org/)
- **Language**: TypeScript

## 📖 Pages

- **Home** - Introduction and featured projects
- **About** - Bio, skills, experience, and education
- **Projects** - Detailed portfolio projects
- **Contact** - Get in touch section

## 🎯 Customization

### Update Your Information
Edit `static/data/data.json` with your projects, skills, and experience.

### Modify Colors
Update Tailwind colors in `tailwind.config.js`

### Change Particle Effects
Customize `static/particlesjs.json` for different animation styles

## 📦 Dependencies

Key dependencies included:
- svelte
- sveltekit
- tailwindcss
- font-awesome
- particles.js

## 📝 License

© 2026 Devadatta Giri. All rights reserved.

## 🤝 Connect

- [LinkedIn](https://www.linkedin.com/in/devadattagiri/)
- [GitHub](https://github.com/1610Deva)

---

**Built with ❤️ using SvelteKit**