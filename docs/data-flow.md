
# Data Flow

---

## Event Creation Flow

1. **Admin Authentication:** Admin logs in via Firebase Auth; session state is established.
2. **Form Submission:** Admin fills out the event creation form in the dashboard UI.
3. **Validation:** Frontend validates all required fields and formats.
4. **Firestore Write:** On submit, frontend calls Firestore `addDoc` to the `events` collection.
5. **Real-time Update:** Firestore triggers listeners; all connected clients receive the new event instantly.
6. **UI Refresh:** Event list UI updates in real time for all users.

---

## Certificate Verification Flow

1. **User Input:** User enters a certificate ID in the verification UI.
2. **Query:** Frontend sends a Firestore query (or API route call) to search the `certificates` collection by `certId`.
3. **Match:** System checks for a matching certificate document.
4. **Response:**
	- If found, certificate details are returned and displayed.
	- If not found, an error message is shown to the user.

---

## Authentication Flow

1. **Login:** User (admin/member) submits credentials via login form.
2. **Firebase Auth:** Credentials are verified by Firebase Auth; session token is issued.
3. **Session State:** Session state is stored in memory; protected routes/components are unlocked.
4. **Route Protection:** UI and API routes check session and role before granting access.

---

## Admin Actions Flow

1. **Admin Login:** Admin authenticates (see Authentication Flow).
2. **Dashboard Access:** Dashboard UI displays CRUD controls for events, blogs, members, certificates, gallery.
3. **Action:** Admin creates/edits/deletes data or uploads media.
4. **Write:** Firestore (for data) or Cloudinary (for media) is updated.
5. **Real-time Sync:** UI reflects changes instantly for all users via Firestore listeners.

---

## User Actions Flow

1. **Browse:** User navigates to events, alumni, blogs, gallery, team, or certificate verification pages.
2. **Fetch:** Frontend fetches data from Firestore (structured data) or Cloudinary (media).
3. **Display:** UI renders data; updates in real time if backend changes.

---

## Media Upload Flow (Gallery)

1. **Admin Upload:** Admin selects images to upload in the gallery UI.
2. **Cloudinary Upload:** Images are sent to Cloudinary via API/service module.
3. **Metadata Write:** Image URLs and metadata are written to Firestore `gallery` collection.
4. **Gallery Update:** UI fetches new images and displays them to all users.
