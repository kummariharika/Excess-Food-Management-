# SecondServe — Excess Food Management System

A MERN-stack educational prototype based on the uploaded project report. It connects surplus-food donors (restaurants, stores and households) with receivers (NGOs, shelters and community groups).

## Included features
- Donor / receiver signup and login using JWT and bcrypt password hashing.
- Role-specific donor and receiver dashboards.
- Donors create food listings with quantity, address, coordinates, preparation time, storage instructions and expiry.
- Receivers browse/search available food, view locations on a Leaflet map, and request donations.
- Donation workflow: available → claimed → deal_confirmed → received; expired listings are hidden from available results.
- Donor waste-reduction insights: xAI Grok API when configured, otherwise clearly labelled rule-based suggestions.
- Contact form and protected admin summary endpoint.
- Responsive React frontend.

## Stack
React + Vite + React Router + Axios + Leaflet; Node.js + Express + MongoDB + Mongoose; JWT + bcrypt.

## Run locally
Requirements: Node.js 18+, npm, MongoDB local or Atlas.

### Backend
```bash
cd server
cp .env.example .env
# Edit MONGODB_URI and JWT_SECRET
npm install
npm run dev
```
API: http://localhost:5000

### Frontend (new terminal)
```bash
cd client
npm install
npm run dev
```
Open the Vite URL, normally http://localhost:5173.

### Create an admin
Register an account first, then:
```bash
cd server
npm run make-admin -- your-email@example.com
```

### Optional Grok integration
Set XAI_API_KEY in server/.env. The app sends aggregate, non-identifying donation counts to xAI. Without a key, rule-based suggestions are shown. Never commit API keys.

## API
POST `/api/auth/signup`, POST `/api/auth/login`, GET `/api/auth/me`, PUT `/api/auth/role`;
GET `/api/foods`, GET `/api/foods/mine`, POST `/api/foods`,
POST `/api/foods/:id/claim`, POST `/api/foods/:id/confirm-deal`,
POST `/api/foods/:id/confirm-receipt`, DELETE `/api/foods/:id`,
GET `/api/insights`, POST `/api/contact`, GET `/api/admin/summary`.

## Notes and limitations
The report describes OTP password reset and automated email notifications; these are not implemented in this starter build. Add a verified email provider and secure OTP storage before production. Map tiles use OpenStreetMap; observe its usage policy. The AI fallback is rules-based, not a trained prediction model. This is an educational prototype, not a food-safety certification system. Donors must list only safe, edible food and provide accurate handling/expiry details.
