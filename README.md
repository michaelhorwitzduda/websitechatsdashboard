# Duda Website Chat Dashboard (password-protected)

This repo hosts a single encrypted, static `index.html` for GitHub Pages — an interactive dashboard over Duda's website chat (Salespeak) sessions: transcripts, buyer intent, conversions, topics, and competitor mentions.

The file is encrypted client-side with [pagecrypt](https://github.com/Greenheart/pagecrypt) (AES via the Web Crypto API, PBKDF2 key derivation). Anyone with the URL can download the file, but it's unreadable without the password — **the password itself is not stored in this repo**. Get it from whoever shared this dashboard with you.

## Refreshing the dashboard

The source dashboard lives at `Salespeak Analysis/dashboard/` in the main ConversationsAnalysis project (private, not this repo). After a new transcript dump lands in `datadumps/Salespeak/files/`:

```bash
node parse-sessions.js   # markdown transcripts → sessions.json
node build.js            # sessions.json → DudaChatSessions_Dashboard.html
npx pagecrypt DudaChatSessions_Dashboard.html index.html -g 24
```

Then replace `index.html` here and push. Each encryption generates a **new** password — share the new one with whoever needs access.

## Access via magic link (optional)

pagecrypt supports appending the password as a URL fragment so the prompt is skipped, e.g. `https://<your-pages-url>/#<password>`. The fragment is never sent to the server, but it will appear in browser history — use with care.
