
# SIT ACM Portal

Production web platform for ACM chapter operations, event management, and member engagement.

> Note: Source code is private. This repository showcases architecture, features, and implementation details.

## Problem

Student chapters require a unified platform to manage events, memberships, alumni, certificates, and communications. Manual processes lead to inefficiency, fragmented data, and poor user experience for students, alumni, and admins.

## Solution

SIT ACM Portal centralizes chapter operations with a modular Next.js frontend, Firebase backend, and Cloudinary media handling. The system provides authenticated admin workflows, public event and certificate access, and real-time data updates. Admins manage content and users via a secure dashboard; students and alumni interact with events, directories, and verification tools.

## Key Features

- Event CRUD with dynamic routing and real-time updates
- Member and alumni directories with profile pages
- Certificate issuance and public verification
- Role-based admin authentication and session management
- Blog publishing with editor and public reading
- Media gallery with Cloudinary-backed uploads
- Contact, FAQ, and team/year pages

## Tech Stack

- **Frontend:** Next.js (App Router), React, Tailwind CSS
- **Backend/Services:** Firebase (Firestore, Auth), Cloudinary
- **Database:** Firestore (NoSQL, flexible schema)
- **Integrations:** Cloudinary (media), Firebase Auth, REST endpoints

## System Architecture (High-level)

Next.js frontend (React, Tailwind) communicates with Firebase (Firestore, Auth) and Cloudinary via service modules and API routes. Admin and public flows are separated by authentication gates. Data is fetched server-side and client-side as required. Media uploads are handled via Cloudinary APIs.

See detailed architecture → ./docs/architecture.md

## Engineering Decisions

**Firebase:** Chosen for real-time updates, flexible NoSQL schema, and integrated authentication. Simplifies backend ops and scales for student org needs.

**Next.js:** Enables hybrid SSR/CSR, modular routing, and rapid UI development. App Router structure supports maintainable codebase.

**Cloudinary:** Provides reliable, scalable media storage and transformation. Offloads image handling from core backend.

## Sample Logic Snippets

```ts
// Fetch events from Firestore
const snapshot = await getDocs(collection(db, "events"));
const events = snapshot.docs.map(doc => doc.data());
```
Retrieves all event records for listing and detail pages.

```ts
// Role-based admin authentication
export async function signInAdmin(email, password) {
	return signInWithEmailAndPassword(auth, email, password);
}
```
Authenticates admin users using Firebase Auth.

```ts
// Certificate verification by certId
const rows = await getByField("certificates", "certId", certId);
return rows[0] ?? null;
```
Looks up a certificate by ID for public verification.

## Modules Overview

Authentication, events, alumni, certificates, admin dashboard, blog, gallery, and team modules each encapsulate UI, logic, and data access. See detailed module breakdown → ./docs/modules.md

## Screenshots

### Events Page
User sees a list of upcoming/past events with details. On load, the frontend queries Firestore for event data and renders cards. Clicking an event triggers dynamic routing to the detail page, fetching the event by slug.

![Events Page](./screenshots/events-page.png)

### Dashboard
Admins access a dashboard with event/member/blog/certificate management. Auth state is checked on load; UI renders CRUD controls. Actions trigger Firestore writes and UI updates in real time.

![Dashboard](./screenshots/dashboard.png)

### Certificate Verification
Public users enter a certificate ID. The system queries Firestore for a matching record and displays verification status and details if found.

![Certificate Verification](./screenshots/verification.png)

### Login
Admins and members authenticate via Firebase Auth. On success, session state is updated and protected routes are unlocked.

![Login](./screenshots/login.png)

## My Role

Led full-stack development, system design, and deployment. Architected modular frontend, integrated Firebase and Cloudinary, implemented authentication, and established admin workflows. Responsible for code quality, scalability, and maintainability.
