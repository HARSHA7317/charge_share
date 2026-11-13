# ⚡ ChargeShare

**Your Neighbourhood is Your Charging Network.**

ChargeShare connects EV owners who need a charge with homeowners who have a safely installed home charger. Its main idea is **Rescue mode**: a host with an EV and a free charger goes live, and low-battery drivers passing nearby, who cannot find a public charging bay, can request an instant charge. The charger earns money instead of sitting idle.

This is a working front-end prototype for a college mini project / hackathon demo. No paid APIs, no build step.

## Quick start

**Option 1: just open it.** Double-click `index.html`.

**Option 2: local server (Node 18+).**
```bash
npm install
npm start        # http://localhost:3000
```

**Option 3: GitHub Pages.** Push this folder to a GitHub repo → Settings → Pages → Branch `main` / root → Save. Your site opens at `https://<username>.github.io/<repo>/`.

## Demo logins (fictional) — password `Demo@123`

| Role | Emails |
|------|--------|
| EV owner | owner1@demo.cs … owner5@demo.cs |
| Host | host1@demo.cs … host5@demo.cs |
| Admin | admin@demo.cs |

## Features

**Everyone:** simple landing page, voice assistant (speech recognition + spoken replies in the browser; type if mic is blocked), nearby home chargers with full details, public-station and "while you charge" demo section, owner–host chat, notifications, help / emergency (112) / report issue, referral code (demo), light and dark mode.

**EV owner:** 🆘 Rescue (low battery → live hosts, drive time, range check, price, one-tap request), search with filters (distance, price, AC/DC, connector, rating, verified, available now), map and list views, best-match recommendation, cost calculator with host comparison and CO₂ estimate, booking with overlap prevention, simulated payment (UPI / card / net banking / cash), booking history, reviews, vehicles and battery tracking, saved chargers.

**Host:** Rescue mode (go live for 1–8 h, optional capped rescue fee, own EV model), add / edit / pause charging points, safety confirmation for qualified installation, accept or reject requests, earnings (today / week / 30 days / total + chart), review replies.

**Admin:** statistics, suspend / reinstate users, approve host verification, resolve reports, set platform fee.

**Demo data:** 5 owners, 5 hosts, 8 charging points, 10 bookings, 5 reviews around Rajahmundry, Kakinada, Surampalem, Peddapuram and Samalkot.

## Project structure

```
chargeshare/
├── index.html            Page shell
├── css/style.css         Styles (light + dark, responsive)
├── js/data.js            Towns and EV model reference data
├── js/app.js             App logic: auth, views, booking, rescue, chat, admin
├── server.js             Optional Express static server
├── package.json
├── supabase/schema.sql   PostgreSQL schema for a shared backend (next step)
├── docs/TEST_JOURNEY.md  5-minute demo script
├── LICENSE               MIT
└── README.md
```

## How it works

- **State** is one object saved in `localStorage` (key `cs1`): users, charging points, bookings, reviews, notifications, chats, reports. Passwords are SHA-256 hashed in the browser (prototype level, not production security).
- **Booking flow:** Pending → host Accepts → owner Pays (simulated) → Confirmed → host marks Completed → earnings update → owner Reviews.
- **Rescue flow:** host goes live → owner sets battery % → app lists live hosts nearest first → request → host accepts → host address is shared privately with that owner only.
- **Privacy:** host locations are shown only as approximate zones until a booking is accepted.
- **Cost:** energy = battery kWh × (target% − current%) / 100; cost = energy × price per kWh; rescue fee applies only at 20% battery or lower and is capped at 25%.

## Limits (honest list)

- Data lives in each browser only; two phones do not see each other's changes. Use `supabase/schema.sql` as the starting point for a shared backend.
- The map is a schematic SVG. Hosted pages that block external tiles cannot load OpenStreetMap, so add Leaflet + OSM when you host it yourself.
- Payments are simulated. "Verified (demo)" badges are not real verification.
- Public stations, entertainment places, amenities and reply times are demo data. Drive time and range are rough estimates.
- Not included: photo galleries, feedback photo upload, real SMS / email OTP.

## Safety

Never offer an ordinary home socket for EV charging. Hosts must use a dedicated EV charger (EVSE) installed by a qualified electrician with proper earthing and protection.

## Roadmap

Supabase auth + database, real-time live status, Leaflet map with real routes, live public-station data, photo uploads, auto-accept for trusted drivers, SMS / WhatsApp alerts, UPI payment gateway.

## License

MIT
