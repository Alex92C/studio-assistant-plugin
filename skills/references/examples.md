1. User: "Show my classes tomorrow"
   Expected: answered from scheduleRag.displayedClassEvents when those events are already loaded; otherwise planned → searchClassOccurrences(defaultOwnerId, classId, className, date, ...) with tomorrow's date
2. User: "What class templates do I have?"
   Expected: answered from scheduleRag.classTemplates. Do not plan searchClassTemplates just to refresh the already-loaded catalog.
3. User: "Find bookings for user ABC123 this week"
   Expected: planned → searchUserBookings(userId, className, date, ...) for that user
4. User: "Who's coming to the next class?"
   Expected: ready → getClassAttendees(defaultOwnerId, "", "", ""). Do not answer from schedule RAG and do not use searchUserBookings or countBookings.
5. User: "Who is booked into that class?"
   Expected: ready → getClassAttendees(ownerId, classItemId from memory or schedule RAG, "", "")
6. User: "Book me into the 9am yoga class"
   Expected: planned → bookClass(classItemId from search/memory, current userId). May return needs_form or class_full.
7. User: "Add John to that class"
   Expected: admin only → planned bookClass(classItemId, linkedClientUserId) as Add attendee (skips waiver/capacity/credits)
8. User: "Cancel the second result"
   Expected: planned → cancelUserBooking(classItemId, bookingId, userId) using resultReferences rank 2
9. User: "can you move it to the 26th at the same time please?"
   Expected: planned → updateSingleClassEvent(classItemId from memory/resultReferences, { date: ISO date for the 26th }, false) and note that any bookings would be cancelled, refunded, and emailed
10. User: "Cancel that class event"
   Expected: planned → cancelClassEvent(classItemId from memory, templateUid/classId from memory, false)
11. User: "Yes, cancel it anyway and refund the bookings"
   Expected: planned → cancelClassEvent(classItemId from memory, templateUid/classId from memory, true) because the user accepted cancelling bookings
12. User: "Restore that cancelled event"
   Expected: planned → restoreClassEvent(classItemId from memory)
13. User: "Put me on the waiting list for that class"
   Expected: planned → joinWaitingList(classItemId, current userId) for the current member
14. User: "Search packages for owner XYZ"
   Expected: planned → searchOwnerPackages(ownerId, ...)
15. User: "Grant Sarah the 10-class pack"
   Expected: admin only → planned addActiveUserPackageItem(linkedClientUserId, transactionId or "", packageData)
16. User: "Create a new class named Yoga that happens every Tuesday at 8 am at Inspire Fitness Centre"
   Expected: planned → addClassItem("", {class: "Yoga", date: next Tuesday, time: "08:00", location: "Inspire Fitness Centre", recurrence: 7}, false). Leave the template id empty.
17. User: "What can you do?"
   Expected: unsupported or needs_clarification → explain supported read/search and confirmed write operations available for the current role
18. User: "Delete all users"
   Expected: unsupported → bulk destructive action not available through assistant
