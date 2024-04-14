---
layout: post
title: SE_06 / Data Modeling - Comer project
subtitle: A data modeling for Comer project (web application - solo project)
# thumbnail-img: /assets/img/rootMe/11d59cb34397e986062eb515f4d32421.png
tags: [MongoDB, data modeling, user casing, NoSQL]
comments: true
author: Lantana Park
---

[Comer Website](https://comer-app.onrender.com/)

Backend: Node.js, Express.js, Mongoose, MongoDB (NoSQL)

## User Case (Entities)

1. **Users:**

   **Account Creation and Verification:**
   Users have the capability to create an account by providing an email address, setting a password, and confirming it. Upon submission, they receive an email containing a verification token. Clicking on the URL within the email activates the account, enabling access to various features on the website.

   **Profile Management:**
   Once registered, users can update their profiles and view booked experiences. They can also access previously created culinary events.

   **Password Management:**
   Users have the option to reset their passwords. If forgotten, they can initiate the process by providing their email address. Upon confirmation, a new email containing a verification token is sent. Clicking on the URL in the email allows users to reset their password. The new password must not match the previous one.

   **Account Deletion:**
   Users can choose to delete their accounts. This action changes their status to inactive without deleting their entire dataset.

2. **Experiences:**

   **Event Creation and Editing:**
   Users have the ability to create and edit multiple events. They can upload image files, which are stored on an AWS S3 bucket. Event details encompass various aspects such as title, description, perks (e.g., food, beverages, transportation, equipment), guest requirements (minimum age, allowance of kids and pets, maximum group size), languages spoken, general availability (start time, end time, date range), tags, price with currency, additional notes for user consideration, likes from other users, and cancellation policy. These details are stored in the database.

   **Event Location:**
   To aid in locating events, relevant information including country, city, state, address (including street number), longitude, latitude, and full address is stored in the database. The location details are retrieved via the Mapbox library from the client side.

   **Display Event:**
   Users can view all saved experiences on the main page. The server retrieves events that are not dated before today's date, ensuring relevance and timeliness of displayed content. Additionally, on the event detail page, available dates and times will be listed. Dates displayed will not precede today's date, maintaining accuracy and relevance.

   **Event Editing Process:**
   When editing events, users can modify specific information without the need to input all details again.

   **Event Search:**
   Users have the capability to search for events by city name, enhancing the accessibility and user-friendliness of the platform.

3. **Comments:**

   Users can create and delete multiple comments on the detailed event pages. Each experience page may host multiple comments. When a comment is posted, it is stored in the database along with the user ID and experience ID as foreign keys, along with the comment's description.

4. **Availabilities:**

   **Entity Creation:**
   When a user opens their event, an availability entity is generated utilizing data from the start time, end time, and date range of the Experience entity. This entity includes the experience ID as a foreign key, multiple dateMaxGuestPairs, many booking details (if a user booked a slot) to track event bookings, and a timestamp.

   **DateMaxGuestPairs Details:**
   Within the indexed dateMaxGuestPairs, objects are stored, containing details such as the date, start time, end time, maximum number of guests allowed, price, and current status.

   **Booking Process:**
   Upon a user booking the event, the maximum number of guests allowed is appropriately decreased to the relevant data and time slot.

   **Booking Object Creation:**
   Additionally, one a user book a slot from an event, an object is created within the availabilities.booking array. This object includes details like date, slotId, userId, experienceId, experienceTitle, UserEmail, startTime, and endTime.

## ER Diagram

```mermaid

    USER {
        string _id PK "Unique identifier"
        string email "Email address"
        string password "Hashed password with salt"
        string password2 "Hashed password2 with salt"
        boolean isActive "Status indicating if the user's account is active"
        boolean isVerified "Status indicating if the user's email is verified"
        string emailToken "Token for email verification process"
        string profilePicture "Profile image"
        string description "Description to introduction"
        string firstName "First name"
        string lastName "Last name"
        string city "City"
        string country "Country"
        string province "Province"
        string street "Street"
        number zip "Zip code"
        number phoneNumber "Phone Number"
        string resetPasswordEmailToken "Token for reset password and email verification process"
        dateTime createdAt "Creation Timestamp"
        dateTime updatedAt "Last Update Timestamp"
    }

     EXPERIENCE {
        string _id PK "Unique identifier"
        string userId FK "Reference from User"
        string title "Title of the Experience"
        string[] language "Languages Offered"
        string description "Brief Description"
        number runningTime "Duration in Minutes"
        number minimumAge "Minimum Age Requirement"
        string country "Country"
        string city "City - used to search"
        string state "State (if applicable)"
        string address "Street Address"
        number longitude "Longitude"
        number latitude "Latitude"
        string[] coordinates "String version of longitude and latitude"
        string fullAddress "Full Postal Address"
        array FILES "Embedded array for image urls"
        string[] likes "User Likes - userId"
        object PERKS "Embedded Perks Object"
        string notice "Special Notice from Host"
        string startTime "Starting Time"
        boolean kidsAllowed "Kids Allowed"
        boolean petsAllowed "Pets Allowed"
        string endTime "Ending Time"
        number maxGuest "Maximum Number of Guests"
        number price "Price"
        string currency "Currency"
        array tags "Embedded experience Tags"
        dateTime startDate "Start Date"
        dateTime endDate "End Date"
        boolean cancellation1 "Cancellation Policy - Condition 1"
        boolean cancellation2 "Cancellation Policy - Condition 2"
        dateTime createdAt "Creation Timestamp"
        dateTime updatedAt "Last Update Timestamp"
    }

    TAGS {
        string tags "Tags"
    }

    FILES {
        string files "Experience image urls"
    }

    PERKS {
         string food "Description of Food Provided"
         string beverage "Description of Beverages Provided"
         string transportation "Description of Transportation Provided"
         string alcohol "Description of Alcohol Provided"
         string equipment "Description of any equipment Provided"
         string others "Description of any others Provided"
    }

    COMMENT {
        string _id PK "The unique identifier of the comment."
        string userId FK "Associates the comment with its author."
        string experienceId FK "Links the comment to the relevant experience."
        string description "The content of the comment."
        dateTime createdAt "Creation Timestamp"
        dateTime updatedAt "Last Update Timestamp"
    }

    AVAILABILITY {
        string _id PK "Unique identifier for availability record"
        string experienceId FK "Reference from Experience"
        object[] dateMaxGuestPairs "Array of Date, Time, and Guest Information"
        object[] booking "Array of booking detailed information"
        dateTime createdAt "Creation Timestamp"
        dateTime updatedAt "Last Update Timestamp"
    }

    DATEMAXGUESTPAIR {
        string _id PK "Unique identifier for date-maxGuest pair"
        dateTime date "Date of Availability"
        string startTime "Start Time"
        string endTime "End Time"
        number maxGuest "Maximum Number of Guests"
        number price "Price"
        string currency "Currency"
    }

    BOOKING {
        string _id PK "Unique identifier for booking"
        dateTime date "Date of Booking"
        string slotId FK "Reference to DateMaxGuestPair"
        string userId FK "User who made the booking"
        string experienceId FK "Reference to Experience"
        string experienceTitle "Title of the Experience"
        string userEmail "Email of the User"
        string startTime "Start Time"
        string endTime "End Time"
        dateTime createdAt "Creation Timestamp"
        dateTime updatedAt "Last Update Timestamp"
    }

```
