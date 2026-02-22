# Portals

Generic captive-portal and login-style pages for **educational use only** — e.g. security awareness workshops, phishing demos, and training.

> **For educational use only.** Do not use these pages to collect credentials or data outside of controlled, consented training environments.

> **I am not the original author of all of these** Some I made, some I have collected. Please let me know if you created one of these and want it removed or attributed. I will happily take it down or tag you.
>
> Thanks

<img width="504" height="531" alt="Screenshot_2026-02-12_13-34-34" src="https://github.com/user-attachments/assets/2c03a414-7ff7-4142-9efb-b618f1523977" />

<img width="488" height="640" alt="Screenshot_2026-02-12_14-16-37" src="https://github.com/user-attachments/assets/fe7f5fbc-22e9-4bda-b532-d134965d1e03" />

<img width="943" height="891" alt="Screenshot_2026-02-12_13-02-14" src="https://github.com/user-attachments/assets/54c0d8c2-b11b-45cf-a46b-8a637972c683" />

## What's included

Static HTML pages that look like common login or "sign in to get internet" screens. Each form submits credentials (or other fields) to a `POST /sendJSON` endpoint as JSON so you can hook them to your own backend for workshops.

| File                   | Description                               |
| ---------------------- | ----------------------------------------- |
| `amaindex.html`        | Generic login with "Remember me"          |
| `angry_coffee.html`    | Coffee shop WiFi login (dark theme)       |
| `coffee.html`          | Coffee shop / generic WiFi login          |
| `db.html`              | DB WLANPortal — German railway guest WiFi |
| `fb.html`              | Facebook-style login                      |
| `google.html`          | Google-style sign-in                      |
| `hotel.html`           | Hotel guest WiFi (room + guest name)      |
| `IG.html`              | Instagram-style login                     |
| `link.html`            | Multi-step Google-style + 2FA flow        |
| `link_2.html`          | Public WiFi style (e.g. Google/Apple SSO) |
| `linkedin.html`        | LinkedIn-style sign-in                    |
| `ms.html`              | Microsoft-style sign-in                   |
| `router_update.html`   | Router firmware update (Wi‑Fi password)   |
| `vpn.html`             | Corporate VPN / work account sign-in      |
| `Xfinity-Tmobile.html` | Xfinity WiFi by T-Mobile (email/password) |

### angry_coffee

- **POC / education only.** The only portal in this repo that includes scripts, download prompts, or shell-style behavior — a proof-of-concept to demonstrate additional attack surface, not a generic login clone.
- **What it is:** A single-file captive-portal clone that looks like “The Coffee House” complimentary WiFi login (dark theme, gold accent, “Sign in with Google” style form). It is intended for security awareness to show how a fake WiFi page can both harvest credentials and deliver a follow-up payload.
- **How it works:**
  1. **Credentials:** The form submits email and password via `POST /sendJSON` as JSON (`username`, `password`, `source: "angry_coffee"`, `timestamp`), same as the other portals.
  2. **Config:** At the top of the inline script, `ATTACK_BOX_IP` and `ATTACK_BOX_PORT` (default `192.168.1.100:4444`) define where the optional payload connects. Set these to your listener before use.
  3. **After a successful submit:** The page builds an HTA (HTML Application) that contains VBScript launching a hidden PowerShell reverse shell to that IP:port, triggers a download of it as `WiFi_Connect.hta`, and opens a popup instructing the user to “Open” or “Run” the file to “complete WiFi setup.” In a real training scenario, participants would see how one click after “logging in” can lead to code execution (e.g. on a Windows VM).
- Use only in controlled, consented environments with proper authorization.

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

> **Question loudly so others can learn quietly.**

**Don't Be A Skid**  
_-Zero_

## License

MIT. See [LICENSE](LICENSE).

---

**For educational use only.** **Seriously** I do not support or endorse inapropriate usage of this content. You are responsible for your actions. No warranty. Provided as is.
