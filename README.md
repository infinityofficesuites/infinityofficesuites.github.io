1. FILE ARCHITECTURE & CONSTRAINTS
====================================
- The ENTIRE application, including HTML, CSS, JavaScript, Web Manifest, and Service Worker, MUST strictly reside inside ONE single file named `index.html`.
- Reference an external logo image at `./logo.png` (used in the navbar, brand header, and WebAPK manifest).

==================================================
2. WebAPK / PWA SINGLE-FILE IMPLEMENTATION
==================================================
- Inject an inline Web App Manifest into the <head> using a Data URL:
  <link rel="manifest" href="data:application/manifest+json;utf8,{...}">
  - App Name: "Infinity Office Suite"
  - Short Name: "Infinity Suite"
  - Display: "standalone"
  - Start URL: "./index.html"
  - Theme/Background Color: Dark slate blue (#0f172a)
  - Icon: Path to "./logo.png"

- Inject an inline Service Worker using a Blob URL in JavaScript:
  const swCode = `
    self.addEventListener('install', (e) => self.skipWaiting());
    self.addEventListener('activate', (e) => event.waitUntil(clients.claim()));
    self.addEventListener('fetch', (e) => e.respondWith(fetch(e.request).catch(() => caches.match(e.request))));
  `;
  const blob = new Blob([swCode], { type: 'application/javascript' });
  navigator.serviceWorker.register(URL.createObjectURL(blob));

==================================================
3. TOP NOTIFICATION BANNER (WebAPK INSTALLER)
==================================================
- Create a sleek, rectangular, fixed top notification bar at the very top of the page.
- Banner Text: "Install the APK Infinity Office Suite. Produced by samuel.i.t"
- Banner Action: Include a prominent "Install" button and an "X" dismiss button.
- JavaScript Logic:
  1. Hide the banner by default (`display: none`).
  2. Listen for the `beforeinstallprompt` event. When triggered, reveal the top banner.
  3. Clicking "Install" triggers the browser's native WebAPK installation prompt.
  4. Automatically hide the banner once the app is installed or dismissed.

==================================================
4. UI / UX DESIGN SYSTEM & LAYOUT
==================================================
- Design Theme: Modern Dark Mode (Tailwind CSS CDN via <script src="https://cdn.tailwindcss.com"></script> or equivalent custom CSS).
- Color Palette: Deep slate background (`#0f172a`), dark card surfaces (`#1e293b`), vibrant accent colors (emerald green and electric indigo).
- Structure:
  1. Top WebAPK Install Banner (Fixed).
  2. Header / Navbar: Displays logo (`./logo.png`), app title ("Infinity Office Suite"), and status indicator ("WebAPK Ready").
  3. Tool Dashboard / Navigation Tabs: Easily switch between built-in tools.
  4. Active Tool Workspace Container.
  5. Footer: "Infinity Office Suite • Produced by samuel.i.t"

==================================================
5. CORE OFFICE SUITE TOOLS TO INCLUDE
==================================================
Build clean, fully functional JavaScript utilities inside the single file:

1. Text & Document Editor:
   - Rich/Plain text formatting, character & word counters, copy-to-clipboard, clear text, and local `.txt` file export.
2. File Converter & Base64 Tool:
   - Convert text/files to Base64 and vice versa, string encoder/decoder, and JSON formatter/validator.
3. Code & Web Sandbox / Playground:
   - HTML/CSS/JS live preview sandbox with real-time iframe rendering.
4. Quick Productivity Utilities:
   - Password/Hash generator, unit converter (bytes, storage, distance), and a quick scratchpad saved in localStorage.

==================================================
6. NON-DISRUPTIVE WEB EXPERIENCE
==================================================
- Installing the WebAPK must be completely optional.
- The website must remain 100% functional inside any web browser, whether the user installs the WebAPK or prefers using it directly in their browser.

Please generate the full, ready-to-use `index.html` file code without truncating any features or logic.
