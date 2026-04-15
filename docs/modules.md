
# Modules

---

## Authentication

**Purpose:** Secure access for admins and members; enforces role-based permissions.

**UI Components:** Login forms, protected route wrappers, session state banners.

**Data Structure:** Firebase Auth user objects; session state stored in memory.

**Key Logic:**
- Email/password login via Firebase Auth
- Session persistence and invalidation
- Role checks for admin vs member

**Navigation Flow:**
- User visits /admin or /member routes → Login form
- On success, session state is set and protected routes are unlocked

**Example:**
```ts
export async function signInAdmin(email, password) {
	return signInWithEmailAndPassword(auth, email, password);
}
```

---

## Events

**Purpose:** Manage and display chapter events for all users.

**UI Components:** Event cards, event detail pages, event calendar, admin event forms.

**Data Structure:** Firestore 'events' collection (title, date, description, images, slug)

**Key Logic:**
- CRUD operations for events
- Slug generation for dynamic routing
- Real-time Firestore listeners for updates

**Navigation Flow:**
- User visits /events → List fetched from Firestore
- Click event card → /events/[slug] detail page
- Admins access /admin/events for management

**Example:**
```ts
const snapshot = await getDocs(collection(db, "events"));
const events = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
```

---

## Alumni

**Purpose:** Directory and engagement for alumni; supports search and profile view.

**UI Components:** Alumni list, alumni profile page, search/filter UI.

**Data Structure:** Firestore 'alumni' collection (name, batch, profile, slug)

**Key Logic:**
- Listing and filtering alumni
- Dynamic routing to /alumni/[slug]

**Navigation Flow:**
- User visits /alumni → List view
- Click alumni card → /alumni/[slug] profile

**Example:**
```ts
const snapshot = await getDocs(collection(db, "alumni"));
const alumni = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
```

---

## Certificates

**Purpose:** Issue and verify certificates for events and achievements.

**UI Components:** Certificate verification form, admin certificate issue form, certificate detail display.

**Data Structure:** Firestore 'certificates' collection (certId, studentName, eventName, date, url)

**Key Logic:**
- Certificate creation by admin
- Public lookup by certId
- Verification API route

**Navigation Flow:**
- User visits /certificate-verification → Enters certId
- System queries Firestore and displays result
- Admins manage certificates in /admin/certificates

**Example:**
```ts
const snapshot = await getDocs(query(collection(db, "certificates"), where("certId", "==", certId)));
const cert = snapshot.docs[0]?.data() ?? null;
```

---

## Admin Dashboard

**Purpose:** Centralized management for all chapter data and content.

**UI Components:** Sidebar navigation, CRUD tables/forms for events, blogs, members, certificates.

**Data Structure:** Aggregates Firestore collections (events, members, blogs, certificates)

**Key Logic:**
- Auth gate for admin-only access
- CRUD UI for all entities
- Real-time sync with Firestore

**Navigation Flow:**
- Admin logs in → /admin dashboard
- Navigates to entity section (events, blogs, etc.)

**Example:**
```ts
if (!user || user.role !== "admin") {
	redirect("/admin/login");
	return null;
}
```

---

## Blog

**Purpose:** Publish and manage articles for chapter news and updates.

**UI Components:** Blog list, blog detail, markdown editor (admin), blog CRUD forms.

**Data Structure:** Firestore 'blogs' collection (title, content, author, date, slug)

**Key Logic:**
- Blog CRUD operations
- Dynamic routing to /blog/[slug]
- Markdown rendering for content

**Navigation Flow:**
- User visits /blog → List view
- Click article → /blog/[slug] detail
- Admins manage blogs in /admin/blog

---

## Gallery

**Purpose:** Showcase event and chapter photos; offloads media to Cloudinary.

**UI Components:** Gallery grid, image upload form (admin), gallery detail modal.

**Data Structure:** Cloudinary media, Firestore 'gallery' records (image url, event, date)

**Key Logic:**
- Image upload to Cloudinary
- Metadata write to Firestore
- Gallery display with CDN-backed images

**Navigation Flow:**
- User visits /gallery → Images loaded from Firestore/Cloudinary
- Admins upload via /admin/gallery

---

## Team

**Purpose:** Display chapter team by year; supports filtering and detail view.

**UI Components:** Team list, year filter, member cards.

**Data Structure:** Firestore 'team' collection (name, role, year)

**Key Logic:**
- Listing by year
- Dynamic routing for team details

**Navigation Flow:**
- User visits /team → List by year

---
