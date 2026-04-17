# Stories by Rushik — Portfolio

A fully custom photography portfolio with a real admin panel, cloud image storage, Google authentication, and an interstellar visual aesthetic.

**Live site:** https://stories-by-rushik.vercel.app  
**Admin panel:** https://stories-by-rushik.vercel.app/admin.html *(bookmark this)*

---

## Tech Stack

| Layer | Tool | Purpose | Cost |
|---|---|---|---|
| Hosting | Vercel | Serves the website globally via CDN | Free |
| Auth | Firebase Auth | Google Sign-In for admin access | Free |
| Database | Firestore (Firebase) | Stores albums, photos, testimonials, videos, inquiries | Free |
| Image Storage | Cloudinary | Stores and serves all photos with auto-optimization | Free (25GB) |
| Frontend | Vanilla HTML/CSS/JS | No frameworks — pure and fast | — |

---

## File Structure

```
stories-by-rushik/
├── index.html      → Public portfolio (what visitors see)
├── admin.html      → Admin panel (only Rushik can access)
└── README.md       → This file
```

That's it. Two files, everything inline. No build tools, no npm, no dependencies to manage.

---

## How It Works — Data Flow

```
Visitor opens index.html
        ↓
Firebase loads albums, photos, testimonials, videos from Firestore
        ↓
Photos are served via Cloudinary CDN (auto-resized, optimised)
        ↓
Visitor sees the portfolio
```

```
Rushik opens admin.html
        ↓
Signs in with Google (rushiksaikashetty@gmail.com only)
        ↓
Firebase Auth verifies identity
        ↓
Admin panel unlocks — Rushik can upload, edit, publish
        ↓
Photos upload to Cloudinary (auto-compressed if > 9MB)
        ↓
Photo metadata saved to Firestore
        ↓
Public site updates instantly
```

---

## Firestore Database Structure

```
settings/
  └── site              → tagline, bio, aboutPhoto, whatsapp, hireTagline, hireEmail

albums/
  └── {albumId}         → name, published, order, createdAt

photos/
  └── {photoId}         → albumId, cloudinaryId, cloudinaryUrl, caption, featured, published, uploadedAt

videos/
  └── {videoId}         → url, title, published, order, createdAt

testimonials/
  └── {testimonialId}   → name, role, text, approved, createdAt

inquiries/
  └── {inquiryId}       → name, email, type, message, createdAt
```

---

## Public Portfolio Sections

| Section | Description |
|---|---|
| **Hero** | Full-screen star animation, title, tagline (editable from admin) |
| **Featured** | Curated wall of starred photos |
| **Work** | Albums with masonry photo grid, lightbox, keyboard/swipe navigation |
| **About** | Bio and profile photo (editable from admin), Instagram + VSCO links |
| **Videos** | YouTube embeds (added from admin) |
| **Testimonials** | Client reviews (added/approved from admin) |
| **Hire Me** | WhatsApp button + contact form (submissions saved to Firestore) |

---

## Admin Panel — What You Can Do

| Tab | What it does |
|---|---|
| **Albums** | Create, rename, delete, publish/draft albums |
| **Photos** | Upload photos, add captions, star for Featured Wall, publish/draft, delete |
| **About** | Edit bio, tagline, upload profile photo |
| **Videos** | Add YouTube URLs, show/hide videos |
| **Testimonials** | Add client testimonials, approve/reject, delete |
| **Hire Me** | Set WhatsApp number, contact email, tagline |
| **Inquiries** | View all contact form submissions |

---

## Design

**Aesthetic:** Interstellar — deep space dark background, warm gold accents, star canvas animation with parallax and shooting stars, nebula glows.

**Palette:**
- Background: `#030308`
- Gold accent: `#c8a96e`
- Text: `#e8e4dc`
- Muted text: `#9a9590`

**Typography:** Georgia (serif) for headings and logo, system sans-serif for UI elements.

**Layout:** CSS columns masonry grid — respects the natural aspect ratio of every photo. Mobile-first responsive. Hamburger nav on mobile. No fancy cursor (intentionally removed for mobile UX).

**Lightbox:** Full-screen image viewer with keyboard navigation (← → Esc) and touch swipe support.

---

## Integrations

### Firebase (console.firebase.google.com)
- Project: `stories-by-rushik`
- Auth: Google Sign-In enabled, support email: rushik.sai@gmail.com
- Authorized domains: `stories-by-rushik.vercel.app`, `rushiksaikashetty.github.io`
- Firestore: Standard edition, asia-south1 (Mumbai), production mode
- Admin email hardcoded: `rushiksaikashetty@gmail.com`

### Cloudinary (cloudinary.com)
- Cloud name: `dfwgpzkwc`
- Upload preset: `portfolio` (unsigned)
- Folder: `stories-by-rushik`
- Photos are auto-compressed client-side to max 2400px / 9MB before upload
- On display: Cloudinary auto-optimises via URL params (w_700, q_auto, f_auto)

### Vercel (vercel.com)
- Connected to GitHub repo: `RushikSaiKashetty/stories-by-rushik`
- Auto-deploys on every push to `main`
- URL: `stories-by-rushik.vercel.app`

---

## Deploying Changes

Any code change → push to GitHub → Vercel auto-deploys in ~30 seconds.

```bash
cd /Users/rushiksaikashetty/Documents/stories-by-rushik
git add index.html admin.html
git commit -m "describe what you changed"
git push
```

---

## Security

- Admin access locked to `rushiksaikashetty@gmail.com` — enforced both in the frontend JS and in Firestore security rules
- Public visitors can only **read** published content
- Only the admin can **write** to any collection
- Contact form submissions are write-only for public, readable only by admin
- Cloudinary unsigned preset is scoped to the `stories-by-rushik` folder
- Admin URL is not linked anywhere — security by obscurity + Google Auth

---

## Social Links

- Instagram: [@rushiksaii](https://www.instagram.com/rushiksaii/)
- VSCO: [@rushikkashetty](https://vsco.co/rushikkashetty/gallery)

---

## Future Ideas

- [ ] Custom domain (storiesbyrushik.com)
- [ ] Video file uploads via Cloudinary
- [ ] Photo reordering via drag-and-drop in admin
- [ ] Client gallery — private password-protected albums
- [ ] Blog / behind the scenes section
