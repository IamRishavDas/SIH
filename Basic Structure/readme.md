# **India Post Delivery Slot Management System**


## Technologies Used
- **Backend:** Spring Boot, Spring Security, Spring Data JPA, Hibernate
- **Frontend:** React, Thymeleaf
- **Database:** MySQL, MongoDB
- **Authentication:** JWT (JSON Web Tokens)
- **Notifications:** Twilio (for SMS), SendGrid (for Email)
- **AI/ML Recommendation Engine:** TensorFlow/Python API (integrated via REST API)
- **Deployment:** Docker, Kubernetes, AWS/GCP

---

## API Endpoints

### 1. **User Authentication and Management APIs**
These APIs manage the users of the system, including senders, recipients, postmen, and admin staff.

- **POST /api/auth/signup**  
  _Registers a new user (sender, recipient, postman, admin)._  
  Input: `name`, `email`, `password`, `role`  
  Output: Success/failure message

- **POST /api/auth/login**  
  _Logs in an existing user and generates a JWT token._  
  Input: `email`, `password`  
  Output: JWT token for authenticated sessions

- **POST /api/auth/logout**  
  _Logs out the current user._  
  Input: JWT token  
  Output: Success/failure message

### 2. **Consignment Management APIs**
Manage consignments and time slots for senders and recipients.

- **POST /api/consignments/book**  
  _Books a consignment and allows time slot selection._  
  Input: Consignment details, time slot  
  Output: Booking confirmation, consignment ID

- **GET /api/consignments/{consignmentId}**  
  _Fetches consignment details by ID._  
  Input: `consignmentId`  
  Output: Consignment details, status, tracking info

- **PUT /api/consignments/{consignmentId}/modify-slot**  
  _Modifies delivery time slot for a consignment._  
  Input: `newTimeSlot`, `consignmentId`  
  Output: Success/failure message

- **GET /api/consignments/track/{trackingNumber}**  
  _Tracks a consignment's delivery status._  
  Input: `trackingNumber`  
  Output: Current location, status, estimated delivery time

### 3. **Time Slot Management APIs**
Handles the selection and modification of delivery time slots.

- **GET /api/timeslots/available**  
  _Retrieves available time slots for a specific delivery location._  
  Input: `postalCode`, `date`  
  Output: List of available time slots

- **POST /api/timeslots/select**  
  _Selects a delivery time slot for a consignment._  
  Input: `timeSlot`, `consignmentId`  
  Output: Success/failure message

- **PUT /api/timeslots/{consignmentId}/modify**  
  _Modifies the selected delivery time slot._  
  Input: `consignmentId`, `newTimeSlot`  
  Output: Success/failure message

### 4. **Notification APIs**
Send notifications to users (senders, recipients) about consignment status updates.

- **POST /api/notifications/send**  
  _Sends an SMS/Email notification to the user._  
  Input: `recipient`, `messageContent`  
  Output: Success/failure message

- **GET /api/notifications/status/{notificationId}**  
  _Checks the delivery status of a notification._  
  Input: `notificationId`  
  Output: Sent/failed status

### 5. **AI-Powered Recommendation APIs**
AI-powered API to recommend the best time slots for deliveries.

- **GET /api/recommendations/timeslots**  
  _Suggests the best delivery time slots based on historical data._  
  Input: `recipientLocation`, `date`  
  Output: Recommended time slot(s)

- **POST /api/recommendations/feedback**  
  _Collects feedback on recommended time slots._  
  Input: `consignmentId`, `selectedTimeSlot`, `feedback`  
  Output: Success/failure message

### 6. **Delivery Personnel APIs**
Delivery personnel use these APIs to manage their assignments.

- **GET /api/delivery/assignments/{postmanId}**  
  _Fetches assigned consignments for a postman._  
  Input: `postmanId`  
  Output: List of consignments

- **PUT /api/delivery/update-status**  
  _Updates the delivery status of a consignment._  
  Input: `consignmentId`, `status`, `reason`  
  Output: Success/failure message

### 7. **Analytics and Reporting APIs**
Provides analytics and insights into the performance of the system.

- **GET /api/analytics/delivery-performance**  
  _Fetches performance data on deliveries._  
  Input: `dateRange`, `postalArea`  
  Output: Performance metrics (charts)

- **GET /api/analytics/timeslot-usage**  
  _Provides insights into time slot preferences and usage._  
  Input: `dateRange`, `location`  
  Output: Usage data (charts)

---

## Security Considerations
- **JWT Authentication**: All APIs are secured using JWT tokens for authorization.
- **Role-Based Access Control (RBAC)**: Different levels of access for senders, recipients, postmen, and admin users.
- **Data Encryption**: Sensitive data such as passwords are encrypted using bcrypt and other security mechanisms.
