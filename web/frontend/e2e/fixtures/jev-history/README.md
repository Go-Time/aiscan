# Synthetic JEV event fixtures

These fixtures retain the event relationships needed for UI regression coverage.
Captured prompts, model output, tool arguments, receipts, run identities, timestamps
and token usage have been replaced with fixed synthetic values. Generic Reflex
programs are reusable examples; no run transcript is retained.

The fixtures cover rejected compilation, publication, dynamic options and feedback.
Set `JEV_EVENTS_FILE`, `JEV_REPLAY_LOG` or `JEV_PROFILE_FLOW_EVENTS` to replay
a local run. Keep those recordings outside Git.
