# Portals

Generic captive-portal and login-style pages for **educational use only** — e.g. security awareness workshops, phishing demos, and training.

> **For educational use only.** Do not use these pages to collect credentials or data outside of controlled, consented training environments.

> **I am not the original author of all of these** Some I made, some I have collected. Please let me know if you created one of these and want it removed or attributed. I will happily take it down or tag you.
>
> Thanks

<img width="504" height="531" alt="Screenshot_2026-02-12_13-34-34" src="https://github.com/user-attachments/assets/2c03a414-7ff7-4142-9efb-b618f1523977" />

<img width="943" height="891" alt="Screenshot_2026-02-12_13-02-14" src="https://github.com/user-attachments/assets/54c0d8c2-b11b-45cf-a46b-8a637972c683" />

## What’s included

Static HTML pages that look like common login or “sign in to get internet” screens. Each form submits credentials (or other fields) to a `POST /sendJSON` endpoint as JSON so you can hook them to your own backend for workshops.

| File                 | Description                               |
| -------------------- | ----------------------------------------- |
| `coffee.html`        | Coffee shop / generic WiFi login          |
| `fb.html`            | Facebook-style login                      |
| `IG.html`            | Instagram-style login                     |
| `google.html`        | Google-style sign-in                      |
| `ms.html`            | Microsoft-style sign-in                   |
| `vpn.html`           | Corporate VPN / work account sign-in      |
| `router_update.html` | Router firmware update (Wi‑Fi password)   |
| `link.html`          | Multi-step Google-style + 2FA flow        |
| `link_2.html`        | Public WiFi style (e.g. Google/Apple SSO) |
| `amaindex.html`      | Generic login with “Remember me”          |

## Running locally

Serve the folder with any static HTTP server. Example with Python:

```bash
python3 -m http.server 8000
```

Then open e.g. `http://localhost:8000/coffee.html` (or any other `.html` file).

## Backend

The pages **do not** implement `/sendJSON`. You need a server that:

- Accepts `POST /sendJSON`
- Reads `Content-Type: application/json` body
- Handles the JSON payload (e.g. `username`, `pwd`, `source`, `timestamp` and any page-specific fields)

Without that backend, form submits will fail in the browser (e.g. 404); the pages still load and display correctly for demos.

---

- **Coffee:** [@iamnotaskid](https://buymeacoffee.com/iamnotaskid)

---

**Question loudly so others can learn quietly.**

**Don't Be A Skid**  
_-Zero_

## License

MIT. See [LICENSE](LICENSE).

---

**For educational use only.** **Seriously**
