---
Name: 🐞 Bug Report
About: Report a reproducible bug or unexpected behavior
Title: "[Bug][FE][BE]: Invalid older check-out dates accepted"
Labels: bug
---

## 📝 Description
The Check-out field on the Shady Meadows website accepts older dates without showing any validation error. Both frontend and backend validation are missing for this scenario.

---

## 🔄 Steps to Reproduce
1. Navigate to [Shady Meadows website](https://automationintesting.online/api/room?checkin=2025-08-28&checkout=2025-08-29).  
2. Scroll down to *Check Availability & Book Your Stay* section.  
3. Select an invalid older date in the *Check Out* field.  
4. Keep the *Check In* date as today's date.  
5. Click the *Check Availability* button.  

---

## 📨 Request & Response

**Request:**  

```http
GET https://automationintesting.online/api/room?checkin=2025-08-28&checkout=2025-08-29 
```

**Path Parameters:** N/A

**Query Parameters:**

- checkin=2025-08-28 && checkout=2025-08-29

**Request Body:** N/A

---

## ✅ Expected Behavior
The Check-out field should only allow valid future dates in the correct format.  
The backend should return a *400 error* for invalid date ranges.

**Expected Response:**
- Status Code: 400
- Response Body: 
```json
{
  "error": "Invalid date range",
  "message": "Check-in date must be before check-out date.",
  "status": 400
}
```

---

## ❌ Actual Behavior
- The Check-out field accepts older invalid values.  
- Backend returns *status 200* with room information instead of an error.

**Actual Response:**
- Status Code: 200
- Response Body: 
```json
{
  "rooms": [
    {
      "roomid": 1,
      "roomName": "101",
      "type": "Single",
      "accessible": true,
      "image": "/images/room1.jpg",
      "description": "Aenean porttitor mauris sit amet lacinia molestie...",
      "features": ["TV","WiFi","Safe"],
      "roomPrice": 100
    },
    {
      "roomid": 2,
      "roomName": "102",
      "type": "Double",
      "accessible": true,
      "image": "/images/room2.jpg",
      "description": "Vestibulum sollicitudin, lectus ac mollis consequat...",
      "features": ["TV","Radio","Safe"],
      "roomPrice": 150
    },
    {
      "roomid": 3,
      "roomName": "103",
      "type": "Suite",
      "accessible": true,
      "image": "/images/room3.jpg",
      "description": "Etiam metus metus, fringilla ac sagittis id...",
      "features": ["Radio","WiFi","Safe"],
      "roomPrice": 225
    }
  ]
}
```

---

## ⚠ Severity
- Low

## ⏫ Priority
- Medium

## 🔍 Root Cause
- Missing backend validation & missing frontend validation

## 📸 Attachment
- [![BR_1 Attachment](BR_1.gif)]( https://drive.google.com/file/d/1tPRZE2iQAZSnBBcCdu_cmJBfPsiTwiM7/view?usp=sharing)
- [📹 BR_1 Attachment](https://drive.google.com/file/d/1v2XArnIvOSi_eUkAU_2Hzc1Ozy23qhuu/view?usp=sharing)
