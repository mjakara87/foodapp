# Food App — Use Cases

> This document describes the primary use cases for the **foodapp** platform — a multi-tenant marketplace that connects restaurants and food stores with customers by offering leftover food packages at discounted prices.

---

## Actors

| Actor               | Description                                                                          |
|---------------------|--------------------------------------------------------------------------------------|
| **Super Admin**     | Platform administrator with full access to all tenants, users, and system settings. |
| **Restaurant User** | Tenant-scoped user managing their store, packages, and reservations via the web app. |
| **Customer**        | End user who browses, reserves, and picks up food packages.                          |

---

## Use Case Index

| ID      | Title                                          | Actor           | Priority |
|---------|------------------------------------------------|-----------------|----------|
| UC-A01  | Register & Approve a Restaurant                | Admin           | High     |
| UC-A02  | Suspend or Deactivate a Tenant                 | Admin           | Medium   |
| UC-A03  | Manage Platform Users                          | Admin           | Medium   |
| UC-A04  | View Platform-Wide Statistics                  | Admin           | Low      |
| UC-R01  | Configure Tenant Settings                      | Restaurant User | High     |
| UC-R02  | Create a Food Package                          | Restaurant User | High     |
| UC-R03  | Duplicate a Package for a New Day              | Restaurant User | High     |
| UC-R04  | Edit or Deactivate a Package                   | Restaurant User | High     |
| UC-R05  | View and Manage Incoming Reservations          | Restaurant User | High     |
| UC-R06  | Mark a Reservation as Picked Up                | Restaurant User | High     |
| UC-R07  | View Daily Sales Summary                       | Restaurant User | Medium   |
| UC-C01  | Register a Customer Account                    | Customer        | High     |
| UC-C02  | Browse Restaurants and Packages                | Customer        | High     |
| UC-C03  | Discover Packages via Recommendations          | Customer        | Medium   |
| UC-C04  | Reserve a Food Package                         | Customer        | High     |
| UC-C05  | Cancel a Reservation                           | Customer        | High     |
| UC-C06  | View Reservation History                       | Customer        | Medium   |
| UC-C07  | Rate and Review a Restaurant                   | Customer        | Low      |

---

## Admin Use Cases

---

### UC-A01: Register & Approve a Restaurant

| Field        | Detail                                                 |
|--------------|--------------------------------------------------------|
| **Actor**    | Super Admin                                            |
| **Goal**     | Onboard a new restaurant/food store as a tenant        |
| **Priority** | High                                                   |

**Preconditions**
- Restaurant has submitted a registration request (name, address, contact, category).

**Main Flow**
1. Admin reviews the pending registration request in the admin panel.
2. Admin verifies the restaurant details.
3. Admin approves the tenant — system creates the tenant account and sends credentials to the restaurant.
4. Restaurant user can now log in and configure their profile.

**Alternative Flows**
- *Admin rejects request:* System notifies the applicant with a reason and removes the pending request.
- *Admin requests more information:* System sends a message to the applicant and keeps the request in a pending state.

---

### UC-A02: Suspend or Deactivate a Tenant

| Field        | Detail                                                |
|--------------|-------------------------------------------------------|
| **Actor**    | Super Admin                                           |
| **Goal**     | Temporarily or permanently disable a tenant account   |
| **Priority** | Medium                                                |

**Main Flow**
1. Admin selects a tenant from the tenant list.
2. Admin chooses Suspend (temporary) or Deactivate (permanent).
3. System hides the tenant's packages from all customers.
4. System notifies the tenant of the action and the reason.
5. Active unresolved reservations are cancelled and customers are notified.

**Alternative Flows**
- *Admin reactivates a suspended tenant:* Packages become visible again; tenant is notified.

---

### UC-A03: Manage Platform Users

| Field        | Detail                                                        |
|--------------|---------------------------------------------------------------|
| **Actor**    | Super Admin                                                   |
| **Goal**     | View, search, and moderate customer and restaurant accounts   |
| **Priority** | Medium                                                        |

**Main Flow**
1. Admin searches or filters users by type, status, or name.
2. Admin views user details and activity history.
3. Admin can disable/re-enable an account or reset credentials.

---

### UC-A04: View Platform-Wide Statistics

| Field        | Detail                                             |
|--------------|----------------------------------------------------|
| **Actor**    | Super Admin                                        |
| **Goal**     | Monitor platform health and key metrics            |
| **Priority** | Low                                                |

**Main Flow**
1. Admin opens the statistics dashboard.
2. System displays metrics: active tenants, total packages listed, total reservations, pickup rate, cancellation rate.
3. Admin filters by date range or tenant.

---

## Restaurant / Tenant Use Cases

---

### UC-R01: Configure Tenant Settings

| Field        | Detail                                                              |
|--------------|---------------------------------------------------------------------|
| **Actor**    | Restaurant User                                                     |
| **Goal**     | Set store-wide defaults that apply to all packages                  |
| **Priority** | High                                                                |

**Preconditions**
- Restaurant user is logged in to their tenant account.

**Main Flow**
1. User opens Store Settings.
2. User fills in store details: name, address, description, logo/photo, cuisine category.
3. User sets **default pickup window** (e.g., 18:00 – 20:00) — applied to every new package unless overridden.
4. User sets **cancellation interval**: number of hours before pickup start after which customers can no longer cancel (e.g., 2 hours).
5. System saves settings and applies defaults to future packages.

**Alternative Flows**
- *Missing required fields:* System highlights errors.

---

### UC-R02: Create a Food Package

| Field        | Detail                                                                |
|--------------|-----------------------------------------------------------------------|
| **Actor**    | Restaurant User                                                       |
| **Goal**     | List leftover food as a discounted package for customers to reserve   |
| **Priority** | High                                                                  |

**Preconditions**
- Tenant settings are configured (UC-R01).

**Main Flow**
1. User selects "New Package".
2. User fills in package details:
   - **Name** (e.g., "Mystery Pasta Box", "Mixed Sushi Combo")
   - **Type**: Single item or combo of multiple items
   - **Description**
   - **Image** (upload)
   - **Original price** and **discounted price**
   - **Available count** (how many packages can be reserved)
   - **Pickup date**
   - **Pickup window** (pre-filled from store default, can be overridden)
   - **Dietary tags** (vegetarian, vegan, contains gluten, etc.)
3. User publishes the package — it becomes immediately visible to customers.

**Alternative Flows**
- *Missing required fields:* System highlights errors and blocks publishing.
- *User saves as draft:* Package is not visible to customers until explicitly published.

---

### UC-R03: Duplicate a Package for a New Day

| Field        | Detail                                                              |
|--------------|---------------------------------------------------------------------|
| **Actor**    | Restaurant User                                                     |
| **Goal**     | Quickly re-create yesterday's package for today with minimal effort |
| **Priority** | High                                                                |

**Preconditions**
- At least one previous package exists.

**Main Flow**
1. User selects an existing package and clicks "Duplicate".
2. System creates a copy with the same name, description, image, price, count, and pickup window.
3. System sets the **pickup date** to today by default (user can change it).
4. User reviews and adjusts any fields if needed (e.g., count, price, pickup window).
5. User publishes the duplicated package.

**Alternative Flows**
- *User cancels:* No new package is created.

---

### UC-R04: Edit or Deactivate a Package

| Field        | Detail                                                |
|--------------|-------------------------------------------------------|
| **Actor**    | Restaurant User                                       |
| **Goal**     | Update package details or remove it from the listing  |
| **Priority** | High                                                  |

**Main Flow**
1. User selects an active package from their package list.
2. User edits one or more fields (count, price, description, pickup window).
3. System saves changes — updates are immediately visible to customers.

**Deactivation Sub-flow**
1. User selects "Deactivate" on a package.
2. System removes the package from customer listings.
3. If there are existing reservations, system cancels them and notifies affected customers.

---

### UC-R05: View and Manage Incoming Reservations

| Field        | Detail                                              |
|--------------|-----------------------------------------------------|
| **Actor**    | Restaurant User                                     |
| **Goal**     | See which customers reserved packages and when      |
| **Priority** | High                                                |

**Main Flow**
1. User opens the Reservations view, filtered by date or package.
2. System displays a list: customer name, package, quantity, reservation time, status.
3. User can expand a reservation to see customer contact details for pickup coordination.

**Alternative Flows**
- *No reservations yet:* System shows an empty state.

---

### UC-R06: Mark a Reservation as Picked Up

| Field        | Detail                                                        |
|--------------|---------------------------------------------------------------|
| **Actor**    | Restaurant User                                               |
| **Goal**     | Confirm that a customer collected their package in person      |
| **Priority** | High                                                          |

**Preconditions**
- A reservation is in "Reserved" status and the pickup window has started.

**Main Flow**
1. User locates the reservation (by name or reservation code / QR scan).
2. User taps/clicks "Mark as Picked Up".
3. System updates the reservation status to **Completed** and records the timestamp.

**Alternative Flows**
- *Customer does not show up:* User marks the reservation as **No-Show** after the pickup window closes.

---

### UC-R07: View Daily Sales Summary

| Field        | Detail                                            |
|--------------|---------------------------------------------------|
| **Actor**    | Restaurant User                                   |
| **Goal**     | See today's (or past) reservation and sales data  |
| **Priority** | Medium                                            |

**Main Flow**
1. User opens the Dashboard / Reports section.
2. System displays for the selected date: packages listed, total reserved, total picked up, no-shows, revenue generated.
3. User can filter by date range or package type.

---

## Customer Use Cases

---

### UC-C01: Register a Customer Account

| Field        | Detail                                              |
|--------------|-----------------------------------------------------|
| **Actor**    | Customer                                            |
| **Goal**     | Create a personal account to reserve packages       |
| **Priority** | High                                                |

**Main Flow**
1. Customer opens the app or platform.
2. Customer enters name, email, and password (or signs in with a social provider).
3. System sends an email verification link.
4. Customer verifies email — account is activated.
5. Customer optionally sets dietary preferences and location.

**Alternative Flows**
- *Email already registered:* System prompts to log in or reset password.

---

### UC-C02: Browse Restaurants and Packages

| Field        | Detail                                                             |
|--------------|--------------------------------------------------------------------|
| **Actor**    | Customer                                                           |
| **Goal**     | Find available food packages nearby or by preference               |
| **Priority** | High                                                               |

**Preconditions**
- At least one active package is listed on the platform.

**Main Flow**
1. Customer opens the browse/explore view.
2. Customer can filter by: location/distance, cuisine category, dietary tags, pickup time range, price range.
3. System displays matching restaurants and their active packages with count remaining.
4. Customer selects a restaurant to view its profile and available packages.
5. Customer selects a package to view full details (description, image, prices, pickup window, slots remaining).

---

### UC-C03: Discover Packages via Recommendations

| Field        | Detail                                                                     |
|--------------|----------------------------------------------------------------------------|
| **Actor**    | Customer                                                                   |
| **Goal**     | Receive personalised food package suggestions without manual searching     |
| **Priority** | Medium                                                                     |

**Main Flow**
1. System analyses the customer's past reservations, dietary preferences, and location.
2. System displays a "Recommended for You" section on the home screen.
3. Customer browses recommended packages and restaurants.
4. Customer can dismiss a recommendation or mark as "Not interested" to refine future suggestions.

**Alternative Flows**
- *New customer with no history:* System shows popular packages near the customer's location.

---

### UC-C04: Reserve a Food Package

| Field        | Detail                                                             |
|--------------|--------------------------------------------------------------------|
| **Actor**    | Customer                                                           |
| **Goal**     | Secure a food package for pickup at the restaurant                 |
| **Priority** | High                                                               |

**Preconditions**
- Customer has a verified account and is logged in.
- The package has at least one unit remaining.

**Main Flow**
1. Customer views a package and selects "Reserve".
2. Customer selects quantity (if more than 1 is available).
3. System confirms availability in real time and creates the reservation.
4. System decrements the available count on the package.
5. System sends a confirmation to the customer (in-app + email) with:
   - Reservation code / QR code
   - Restaurant name and address
   - Pickup window
   - Payment reminder (pay on pickup — no online payment)
6. Restaurant user is notified of the new reservation.

**Alternative Flows**
- *Package sells out before confirmation:* System informs the customer and aborts.
- *Customer is not logged in:* System prompts to log in or register first.

---

### UC-C05: Cancel a Reservation

| Field        | Detail                                                                  |
|--------------|-------------------------------------------------------------------------|
| **Actor**    | Customer                                                                |
| **Goal**     | Free a reserved package when the customer can no longer pick it up      |
| **Priority** | High                                                                    |

**Preconditions**
- Reservation is in "Reserved" status.
- Current time is before the **cancellation deadline** (pickup start minus the restaurant's cancellation interval).

**Main Flow**
1. Customer opens their active reservations and selects "Cancel".
2. System checks the cancellation deadline.
3. System cancels the reservation and returns the slot to the package's available count.
4. System notifies the restaurant of the cancellation.
5. Customer receives a cancellation confirmation.

**Alternative Flows**
- *Cancellation deadline has passed:* System informs the customer that cancellation is no longer possible.

---

### UC-C06: View Reservation History

| Field        | Detail                                                     |
|--------------|------------------------------------------------------------|
| **Actor**    | Customer                                                   |
| **Goal**     | Review past and upcoming reservations                      |
| **Priority** | Medium                                                     |

**Main Flow**
1. Customer opens "My Reservations".
2. System displays reservations grouped into:
   - **Upcoming** — Reserved, not yet picked up.
   - **Past** — Completed or no-showed.
   - **Cancelled** — Cancelled by customer or restaurant.
3. Customer can select any entry to view its full details.

---

### UC-C07: Rate and Review a Restaurant

| Field        | Detail                                                        |
|--------------|---------------------------------------------------------------|
| **Actor**    | Customer                                                      |
| **Goal**     | Leave feedback after picking up a package                     |
| **Priority** | Low                                                           |

**Preconditions**
- Customer has at least one reservation with **Completed** status.

**Main Flow**
1. After a completed pickup, system prompts the customer to leave a review.
2. Customer gives a star rating (1–5) and optional text comment.
3. System saves the review and attaches it to the restaurant's public profile.
4. Restaurant user can view all reviews from their dashboard.

**Alternative Flows**
- *Customer skips:* No review is recorded; system does not prompt again for the same reservation.

---

*Document version: 2.0 — April 2026*

