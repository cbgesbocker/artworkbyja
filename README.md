# Artwork by JA

Portfolio website for JA's artwork.

🌐 **Live site:** https://artworkbyja.com

## Local Development

Just open `index.html` in a browser, or use a local server:

```bash
# Python
python -m http.server 8000

# Node
npx serve
```

Then visit http://localhost:8000

## Adding Artwork

1. Add images to the `images/` folder
2. Edit `index.html` — find the gallery section and update:
   - Image `src` paths
   - Artwork titles
   - Medium/year info

## Structure

```
├── index.html      # Main page
├── css/
│   └── style.css   # Styles
├── images/         # Artwork images
├── CNAME           # Custom domain config
└── README.md
```

## Customization

- **Colors:** Edit CSS variables in `css/style.css` (`:root` section)
- **Fonts:** Change Google Fonts link in `index.html`
- **Content:** Edit text directly in `index.html`

## Deployment

Hosted on GitHub Pages. Push to `main` branch to deploy.

DNS records for artworkbyja.com:

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
