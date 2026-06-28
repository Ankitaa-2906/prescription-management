# AI Prescription Reader & Managed Dosage Tracker

## Functional Requirements

### 1. Prescription Upload
- The user can upload or enter a doctor's prescription.
- The system extracts:
  - Medicine name
  - Dosage
  - Frequency
  - Duration

### 2. Medicine Schedule
- The system generates a daily medicine schedule based on the prescription.
- Users can view upcoming doses.

### 3. Medication Reminders
- The chatbot reminds users when it is time to take a medicine.
- Users can confirm whether they have taken the dose.

### 4. Compliance Tracking
- The system records whether each scheduled dose was taken or missed.
- Users can view their medication history.

### 5. User Login
- Each user can access only their own medication schedule and history.

---

# Acceptance Criteria

- Prescription details are extracted correctly.
- Medicine schedules are generated automatically.
- Users receive reminders at the correct time.
- Users can mark doses as Taken or Missed.
- Compliance history is saved and displayed.
- The chatbot responds appropriately to user interactions.

---

# Out of Scope (Version 1)

The following features are not included in the first version:

- OCR from handwritten prescriptions
- Doctor or pharmacy integration
- Automatic medicine refill ordering
- SMS or email reminders
- Multi-language support
- Family account management