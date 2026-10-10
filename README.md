# AnnaConnect

A food-surplus rescue platform prototype for Coimbatore, Tamil Nadu. It connects hotels, hostel messes and event organisers with verified local NGOs and community feeding groups, so that good, freshly cooked surplus food reaches people who need it.

> **Status:** Working prototype. It has not been deployed publicly or piloted with real users yet. The source code is in a private repository (details below).

## The problem

Hotels, hostel messes and event halls often end up with surplus cooked food at the end of the day. At the same time, shelters, orphanages and old age homes struggle to arrange meals. The gap is usually coordination: who has food, how much, where, and who can collect it in time.

## What it does

AnnaConnect only connects people. It does not handle food, money or delivery. Donors and receivers coordinate pickup directly.

1. **Donor posts a listing:** food description, veg/non-veg, approximate number of people it can feed, cooking time, pickup-by time and address.
2. **System matches receivers:** it filters verified, active receivers by radius, diet preference, working hours and capacity, then ranks them by distance, estimated arrival time and past reliability.
3. **First receiver to accept gets it:** the listing locks immediately, even if two receivers click at the same moment.
4. **Contact details are shared only after acceptance.**
5. **Pickup is marked complete,** and impact numbers update.

## Key features

- Tamil-first UI with an English/Tamil toggle, mobile-first, installable as a PWA
- Role-based access: donor, receiver, admin
- Phone OTP sign-in (console OTP in development)
- Admin verification of receivers before they can receive listings
- Matching module: radius, capacity, diet and working-hours filters; Haversine distance; reliability-based ranking; wider second pass if nobody accepts
- Race-condition-safe claiming with an atomic database update
- Food safety rules enforced on the server: freshly cooked, covered, unserved food only, with a maximum window from cooking to pickup (default 3 hours)
- Expiry countdown, auto-expiry, and reminders to donors when nobody has accepted
- Option to donate anonymously
- Cancel, no-show and post-pickup quality-report handling
- Audit log for admin actions
- Impact dashboard (pickups, estimated meals)
- Optional Tamil voice input where the browser supports it
- Offline drafts for listings on poor networks

## Screenshots

| Landing page | Donor: post surplus food |
|---|---|
| ![Landing](Screenshot (18).png) | ![Donor form](docs/screenshots/donor-form.png) |

| Receiver: nearby listings | Admin / impact dashboard |
|---|---|
| ![Receiver feed](docs/screenshots/receiver-feed.png) | ![Admin](docs/screenshots/admin.png) |

## Demo video

[Watch the demo](PASTE-YOUR-VIDEO-LINK-HERE)

## Tech stack

- **Frontend:** React, TypeScript, Vite, Tailwind CSS, Leaflet / OpenStreetMap
- **Backend:** Node.js, Express, TypeScript
- **Database:** MongoDB with Mongoose
- **Auth and security:** JWT in an HttpOnly cookie, role and ownership checks in middleware, rate limiting
- **Testing and tooling:** Vitest, ESLint, Prettier
- Built with the help of GitHub Copilot

## Architecture (simple view)

```text
React PWA (Tamil / English)
        |
        v
Express REST API
 - auth and role checks
 - matching module
 - food safety validation
 - notifications (in-app, email, WhatsApp link)
 - scheduled expiry job
        |
        v
     MongoDB
```

## Food safety and limitations

- Listings are donor-provided estimates. The app cannot inspect, store or transport food, or guarantee its quality.
- Donors and receivers are responsible for food quality and handling.
- Food donation practices should follow current FSSAI guidance. This project does not claim legal or FSSAI compliance.
- Real SMS OTP is not integrated yet (development uses console OTP).

## Next steps

- Talk to local hotels, hostel messes and NGOs to learn what works on the ground
- Run a small, controlled pilot
- Add production OTP (SMS or email), a security review and deployment

## Code access

The source code is kept in a private repository. If you are a recruiter, interviewer or NGO and would like a walkthrough or code access, please reach out.

## Author

**YOUR NAME**
Information Technology student | Coimbatore
LinkedIn: [your-linkedin-link](https://www.linkedin.com/in/gokulnath01)
Email: gokulsaravanan034@gmail.com
