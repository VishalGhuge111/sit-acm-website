
# Architecture

---

## System Structure

- **Frontend:** Next.js (App Router) monorepo with modular `/app` and `/components` directories.
- **Service Layer:** Abstracts Firebase (Firestore, Auth), Cloudinary, and utility logic for clean separation of concerns.
- **API Routes:** Used for server-side operations (certificate verification, uploads) and to encapsulate sensitive logic.

---

## Frontend Structure

- **App Router (`app/`):** Organizes pages by feature (events, alumni, admin, etc.) using file-based routing.
- **Components:** Grouped by domain (e.g., events, admin, gallery) for maintainability and reusability.
- **UI State:** Managed with React hooks and context for predictable state flow.
- **Styling:** Tailwind CSS for utility-first, responsive design.
- **Dynamic Routing:** Used for event, alumni, blog, and certificate detail pages (e.g., `/events/[slug]`).
- **Layouts:** Separate admin and public UIs; admin layout includes navigation and access gates.

---

## Data Handling

- **Firestore:** All structured data (events, members, alumni, blogs, certificates, gallery) is stored in Firestore collections. Each entity has its own collection; documents use flexible fields.
- **Real-time Listeners:** UI subscribes to Firestore updates for instant data sync across clients.
- **Service Modules:** Encapsulate Firestore queries/mutations and Cloudinary API calls for maintainability.

---

## Firestore Collections

- `events`: { title, date, description, images, slug }
- `alumni`: { name, batch, profile, slug }
- `certificates`: { certId, studentName, eventName, date, url }
- `blogs`: { title, content, author, date, slug }
- `gallery`: { imageUrl, event, date }
- `team`: { name, role, year }
- `members`: { name, email, role, year }

---

## Authentication Gates

- **Firebase Auth:** Manages sessions for admins and members. Auth state is watched via `onAuthStateChanged`.
- **Role Checks:** Admin login triggers session state and role checks. Only admins can access `/admin` routes and perform CRUD operations.
- **Protected Routes:** UI and API routes enforce access control; unauthorized users are redirected or denied.

---

## Admin vs Public Flows

- **Admin Flows:**
	- Access via `/admin` routes (dashboard, events, blogs, certificates, gallery)
	- CRUD operations for all entities
	- Media uploads via Cloudinary
	- All actions require authentication and admin role

- **Public Flows:**
	- Browse events, alumni, blogs, gallery, team
	- Verify certificates
	- Submit recruitment forms
	- No authentication required for read-only access

- **Security:** Certificate verification and uploads handled via API routes to prevent direct client access to sensitive operations.

---

## Integrations

- **Firebase SDK:** For authentication and Firestore access
- **Cloudinary API:** For media upload, transformation, and CDN delivery
- **REST Endpoints:** For uploads and certificate verification

---

## Deployment

- **Next.js:** Deployed as a hybrid of static and serverless functions (SSR/CSR as needed)
- **Environment Variables:** Used for API keys and secrets; not exposed to client
- **CDN-backed Assets:** All media and static assets delivered via CDN for performance
