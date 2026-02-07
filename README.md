# Artwork by Jake Allen

Portfolio website for Jake Allen's artwork - Built with Vue.js 3 as a Single Page Application (SPA).

🌐 **Live site:** https://artworkbyja.com

## About This Project

This is a modern Vue.js 3 SPA (Single Page Application) built with Vite, featuring fast development and optimized production builds. The site is automatically deployed to GitHub Pages via GitHub Actions on every push to the master/main branch.

## Quick Start

### Adding New Artwork (Super Easy!)

1. **Add the image** to the `public/images/` folder
   - Name it something simple (e.g., `painting-1.jpg`)

2. **Edit `public/artwork.json`** and add an entry to the `"gallery"` array:
   ```json
   {
     "id": 4,
     "title": "My Artwork Title",
     "medium": "Oil on canvas, 2026",
     "image": "painting-1.jpg",
     "description": "Optional description"
   }
   ```

3. **Done!** Commit and push to master/main - your site updates automatically!

## Local Development

```bash
# Install dependencies
npm install

# Start dev server (opens in browser at http://localhost:5173)
npm run dev
```

The dev server includes hot module reloading (HMR), so your changes appear instantly without refreshing.

## Building for Production

```bash
# Build optimized production bundle
npm run build

# Preview the production build locally
npm run preview
```

The production build outputs to the `dist/` folder, which is automatically deployed by GitHub Actions.

## Project Structure

```
artworkbyja/
├── .github/
│   └── workflows/
│       └── deploy.yml           # GitHub Actions deployment config
├── public/
│   ├── index.html              # SPA entry point
│   ├── artwork.json            # Gallery & artist data ← EDIT THIS
│   └── images/                 # Artwork images (add images here)
├── src/
│   ├── main.js                 # Vue app entry point
│   ├── App.vue                 # Root Vue component
│   ├── components/
│   │   ├── Gallery.vue         # Gallery section component
│   │   ├── About.vue           # About section component
│   │   └── Contact.vue         # Contact section component
│   └── assets/
│       └── style.css           # Global styles
├── package.json                # Dependencies & scripts
├── vite.config.js              # Vite configuration
├── CNAME                        # Custom domain config
└── README.md
```

## Customizing Content

### Gallery
- Add/remove pieces in `public/artwork.json` under the `"gallery"` array
- Images should be placed in `public/images/`

### Artist Bio & Info
- Edit `public/artwork.json` → `"artist"` section
- Update the `bio` field with your biography

### Contact Info
- Email is set to `studioja@yahoo.com` in Contact.vue component
- Update `src/components/Contact.vue` to change email and social links

### Colors & Styling
- Edit `src/assets/style.css` - CSS variables are defined in `:root`
- Component-specific styles are in scoped `<style>` blocks in each `.vue` file

### Fonts
- Google Fonts link is in `public/index.html`
- Font references are in the CSS variables in `src/assets/style.css`

## Deployment

### Automatic Deployment via GitHub Actions

The site is automatically deployed when you push to the `master` or `main` branch:

```bash
# Make changes, then:
git add .
git commit -m "Updated gallery"
git push origin master
```

GitHub Actions will:
1. Install dependencies
2. Build the production bundle
3. Deploy to GitHub Pages
4. Your site updates within ~1-2 minutes

### Manual Deployment

If needed, you can trigger a manual build and preview:

```bash
npm run build
npm run preview
```

## DNS Setup

Custom domain `artworkbyja.com` is configured with:

```
A Records:
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153

CNAME Record:
  Name: www
  Value: <username>.github.io
```

## Technology Stack

- **Vue.js 3** - Progressive JavaScript framework
- **Vite** - Next-generation frontend build tool
- **GitHub Pages** - Free static hosting
- **GitHub Actions** - CI/CD automation

## Features

✨ **Fast Performance** - Optimized Vite build with code splitting
⚡ **Hot Module Reloading (HMR)** - Instant updates during development
📱 **Responsive Design** - Works beautifully on all devices
🎨 **Easy Content Updates** - Just edit JSON and push
🚀 **Automatic Deployment** - Push to master/main and watch it deploy
🔄 **Component-based Architecture** - Reusable Vue components

## Development Workflow

1. Create a feature branch: `git checkout -b feat/your-feature`
2. Make changes to components, styles, or content
3. Test locally: `npm run dev`
4. Commit and push: `git push origin feat/your-feature`
5. Create a Pull Request to merge into master/main
6. Once merged to master/main, GitHub Actions automatically deploys

## Troubleshooting

### Images not showing
- Make sure images are in `public/images/` directory
- Check that the filename in `artwork.json` matches exactly (case-sensitive)

### Changes not appearing
- Run `npm run build` locally to check for errors
- Check GitHub Actions logs in the repository
- Make sure you pushed to `master` or `main` branch

### Build errors
- Delete `node_modules` folder and `package-lock.json`
- Run `npm install` again
- Try `npm run build` to identify the issue

## Resources

- [Vue.js 3 Documentation](https://vuejs.org/)
- [Vite Documentation](https://vitejs.dev/)
- [GitHub Pages](https://pages.github.com/)
- [GitHub Actions](https://github.com/features/actions)

---

Questions? Edit `public/artwork.json`, commit, and push. The site handles the rest! 🎨
