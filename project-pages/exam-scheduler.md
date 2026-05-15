# Overview

The Exam Retake Scheduler is a web-based booking system designed to manage administrator created exam retake sessions. The system supports capacity limits, scheduled time ranges, and multiple student bookings within each session

## Admin Instructions

### How to Log In

![LoginPage](/assets/images/Login.png)

1. Go to /admin/login
2. Enter the admin password: admin123
3. Click “Log In”

### How to Create a Session Slot

![CreateSession](/assets/images/CreateSession.png)

1. Navigate to the Create Slots tab
2. Select a department from the dropdown
3. Enter:

- Session name
- Date
- Capacity
- Start time
- End time

4. Click “Create Session”

### How to View Created Slots

![CreatedSlots](/assets/images/CreatedSlots.png)

1. Go to the Created Slots tab
2. Click “Refresh Slots”
3. View all sessions for the currently selected department

### How to Modify a Slot

![ModifySlot](/assets/images/ModifySlot.png)

1. In Created Slots, click “Edit” on a session
2. Modify fields as needed
3. Click “Save”

### How to Delete a Slot

![DeleteSlot](/assets/images/DeleteSlot.png)

1. Click “Delete” on a session
2. Confirm the deletion

### How to View Student Bookings

![ViewBookedSeats](/assets/images/Booked.png)

1. Go to the Booked Appointments tab
2. Click “Refresh Bookings”
3. View student information for each booking

## Student Instructions

### Booking a Session

![Booking](/assets/images/Booking.png)

1. Navigate to the student page
2. Select a department
3. View available sessions
4. Choose a session
5. Enter:

- Name
- Email
- Course code
- Instructor
- Exam type

6. Submit the form

## Notes and Limitations

- Students book a retake session as a whole rather than selecting a specific time within that session.
- Retake sessions must be created individually; recurring sessions are not currently supported.
- Administrator access is protected by a simple password system intended for demonstration purposes.
- Data is stored locally and is not connected to a persistent database.
- Bookings are automatically confirmed upon submission.
- Administrator approval (confirm/reject workflow) was considered but is not implemented in the current version of the system.
