# Attendance Confirmation

## Overview

The Attendance Confirmation App is a lightweight, mobile-friendly Power Apps application designed to ensure that reserved desks are actually used.

While the reservation system allows users to book desks in advance, the confirmation system enforces physical attendance by requiring users to check in at their assigned desk.

This component is critical to preventing no-shows, improving desk utilization, and maintaining fairness across users.

---

## Design Philosophy

The confirmation system was designed with the following goals:

- **Speed**: Confirmation should take only a few seconds  
- **Simplicity**: Minimal UI to reduce friction  
- **Enforcement**: Prevent false or remote check-ins  
- **Reliability**: Work consistently across devices  

---

## Application Structure

The Attendance Confirmation App contains a minimal interface with the following components:

### 1. Status Banner

Displays real-time system feedback:

- Whether the user has an active reservation for the current day  
- Whether the user is inside or outside the office (geofencing status)  
- Whether location services are enabled  

---

### 2. Desk ID Input

- Users enter the desk ID printed on the physical desk  
- The desk ID corresponds to the reservation record  

---

### 3. Submit Button

- Confirms attendance  
- Updates the reservation status to **Confirmed**  
- Stores confirmation metadata (user, timestamp)

---

## Confirmation Workflow

The system follows a strict validation sequence before confirming attendance:

1. User opens the Attendance Confirmation App  
2. System checks if the user has an active reservation for the current day  
3. System retrieves device location  
4. Geofencing validation is performed  
5. User enters desk ID  
6. System validates:
   - desk ID matches reservation  
   - reservation is still valid  
7. Reservation is updated to **Confirmed**  

---

## Geofencing Enforcement

To prevent users from confirming attendance remotely, the system uses geofencing.

### How It Works

- The app retrieves the user's device location  
- Calculates distance from the office location  
- Compares distance against a predefined radius  

If the user is:

- **Inside the radius** → confirmation allowed  
- **Outside the radius** → confirmation blocked  

---

### Configuration

- Office coordinates (latitude and longitude)  
- Allowed radius (e.g., 300 meters)  

---

### Purpose

This ensures:

- users are physically present in the office  
- QR codes cannot be exploited remotely  
- attendance reflects real-world usage  

---

## Time-Based Enforcement Rules

The system enforces strict time constraints to ensure desks are not left unused.

### 1. Reservations Before 11:00 AM

- Users must confirm attendance before 11:00 AM  

If not confirmed:
- reservation is automatically cancelled  
- desk becomes available  

---

### 2. Same-Day Reservations After 11:00 AM

- Users have **1 hour** from booking time to confirm  

If not confirmed:
- reservation is cancelled  

---

## Automatic Release Mechanism

If confirmation does not occur within the allowed time window:

- Reservation status changes to **Cancelled**  
- Desk is released back into the system  
- Other users can reserve the desk  

---

## Data Updates

Upon successful confirmation, the system updates:

- Status → Confirmed  
- Confirmer Email  
- Confirmation Date/Time  

This ensures accurate tracking of desk usage.

---

## User Feedback

The app provides immediate feedback to guide user actions.

### Possible States

- **Active Reservation + In Office** → Ready to confirm  
- **Active Reservation + Out of Office** → Confirmation blocked  
- **No Active Reservation** → Cannot confirm  
- **Location Disabled** → Prompt to enable location services  

---

## Edge Cases Handled

The system explicitly handles:

- Users attempting confirmation without a reservation  
- Users entering incorrect desk ID  
- Users outside the allowed geofencing radius  
- Users with disabled location services  
- Expired reservations  

---

## Why This Component Matters

Without attendance confirmation:

- Users could reserve desks and not show up  
- Desk availability would become unreliable  
- System fairness would degrade  

By enforcing confirmation:

- unused desks are automatically released  
- utilization improves  
- user behavior aligns with system goals  

---

## Summary

The Attendance Confirmation App transforms the reservation system from a passive booking tool into an actively enforced workspace management solution.

By combining:
- simple UX  
- geofencing validation  
- time-based rules  
- automatic release logic  

the system ensures that desk reservations reflect actual physical usage in the office.