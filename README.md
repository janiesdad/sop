# NSW INTRA Operations Manual - Implementation Guide

## Overview

This documentation site provides a comprehensive operations manual for the INTRA system deployed at New South Wealth Management. The site consists of four main pages with a clean, modern design matching the specifications from the Wix Studio editor.

## File Structure

```
/
├── index.html              # Landing page
├── how-to-use.html         # User guide and best practices
├── docs.html               # Documentation categories
├── whats-inside.html       # System capabilities and roadmap
├── styles.css              # Shared stylesheet
└── README.md               # This file
```

## Design Specifications

The site follows these core design principles:

- **Color Palette:** Neutral backgrounds (white/light gray), navy accent (#2C3E50), moss accent (#6B8E7F)
- **Typography:** Newsreader (serif) for headlines, Inter (sans-serif) for body text
- **Layout:** Maximum width 1600px, minimal padding, centered content
- **Responsive:** Mobile-friendly with breakpoints at 768px and 480px
- **Accessibility:** High contrast, readable fonts, semantic HTML

## Deployment to Wix Studio

### Option 1: Custom Code Embedding

1. **Create a new blank page in Wix Studio** for each HTML file
2. **Add a Custom Element:**
   - Click "Add" → "Embed Code" → "Custom Element"
   - Set to full width and height
   - Paste the HTML content from each file

3. **Add the CSS:**
   - Go to Site Settings → Custom Code
   - Add the contents of `styles.css` in the Head section
   - Or use Wix's Advanced CSS editor

4. **Configure URLs:**
   - Set up clean URLs for each page:
     - `/` → index.html
     - `/how-to-use` → how-to-use.html
     - `/docs` → docs.html
     - `/whats-inside` → whats-inside.html

### Option 2: External Hosting + Wix iFrame

1. **Host files externally** (GitHub Pages, Netlify, Vercel, etc.)
2. **Embed in Wix** using iFrame elements
3. **Benefit:** Easier updates, direct file editing

### Recommended: External Hosting

For maximum flexibility and ease of maintenance, host these files externally:

1. **GitHub Pages (Free):**
   ```bash
   # Create new repository
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin [your-repo-url]
   git push -u origin main
   
   # Enable GitHub Pages in repo settings
   # Your site will be at: https://[username].github.io/[repo-name]
   ```

2. **Netlify (Free):**
   - Drag and drop folder to Netlify dashboard
   - Get instant HTTPS URL
   - Auto-deploys on git push

3. **Vercel (Free):**
   - Connect to GitHub repository
   - Automatic deployments
   - Custom domain support

## Password Protection

### Wix Studio Method

1. **Navigate to Site Settings** → "Permissions"
2. **Enable password protection** for the entire site or specific pages
3. **Set password:** Create a secure password for team access
4. **Alternative:** Use Wix Members Area for user-specific access

### External Hosting Method

If hosting on external platform, add this JavaScript before closing `</body>` tag in all HTML files:

```html
<script>
(function() {
    const correctPassword = "YOUR_PASSWORD_HERE";
    const hasAccess = sessionStorage.getItem('intra_access');
    
    if (!hasAccess) {
        const userPassword = prompt("Enter password to access INTRA:");
        if (userPassword === correctPassword) {
            sessionStorage.setItem('intra_access', 'true');
        } else {
            alert("Incorrect password");
            window.location.href = "about:blank";
        }
    }
})();
</script>
```

**Security Note:** This JavaScript method provides basic protection but is not cryptographically secure. For production use, implement server-side authentication.

### Recommended: Basic Auth (Server-Side)

For stronger security with external hosting:

**Netlify:**
Create `_headers` file:
```
/*
  Basic-Auth: username:password_hash
```

**Vercel:**
Add to `vercel.json`:
```json
{
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/$1",
      "headers": {
        "WWW-Authenticate": "Basic realm=\"INTRA\""
      }
    }
  ]
}
```

## Image Placeholders

The landing page (`index.html`) includes a placeholder for a hero image:

```html
<div class="image-placeholder">
    <span>Space reserved for hero image (1169 x 459 aspect ratio)</span>
</div>
```

### To Add Real Image:

Replace the placeholder div with:

```html
<img src="path/to/your/image.jpg" 
     alt="INTRA Operations Manual" 
     style="max-width: 1169px; width: 100%; height: auto; margin: 48px auto; display: block; border-radius: 4px;">
```

**Recommended Image Specifications:**
- Dimensions: 1169 x 459 pixels (or 2338 x 918 for Retina displays)
- Format: WebP (best compression) or JPG
- File size: Under 200KB
- Content: Professional imagery related to financial services or technology

## Customization Guide

### Updating Colors

Edit CSS variables in `styles.css`:

```css
:root {
    --bg-primary: #FFFFFF;
    --bg-secondary: #F8F8F8;
    --text-primary: #2A2A2A;
    --text-secondary: #6B6B6B;
    --accent-navy: #2C3E50;
    --accent-moss: #6B8E7F;
    --border-light: #E0E0E0;
}
```

### Updating Fonts

Current fonts are loaded from Google Fonts. To change:

1. Update font imports in HTML `<head>`:
```html
<link href="https://fonts.googleapis.com/css2?family=YourFont&display=swap" rel="stylesheet">
```

2. Update CSS variables:
```css
--font-headline: 'YourHeadlineFont', serif;
--font-body: 'YourBodyFont', sans-serif;
```

### Adding Contact Information

Replace placeholder text in footer across all pages:

```html
<p style="font-size: 0.875rem; color: var(--text-secondary); line-height: 1.6;">
    123 Main Street, Suite 100<br>
    City, State 12345<br>
    (555) 123-4567<br>
    info@newsouthwealth.com
</p>
```

### Updating "Access INTRA" Links

Search for `href="#"` and replace with actual INTRA system URL:

```html
<a href="https://your-intra-system-url.com" class="cta-button">Access INTRA</a>
```

## Testing Checklist

Before deployment, verify:

- [ ] All internal links work correctly
- [ ] Navigation highlights active page
- [ ] Responsive design works on mobile (test at 768px and 480px widths)
- [ ] All fonts load properly
- [ ] Footer contact information is updated
- [ ] Password protection is functional
- [ ] "Access INTRA" links point to correct URL
- [ ] Images load and display correctly
- [ ] Cross-browser testing (Chrome, Firefox, Safari, Edge)
- [ ] Accessibility: keyboard navigation works
- [ ] Print stylesheets (optional: add print-specific CSS)

## Browser Support

This site is optimized for:
- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- iOS Safari (latest 2 versions)
- Chrome for Android (latest version)

## Accessibility Features

- Semantic HTML5 structure
- Proper heading hierarchy (h1 → h2 → h3)
- High contrast ratios (WCAG AA compliant)
- Keyboard navigation support
- Descriptive link text
- Alt text for images (add when replacing placeholders)

To enhance accessibility further:
- Add ARIA labels where appropriate
- Include skip-to-content link
- Ensure form inputs have associated labels
- Test with screen readers

## Maintenance

### Regular Updates

1. **Quarterly:** Review and update carrier information in Documentation page
2. **As needed:** Update regulatory compliance information
3. **Monthly:** Check all external links
4. **Continuous:** Monitor for security updates if using external dependencies

### Version Control

Recommended practice:
```bash
git tag -a v1.0 -m "Initial release"
git push origin v1.0
```

## Support & Contact

For questions or issues with implementation:
- Contact The Janie Group
- Refer to Wix Studio documentation
- Check hosting platform documentation (GitHub Pages, Netlify, Vercel)

## License

© 2025 New South Wealth Management. All rights reserved.

---

**Last Updated:** January 2025  
**Version:** 1.0  
**Build Time:** Under 60 days from concept to deployment
