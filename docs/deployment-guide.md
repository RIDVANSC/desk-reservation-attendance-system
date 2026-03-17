# Deployment Guide

## Overview

This guide provides step-by-step instructions to deploy the Desk Reservation Attendance System using Power Apps, SharePoint, and Power Automate.

The system consists of:
- Desk Reservation App (Power Apps)
- Attendance Confirmation App (Power Apps)
- SharePoint lists (data layer)
- Power Automate flows (automation layer)

---

## Prerequisites

Before deployment, ensure you have:

- Access to Microsoft Power Apps
- Access to SharePoint Online
- Access to Power Automate
- Permissions to create SharePoint lists and flows
- A SharePoint site to host the lists

---

## Step 1: Create SharePoint Lists

Create the following three lists in your SharePoint site:

- Active_Reservations
- SuperUsers
- Archived_Reservations

Refer to sharepoint-schema.md for exact column definitions.

### Important Notes

- Ensure column names match exactly
- Use correct data types (especially Date/Time and Choice fields)
- Configure the Status column with values:
  - Active
  - Confirmed
  - Cancelled
  - Expired

---

## Step 2: Import Power Apps

### Desk Reservation App

1. Open Power Apps Studio  
2. Click File → Open  
3. Upload: powerapps/desk-reservation.msapp  
4. Save the app  

---

### Attendance Confirmation App

1. Open Power Apps Studio  
2. Click File → Open  
3. Upload: powerapps/attendance-confirmation.msapp  
4. Save the app  

---

## Step 3: Configure Data Connections

For both apps:

1. Go to Data → Add Data  
2. Connect to your SharePoint site  
3. Add the following lists:
   - Active_Reservations
   - SuperUsers
   - Archived_Reservations  

### Verify Bindings

Ensure that:
- All formulas reference the correct list names
- Column names match the schema exactly
- No broken references exist

---

## Step 4: Configure Environment Variables

Update the following variables inside the apps:

### Geofencing Configuration

Set the office location and radius:

- varSiteLat → your office latitude  
- varSiteLng → your office longitude  
- varAllowedRadius → allowed radius in meters (e.g., 300)

---

### Reservation Limits

Configure variables such as:

- varMaxActive → max active reservations (e.g., 6)  
- varMaxPerDay → max reservations per day  
- varMinAdvanceDays → minimum booking lead time  

---

## Step 5: Configure Power Automate Flows

Flows must be recreated manually.

Refer to:
docs/power-automate-flows.md

### Required Flows

1. Reservation Confirmation Email  
2. Reservation Cancellation Email  
3. Daily Archival Flow  

---

### Daily Archival Flow (Critical)

Trigger:
- Scheduled (every day at 6:00 AM)

Filter expression:
concat('ReservationDate lt ''', variables('TodayLocal'), '''')

Actions:
- Move expired reservations to Archived_Reservations  
- Delete them from Active_Reservations  

---

## Step 6: Configure Permissions

### SharePoint Lists

Ensure:
- Users have read/write access to Active_Reservations  
- Only authorized users modify SuperUsers  

---

### Power Apps

- Share both apps with users  
- Assign appropriate access levels  

---

## Step 7: Test the System

### Reservation Flow

- Select a desk and date  
- Create reservation  

Verify:
- Reservation is saved in SharePoint  
- Email notification is sent  

---

### Attendance Confirmation Flow

- Open Attendance Confirmation App  
- Enter desk ID  

Verify:
- Active reservation is detected  
- Geofencing validation works  
- Status updates to "Confirmed"  

---

### Geofencing Test

- Inside allowed radius → should pass  
- Outside radius → should fail  

---

### Archival Flow

- Create past reservations  
- Run flow manually  

Verify:
- Data moves to Archived_Reservations  
- Removed from Active_Reservations  

---

## Step 8: Deployment Checklist

Before going live, confirm:

- SharePoint lists created correctly  
- Power Apps imported successfully  
- Data connections configured  
- Environment variables updated  
- Power Automate flows configured  
- Permissions assigned  
- End-to-end testing completed  

---

## Common Issues & Fixes

### Issue: App cannot find SharePoint list
- Verify connection  
- Check list name spelling  

---

### Issue: Reservation not saving
- Check column mappings  
- Validate required fields  

---

### Issue: Geofencing not working
- Ensure location services are enabled  
- Verify latitude/longitude configuration  

---

### Issue: Delegation warnings
- Confirm archival flow is active  
- Ensure Active_Reservations list remains small  

---

## Summary

This deployment process ensures that the system is correctly configured, scalable, and ready for real-world use.

By following these steps, you will have a fully functional desk reservation and attendance confirmation system with enforced business rules, geofencing validation, and automated data management.