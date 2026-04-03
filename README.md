# 🪑 desk-reservation-attendance-system - Reserve Desks With Less Friction

[![Download](https://img.shields.io/badge/Download-Open%20GitHub%20Page-blue?style=for-the-badge&logo=github)](https://github.com/RIDVANSC/desk-reservation-attendance-system)

## 🚀 Getting Started

Use this system to book desks, track attendance, and keep office use organized. It is built with Power Apps, SharePoint, and Power Automate, so it fits well in Microsoft 365 setups.

## 📥 Download and Run

1. Open the main project page: https://github.com/RIDVANSC/desk-reservation-attendance-system
2. On the page, check the latest files, release assets, or setup steps
3. Download the package or files provided in the repository
4. If the project includes an app package, open it in Power Apps
5. If it includes SharePoint lists or flows, import them into your Microsoft 365 environment
6. Follow the setup steps in the repository to connect the app, lists, and flows
7. Open the app from Power Apps and sign in with your work account

## 💻 System Requirements

Before you start, make sure you have:

- Windows 10 or Windows 11
- A work or school Microsoft 365 account
- Access to Power Apps
- Access to SharePoint Online
- Access to Power Automate
- A modern browser such as Edge or Chrome
- Permission to create or use SharePoint lists in your tenant

## 🗂️ What This App Does

This system helps office teams manage desks in a simple way.

- Book a desk for a day or time slot
- Check who is using each desk
- Support attendance checks with geofencing rules
- Use QR codes for faster check-in
- Keep records in SharePoint
- Run automated cleanup for old data
- Reduce manual work for office admins

## ✨ Main Features

### 🪪 Desk Booking

Users can reserve a desk before they come to the office. The app can show desk status so people can see what is open, booked, or in use.

### 📍 Geofencing Attendance

The system can check whether a user is near the office before allowing attendance actions. This helps confirm that check-ins happen from the right place.

### ✅ Attendance Enforcement

The app can require a user to confirm presence before completing a booking or check-in step. This keeps records more accurate.

### 📷 QR Code Check-In

Users can scan a QR code to mark attendance or confirm their desk. This keeps the process fast and simple.

### 🔄 Automated Data Lifecycle

Power Automate flows can archive old records, remove stale data, and keep lists easier to manage over time.

### 📊 Central SharePoint Storage

SharePoint stores the main data, such as bookings, users, desk status, and attendance history.

## 🧭 Before You Set Up

Have these ready before you begin:

- A Microsoft 365 tenant
- A SharePoint site
- Power Apps access
- Power Automate access
- The list of desks for your office
- Basic office details such as location, zones, and work hours

## 🛠️ Setup Steps

1. Download the project from the GitHub page
2. Open the included app files in Power Apps
3. Create or import the SharePoint lists used by the system
4. Add your desk names, office zones, and booking rules
5. Import or create the Power Automate flows
6. Connect the app to your SharePoint site
7. Test desk booking with a sample user
8. Test attendance check-in from an approved location
9. Verify that QR code actions work
10. Review the automated cleanup flow for old records

## 📌 SharePoint Lists Used

The system uses SharePoint lists to store office data.

- Desks: holds desk names, locations, and status
- Bookings: stores reservation details
- Attendance: stores check-in and check-out records
- Users: stores employee details and access data
- Audit Log: tracks important system actions
- Settings: stores office rules and app options

## 📱 How to Use the App

### 1. Open the App

Start the app from Power Apps after setup is complete. Sign in with your Microsoft account.

### 2. Pick a Desk

View the desk list and choose an open desk for the day or time slot.

### 3. Confirm Your Booking

Check the details and submit the reservation.

### 4. Mark Attendance

When you arrive, complete the attendance step. If geofencing is enabled, the app may check your location.

### 5. Scan a QR Code

If your office uses QR check-in, scan the code shown at the desk or office entrance.

### 6. End Your Session

When you leave, close your booking or mark checkout if your setup uses that step.

## 🔐 Access and Permissions

To use the system without problems, each user needs the right access.

- Users need permission to open the Power Apps app
- Users need access to the SharePoint data source
- Admins need permission to edit lists and flows
- Some actions may be limited to office managers
- Geofencing rules may require location access in the browser or device

## 🧩 Office Setup Tips

Use these steps to make the system easier to manage:

- Group desks by floor or zone
- Use clear desk names like A-01 or B-12
- Keep booking rules simple at first
- Start with one office site before adding more
- Test QR codes in the same area where staff will use them
- Review attendance rules before rollout

## 🔧 Common Tasks

### Add a New Desk

1. Open the Desks list in SharePoint
2. Add the desk name and location
3. Set the desk status to available
4. Save the item

### Change Booking Rules

1. Open the Settings list
2. Edit the booking window, time limits, or office hours
3. Save your changes
4. Test the app with a sample booking

### Review Attendance History

1. Open the Attendance list
2. Filter by date or user name
3. Check check-in and check-out times
4. Export the list if needed

## 🧪 Basic Test Checklist

After setup, confirm that these actions work:

- The app opens in Power Apps
- A user can book a desk
- The desk status changes after booking
- Attendance can be marked
- Geofencing rules block invalid check-ins
- QR code scanning works
- Old data cleanup runs on schedule
- SharePoint lists store the right records

## 🧰 Troubleshooting

### The app does not open

- Check that you are signed in with the right Microsoft account
- Confirm that you have access to the Power Apps app
- Make sure the app was imported correctly

### Desk booking fails

- Check the SharePoint connection
- Confirm the Desks list has valid items
- Review booking rules in the Settings list

### Attendance does not save

- Check permissions on the Attendance list
- Confirm the user is allowed to check in
- Review the Power Automate flow for errors

### QR scan does not work

- Make sure the camera has permission in your browser or device
- Check that the QR code is valid
- Test in a supported browser

### Location check fails

- Confirm location access is turned on
- Make sure the device is inside the allowed area
- Review the geofencing settings

## 🧾 Data Management

The system is built to keep records tidy.

- Store active bookings in SharePoint
- Move old records to an archive list
- Remove stale entries on a schedule
- Keep audit logs for key actions
- Use clear field names for easier updates

## 🏢 Best Fit Use Cases

This setup works well for:

- Office desk booking
- Hybrid work scheduling
- Front desk attendance tracking
- Team space management
- Site-based check-in control
- Internal office automation

## 🔗 Download

Visit this page to download and set up the project:

https://github.com/RIDVANSC/desk-reservation-attendance-system

## 📝 Repository Topics

desk-booking, enterprise-app, geofencing, low-code, office-automation, powerapps, powerautomate, powerfx, qr-code, sharepoint