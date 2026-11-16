# Tenicor I&F Hub

Static site for GitHub Pages. Push this folder to a repo, then Settings > Pages > Deploy from branch (main, root).

## Password gate: client-side only
The hub content (artifact titles, summaries, and links) is encrypted in index.html with AES-256-GCM, using a key derived from the shared password (PBKDF2-SHA256, 600,000 iterations). The browser decrypts it only when the right password is entered. A wrong password reveals nothing.

This is NOT server-enforced. GitHub Pages serves every file publicly, so anyone can download index.html and try to guess the password offline. The protection is only as strong as the password, which is a random 6-word passphrase (about 77 bits), so offline guessing is impractical. Anyone who has the password can also copy the Claude share links and pass them on, and those links do not require this password. Rotate the password (and re-share the Claude links if needed) when someone leaves the team.

The password unlocks once per browser tab session. "Lock" clears it.

## Changing the password or adding an artifact
The build script is kept off the site (on Murphy's computer at /workspace/inf-hub-build/build.py). Edit the artifact list or password there and rerun it to regenerate index.html. Old artifacts/*.html files redirect into the hub.
