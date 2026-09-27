# ReDrop

**A self-service redelivery and delivery-preferences experience**

Built for the **TS Academy Hajime Cohort 2026 Capstone — Logistics / Delivery Experience Theme**
**Group 34**

**Live Demo:** https://redrop-your-delivery-buddy.lovable.app
**GitHub Repository:** https://github.com/kessien908-tech/ReDrop-Capstone

---

## 1. Project Overview

ReDrop is a customer-facing prototype designed to make **failed delivery recovery** simpler and more transparent.

Instead of leaving customers unsure about what happens after a failed delivery, ReDrop allows them to:

1. View their current order status
2. Understand when and why a delivery failed
3. Choose a new delivery date and time
4. Add optional delivery instructions
5. Confirm the new delivery arrangement
6. Return to the order status page and see the updated delivery information

The project focuses on the **customer recovery experience** after a failed delivery, rather than attempting to build a complete logistics platform.

---

## 2. Problem We Wanted to Solve

A failed delivery can leave customers with several unanswered questions:

* What happened to my delivery?
* Will another attempt be made?
* When will it arrive?
* Do I need to contact someone?
* Can I choose a more convenient time?

ReDrop explores how a self-service recovery experience could give customers clearer information and more control without requiring them to contact customer support.

---

## 3. Our Solution

We designed a simple recovery flow:

```text
Customer opens app
        ↓
Views Order Status
        ↓
Delivery fails
        ↓
Sees Delivery Failed notification
        ↓
Chooses recovery options
        ↓
Selects new date + time
        ↓
Adds optional delivery instructions
        ↓
Confirms reschedule
        ↓
Sees Recovery Confirmation
        ↓
Order Status reflects new delivery arrangement
```

The prototype focuses on keeping the customer informed at each stage and reducing uncertainty after a failed delivery.


## 4. MVP Scope

### Included in the MVP

* Order status tracking
* Four-stage delivery tracker
* Delivery failure notification
* Self-service rescheduling
* Date and time-slot selection
* Optional delivery instructions
* Confirmation after rescheduling
* Loading, empty and error states
* Mock order and delivery data
* Desktop and mobile browser layouts

### Deliberately Out of Scope

| Feature                     | Reason                                                                                                                                                          |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Real GPS/location tracking  | Explored during an early technical trial but removed because the complexity was not justified within the project timeline. See `Scope-Update-TrackIt-Pivot.md`. |
| Real payments               | Not required to test the core failed-delivery recovery problem.                                                                                                 |
| Rider-side app              | Outside the customer-facing scope of this MVP.                                                                                                                  |
| SMS/push notifications      | In-app notifications were sufficient to demonstrate the concept.                                                                                                |
| Confirmation/warning popups | Deprioritised because they were not required by the brief and team time was better spent on usability testing.                                                  |

---

## 5. Key User Flows

### Flow 1 — Track an Order

The customer opens the application and views their current order status.

The prototype includes four delivery stages:

**Placed → Preparing → Out for Delivery → Delivered**

Different mock orders are used to demonstrate different points in the journey.

### Flow 2 — Recover From a Failed Delivery

When a delivery fails, the customer sees a delivery failure notification and can access the recovery flow.

They can:

* Review their delivery situation
* Select a new date
* Select an available time window
* Add optional delivery instructions
* Confirm the new delivery arrangement

The customer then receives confirmation and can return to the order status screen.

---

## 6. What We Built With Lovable

ReDrop was built using **Lovable**, an AI-assisted "vibe coding" tool.

The team did not write the application code directly. Instead, we described requirements and functionality in natural language, reviewed the generated output, tested the experience, and iteratively adjusted the product.

### Generated With Lovable

* Overall application structure and navigation
* Home, Order Status and Reschedule screens
* Four-step order status tracker
* Loading, empty and error states
* Delivery failure notification
* Reschedule form
* Date and time-window selection
* Recovery confirmation screen
* Mock order and delivery data
* Available time-slot logic
* Initial visual styling

### Adjusted by the Team

Through review and testing, we identified areas where the generated experience needed improvement.

We:

* Adjusted the colour scheme to match our design system
* Added a consistent branded header
* Fixed mobile spacing and edge padding
* Added validation requiring a time window before submission
* Reviewed the recovery journey through a usability-focused test
* Identified state, wording and accessibility issues for further iteration

This iterative process was an important part of the project: rather than treating the generated prototype as finished, we used testing to identify where the experience needed improvement.

---

## 7. Technical Architecture

```text
┌──────────────────────┐
│       Customer       │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    ReDrop Frontend   │
│       (Lovable)      │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     Mocked Data      │
│                      │
│ • Orders             │
│ • Delivery attempts  │
│ • Time slots         │
│ • Reschedule data    │
└──────────────────────┘
```

### Frontend

Built and deployed using Lovable's built-in hosting.

### Data

The prototype uses mocked data rather than a production database.

There is currently no real backend integration.

### Persistence

Reschedule information is stored temporarily in the application's session memory and is not persisted between sessions.

---

## 8. Mock Data

The prototype contains three sample orders:

| Order           | Purpose                                         |
| --------------- | ----------------------------------------------- |
| Delivered order | Demonstrates the completed/happy path           |
| Failed delivery | Demonstrates the recovery and rescheduling flow |
| Preparing order | Demonstrates an order that is still in progress |

For the failed order, the prototype also includes:

* Attempt number
* Delivery timestamp
* Failure reason
* Available rescheduling slots

The available-slot data also includes fully booked options so that an unavailable-slot scenario can be demonstrated.

---

## 9. Testing & Validation

We conducted a usability review of the main rescheduling journey.

The test followed the same path a customer would take:

```text
Open recovery options
        ↓
Choose to reschedule
        ↓
Select date
        ↓
Select time
        ↓
Add delivery note
        ↓
Confirm change
        ↓
Return to order status
        ↓
Check updated delivery information
```

### Basic Functional Test Plan

| Test                                                      | Result              |
| --------------------------------------------------------- | ------------------- |
| View order status                                         | ✅ Passed            |
| View different order states                               | ✅ Passed            |
| See delivery failure notification                         | ✅ Passed            |
| Complete rescheduling flow                                | ✅ Passed            |
| Update order after rescheduling                           | ⚠️ Needs refinement |
| Responsive desktop/mobile layout                          | ✅ Passed            |
| Validate required time window                             | ✅ Passed            |
| Test loading/empty/error states                           | ✅ Implemented       |
| Confirm all customer-facing controls are production-ready | ⚠️ Needs refinement |

---

## 10. Usability Testing Findings

The core rescheduling journey was understandable and could be completed successfully.

The main issues identified were related to **state clarity, wording and consistency**, rather than the overall structure of the flow.

### Critical

**Conflicting order status after rescheduling**

After a customer schedules a redelivery, the interface can show "Redelivery scheduled" while simultaneously displaying "Out for Delivery."

**Recommended fix:**
Keep the status as **"Redelivery scheduled"** or **"Awaiting redelivery"** until the next delivery attempt actually begins.

---

### High Priority

**Expired time slots remain selectable**

"Today" can remain available even after all of today's delivery windows have passed.

**Recommended fix:**
Automatically disable or remove expired time slots.

**Failed delivery isn't represented in the status tracker**

The tracker continues to show:

**Placed → Preparing → Out for Delivery → Delivered**

even after a delivery has failed.

**Recommended fix:**
Introduce a visible failure state such as:

**Delivery Failed → Redelivery Required**

**Demo controls are visible to customers**

Controls such as:

* Advance status
* Restart
* Show error
* Show empty state

appear alongside the customer-facing experience.

**Recommended fix:**
Hide these controls during customer sessions or clearly separate them into a tester/admin area.

**Confirmation could provide stronger reassurance**

After a failed delivery, the customer needs confidence that the new arrangement has actually been saved.

**Recommended fix:**
Clearly display:

* Confirmation that the change was saved
* The new delivery date
* The new time window
* What the customer should expect next

---

### Medium Priority

**"See recovery options" could be clearer**

This wording may require the customer to stop and interpret what it means.

**Possible alternative:**
"Choose what to do next"

**"Attempt 1 of 2 allowed" lacks context**

Customers aren't told what happens if the final attempt also fails.

**Recommended fix:**
Briefly explain what happens after the final allowed attempt.

**Selected date/time could be more prominent**

The selected option should have a stronger visual state and a checkmark rather than relying primarily on colour.

**Delivery instructions need guidance**

Add helper text explaining what customers should use this field for, such as access, drop-off or contact instructions.

**Accessibility needs further review**

Some status indicators rely partly on colour and some secondary text may need stronger contrast.

Important states should remain understandable without relying on colour alone.

---

### Low Priority

**Button labels could be more specific**

Instead of generic labels such as:

* "Back"
* "Confirm"

consider:

* "Back to recovery options"
* "Confirm reschedule"

**Spacing**

Some screens have large amounts of unused white space around the main card. This could be tightened while maintaining comfortable spacing.

---

## 11. What We Learned

The project highlighted an important distinction between **a working prototype and a clear customer experience**.

The rescheduling functionality itself was relatively straightforward. The more significant usability challenges came from making sure the system communicated one consistent state to the customer.

For example, after a customer successfully reschedules, every part of the interface needs to communicate the same thing:

> The previous delivery failed, a new delivery has been booked, and the next attempt has not started yet.

This reinforced the importance of testing not just whether a feature works, but whether the customer understands what the system is telling them.

---

## 12. Known Limitations & Technical Debt

The current prototype is intentionally an MVP and has several limitations:

* No production backend
* No persistent database
* No real-time order data
* No real GPS tracking
* No real SMS or push notifications
* Mocked delivery attempts and time slots
* Reschedule data does not persist between sessions
* Failed delivery state needs to be integrated into the main tracker
* Demo/testing controls need to be separated from the customer experience
* Expired time slots are not automatically disabled
* Accessibility and colour contrast require further auditing

---

## 13. What We Would Build Next

If the project continued beyond the MVP, our next priorities would be:

### 1. Improve state consistency

Ensure order status, delivery banners, confirmation screens and tracking information always reflect the same delivery state.

### 2. Improve the failed-delivery experience

Make the failed state a first-class part of the tracking journey rather than treating it as a separate notification.

### 3. Connect real data

Replace mocked data with a backend such as Firebase or Supabase and connect the experience to real order and delivery information.

### 4. Improve accessibility

Conduct a formal accessibility review covering:

* Colour contrast
* Text size
* Keyboard navigation
* Screen-reader support
* Non-colour status indicators

### 5. Separate customer and testing experiences

Move prototype controls into a dedicated testing/admin environment.

### 6. Add real notifications

Introduce SMS and/or push notifications for important delivery updates.

---

## 14. Project Status

**Current status:** Working MVP / prototype

The core customer journey can be demonstrated end-to-end using mocked data.

The main remaining improvements relate to **state consistency, failed-delivery tracking, accessibility and separating demo controls from the customer-facing experience.**

---

## 15. Team

**Group 34 — TS Academy Hajime Cohort 2026**

Built as part of the **Product Management Capstone — Logistics / Delivery Experience Theme**.

---

## 16. Links

**Live Demo:** https://redrop-your-delivery-buddy.lovable.app

**GitHub Repository:** https://github.com/kessien908-tech/ReDrop-Capstone
