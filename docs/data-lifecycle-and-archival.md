# Data Lifecycle and Archival

## Overview

The Desk Reservation Attendance System is designed to operate efficiently at scale by actively managing the lifecycle of reservation data.

Rather than allowing operational data to grow indefinitely, the system separates:
- active (real-time) data  
- historical (archived) data  

This approach ensures:
- consistent performance  
- avoidance of SharePoint delegation issues  
- long-term data retention for analysis  

---

## Why Data Lifecycle Management Matters

Power Apps and SharePoint have practical limitations when handling large datasets.

If not managed properly, large lists can lead to:
- delegation warnings  
- incomplete query results  
- slow app performance  
- unreliable user experience  

To address this, the system enforces a structured data lifecycle.

---

## High-Level Lifecycle

Each reservation follows a defined lifecycle:

1. Reservation is created → stored in Active_Reservations  
2. Reservation is used or expires → status updated  
3. Reservation becomes past data → archived  
4. Reservation is removed from active dataset  

---

## Reservation States in Lifecycle

A reservation progresses through one of the following states:

- Active → awaiting confirmation  
- Confirmed → successfully used  
- Cancelled → manually cancelled by user  
- Expired → automatically cancelled due to no-show  

All states are preserved when data is archived.

---

## Data Separation Strategy

The system uses two main data layers:

### 1. Active Data (Operational Layer)

List:
- Active_Reservations  

Characteristics:
- contains only current and future reservations  
- optimized for real-time queries  
- directly used by Power Apps  

---

### 2. Archived Data (Historical Layer)

List:
- Archived_Reservations  

Characteristics:
- contains past reservations  
- not used in real-time app logic  
- supports reporting and analysis  

---

## Archival Strategy

A scheduled Power Automate flow runs daily to move past reservations.

---

## Archival Trigger

- Runs every day at 6:00 AM  

---

## Archival Condition

A reservation is eligible for archival when:

Reservation Date < Today  

---

## Filter Logic

The system uses the following filter expression:

concat('ReservationDate lt ''', variables('TodayLocal'), '''')

---

## Archival Process

For each eligible reservation:

### Step 1: Copy Data

- Create a new record in Archived_Reservations  
- Copy all relevant fields  

---

### Step 2: Preserve State

Ensure the final status is retained:

- Active  
- Confirmed  
- Cancelled  
- Expired  

---

### Step 3: Delete Original Record

- Remove the item from Active_Reservations  

---

## Data Integrity Considerations

The archival process is designed to:

- avoid data loss  
- maintain historical accuracy  
- preserve auditability  

All important fields are copied, including:
- user information  
- desk details  
- reservation timing  
- confirmation data  
- final status  

---

## Performance Benefits

This approach provides several advantages:

### 1. Delegation Safety

- Keeps Active_Reservations small  
- Ensures queries remain fully delegable  

---

### 2. Faster App Performance

- Reduces dataset size  
- Improves load times and responsiveness  

---

### 3. Predictable Behavior

- Prevents inconsistent results from partial queries  

---

## Business Benefits

Beyond performance, this design enables:

- analysis of desk utilization  
- tracking of no-show behavior  
- identification of cancellation patterns  
- long-term reporting  

---

## Example Lifecycle

### Scenario 1: Normal Reservation

1. User reserves desk → Active  
2. User confirms attendance → Confirmed  
3. Day passes → archived  

---

### Scenario 2: No-Show

1. User reserves desk → Active  
2. User does not confirm → Expired  
3. Day passes → archived  

---

### Scenario 3: User Cancellation

1. User reserves desk → Active  
2. User cancels → Cancelled  
3. Day passes → archived  

---

## Edge Cases Handled

The system accounts for:

- same-day reservations  
- late confirmations  
- last-minute cancellations  
- partially completed reservations  

All outcomes are consistently archived.

---

## Design Decisions

### 1. Daily Archival

- Chosen over real-time archival for simplicity and reliability  
- Reduces system complexity  

---

### 2. Full Record Copy

- Ensures historical completeness  
- Avoids dependency on Active_Reservations  

---

### 3. Status Preservation

- Maintains distinction between:
  - Cancelled (user action)  
  - Expired (system action)  

---

## Limitations

- Archival runs once daily (not real-time)  
- Data may remain in Active_Reservations for a short time after becoming irrelevant  
- Historical data is not directly queryable from the app  

---

## Future Enhancements

Potential improvements include:

- real-time archival triggers  
- automated reporting dashboards  
- analytics on no-show rates  
- predictive reservation optimization  
- data export pipelines  

---

## Summary

The data lifecycle and archival strategy is a key component of the system’s scalability.

By:
- separating active and historical data  
- automating daily archival  
- preserving full reservation history  

the system ensures:

- high performance  
- reliable behavior  
- long-term maintainability  