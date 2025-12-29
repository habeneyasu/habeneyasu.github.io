# Haben Eyasu Akelom - Portfolio Website

> Professional portfolio website showcasing expertise in Software Engineering, FinTech Systems, and AI/ML Solutions

[![Portfolio](https://img.shields.io/badge/Portfolio-Live-brightgreen)](https://habeneyasu.github.io)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-blue)](https://pages.github.com)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🌐 Live Demo

**Visit the live portfolio:** [habeneyasu.github.io](https://habeneyasu.github.io)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Deployment](#deployment)
- [Performance](#performance)
- [Accessibility](#accessibility)
- [Browser Support](#browser-support)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## 🎯 Overview

This is a modern, responsive portfolio website designed to showcase professional experience, technical skills, and project portfolio. The site emphasizes both Software Engineering expertise and AI/ML capabilities, making it ideal for senior engineering roles and AI training programs.

### Key Highlights

- **8+ years** of software engineering experience
- **50M+ transactions** processed in production systems
- **99.8% uptime** achieved in financial systems
- Expertise in **FinTech**, **Microservices**, and **AI/ML Solutions**

## ✨ Features

### Core Features

- ✅ **Responsive Design** - Fully responsive across all devices (mobile, tablet, desktop)
- ✅ **Modern UI/UX** - Clean, professional design with smooth animations
- ✅ **SEO Optimized** - Comprehensive meta tags, Open Graph, and Twitter Card support
- ✅ **Accessibility** - WCAG compliant with ARIA labels and semantic HTML
- ✅ **Performance** - Optimized loading with critical CSS and efficient animations
- ✅ **Interactive Elements** - Animated counters, smooth scrolling, mobile navigation
- ✅ **Project Showcase** - Organized display of AI/ML and Software Engineering projects
- ✅ **Contact Integration** - Multiple contact methods with resume download option

### Technical Features

- **Mobile-First Design** - Hamburger menu for mobile navigation
- **Animated Statistics** - Counters animate on scroll using Intersection Observer
- **Project Badges** - Visual indicators for AI/ML vs Software projects
- **Enhanced Visuals** - Gradient effects, hover animations, and visual hierarchy
- **Error Handling** - Graceful fallbacks for all JavaScript features
- **Semantic HTML5** - Proper use of semantic elements and ARIA attributes

## 🛠 Technologies

### Frontend

- **HTML5** - Semantic markup
- **CSS3** - Modern styling with CSS Variables, Flexbox, Grid
- **JavaScript (ES6+)** - Vanilla JS with modern features
- **Google Fonts** - Inter font family

### Tools & Libraries

- **GitHub Pages** - Hosting platform
- **Intersection Observer API** - Scroll-based animations
- **CSS Custom Properties** - Theme management
- **CSS Grid & Flexbox** - Responsive layouts

### Design Principles

- Mobile-first responsive design
- Progressive enhancement
- Accessibility-first approach
- Performance optimization

## 📁 Project Structure

```
habeneyasu.github.io/
├── index.html          # Main HTML file
├── style.css          # Stylesheet with all CSS
├── README.md          # This file
└── .git/              # Git repository
```

### File Organization

- **index.html** - Single-page application with all sections
- **style.css** - Complete stylesheet with:
  - CSS Variables for theming
  - Responsive breakpoints
  - Component-based styling
  - Animation definitions

## 🚀 Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge)
- Git (for cloning the repository)
- GitHub account (for deployment)

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/habeneyasu/habeneyasu.github.io.git
   cd habeneyasu.github.io
   ```

2. **Open in browser**
   ```bash
   # Option 1: Open directly
   open index.html

   # Option 2: Use a local server (recommended)
   python -m http.server 8000
   # Then visit http://localhost:8000
   ```

3. **Make changes**
   - Edit `index.html` for content/structure
   - Edit `style.css` for styling
   - Test in multiple browsers

### Development Tips

- Use a local server to avoid CORS issues
- Test responsive design using browser DevTools
- Validate HTML/CSS using online validators
- Check accessibility with Lighthouse

## 📦 Deployment

### GitHub Pages (Current)

This portfolio is automatically deployed via GitHub Pages:

1. **Repository Setup**
   - Repository name: `habeneyasu.github.io`
   - Branch: `main`
   - Source: `/ (root)`

2. **Automatic Deployment**
   - Push to `main` branch
   - GitHub Pages automatically builds and deploys
   - Site available at `https://habeneyasu.github.io`

3. **Custom Domain (Optional)**
   - Add `CNAME` file with your domain
   - Configure DNS settings
   - Update GitHub Pages settings

### Manual Deployment

```bash
# Build and commit
git add .
git commit -m "Update portfolio"
git push origin main

# GitHub Pages will automatically deploy
```

## ⚡ Performance

### Optimizations Implemented

- **Critical CSS** - Inline critical styles for faster initial render
- **Font Optimization** - Preconnect to Google Fonts
- **Efficient Animations** - CSS transforms and requestAnimationFrame
- **Lazy Loading** - Intersection Observer for scroll-based features
- **Minimal Dependencies** - No external JavaScript libraries

### Performance Metrics

- **Lighthouse Score**: 90+ (Performance, Accessibility, Best Practices, SEO)
- **First Contentful Paint**: < 1.5s
- **Time to Interactive**: < 3s
- **Cumulative Layout Shift**: < 0.1

### Optimization Tips

- Compress images if adding any
- Use WebP format for images
- Enable GZIP compression on server
- Consider CDN for static assets

## ♿ Accessibility

### WCAG 2.1 Compliance

- **Level AA** compliance target
- Semantic HTML5 elements
- ARIA labels and roles
- Keyboard navigation support
- Screen reader compatibility
- Color contrast ratios (4.5:1 minimum)
- Focus indicators on interactive elements

### Accessibility Features

- ✅ Semantic HTML structure
- ✅ ARIA labels on all interactive elements
- ✅ Keyboard navigation support
- ✅ Focus management
- ✅ Alt text for icons (via ARIA labels)
- ✅ Proper heading hierarchy
- ✅ Form labels (if forms added)

### Testing

Use these tools to test accessibility:
- [WAVE](https://wave.webaim.org/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [axe DevTools](https://www.deque.com/axe/devtools/)

## 🌐 Browser Support

### Supported Browsers

- ✅ Chrome (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)
- ✅ Opera (latest)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

### Polyfills

No polyfills required - uses only modern, well-supported features.

## 🤝 Contributing

This is a personal portfolio website. While contributions are welcome, please note:

1. **Fork the repository** (if you want to use as a template)
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request** (if contributing improvements)

### Using as a Template

Feel free to use this portfolio as a template for your own! Just:

1. Fork or clone the repository
2. Update content in `index.html`
3. Customize colors in `style.css` (CSS variables)
4. Replace with your own information
5. Deploy to your own GitHub Pages

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Haben Eyasu Akelom

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 📧 Contact

**Haben Eyasu Akelom**

- 🌐 **Portfolio**: [habeneyasu.github.io](https://habeneyasu.github.io)
- 📧 **Email**: [habeneyasu@gmail.com](mailto:habeneyasu@gmail.com)
- 💼 **LinkedIn**: [linkedin.com/in/habeneyasu](https://linkedin.com/in/habeneyasu)
- 💻 **GitHub**: [github.com/habeneyasu](https://github.com/habeneyasu)
- 📱 **Phone**: +251 942 707 424

## 🙏 Acknowledgments

- **Google Fonts** - Inter font family
- **GitHub Pages** - Free hosting platform
- **Open Source Community** - Inspiration and best practices

## 📊 Project Status

![GitHub last commit](https://img.shields.io/github/last-commit/habeneyasu/habeneyasu.github.io)
![GitHub repo size](https://img.shields.io/github/repo-size/habeneyasu/habeneyasu.github.io)
![GitHub language count](https://img.shields.io/github/languages/count/habeneyasu/habeneyasu.github.io)

---

**Built with ❤️ by Haben Eyasu Akelom**

*Last updated: January 2025*

