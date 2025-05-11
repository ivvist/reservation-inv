# Reservation System Use Cases

## 1. Use Case: Make a Reservation

**Actor**: Guest (widget, mobile app, phone)
**Preconditions**: Guest can access booking interface; tables available in requested window.
**Trigger**: Guest selects desired date, time, and party size.

### Main Flow

1. Guest opens booking interface.
2. System prompts for date, time, and party size.
3. Guest enters details and submits.
4. System searches available tables based on criteria.
5. System displays available slots.
6. Guest selects a slot.
7. System requests guest details (name, contact, preferences).
8. Guest provides details.
9. System creates reservation and assigns one or more tables.
10. System sends confirmation notification (email/SMS/push).

### Alternative Flows

* **No Availability**: System offers waitlist option (go to Waitlist Flow).
* **Modification**: Guest edits before cut-off; system updates reservation.
* **Cancellation**: Guest cancels; system frees table and notifies staff.

### Postconditions

* Reservation status is `confirmed`.
* Guest receives confirmation and reminder per settings.

---

## 2. Use Case: Check-In Guest

**Actor**: Host/Server
**Preconditions**: Reservation exists and check-in window is open.
**Trigger**: Guest arrives and identifies themselves.

### Main Flow

1. Host searches reservation by guest name or QR code.
2. System retrieves reservation details.
3. Host marks guest as `arrived`.
4. System updates reservation status to `occupied` and notifies floor staff.

### Alternative Flows

* **No-show**: After grace period, host marks as `no-show`, system applies fees per policy.

---

## 3. Use Case: Manage Waitlist

**Actor**: Guest, Host
**Preconditions**: All tables booked.
**Trigger**: Guest opts into waitlist.

### Main Flow

1. System prompts guest to join waitlist.
2. Guest provides party size and contact.
3. System places entry in queue and assigns position.
4. When table frees, system notifies next guest (SMS/email).
5. Guest confirms and system converts entry into reservation.

### Alternative Flows

* **Timeout/No Response**: If guest doesn’t confirm in X minutes, system moves to next entry.
* **Cancellation**: Guest cancels waitlist entry; system updates queue.

---

## 4. Use Case: Modify Reservation

**Actor**: Guest
**Preconditions**: Reservation is `confirmed` and within modifiable window.
**Trigger**: Guest requests change (date, time, party size).

### Main Flow

1. Guest accesses reservation via link or profile.
2. System displays current details.
3. Guest edits fields.
4. System validates new slot availability.
5. System updates reservation and notifies guest.

### Alternative Flows

* **New Slot Unavailable**: System offers nearest alternatives.

---

## 5. Use Case: Cancel Reservation

**Actor**: Guest
**Preconditions**: Reservation is `confirmed` and within cancellable window.
**Trigger**: Guest initiates cancellation.

### Main Flow

1. Guest selects cancel option.
2. System requests confirmation.
3. Guest confirms.
4. System updates status to `cancelled`.
5. System frees table and notifies staff.
6. System sends cancellation confirmation to guest.

### Postconditions

* Reservation removed from availability grid.
* Guest notified and any penalties applied per policy.

---

## 6. Use Case: Process Payment

**Actor**: System, Guest
**Preconditions**: Reservation has deposit or payment due.
**Trigger**: Payment at booking, on arrival, or post-dining.

### Main Flow

1. System presents payment options (deposit, card-on-file).
2. Guest provides payment details.
3. System processes payment via gateway.
4. System updates payment record and reservation balance.
5. System sends receipt.

---

## 7. Use Case: Manage Floor Plan

**Actor**: Manager, Host
**Preconditions**: Floor plan configured in the system.
**Trigger**: Manager or host needs to adjust layout or view table status.

### Main Flow

1. User opens floor-plan module.
2. System displays drag-and-drop layout of tables and zones.
3. User adds, removes, or moves tables and sections.
4. System saves layout changes and updates table metadata.
5. Host views updated plan in real time when seating guests.

### Alternative Flows

* **Block Sections**: Manager blocks off sections for private events; system marks tables as unavailable.

### Postconditions

* Floor plan reflects current restaurant layout and blockings.

---

## 8. Use Case: Send Automated Notifications

**Actor**: System
**Preconditions**: Notification templates configured; reservation or event triggers defined.
**Trigger**: Reservation creation, modification, reminder schedule, or waitlist update.

### Main Flow

1. System evaluates triggers (e.g., new booking, upcoming reservation in 24h).
2. System selects appropriate template and channel (email, SMS, push).
3. System populates template with guest and reservation details.
4. System sends notification to guest.
5. System logs delivery status and retries on failure.

### Alternative Flows

* **Opt-Out**: If guest has unsubscribed, system skips sending and records preference.

### Postconditions

* Notifications sent as per schedule; logs updated.

---

## 9. Use Case: Generate Reports

**Actor**: Manager, Analyst
**Preconditions**: Data available for reservations, covers, payments, etc.
**Trigger**: User requests report or scheduled report time arrives.

### Main Flow

1. User selects report type (e.g., daily covers, no-show rate, revenue).
2. System aggregates data from relevant tables.
3. System generates report in chosen format (dashboard, PDF, CSV).
4. System displays report or emails it to stakeholders.

### Alternative Flows

* **Custom Date Range**: User specifies custom date range; system validates and fetches accordingly.

### Postconditions

* Report delivered; data stored for historical analysis.

---

## 10. Use Case: Integrate with Calendar Systems

**Actor**: System, Host
**Preconditions**: User has connected a calendar (Google, Outlook).
**Trigger**: New reservation, cancellation, or modification.

### Main Flow

1. System detects reservation event.
2. System formats event details into calendar entry.
3. System uses API to create/update/delete event in user’s calendar.
4. Host sees reservation on their personal or shared calendar.

### Alternative Flows

* **Sync Failure**: On API error, system retries and logs failure for admin review.

### Postconditions

* Reservation events synchronized with external calendars.
