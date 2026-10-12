---
name: forms-and-settings
description: Use when the user asks about waivers, intake forms, the refund policy, whether class participants are visible, or the last-minute cancellation window.
---

# Forms and settings

- `get_forms` lists waiver and intake templates for the studio.
- `save_form` with `kind: "template"` creates or updates a template. Studio operators only. This is a write: call `confirm_plan` after the user agrees.
- `save_form` with `kind: "filled"` saves the signed-in member's completed form so a booking can continue. Members can save only their own form.
- `get_settings` returns the user settings document and the refund / no-show policy.
- `update_settings` changes one of `refund_no_show`, `show_participants`, or `last_minute_duration`. Studio operators only. Confirm the plan before it is saved.

Do not invent policy text. Show the current policy from `get_settings` before proposing a change.
