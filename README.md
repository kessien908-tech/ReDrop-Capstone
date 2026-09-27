# ReDrop

### A self-service redelivery and delivery-preferences experience

**TS Academy Hajime Cohort 2026 — Product Management Capstone**
**Logistics / Delivery Experience Theme | Group 34**

**Live Demo:** https://redrop-your-delivery-buddy.lovable.app
**GitHub Repository:** https://github.com/kessien908-tech/ReDrop-Capstone

---

## 1. Project Overview

ReDrop is a customer-facing prototype designed to make **failed delivery recovery** simpler, clearer, and more self-service.

When a delivery fails, customers can use ReDrop to understand what happened, choose a new delivery date and time, add optional delivery instructions, and confirm their redelivery.

The project focuses specifically on the **customer recovery experience after a failed delivery**, rather than attempting to build a complete logistics platform.

### Core journey

```text
View Order Status
       ↓
Delivery Fails
       ↓
See Delivery Failed Notification
       ↓
Choose Recovery Options
       ↓
Select New Date & Time
       ↓
Add Delivery Instructions
       ↓
Confirm Reschedule
       ↓
View Updated Delivery Information
```

---

## 2. The Problem

A failed delivery can leave customers unsure about what happens next.

They may not know:

* Why the delivery failed
* Whether another attempt will be made
* When the next attempt will happen
* Whether they need to contact customer support
* Whether they can choose a more convenient delivery time

ReDrop explores how a simple self-service experience could give customers **more clarity and control** after a failed delivery.

---

## 3. The Solution

ReDrop provides a single place where customers can:

* Track their order
* See when a delivery has failed
* Understand the recovery options available
* Choose a new delivery date
* Select an available time window
* Add delivery instructions
* Confirm the new delivery arrangement
* Return to the order status page and see the updated information

The goal is to reduce uncertainty and make the recovery process feel straightforward.

---

# 4. MVP Scope

## Included

The MVP includes:

* Order status tracking
* Four-stage delivery tracker
* Delivery failure notification
* Self-service rescheduling
* Date selection
* Time-window selection
* Optional delivery instructions
* Reschedule confirmation
* Loading, empty and error states
* Mock order and delivery data
* Responsive desktop and mobile layouts

## Not Included

| Feature                     | Reason                                                                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Real GPS/location tracking  | Explored during development but removed because the additional technical complexity was not justified within the project timeline. |
| Real payments               | Not required to test the core failed-delivery recovery experience.                                                                 |
| Rider-side application      | Outside the scope of the customer-facing MVP.                                                                                      |
| SMS/push notifications      | An in-app notification was sufficient to demonstrate the concept.                                                                  |
| Confirmation/warning popups | Deprioritised because they were not required for the core journey and the team prioritised usability testing instead.              |

---

# 5. Key User Flows

## Flow 1 — Track an Order

The customer opens the application and views their current order status.

The prototype includes four delivery stages:

**Placed → Preparing → Out for Delivery → Delivered**

Three different mock orders are available to demonstrate different states.

---

## Flow 2 — Recover From a Failed Delivery

When a delivery fails, the customer sees a notification and can access the recovery flow.

They can:

1. Review the failed delivery
2. Choose to reschedule
3. Select a new date
4. Select an available time window
5. Add optional delivery instructions
6. Confirm the change
7. Return to the order status page

The prototype then reflects the new delivery arrangement.

---

# 6. How We Built It

ReDrop was built using **Lovable**, an AI-assisted "vibe coding" tool.

The team did not write the application code directly. Instead, we described the functionality and requirements in plain language, reviewed the generated output, tested the experience, and made adjustments based on what we found.

This allowed us to rapidly prototype and iterate on the customer journey within the capstone timeline.

---

## What Lovable Generated

* Overall application structure
* Navigation between screens
* Home screen
* Order Status screen
* Reschedule screen
* Four-step order tracker
* Loading, empty and error states
* Delivery failure notification
* Rescheduling form
* Date and time selection
* Recovery confirmation screen
* Mock order data
* Mock delivery attempts
* Mock available time slots

---

## What We Adjusted

After reviewing and testing the generated experience, we made several changes ourselves:

* Adjusted the colour scheme to match our design system
* Added a consistent branded header across screens
* Fixed spacing and mobile layout issues
* Added validation requiring a time window before submission
* Reviewed the complete recovery journey
* Identified usability and accessibility issues for further improvement

The process was iterative: we treated the generated prototype as a starting point and used testing to identify what needed to change.

---

# 7. Technical Architecture

```text
┌─────────────────────┐
│      Customer       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   ReDrop Frontend   │
│      Lovable        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│     Mocked Data     │
│                     │
│ • Orders            │
│ • Delivery attempts │
│ • Time slots        │
│ • Reschedule data   │
└─────────────────────┘
```

### Frontend

Built and deployed using Lovable's built-in hosting.

### Backend

There is currently **no real backend integration**.

The prototype uses mocked data to demonstrate the intended experience.

### Data Persistence

Reschedule information is stored temporarily in the application's memory during the session and is not persisted to a database.

---

# 8. Data & Mock Scenarios

The prototype contains three sample orders:

| Sample Order    | Purpose                                         |
| --------------- | ----------------------------------------------- |
| Delivered       | Demonstrates the completed/happy path           |
| Failed delivery | Demonstrates the recovery and rescheduling flow |
| Preparing       | Demonstrates an order that is still in progress |

For the failed order, the prototype includes:

* Delivery attempt number
* Timestamp
* Failure reason
* Available delivery slots

The available-slot data also includes fully booked options to demonstrate an unavailable-slot scenario.

---

# 9. Testing & Validation

We tested the main customer journey from the perspective of someone recovering from a failed delivery.

The usability review followed this sequence:

```text
Open recovery options
        ↓
Choose reschedule
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

## Basic Test Plan

| Test                                                | Result              |
| --------------------------------------------------- | ------------------- |
| Customer can view order status                      | ✅ Passed            |
| Customer can view different order states            | ✅ Passed            |
| Failed delivery triggers a visible notification     | ✅ Passed            |
| Customer can complete the reschedule flow           | ✅ Passed            |
| Reschedule information appears on the order page    | ⚠️ Needs refinement |
| App works on desktop and mobile browser widths      | ✅ Passed            |
| Required time window is validated                   | ✅ Passed            |
| Loading, empty and error states are available       | ✅ Implemented       |
| Customer-facing experience is free of demo controls | ⚠️ Needs refinement |

---

# 10. Usability Testing Findings

### Overall Finding

The core rescheduling journey works and the main next steps are generally easy to understand.

The biggest issues identified were related to **state consistency and clarity**, rather than the overall structure of the journey.

The customer should always receive one consistent message about what is happening with their delivery.

---

## Critical

### Conflicting status after rescheduling

After rescheduling, the interface can show **"Redelivery scheduled"** while the order status simultaneously shows **"Out for Delivery."**

This creates uncertainty about whether the driver is already on the way.

**Recommended fix:**
Keep the status as **"Redelivery scheduled"** or **"Awaiting redelivery"** until the next delivery attempt actually begins.

---

## High Priority

### Expired time slots remain selectable

"Today" can remain available even after all of today's time windows have passed.

**Recommended fix:**
Automatically disable or remove expired time slots.

### Failed delivery is not represented in the status tracker

The tracker continues to show:

**Placed → Preparing → Out for Delivery → Delivered**

even after a delivery has failed.

**Recommended fix:**
Introduce a clear failure state, such as:

**Delivery Failed → Redelivery Required**

### Demo controls are visible in the customer experience

Controls such as:

* Advance status
* Restart
* Show error
* Show empty state

appear directly below the customer-facing order information.

**Recommended fix:**
Hide these controls during customer-facing use or separate them into a dedicated tester/admin area.

### Confirmation could provide stronger reassurance

After a failed delivery, customers need confidence that their new delivery arrangement has been successfully saved.

**Recommended fix:**
Clearly display:

* Confirmation that the change was saved
* New delivery date
* New time window
* What happens next

---

## Medium Priority

### "See recovery options" could be clearer

The phrase may cause a short pause because it is not typical everyday delivery language.

**Possible alternative:**
"Choose what to do next"

### "Attempt 1 of 2 allowed" lacks context

The interface does not explain what happens if the second attempt also fails.

**Recommended fix:**
Add a short explanation of what happens after the final allowed attempt.

### Selected date and time need stronger visual feedback

The selected option is not visually prominent enough.

**Recommended fix:**
Use a stronger selected state and a checkmark rather than relying on colour alone.

### Delivery instructions need guidance

The field does not clearly explain what customers should include.

**Recommended fix:**
Add helper text explaining that the field can be used for access, drop-off or contact instructions.

### Accessibility needs further review

Some status indicators rely partly on colour, and some secondary text may not have sufficient contrast.

**Recommended fix:**
Review colour contrast, text size and ensure important information is communicated through text or icons as well as colour.

---

## Low Priority

### Button labels could be more specific

Instead of:

* "Back"
* "Confirm"

consider:

* "Back to recovery options"
* "Confirm reschedule"

### Excessive whitespace

Some screens have large amounts of unused space around the main card.

**Recommended fix:**
Tighten the vertical spacing while maintaining comfortable touch targets and readability.

---

# 11. What We Learned

One of the main lessons from this project was that **a feature working technically does not necessarily mean the customer experience is clear**.

The rescheduling flow itself was relatively straightforward. The bigger challenge was making sure the interface communicated the correct delivery state at every point.

For example, once a customer has successfully rescheduled, the entire experience should communicate the same message:

> The previous delivery failed, a new delivery has been booked, and the next delivery attempt has not started yet.

This showed us the importance of testing not just whether a feature works, but whether the customer understands what the product is telling them.

---

# 12. Known Limitations & Technical Debt

As an MVP prototype, ReDrop currently has several limitations:

* Data is fully mocked
* No production backend
* No persistent database
* No real-time order data
* No real GPS tracking
* No real SMS or push notifications
* Reschedule data does not persist between sessions
* Failed delivery is not yet integrated into the main status tracker
* Demo/testing controls are visible in the customer-facing experience
* Expired time slots are not automatically disabled
* Accessibility and colour contrast have not been formally audited
* Order status can become inconsistent after rescheduling

---

# 13. Future Improvements

If we continued developing ReDrop beyond the MVP, our next priorities would be:

### 1. Improve status consistency

Ensure the order tracker, banners, confirmation screen and delivery information always communicate the same delivery state.

### 2. Make failed delivery a first-class status

Integrate the failed state directly into the order tracking journey instead of treating it as a separate notification.

### 3. Introduce a real backend

Replace mocked data with a database and real order/delivery data, potentially using a service such as Firebase or Supabase.

### 4. Improve accessibility

Conduct a formal accessibility review covering:

* Colour contrast
* Text size
* Keyboard navigation
* Screen-reader support
* Non-colour status indicators

### 5. Separate customer and testing experiences

Move prototype controls into a dedicated tester/admin environment.

### 6. Add real notifications

Introduce SMS and/or push notifications for important delivery events.

### 7. Revisit location tracking

If future user research shows that live location tracking provides meaningful value, this could be reconsidered as a later feature once the core recovery experience is validated.

---

# 14. Project Status

**Status: Working MVP / Prototype**

The core customer journey can be demonstrated end-to-end using mocked data.

The main remaining improvements relate to:

* State consistency
* Failed-delivery tracking
* Accessibility
* Expired time-slot handling
* Separating demo controls from the customer-facing experience

---

# 15. Team

**Group 34 — TS Academy Hajime Cohort 2026**

Built as part of the **Product Management Capstone — Logistics / Delivery Experience Theme**.

---

# 16. Project Links

**Live Demo:** https://redrop-your-delivery-buddy.lovable.app

**GitHub Repository:** https://github.com/kessien908-tech/ReDrop-Capstone
