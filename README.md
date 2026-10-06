Replace the entire ### Required Clarifications (NEEDS CLARIFICATION) section with the following ### Resolved Decisions section. Delete all existing clarification bullets in that section. Remove every occurrence of NEEDS CLARIFICATION related to US-02 and US-05. Do not add, invent, or ask any new clarification questions. Do not modify unrelated sections of plan.md. Use the following decisions exactly as specified:



### Resolved Decisions

#### US-02 - Edit Event Details

- Event Manager/Admin can edit the following event fields:
  - `Title`
  - `Description`
  - `StartDateTime`
  - `EndDateTime`
  - `Venue`
  - `Capacity`
- `EventId`, `OwnerUserId`, `CreatedAt`, and `UpdatedAt` are system-managed and cannot be edited by the user.
- `Status` is not directly edited through the Edit Event operation. Event lifecycle changes such as Publish, Cancel, and Close are handled by their respective operations.
- Event details can be edited before or after publication, subject to business rules.
- `StartDateTime` must be before `EndDateTime`.
- `Capacity` cannot be reduced below the number of confirmed registrations.
- Only the Event Manager/Admin who has management rights for the event can perform the edit.
- Successful edits update `UpdatedAt`.
- Invalid input or business-rule violations reject the update without modifying the event.

#### US-05 - View Available Events

- Attendees can view only events whose `Status` is `Published`.
- `Draft`, `Cancelled`, and `Closed` events are not included in the attendee available-events listing.
- The available-events response displays:
  - `EventId`
  - `Title`
  - `StartDateTime`
  - `EndDateTime`
  - `Venue`
  - `Status`
  - `SeatsLeft`
- `SeatsLeft` is calculated as `Capacity - ConfirmedRegistrations` and is not stored as a separate field in the `Events` table.
- Search is supported by `Title` and `Description`.
- Filtering is supported by event date range and `Venue`.
- Results are ordered by `StartDateTime` ascending, with `EventId` ascending as the secondary ordering.
- Pagination is 1-based.
- Default page number is `1`.
- Default page size is `10`.
- Maximum page size is `50`.
- When no events match the search/filter criteria, the API returns HTTP `200` with an empty collection.
- Attendee listing does not expose `OwnerUserId`, `CreatedAt`, or `UpdatedAt`.
