# Café Bistro
React + TypeScript + Vite + Tailwind + Firebase cafe application.

## Local setup
1. Install Node 20+.
2. Copy .env.example to .env.local and fill Firebase Web App values.
3. npm install
4. npm run dev

## Firebase
Create a Firebase project. Enable Authentication (Email/Password and optionally Google), Firestore and Storage. Register a Web App and add its values to .env.local. Deploy rules with Firebase CLI: firebase deploy --only firestore:rules,storage

## First admin
There is no public admin checkbox. Deploy functions and configure a server-side ADMIN_BOOTSTRAP_EMAIL for the exact account being promoted. The bootstrapAdmin callable grants a Firebase custom claim. Sign out and back in after promotion. For production, disable/remove the bootstrap endpoint after first provisioning.

## Collections
users, menuItems, categories, orders, reservations, reservationSlots, tables, reviews, offers, gallery, contactMessages, settings.

## Security
Admin authorization uses Firebase custom claims in Firestore and Storage rules; the client-side /admin check is only UX. Passwords are never stored in Firestore. Reservation slot creation uses a deterministic document inside a Firestore transaction to prevent duplicate date/time/table writes.

## Payments
Pay-at-Cafe is functional. Online payment is intentionally not faked. Add Razorpay or Stripe with server-side order creation and signature/webhook verification before marking orders Paid. Never expose secret payment keys in VITE_ variables.

## Vercel
Import this GitHub repository into Vercel. Add all VITE_FIREBASE_* variables to the Vercel project and deploy. Build command: npm run build. Output: dist.

## Production configuration still required
Firebase credentials/providers, business contact details, owned/licensed images, payment gateway, email/SMS provider, domain, and final business rules such as taxes, cancellation windows and timezone/holiday handling.