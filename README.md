ReDrop — README
What This Project Is

A working prototype of ReDrop, a self-service redelivery and delivery-preferences experience, built for the TS Academy Hajime Cohort 2026 capstone (Logistics/Delivery Experience theme, Group 34).

Live demo link: [paste your Lovable published link here] GitHub repo: [paste your repo link here]

How This Was Built

This project was built using Lovable, an AI-assisted "vibe coding" tool. The team did not write code directly; instead, features were built by describing what was needed in plain language and reviewing/testing what the tool generated.

What Was Generated
Overall app structure and navigation (Home, Order Status, and Reschedule screens)
Order status tracking screen with a 4-step stepper (Placed, Preparing, Out for delivery, Delivered)
Loading, empty, and error states for the order status screen
Delivery failed notification banner
Reschedule form (date and time window selection, optional delivery instructions)
Recovery confirmation screen
Branded header and full color scheme applied across all screens
Mocked sample data for orders, delivery attempts, and available time slots
What We Modified or Adjusted Ourselves
Adjusted the color scheme to match our design system (accent blue, amber for warnings, green for success)
Added a branded header bar consistently across every screen after identifying it was missing
Fixed spacing so content wasn't touching the edges of the mobile frame
Added inline validation on the reschedule form to require a time window before submission
What We Chose Not to Build, and Why
Real GPS/location tracking: explored via a technical trial early in the project, but deliberately dropped — the team lacked prior experience with map/GPS integration and the added complexity wasn't justified given the project timeline (see Scope-Update-TrackIt-Pivot.md)
Real payments processing: out of scope for this MVP, since it doesn't affect the core problem being tested
Rider-side mobile app: not needed to validate the customer-facing recovery experience
Real SMS/push notifications: in-app notification is sufficient to demonstrate the concept for this MVP
Warning/confirmation popups (e.g., "are you sure you want to leave?"): reviewed and deliberately deprioritized, since none are required by the capstone brief and team time was directed to usability testing instead
Architecture Overview
[Customer]
    → opens app
    → views Order Status screen (Flow 1)
    → if delivery fails → sees Delivery Failed banner
    → taps "See recovery options" → Reschedule flow (Flow 2)
    → confirms new time → Recovery Confirmed screen
    → Order Status updates to reflect new delivery time
    → Delivered
Frontend: Built in Lovable, deployed via Lovable's built-in hosting
Data: Mocked sample orders, delivery attempts, and available time slots — hardcoded, not a real database
No real backend integration — all data is simulated for demo purposes, matching an MVP built with mocked data per the capstone brief's allowances
API / Data Approach

Since this is an MVP, data is mocked, not connected to a real backend:

Order data: 3 sample orders hardcoded into the app, each with a different status (one "delivered" to demo the happy path, one "failed" to demo the recovery flow, one "preparing" to show an in-progress state)
Delivery attempts: for the failed order, a mock attempt record includes the attempt number, timestamp, and failure reason
Reschedule requests: when a user submits the reschedule form, the new date, time window, and optional delivery instructions are stored temporarily in the app's memory during the session, not persisted to a database
Available slots: a small mocked list of date/time combinations marked as available or fully booked, used to demo the "no slots available" edge case

If this were built beyond the MVP stage, this section would describe a real database (e.g., Firebase, Supabase) and real vendor/rider data feeds.

Testing Evidence

Basic test plan:

 Customer can view order status and see it update through all states
 Failed delivery triggers a visible notification
 Customer can complete the reschedule flow end-to-end
 App works on both desktop and mobile browser width
 No broken links/buttons in either flow (see findings below — demo controls need separating from customer view)

Test results:

A full usability review was conducted on the reschedule/recovery flow, following the same path a customer would take: opening recovery options, choosing to reschedule, selecting a new date and time, adding a delivery note, confirming the change, and checking the order page afterward.

Overall finding: The core rescheduling journey works and next steps are generally easy to find. The main improvement needed is ensuring the interface always tells the customer one consistent story (e.g., if a redelivery is booked for tomorrow, every status shown on the page should support that, rather than conflicting labels appearing in different places).

Key issues found, by severity:

Severity	Issue	Recommended Fix
Critical	After rescheduling, the page shows "Redelivery scheduled" but the order status simultaneously changes to "Out for Delivery" — conflicting information about whether the driver is already coming	Keep status as "Redelivery scheduled" / "Awaiting redelivery" until the order actually goes out again
High	"Today" remains selectable as a time option even after all time windows for the day have passed	Remove or disable expired time windows
High	The status stepper still shows Placed → Preparing → Out for delivery → Delivered even when a delivery has failed, with no failure state reflected in the tracker itself	Show "Delivery Failed / Redelivery Required" directly in the status tracker area
High	Demo/testing controls (Advance status, Restart, Show error, Show empty state) appear directly under the real customer-facing order information	Hide these during customer-facing sessions or clearly separate them as tester/admin-only controls
High	The final confirmation after rescheduling doesn't provide strong enough reassurance, given the customer is already recovering from a failed delivery	Clearly show the reschedule was saved, repeat the new date/time, and explain what happens next
Medium	"See recovery options" wording isn't everyday delivery language, causing a brief pause before customers understand its meaning	Consider simpler wording such as "Choose what to do next"
Medium	"Attempt 1 of 2 allowed" doesn't explain what happens if the second attempt also fails	Add a short explanation of what happens after the final allowed attempt
Medium	Selected date/time on the reschedule form isn't visually prominent enough	Use a stronger selected-state style plus a checkmark, not color alone
Medium	Delivery instructions field lacks guidance on what it's for	Add helper text clarifying it's for access/drop-off/contact instructions, with any limits stated
Medium	Some secondary text and status colors may not be distinguishable for users with low vision or color-vision differences	Check contrast/text size; ensure important states are never conveyed by color alone
Low/Medium	"Back" and "Confirm" button labels are generic	Use more specific labels like "Back to recovery options" and "Confirm reschedule"
Low	Some screens have excessive white space around the main card, giving a prototype-like feel	Tighten vertical spacing without crowding the screen

Note on scope: The rescheduling flow itself was not found to be unnecessarily complicated — the general sequence is understandable. Most issues identified are about wording or system state clarity, not structural redesign.

Known Limitations / Tech Debt
Data is fully mocked — no real backend, so nothing persists between sessions
No real notification delivery (SMS/push) — in-app only
Status labeling inconsistency: the order status can show conflicting information after a reschedule (see Critical finding above) — flagged for fix, not yet resolved as of this writing
Demo/testing controls are visible on the same screen as the customer-facing view — these were added to simulate status changes for demo purposes but are not separated from the real UI, which could confuse a first-time viewer
Failed delivery state is not reflected in the main status tracker — the tracker continues showing the standard 4-stage progression even when a delivery has failed, so failure feels disconnected from the tracking experience
Expired time slots (e.g., "Today" late in the day) are not automatically disabled
Accessibility: some status indicators may rely partly on color, and contrast on secondary text has not been formally audited
Team

Built by Group 34, Hajime Cohort 2026, for the TS Academy Product Management Capstone.
