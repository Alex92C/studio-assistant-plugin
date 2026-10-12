---
name: bookings
description: Use when the user wants to book a class, cancel a booking, or join or leave a waiting list. Also use when they ask for one person's bookings.
---

# Bookings

`search_bookings` lists one person's bookings. It does not list who is coming to a class. Use the attendees skill for a roster.

- `book_class` books one occurrence. Members book themselves. The server checks the waiver, capacity, and credits, and may return `needs_form` or `class_full`. Studio operators add a linked client and those checks are skipped.
- `cancel_booking` cancels one booking, including reminders, credit refunds, and waiting-list promotion. Members cancel themselves. Operators cancel a linked client's booking.
- `join_waitlist` and `leave_waitlist` are member self-service for a full class.

These tools are writes. Tell the user what will happen, then call `confirm_plan` with the returned `planId` after they agree.

Use `classItemId` from `get_schedule` or `search_classes`. Do not invent it.
