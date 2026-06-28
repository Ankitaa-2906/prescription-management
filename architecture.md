# Architecture Design: System Blueprint & Data Flow

## 1. Text-Based Architectural Overview

```text
+--------------------------------------------------+
|              HTML/CSS CLIENT UI                  |
| - Prescription Upload  - Chat Interface          |
+-------------------------+------------------------+
                          |
                 (1) HTTP Request
                          |
                          v
+-------------------------+------------------------+
|             PYTHON BACKEND                        |
| - Web Server Controller                          |
| - Request Handler                                |
+-------------------------+------------------------+
                          |
                 (2) Prescription Text
                          |
                          v
+-------------------------+------------------------+
|            ANTIGRAVITY AI ENGINE                 |
| - Prescription Parser                            |
| - Medicine Information Extractor                 |
+-------------------------+------------------------+
                          |
                 (3) Structured Response
                          |
                          v
+--------------------------------------------------+
|              Python Backend                      |
| - Formats extracted information                  |
| - Sends response to frontend                     |
+-------------------------+------------------------+
                          |
                 (4) JSON Response
                          |
                          v
+--------------------------------------------------+
|              HTML/CSS CLIENT UI                  |
| Displays:                                        |
| • Medicine Name                                  |
| • Dosage                                         |
| • Frequency                                      |
| • Duration                                       |
| Prompts user: "Have you taken this medicine?"    |
+--------------------------------------------------+
```

---

## 2. Step-by-Step Data Flow

```
[Client UI]            [Python Backend]        [Antigravity AI]
     |                        |                       |
     |-- Upload Prescription->|                       |
     |                        |-- Send Text --------->|
     |                        |                       |
     |                        |<-- Extracted Details--|
     |                        |                       |
     |<-- Display Medicines --|                       |
     |                        |                       |
     |-- "Taken"/"Not Taken"->|                       |
     |                        |                       |
     |<-- Confirmation -------|                       |
```

### Workflow

1. **Prescription Upload:** The user uploads or pastes the prescription into the application.

2. **Prescription Parsing:** The Python backend sends the prescription text to Antigravity AI for processing.

3. **Information Extraction:** The AI extracts:

   * Medicine name
   * Dosage
   * Frequency
   * Duration

4. **Display Results:** The backend returns the extracted information to the frontend, where it is displayed in a clear, structured format.

5. **Basic Chat Interaction:** The chatbot asks the user:

   > "Have you taken this medicine?"

6. **User Response:** The user replies **Taken** or **Not Taken**, and the chatbot acknowledges the response.

---

## Future Enhancements (Not Included in Version 1)

The following features are planned for future versions:

* Automatic medicine schedule generation
* Time-based reminders
* Background scheduler
* Compliance tracking dashboard
* Local or cloud database storage
* Daily medication history and analytics
