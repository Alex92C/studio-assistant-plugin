---
name: class-schedule
description: Use when the user asks what is on the schedule, wants to create or change a recurring class, or wants to move, cancel, or restore a single class occurrence.
---

# Class schedule

Call `get_schedule` before searching. If the class is already in that snapshot, answer from it or use its ids. Do not search only to refresh the schedule.

- `classItemId` is one dated occurrence.
- `templateUid` / `classId` is the recurring template.
- Past occurrences cannot be changed, cancelled, or restored.
- A new class does not need an existing template id. Call `save_class_template` with an empty `templateId`. The server assigns the id. Do not send `classCode` or `instructorCode`.
- `recurrence` is the number of days between sessions: 7 for every week, 1 for every day. "Every Tuesday at 8:00" uses the next Tuesday as `date`, time `08:00`, and recurrence 7.
- Change one occurrence with `update_class_event`, `cancel_class_event`, or `restore_class_event`.
- Change or delete the recurring series with `save_class_template` or `delete_class_template`.

## Bookings on a class

Changing one class's date or time keeps its bookings. Set `confirmBookingCancellation` to false for that move.

Cancelling a booked class, or changing a template so booked sessions leave the schedule, cancels those bookings, refunds in-app credits, and emails the attendees. Leave `confirmBookingCancellation` false until the user explicitly agrees. Then call the write tool again with `confirmBookingCancellation` true, and `confirm_plan` only after that plan is returned.

With the flag false, booked sessions that would leave the schedule are left untouched.

Dates must fall inside the booking window from `get_session`. If `canViewPastClasses` is false, do not request past dates.

Shared rules: [class event rules](../references/class-event-rules.md).
