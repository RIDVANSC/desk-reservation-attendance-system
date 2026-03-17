x# Geofencing Logic

## Overview

The geofencing component is a critical part of the Attendance Confirmation App, designed to ensure that users can only confirm attendance when they are physically present in the office.

Without this mechanism, users could potentially confirm attendance remotely (e.g., by scanning a QR code image from home), which would undermine the integrity of the desk reservation system.

This implementation enforces location-based validation using device GPS data and distance calculations.

---

## Objectives

The geofencing system was designed to achieve the following:

- **Prevent Remote Check-ins**  
  Ensure users cannot confirm attendance outside the office  

- **Enforce Physical Presence**  
  Guarantee that confirmed reservations correspond to real desk usage  

- **Maintain System Integrity**  
  Protect against misuse of QR codes or reservation loopholes  

- **Provide Clear User Feedback**  
  Inform users whether they are eligible to confirm attendance  

---

## How It Works

The geofencing logic follows these steps:

1. Retrieve the user’s current GPS coordinates from the device  
2. Compare the user’s location with the office location  
3. Calculate the distance between the two points  
4. Check if the distance is within the allowed radius  
5. Allow or block attendance confirmation accordingly  

---

## Configuration

The system uses the following parameters:

- **Office Latitude**
- **Office Longitude**
- **Allowed Radius (meters)**

Example:

- Latitude: 30.03221  
- Longitude: 31.462774  
- Radius: 300 meters  

These values can be adjusted depending on building size and GPS accuracy requirements.

---

## Distance Calculation (Haversine Formula)

To accurately measure the distance between two geographic points, the system uses the **Haversine formula**, which calculates the great-circle distance between two coordinates on a sphere.

### Why Haversine?

- Accounts for Earth’s curvature  
- More accurate than simple Euclidean distance  
- Suitable for GPS-based proximity checks  

---

## Power Fx Implementation

The geofencing logic is implemented directly in Power Fx within the Attendance Confirmation App.

```powerfx
// Site center and allowed radius
Set(varSiteLat, 30.03221);
Set(varSiteLng, 31.462774);
Set(varAllowedRadius, 300);

// Guard: ensure location is available
If(
    IsBlank(Location.Latitude) || IsBlank(Location.Longitude),
    Set(LocationStatus, "Please allow Location Services."),
    
    With(
        {
            lat1Deg: Location.Latitude,
            lon1Deg: Location.Longitude,
            lat2Deg: varSiteLat,
            lon2Deg: varSiteLng
        },
        With(
            {
                dLat: Radians(lat2Deg - lat1Deg),
                dLon: Radians(lon2Deg - lon1Deg),
                lat1: Radians(lat1Deg),
                lat2: Radians(lat2Deg),
                R: 6371000
            },
            Set(
                varDist,
                2 * R * Asin(
                    Sqrt(
                        Sin(dLat/2)^2 +
                        Cos(lat1) * Cos(lat2) * Sin(dLon/2)^2
                    )
                )
            );

            If(
                varDist <= varAllowedRadius || User().Email = "Adham.Elkhouly@eg.nestle.com",
                Set(LocationStatus, "You are at the office"),
                Set(LocationStatus, "You are out of the office")
            )
        )
    )
);