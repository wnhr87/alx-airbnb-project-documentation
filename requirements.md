# Backend Requirements

## 1. User Authentication
- **Endpoints**  
  - POST /api/auth/register  
    - Input: { name, email, password }  
    - Output: { userId, token }  
  - POST /api/auth/login  
    - Input: { email, password }  
    - Output: { userId, token }  
- **Validation**  
  - Email: valid format, unique  
  - Password: min 8 chars, at least one number & symbol  
- **Performance**  
  - Response time < 300ms under 200 RPS  

## 2. Property Management
- **Endpoints**  
  - GET /api/properties  
    - Query: { location, startDate, endDate, priceMin, priceMax }  
    - Output: [ { property } ]  
  - POST /api/properties  
    - Input: { title, description, price, amenities[], availability[] }  
    - Output: { propertyId }  
  - PUT /api/properties/:id  
  - DELETE /api/properties/:id  
- **Validation**  
  - Price > 0  
  - Dates in availability must be future dates  
- **Performance**  
  - Search queries cached for 60s  

## 3. Booking System
- **Endpoints**  
  - POST /api/bookings  
    - Input: { propertyId, userId, startDate, endDate }  
    - Output: { bookingId, status }  
  - PATCH /api/bookings/:id/approve  
  - PATCH /api/bookings/:id/reject  
- **Validation**  
  - startDate < endDate  
  - No overlapping confirmed bookings  
- **Performance**  
  - Booking write latency < 200ms  
