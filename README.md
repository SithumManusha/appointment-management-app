# 🏥 MedWizard — Clinical Appointment Management Web Application
> **Pre-Screening Practical Assessment Assignment 1**  
> **Candidate:** Sithum Manusha Appuhamy · University of Moratuwa  
> **Target Role:** AI Engineering Intern · Medical Wizard (MedNext Group)

---

## 🌟 Overview
**MedWizard** is a modern, high-reliability clinical appointment management system designed specifically for outpatient specialist clinics and day surgeries. It provides real-time clinician scheduling, dynamic conflict-prevention booking, appointment lifecycle tracking (Upcoming, In-Progress, Completed, Cancelled), and clinical workload analytics.

---

## ✨ Key Features & Architectural Highlights

1. **Deterministic Time-Slot Conflict Detection:**
   - Automatically cross-references doctor ID, appointment date, and time slot to prevent double-booking.
   - Live visual indicator disallows reserving already allocated clinician intervals.
2. **Clinical Appointment Lifecycle Engine:**
   - Full status state transitions: `Upcoming` ➔ `In-Progress` ➔ `Completed` or `Cancelled`.
   - In-place rescheduling modal with pre-filled patient records.
3. **Specialist Clinician Directory:**
   - Multi-specialty support (Cardiology, General Practice, Pediatrics, Orthopedics, Dermatology).
   - Real-time today's load calculation and room allocations.
4. **Instant Search & Multi-Parametric Filtering:**
   - Instant live search across Patient Name, Reference ID, and Attending Doctor.
   - Filter by Status (`ALL`, `Upcoming`, `In-Progress`, `Completed`, `Cancelled`), Doctor, or Specific Calendar Date.
5. **Data Portability & Resilience:**
   - Persistent browser-based `localStorage` cache.
   - **One-Click JSON Export** to download all clinical logs for audit or backup.
   - **One-Click Demo Reset** to restore clean seed data for assessment testing.
6. **Practice Analytics Dashboard:**
   - Consultation urgency ratio visualization (Routine vs. Follow-up vs. Urgent).
   - Specialty patient load distribution metrics.

---

## 🚀 How to Run the Application

The project is built with dual run modes for maximum convenience:

### Option A: Zero-Dependency Instant Run (Recommended)
Simply double-click or open **`index.html`** in any modern web browser (Google Chrome, Microsoft Edge, Mozilla Firefox, Safari).
- **No Node.js, npm, or installation required!**
- Uses standalone React 18, Babel standalone, Tailwind CSS, and Lucide icons loaded via high-availability CDNs.

### Option B: Local Development Server (Vite + React)
```bash
# 1. Navigate to the project root
cd appointment-management-app

# 2. Install dependencies
npm install

# 3. Launch the Vite development server
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 🧪 Testing Strategy & Verification

1. **Double Booking Prevention:**
   - Select Dr. Sarah Jenkins on today's date.
   - Verify that 09:00 AM (already booked by Kumara Silva) is disabled and marked as reserved with a strike-through.
   - Attempting to force an overlapping slot is caught and blocked with a warning dialog.
2. **Appointment Lifecycle State Machine:**
   - Transition an `Upcoming` visit to `In-Progress` (clinical intake).
   - Complete the consultation (`Completed`), updating stats counters in real-time.
3. **Filtering & Search:**
   - Search for patient `"Amara"` or ID `"APT-1002"` to verify sub-millisecond filtering.
   - Filter by `"Urgent"` status to view triage priority patients.
4. **Data Persistence:**
   - Book a new appointment, reload the browser tab, and confirm that the record persists seamlessly via `localStorage`.

---

## 🤖 AI-Assisted Engineering Retrospective

* **AI Tooling Used:** Google Gemini Pro, Claude 3.5 Sonnet, Cursor IDE.
* **Role of AI in Development:** Scaffolding the React state machine, rapid UI prototyping with Tailwind CSS, synthesizing realistic clinical seed datasets, and crafting robust date/time slot conflict detection algorithms.
* **Key Prompts Used:**
  1. *"Design an algorithmic conflict detection function in React that checks if a doctor has an overlapping slot for a given date, ignoring cancelled records."*
  2. *"Generate realistic outpatient clinical appointment records with specialties, room numbers, and patient contact details."*
  3. *"Create an accessible, modern healthcare UI in Tailwind CSS using medical blues, emerald status badges, and responsive tables."*
* **AI Error Encountered & Corrected:**
  - *Issue:* Initial AI suggestion used a simple array `.find()` comparison on appointment time strings across all records without filtering out `Cancelled` appointments. As a result, when a patient cancelled an appointment, that slot remained blocked for subsequent bookings.
  - *Resolution:* Identified the flaw during manual cancellation testing and added an explicit `status !== 'Cancelled'` predicate to `getBookedSlotsForDoctorDate()`, allowing freed slots to become instantly bookable again.

---

## 🔮 Future Enhancements (With 2 Additional Hours)
1. **Automated Patient SMS/Email Reminders:** Webhook integration with Twilio / SendGrid for 24h appointment alerts.
2. **Doctor Multi-Room Calendar Matrix:** Full week-view timeline grid showing all 5 doctors side-by-side with drag-and-drop rescheduling.
3. **FHIR / HL7 Data Compliance:** Export clinical appointments in standardized healthcare interoperability schemas.
