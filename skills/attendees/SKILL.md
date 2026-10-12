---
name: attendees
description: Use when the user asks who is coming, who is booked, or for the roster of a class. Do not answer a roster from the schedule snapshot.
---

# Attendees

Call `get_class_attendees`. It is the only roster read.

- For the next class, omit `classItemId`, `className`, and `date`. The server picks the next occurrence for the studio.
- For a class already in the schedule or a previous tool result, pass that `classItemId`.
- For a named or dated class, pass `className` and/or `date`.

`search_bookings` lists one user's bookings. It does not list who is coming to a class.

If participant names are hidden for this studio, the server returns a count without names. Say that plainly.
