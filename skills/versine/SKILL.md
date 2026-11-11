---
name: versine
description: Use when the user wants to send someone money, pay someone back, settle up with one or several people, send their Versine gifts, ask someone for money, or schedule a settle-up or request through their connected Versine account. Versine settle-ups are drafts. Nothing is sent until the user approves each one in the Versine app with their passkey.
---

# Using Versine

The user connected their own Versine account to this assistant. Settle-ups
you submit, to one person, to several or on a schedule, are drafts that wait
for the user to approve them in the Versine app with their passkey. Requests
ask other people to pay the user; nothing leaves the user's account.

Use the amount the user gives. If they didn't say how much, ask.

## Find people

- Look someone up with `find_contact`, by name or mobile number. Use
  `list_contacts` to browse. Ask the user if the person is unclear.
- For someone who isn't in their contacts, ask the user for their US or
  Canadian mobile number and save them with `add_contact`.
- If the user has no contacts yet, the answer includes
  `import_contacts_url`. Suggest they import their phone's contacts and give
  them the link to open on their phone.
- If a settle-up is refused with `recipient_phone_not_us` or
  `recipient_no_phone_or_email`, ask the user for the person's US or
  Canadian mobile number, save it with `update_contact`, and try again.

## Settle up with one person

Call `settle_up` with their `contact_id`, the amount and a new
`idempotency_key`.

## Settle up with several people

Call `settle_up_group` once, with one item per person and one
`idempotency_key` for the call. It's all or nothing: if anyone can't be
paid, nothing is sent, and each item's `code` says why. Fix those items or
leave them out, then call again with a new `idempotency_key`.

## Send gifts

1. Call `get_gifts` to see how many gifts the user has left.
2. Ask which friends should get one, by name, and find each with
   `find_contact`.
3. Confirm in one line, for example: "Send your $25 gift to Maya?"
4. Once the user says yes, send them all in one `settle_up_group` call, each
   item with its `contact_id` and `gift: true`, and no amount.

## Ask for money

- Ask one person with `ask_to_settle`, or several people on Versine with
  `ask_to_settle_group`. Add a short `note` if the user gave a reason.
- If the result has an `approval_id`, the request waits for the user to
  approve it in the app. `get_request_approval` shows what they decided.
- To take back a request nobody has paid yet, use `cancel_request`.

## Later or on repeat

- To settle up later or on a schedule (once at a set time, or every day,
  week or month), use `schedule_settle_up`. The user sets it up in the
  Versine app.
- To ask for money later or on repeat, use `schedule_request`.
- `list_scheduled_settle_ups` and `list_request_schedules` show what's set
  up. `pause_scheduled_settle_up` pauses a scheduled settle-up, and
  `stop_request_schedule` stops a scheduled request. Only the user can
  resume or stop a scheduled settle-up for good, in the app.

## Report and retry

- Tell the user briefly what each result says. If it includes a link, give
  it to them.
- If a call is interrupted, check `get_status` or `list_activity` before
  trying again. To retry, send the same `idempotency_key` and the same
  input.
- If something fails, is confusing or is missing, tell the Versine team with
  `submit_feedback`.
