# Reservation Rules

## Overview

The Desk Reservation Attendance System enforces a set of business rules designed to ensure fair usage, prevent desk hoarding, and maximize workspace utilization.

These rules govern how users create, manage, and confirm desk reservations.

---

## Core Principles

The system is built around the following principles:

- **Fair Access**: Prevent a small number of users from monopolizing desks  
- **Utilization Efficiency**: Ensure reserved desks are actually used  
- **Operational Simplicity**: Keep rules clear and enforceable  
- **Scalability**: Support growing teams without performance degradation  

---

## Reservation Eligibility

A desk can only be reserved if all the following conditions are met:

1. The desk is not already reserved for the selected date  
2. The user has not exceeded their reservation limits  
3. The selected date meets advance booking requirements  
4. The user is authorized to reserve desks  

---

## Reservation Limits

### 1. Active Reservation Limit

- Regular users may have up to **6 active reservations** at any given time  
- Active reservations include:
  - future reservations
  - same-day reservations not yet completed  

If this limit is reached:
- the system blocks additional reservations  

---

### 2. Daily Reservation Limit

- Users are limited in how many desks they can reserve per day  
- The system checks existing reservations for the selected date  

If the daily limit is reached:
- no additional reservations can be made for that day  

---

### 3. SuperUser Privileges

Certain users are granted elevated privileges.

SuperUsers:
- are stored in the `SuperUsers` SharePoint list  
- can hold up to **500 active reservations**  
- are exempt from standard reservation limits  

---

## Desk Availability Rules

A desk is considered **unavailable** if:

- it already has an **Active** reservation for the selected date  
- it has already been **Confirmed** by another user  

---

### Ownership Rule

If a desk is already reserved:

- If reserved by another user:
  - reservation is blocked  

- If reserved by the current user:
  - the user may cancel their own reservation  

---

## Advance Booking Rules

The system enforces a minimum advance booking period.

- Reservations must be made at least **N days in advance**  
- This value is controlled by:
  - `varMinAdvanceDays`  

If the selected date violates this rule:
- the reservation is blocked  

---

## Same-Day Reservation Rules

Same-day reservations are allowed but handled with additional constraints.

- Marked using the `Same Day` flag  
- Subject to stricter attendance confirmation rules  

---

## Reservation Status Lifecycle

Each reservation progresses through the following states:

### 1. Active
- Reservation is created
- Awaiting attendance confirmation  

---

### 2. Confirmed
- User has arrived and confirmed attendance  
- Desk is considered occupied  

---

### 3. Cancelled
- Reservation was:
  - manually cancelled by the user, or  
  - automatically cancelled due to no-show  

---

## Attendance Confirmation Rules

Reservations must be confirmed to remain valid.

### Before 11:00 AM

- If a reservation is made before 11:00 AM:
  - user must confirm attendance **before 11:00 AM**  

If not confirmed:
- reservation is automatically cancelled  
- desk becomes available  

---

### After 11:00 AM (Same-Day Reservations)

- If a reservation is made after 11:00 AM:
  - user has **1 hour** from booking time to confirm  

If not confirmed:
- reservation is cancelled  

---

## Automatic Release of Reservations

The system automatically releases desks when:

- a user does not confirm attendance within the allowed time  
- a reservation expires  

This ensures:
- desks are returned to the pool  
- other users can reserve them  

---

## Validation Logic (Enforced in Power Fx)

Before creating a reservation, the system validates:

- desk availability  
- user daily reservation count  
- user total active reservations  
- advance booking constraints  

If any rule is violated:
- reservation is blocked  
- user receives a clear error message  

---

## User Feedback

The system provides real-time feedback through:

- color-coded desk indicators:
  - Green → available  
  - Red → reserved by another user  
  - Blue → reserved by current user  
  - Light color → confirmed  
  - Gray → unavailable due to limits  

- tooltips explaining:
  - availability  
  - ownership  
  - limit violations  

---

## Edge Cases Handled

The system explicitly handles:

- multiple users attempting to reserve the same desk  
- users exceeding limits  
- same-day booking edge cases  
- users reserving but not showing up  
- users attempting to confirm outside the office  

---

## Summary

These reservation rules ensure that the system remains fair, efficient, and scalable.

By combining reservation limits, confirmation enforcement, and automatic release mechanisms, the system guarantees that desks are actively used rather than passively reserved.