# Features

## User Features
- **Event browsing:** Users view upcoming/past events; data fetched from Firestore and rendered dynamically.
- **Event registration:** Users register for events; submissions are written to Firestore and confirmed in UI.
- **Member/alumni directories:** Users browse searchable lists; directory data loaded from Firestore collections.
- **Certificate verification:** Users enter cert ID; system queries Firestore and returns verification result.
- **Blog reading:** Users read articles; blog content is loaded from Firestore and rendered with markdown support.
- **Gallery viewing:** Users browse event photos; images are loaded from Cloudinary and Firestore records.
- **Contact/FAQ:** Users access static and dynamic info pages; content managed via Firestore or static files.

## Admin Features
- **Authentication and access control:** Admins log in via Firebase Auth; session state controls dashboard access.
- **Event management:** Admins create/edit/delete events; actions update Firestore and trigger UI refresh.
- **Blog publishing:** Admins write and publish blogs; content is stored in Firestore and rendered for users.
- **Certificate issuance:** Admins generate certificates; records are created in Firestore for verification.
- **Member/alumni management:** Admins add/edit/remove records; changes update Firestore collections.
- **Gallery uploads:** Admins upload images; files sent to Cloudinary, metadata stored in Firestore.

## System Features
- **Component-based frontend:** UI built with modular React components for maintainability.
- **Responsive design:** Tailwind CSS ensures mobile and desktop usability.
- **Secure authentication:** Firebase Auth manages sessions and role checks.
- **Real-time data updates:** Firestore listeners keep UI in sync with backend changes.
- **Media storage/optimization:** Cloudinary handles image uploads, transformations, and CDN delivery.
