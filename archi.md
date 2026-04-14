# Architecture

## System Structure
- Next.js monorepo with modular /app and /components directories
- Service layer abstracts Firebase, Cloudinary, and utility logic
- API routes for server-side operations (certificate verification, uploads)

## Frontend Structure
- App Router (app/) organizes pages by feature (events, alumni, admin, etc.)
- Components are grouped by domain (e.g., events, admin, gallery)
- UI state managed with React hooks and context
- Tailwind CSS for utility-first, responsive design
- Dynamic routing for event, alumni, blog, and certificate detail pages
- Layouts separate admin and public UIs

## Data Handling
- Firestore used for all structured data: events, members, alumni, blogs, certificates, gallery
- Collections per entity; documents store flexible fields
- Real-time listeners update UI on data changes
- Service modules encapsulate Firestore queries and mutations

## Authentication Flow
- Firebase Auth manages sessions for admins and members
- Admin login triggers session state and role checks
- Protected routes/components enforce access control
- Auth state is watched via onAuthStateChanged; UI updates accordingly

## Admin vs Public Flow
- Admin routes (e.g., /admin) gated by authentication and role
- Admins can create, edit, and delete events, blogs, certificates, gallery items
- Public users can browse events, verify certificates, view blogs/gallery, and access directories
- Certificate verification and uploads handled via API routes for security

## Integrations
- Firebase SDK for authentication and Firestore access
- Cloudinary API for media upload, transformation, and delivery
- REST endpoints for uploads and certificate verification

## Deployment
- Next.js deployed as static and serverless functions (hybrid SSR/CSR)
- Environment variables for API keys and secrets
- CDN-backed asset delivery for performance
