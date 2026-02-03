# Artwork by Jake Allen

Portfolio website for Jake Allen's artwork.

🌐 **Live site:** https://artworkbyja.com

## Quick Start

### Adding New Artwork (Super Easy!)

1. **Add the image** to the `images/` folder
   - Name it something simple (e.g., `painting-1.jpg`)

2. **Edit `artwork.json`** and add an entry to the `"gallery"` array:
   ```json
   {
     "id": 4,
     "title": "My Artwork Title",
     "medium": "Oil on canvas, 2026",
     "image": "painting-1.jpg",
     "description": "Optional description"
   }
   ```

3. **Done!** The image will appear on the website automatically.

That's it. No HTML editing needed.

## Local Development

```bash
# Python
python -m http.server 8000

# Node
npx serve
```

Then visit http://localhost:8000

## File Structure

```
ArtworkByJA/
├── index.html          # Main page (no editing needed for artwork)
├── artwork.json        # All content lives here ← EDIT THIS
├── css/
│   └── style.css       # Styling
├── images/             # Put artwork images here
├── CNAME               # Custom domain config
└── README.md
```

## Customizing Content

### Gallery
- Add/remove pieces in `artwork.json` under `"gallery"`

### Artist Bio
- Edit `artwork.json` → `"artist"` → `"bio"`

### Contact Info
- Email is already set to `studioja@yahoo.com` (update in `artwork.json` if needed)

### Colors & Styling
- Edit `css/style.css` (CSS variables in `:root` section)

### Fonts
- Edit the Google Fonts link in `index.html`

## Deployment

Hosted on GitHub Pages. Just push to `main` branch:

```bash
git add .
git commit -m "Updated gallery"
git push origin main
```

Changes appear live in ~30 seconds.

## DNS Setup

Custom domain `artworkbyja.com` configured with:

```
Type: A
Name: @
Values:
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153

Type: CNAME  
Name: www
Value: <username>.github.io
```

---

Questions? Just edit `artwork.json` and push. The site will handle the rest.
