# Power Automate Flows

## Overview

Power Automate serves as the automation layer of the Desk Reservation Attendance System.

It is responsible for:
- sending reservation-related emails
- enforcing reservation lifecycle rules
- maintaining system performance through data archival

Although flows are not exported in this repository, this document provides full guidance to recreate them.

---

## Flow Inventory

1. Reservation Confirmation Email  
2. Reservation Cancellation / Expiry Email  
3. Daily Archival Flow  

---

# 1. Reservation Confirmation Email

## Purpose

Sends an email when a reservation is successfully created.

---

## Trigger

- When an item is created in `Active_Reservations`

---

## Trigger Condition (Recommended)

Only trigger when:

Status = Active

---

## Inputs

- User
- Desk ID
- Reservation Date
- Floor
- Same Day
- Date Reserved

---

## Actions

1. Get item from SharePoint  
2. Extract reservation details  
3. Build email body  
4. Send email from dedicated mailbox  

---

## Email Content (Suggested)

- Desk ID  
- Reservation Date  
- Floor  
- Confirmation instructions  
- Reminder about attendance rules  

---

## Value

- Confirms successful reservation  
- Provides clarity to user  
- Reduces confusion  

---

# 2. Reservation Cancellation / Expiry Email

## Purpose

Sends an email when a reservation becomes invalid.

Two cases:
- Cancelled → user cancelled  
- Expired → user did not confirm attendance  

---

## Trigger

- When an item is modified in `Active_Reservations`

---

## Trigger Logic

Proceed only if:

Status = Cancelled  
OR  
Status = Expired  

---

## Inputs

- User  
- Desk ID  
- Reservation Date  
- Floor  
- Status  

---

## Actions

1. Detect status change  
2. Branch logic based on status  
3. Build appropriate email  
4. Send email  

---

## Messaging Logic

### Cancelled

- Reservation cancelled successfully  
- Desk is now available  

### Expired

- Reservation expired due to no confirmation  
- Desk has been released  

---

## Value

- Improves transparency  
- Differentiates user vs system actions  
- Reduces support queries  

---

# 3. Daily Archival Flow

## Purpose

Moves past reservations from Active_Reservations to Archived_Reservations.

This prevents:
- delegation issues  
- performance degradation  

---

## Trigger

- Scheduled flow  
- Runs daily at 6:00 AM  

---

## Source

Active_Reservations  

## Destination

Archived_Reservations  

---

## Filter Logic

Use this filter to get past reservations:

concat('ReservationDate lt ''', variables('TodayLocal'), '''')

---

## Flow Steps

### Step 1: Initialize Variable

Name: TodayLocal  
Type: String  

Value example:

formatDateTime(utcNow(), 'yyyy-MM-dd')

---

### Step 2: Get Items

- From Active_Reservations  
- Use filter query above  

---

### Step 3: Apply to Each

For each item:

#### Create Item in Archived_Reservations

Map fields:

- Reservation ID → ID  
- Status → Status  
- Desk ID → Desk ID  
- Floor → Floor  
- Key → Key  
- User Email → User.Email  
- Manager's Email → Manager's Email  
- Guest Email → Guest Email  
- SuperUser → SuperUser  
- Date Reserved → Reservation Date  
- Same Day → Same Day  
- Confirmer Email → Confirmer Email  
- Confirmation Date → Confirmation Date/Time  

---

#### Delete Item

- Delete the item from Active_Reservations  

---

## Important Notes

- Preserve final status:
  - Active
  - Confirmed
  - Cancelled
  - Expired  

- Ensure archive happens before delete  

---

## Value

- Keeps Active_Reservations small  
- Prevents delegation issues  
- Maintains historical records  

---

# Best Practices

## 1. Avoid Duplicate Emails

Use trigger conditions to prevent:
- multiple sends  
- unnecessary triggers  

---

## 2. Maintain Clean Data

Ensure:
- no past reservations remain in Active_Reservations  
- archive runs daily  

---

## 3. Keep Flows Idempotent

Flows should:
- not duplicate actions  
- handle retries safely  

---

## 4. Use Clear Email Messaging

Always explain:
- what happened  
- why it happened  
- what the user should do next  

---

# Future Enhancements

- Reminder emails before reservation  
- No-show analytics  
- Admin dashboards  
- Weekly usage reports  
- Behavioral insights (no-show rate)  

---

# Summary

Power Automate transforms the system into a fully operational solution.

It ensures:
- communication with users  
- enforcement of lifecycle rules  
- long-term scalability  

Without these flows, the system would function, but not reliably at scale.