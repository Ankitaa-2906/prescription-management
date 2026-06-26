# Implementation Plan: Cumulative Stack Build

This project is built from the bottom up. Each layer acts as a verified, functional dependency for the layer above it.

```
+--------------------------------------------------------------+
| Layer 3: Presentation & Integration                          |
| (HTML/CSS Interface, Chat Panel, Fetch API Endpoint bindings)|
+----------------------------------------------+---------------+
                                               |
                                               v (Consumes States)
+----------------------------------------------+---------------+
| Layer 2: State & Time Tracking Logic                         |
| (Database Model, Scheduling Engine, Temporal clock checks)   |
+----------------------------------------------+---------------+
                                               |
                                               v (Consumes Schemas)
+----------------------------------------------+---------------+
| Layer 1: Core Parsing Engine                                 |
| (Python API + Antigravity AI NLP extraction schema)          |
+--------------------------------------------------------------+
```

## Layer 1: Core Parsing Engine (Foundation)
* **Goal:** Turn unstructured text into clean structured JSON.
* **Tasks:**
  * Configure system prompt for Antigravity AI to isolate medication name, dosage, frequency, and duration.
  * Construct Python Flask endpoint (`POST /api/parse`) to ingest raw user messages.
  * Verify parsing integrity using structured schemas.

## Layer 2: State & Time Tracking Logic (Logic)
* **Goal:** Schedule management and compliance evaluation.
* **Tasks:**
  * Build a scheduling engine that maps frequencies into concrete timestamp events in `dosage_schedule.json`.
  * Create a temporal check function to compare current computer time against scheduled times.
  * Build logging routes (`POST /api/log`) to update status variables to `taken` or `missed`.

## Layer 3: Presentation & Integration (Interface)
* **Goal:** Render a real-time responsive client workspace.
* **Tasks:**
  * Design HTML layout with a glassmorphic prescription input form, schedule list, and floating chat UI.
  * Connect frontend event listeners to Python routes using Fetch API.
  * Synchronize status logs to trigger dynamic DOM redraws immediately on update.
