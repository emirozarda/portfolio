# Emir Ozarda — Mechanical Design Portfolio

A static HTML/CSS/JS portfolio site. No build step, no framework, no npm install —
open `index.html` in a browser and it works. This makes it free to host and simple
to keep updating yourself.

## File structure

```
/
├── index.html              Home page
├── about.html               About page (education, skills, bio)
├── experience.html          Work experience timeline
├── resume.html               Resume viewer/download page
├── resume.pdf                 Your resume — replace this file to update
├── contact.html              Contact page
├── robots.txt                 Tells search engines what to crawl
├── sitemap.xml                Lists all pages for search engines
│
├── projects/
│   ├── index.html            Projects gallery (grid of all projects)
│   ├── quadcopter.html        Flagship case study — 3D Printed Quadcopter
│   ├── cnc-frame.html         CNC Machined Quadcopter Frame
│   └── smart-carrier.html    Smart Carrier
│
├── css/
│   └── style.css              All site styling — one file, shared by every page
│
├── js/
│   └── main.js                 Mobile nav toggle + scroll-reveal animation
│
├── images/
│   ├── quadcopter/            Quadcopter project images
│   └── cnc/                    CNC frame project images
│
└── videos/
    ├── camera-tilt-pan.mp4     Camera gimbal motion study
    └── quadcopter-turntable.mp4  Assembled frame turntable clip
```

## How the design works

Every page shares the same `<head>` → `css/style.css` → `js/main.js` pattern.
There's no templating system — each `.html` file is a complete, self-contained
page with its own copy of the header nav and footer. This is slightly more
repetitive to edit than a framework, but it means:

- Zero build step. Edit a file, save it, refresh the browser.
- Deploys as-is to any static host — just upload the folder.
- No dependency updates, no breaking framework changes, ever.

See `DEPLOYMENT.md` for hosting, domain, and update instructions.
