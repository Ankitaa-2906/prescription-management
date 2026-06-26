# Architecture Design: System Blueprint & Data Flow

## 1. Text-Based Architectural Overview

```
+-----------------------------------------------------------+
|                   HTML/CSS CLIENT UI                      |
| - Ingestion Form     - Schedule Timeline    - Chat Panel  |
+-----------------------------+-----------------------------+
                              |
                     (1) HTTP | (4) JSON
                     Requests | DOM Redraws
                              v
+-----------------------------+-----------------------------+
|                 PYTHON BACKEND PIPELINE                   |
| - Web Server Controller     - Core Database API           |
| - Time Evaluator Engine     - Scheduling Algorithm        |
+----------------------+----------------------+--------------+
                       |                      ^
              (2) Context                     | (3) Parsed
                  Prompt                      |     JSON
                       v                      |
+----------------------+----------------------+--------------+
|                ANTIGRAVITY AI ENGINE                      |
| - Schema Parser      - Conversational Agent                 |
+------------------------------------------------------------+
                       |
               Reads / Writes Local State
                       v
            [ dosage_schedule.json ]
```

## 2. Step-by-Step Data Cycle

When a user logs in, checks status, and replies:

```
[Client UI]                [Python API]            [Antigravity AI]       [JSON Storage]
     |                           |                        |                      |
     |--- (Login Request)------->|                        |                      |
     |                           |--- (Read Records)---------------------------->|
     |                           |<-- (Return Log State)-------------------------|
     |                           |                        |                      |
     |                           |--- (Evaluate Time)---->|                      |
     |                           |    Finds pending dose  |                      |
     |                           |    at 08:00 AM.        |                      |
     |                           |<-- (Generate Prompt)---|                      |
     |                           |    "Did you take..."   |                      |
     |<-- (Render Chat Prompt)---|                        |                      |
     |                           |                        |                      |
     |--- (Text: "Yes, did it")->|                        |                      |
     |                           |--- (Detect Intent)---->|                      |
     |                           |    Resolves: log_taken |                      |
     |                           |                        |                      |
     |                           |--- (Write taken status)---------------------->|
     |                           |<-- (Ack Update)-------------------------------|
     |<-- (Trigger DOM redraw)---|                        |                      |
```

1. **Session Access:** The user logs into the UI. The frontend fires a request to `/api/status`.
2. **State Check:** The Python backend reads `dosage_schedule.json` and loads active medication schedules.
3. **Temporal check:** The backend compares the current local clock against target dose times. It finds a pending dose that was scheduled in the past.
4. **Chat Ingress:** The backend asks Antigravity AI to formulate a custom check-in prompt: *"Hi! Did you take your 8 AM Amoxicillin?"* This is rendered in the chat panel.
5. **Log Processing:** The user replies *"Yes, did it."* The text is submitted to `/api/chat`. The backend identifies the affirmative intent, logs the event as `taken` in `dosage_schedule.json`, and returns success.
6. **Interface Sync:** The frontend triggers a UI refresh, updating status badges and compliance progress indicators instantly.
