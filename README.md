# Haptic Control — GitHub Pages version

## What this is

This is the simplest possible version:

GitHub Pages → Adafruit IO → ESP32

GitHub Pages is static hosting, so there is no server/database to configure.

## Setup

1. Create a NEW public GitHub repository.
2. Name it something like `haptic-control`.
3. Upload `index.html`.
4. Open `index.html` in GitHub and click the pencil/edit button.
5. Find:

   const PASSWORD_HASH="CHANGE_ME";

6. Replace CHANGE_ME with the SHA-256 hash of the password you want.

   You can generate the hash in your browser console with:

   crypto.subtle.digest("SHA-256",new TextEncoder().encode("YOUR_PASSWORD")).then(x=>console.log([...new Uint8Array(x)].map(x=>x.toString(16).padStart(2,"0")).join("")))

7. Commit the change.
8. Go to repository Settings → Pages.
9. Under Build and deployment choose:
   Source: Deploy from a branch
   Branch: main
   Folder: / (root)
10. Click Save.

GitHub will give you a github.io URL.

## Adafruit IO setup

When you open the site:

- Enter your Adafruit IO username.
- Enter your Adafruit IO key.
- Enter `haptic` as the feed key if that is your existing feed.
- Click Save settings.
- Send a test message.

The key is stored only in that browser's localStorage. It is not put into this GitHub repository.

## Important security limitation

This is NOT a true secure login.

Because GitHub Pages only serves static HTML/CSS/JavaScript, the password check happens in the visitor's browser. Someone who knows what they are doing can inspect the page and bypass it.

Also, if a person has the Adafruit IO key in their browser, they can potentially use it themselves.

Therefore this version is good for a personal/family hobby project where you trust the people using it. It is not appropriate for a public service where strangers should be allowed to send messages without seeing your Adafruit IO credential.

For true server-side password protection, use the Cloudflare Worker version instead.

GitHub Pages itself is free for public repositories on GitHub Free.
