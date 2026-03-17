# System Architecture

## Overview

The Desk Reservation Attendance System is an end-to-end workspace management solution built using Power Apps, SharePoint, and Power Automate.

The system is designed to solve office overcrowding by enabling employees to reserve desks through an interactive interface, while enforcing physical attendance using QR-based confirmation and geofencing validation. It also incorporates automated workflows and a data archival strategy to ensure long-term scalability and performance.

---

## High-Level Architecture

The system consists of four main layers:

1. **Client Layer (User Interaction)**
2. **Application Layer (Power Apps)**
3. **Data Layer (SharePoint)**
4. **Automation Layer (Power Automate)**

---

## 1. Client Layer (User Interaction)

Users interact with the system through two primary applications:

### Desk Reservation App
- Used to browse desk availability and create or cancel reservations
- Provides an interactive visual experience using floor maps and desk icons
- Optimized for desktop, laptop, and tablet usage

### Attendance Confirmation App
- Lightweight, responsive application designed for mobile use
- Used to confirm physical presence at a reserved desk
- Requires users to enter desk ID (from QR-coded desks)

---

## 2. Application Layer (Power Apps)

### Desk Reservation App

Responsibilities:
- Display desk availability by floor, section, and date
- Allow users to reserve or cancel desks
- Enforce business rules before confirming reservations
- Provide visual feedback using color-coded desk states

Key Features:
- Interactive desk map using icons overlaid on floor images
- Real-time validation using Power Fx
- Dynamic UI updates based on reservation status

---

### Attendance Confirmation App

Responsibilities:
- Validate whether the user has an active reservation for the current day
- Verify physical presence using geofencing
- Confirm attendance and update reservation status

Key Features:
- Minimal UI for fast interaction
- Device-responsive design
- Geofencing validation using location services and distance calculation

---

## 3. Data Layer (SharePoint)

The system uses SharePoint lists as its primary data storage.

### Active_Reservations

Stores all current and future reservations.

Includes:
- user information
- desk ID
- reservation date
- status (Active / Confirmed / Cancelled)
- confirmation metadata

---

### SuperUsers

Stores users with extended privileges.

Used to:
- bypass standard reservation limits
- allow up to 500 active reservations

---

### Archived_Reservations

Stores historical reservation data.

Used for:
- long-term data retention
- reporting and analytics
- maintaining performance of the active dataset

---

## 4. Automation Layer (Power Automate)

Power Automate is used to handle system workflows and background processes.

### Email Notifications

Triggered when:
- a reservation is created
- a reservation is cancelled

Purpose:
- notify users with reservation details
- provide confirmation of actions

---

### Daily Archival Flow

Trigger:
- Scheduled (runs daily at 6:00 AM)

Responsibilities:
- identify past reservations
- move them to the archive list
- delete them from the active list

Purpose:
- prevent SharePoint delegation issues
- maintain performance and scalability

---

## Data Flow

The system follows this typical flow:

1. User selects a desk and date in the Reservation App  
2. Reservation is validated and stored in `Active_Reservations`  
3. Email notification is sent via Power Automate  
4. User arrives at the office  
5. User opens Attendance Confirmation App  
6. App verifies:
   - active reservation
   - geofencing (location within allowed radius)  
7. User confirms attendance  
8. Reservation status is updated to **Confirmed**  
9. Daily archival flow moves past reservations to `Archived_Reservations`  

---

## Geofencing Integration

Geofencing is implemented within the Attendance Confirmation App using Power Fx.

- The system retrieves the user’s device location
- Calculates distance from the office location using the Haversine formula
- Compares distance against an allowed radius

If the user is outside the allowed range:
- attendance confirmation is blocked

This ensures:
- physical presence in the office
- prevention of remote check-ins

---

## Design Principles

The system was designed with the following principles:

### 1. Simplicity
- Minimal UI for confirmation app
- Clear visual indicators for reservation status

### 2. Enforcement of Real-World Constraints
- Attendance confirmation required
- Automatic release of unused reservations

### 3. Scalability
- Daily archival of past reservations
- Reduced risk of delegation issues in SharePoint

### 4. Separation of Concerns
- Reservation and confirmation handled in separate apps
- Data, logic, and automation clearly separated

### 5. Performance Optimization
- Lean active dataset
- Efficient filtering and querying

---

## Summary

This architecture provides a scalable, enforceable, and user-friendly solution for managing desk reservations in a growing organization.

By combining interactive reservation tools, attendance enforcement, geofencing validation, and automated data management, the system ensures efficient workspace utilization while maintaining long-term performance and reliability.