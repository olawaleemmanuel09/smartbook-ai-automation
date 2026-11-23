# SmartBook AI

An Axia Africa capstone exploring how service businesses can handle appointment intake, reminders, cancellations and feedback through one workflow.

[Inspect the 24-node export](Smart_Book_AI.json) · [View the workflow diagram](workflow.png)

The booking webhook validates the submission and writes a record to Supabase. Scheduled branches look for reminder windows, send email or SMS and mark the corresponding reminder fields. Cancellation updates the booking record. The evening feedback branch requests a rating and records the request.

## Scope of the export

The graph includes a high-risk decision. The proposed FastAPI/XGBoost inference service is outside this repository. The export alone cannot reproduce model inference or establish any reduction in missed appointments.

## Try it in isolation

Import the JSON into a separate n8n workspace with schedules disabled. Use a disposable Supabase project, test recipients and your own credentials. Trace a synthetic booking through validation, cancellation and each reminder window. Inspect the saved reminder flags before repeating a run. A provider succeeding just before a failed state update can still produce a duplicate notification.

See [configuration names](env.example) and the [security policy](SECURITY.md).
