# SharePoint Schema

## Overview

The Desk Reservation Attendance System uses SharePoint lists as its primary data storage layer.

The schema is designed to:
- support real-time reservation operations  
- enforce business rules  
- track attendance confirmation  
- enable historical data archival  
- maintain performance and scalability  

The system uses three main lists:

- Active_Reservations (operational data)
- SuperUsers (privilege control)
- Archived_Reservations (historical data)

---

## Design Principles

The schema was designed with the following principles:

- **Clarity**: Clear and descriptive column names  
- **Extensibility**: Ability to add new features without breaking existing logic  
- **Performance**: Minimize complexity for Power Apps queries  
- **Separation of Concerns**: Active vs historical data stored separately  

---

# 1. Active_Reservations

## Purpose

Stores all current and future reservations that are actively used by the system.

This list is optimized for:
- real-time queries  
- reservation validation  
- attendance confirmation  

---

## Columns

| Column Name | Type | Required | Description |
|------------|------|----------|-------------|
| User | Person or Group | Yes | The user who created the reservation |
| Desk ID | Number | Yes | Unique identifier of the desk |
| Reservation Date | Date and Time | Yes | Date of the reservation |
| Floor | Single line of text | Yes | Floor identifier |
| Key | Single line of text | Yes | Unique reservation key (used for indexing/lookup) |
| Status | Choice | Yes | Reservation status (Active, Confirmed, Cancelled, Expired) |
| Manager's Email | Single line of text | No | Optional manager notification |
| Guest Email | Single line of text | No | Guest reservation (SuperUsers only) |
| SuperUser | Number | Yes | Indicates elevated privilege (0 or 1) |
| Same Day | Number | Yes | Indicates same-day reservation (0 or 1) |
| Date Reserved | Date and Time | Yes | Timestamp of reservation creation |
| Confirmer Email | Single line of text | No | User who confirmed attendance |
| Confirmation Date/Time | Date and Time | No | Timestamp of attendance confirmation |
| Created | Date and Time | System | Record creation time |
| Modified | Date and Time | System | Last update time |
| Created By | Person or Group | System | Record creator |
| Modified By | Person or Group | System | Last modifier |

---

## Reservation Status Definitions

The system uses four distinct reservation states:

### Active
- Reservation is created and awaiting attendance confirmation  

---

### Confirmed
- User has successfully confirmed attendance  
- Desk is actively occupied  

---

### Cancelled
- Reservation was manually cancelled by the user  

---

### Expired
- Reservation was not confirmed within the allowed time window  
- Automatically cancelled by the system due to no-show  

---

## Key Business Rules Embedded in Schema

### 1. Desk Uniqueness Constraint

- A desk can only have one active reservation per date  
- Enforced using:
  - Desk ID  
  - Reservation Date  

---

### 2. Guest Reservation Rule

- Only users listed in `SuperUsers` can reserve desks on behalf of others  
- This is enforced through:
  - Guest Email column  
  - SuperUser flag  

If a non-SuperUser attempts to reserve for a guest:
- the reservation is blocked  

---

### 3. Status-Driven Logic

- System behavior depends heavily on Status:
  - Active → awaiting confirmation  
  - Confirmed → completed usage  
  - Cancelled → user-initiated release  
  - Expired → system-initiated release  

---

### 4. Same-Day Flag

- Used to trigger stricter confirmation rules  
- Enables time-based enforcement logic  

---

# 2. SuperUsers

## Purpose

Stores users with elevated privileges.

These users can:
- bypass reservation limits  
- create guest reservations  

---

## Columns

| Column Name | Type | Required | Description |
|------------|------|----------|-------------|
| Email | Single line of text | Yes | Identifier for SuperUser |
| Guest Email | Single line of text | No | Optional mapping for guest reservations |
| Created | Date and Time | System | Record creation time |
| Modified | Date and Time | System | Last update time |
| Created By | Person or Group | System | Record creator |
| Modified By | Person or Group | System | Last modifier |

---

## Key Notes

- SuperUsers can hold up to 500 active reservations  
- Only SuperUsers can create reservations for guests  
- Checked during reservation validation  

---

# 3. Archived_Reservations

## Purpose

Stores historical reservation data that is no longer actively used.

This improves:
- performance of Active_Reservations  
- scalability of the system  
- long-term data retention  

---

## Columns

| Column Name | Type | Required | Description |
|------------|------|----------|-------------|
| Reservation ID | Number | Yes | Reference to original reservation |
| Status | Single line of text | Yes | Final status (Active, Confirmed, Cancelled, Expired) |
| Desk ID | Number | Yes | Desk identifier |
| Floor | Single line of text | Yes | Floor identifier |
| Date Created | Date and Time | Yes | Original creation date |
| Key | Single line of text | Yes | Reservation reference key |
| User Email | Single line of text | Yes | Reservation owner |
| Manager's Email | Single line of text | No | Manager info |
| Guest Email | Single line of text | No | Guest info |
| SuperUser | Number | Yes | Privilege flag |
| Date Reserved | Date and Time | Yes | Reservation date |
| Same Day | Number | Yes | Same-day flag |
| Confirmer Email | Single line of text | No | Attendance confirmer |
| Confirmation Date | Date and Time | No | Confirmation timestamp |
| Created | Date and Time | System | Record creation time |
| Modified | Date and Time | System | Last update time |
| Created By | Person or Group | System | Record creator |
| Modified By | Person or Group | System | Last modifier |

---

## Key Notes

- Data is copied from Active_Reservations during archival  
- Includes Expired reservations for analysis  
- Not used in real-time application logic  

---

# Relationships Between Lists

- Active_Reservations → main operational dataset  
- SuperUsers → used for privilege validation  
- Archived_Reservations → stores expired and historical data  

Relationships are maintained through:

- user email  
- reservation key  
- desk ID  

---

# Data Lifecycle

The system follows this lifecycle:

1. Reservation created → Active (Active_Reservations)  
2. Reservation confirmed → Confirmed  
3. Reservation cancelled by user → Cancelled  
4. Reservation not confirmed → Expired  
5. Record archived → Archived_Reservations  

---

# Performance Considerations

To avoid SharePoint delegation issues:

- Active_Reservations is kept small  
- Past and expired reservations are archived daily  
- Filters are designed to be delegation-safe  

---

# Summary

The SharePoint schema provides a structured and scalable data model that supports both operational workflows and long-term system performance.

By distinguishing between Active, Confirmed, Cancelled, and Expired states, and enforcing role-based permissions for guest reservations, the system ensures:

- accurate tracking  
- fair usage  
- high integrity  
- scalable growth  