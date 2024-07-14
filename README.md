# Product Management System DOCUMENTATION

## Table of Contents
* [Overview](#Overview)
* [Entities and Relationships](Entities and Relationships)
* [API Endpoints](API Endpoints)

# Product Management System

## Overview

This document outlines the database schema and API endpoints for a product management system. The schema is defined using DBML and covers core functionalities such as user management, organizations, authentication, payments, notifications, and more.

## Entities and Relationships

### Users
Represents a user entity with attributes such as id, name, email, password, and other personal details. A User has many activity logs, notifications, blogs, messages, authentication methods, random data, payments, and invites. A user has one profile setting.

### Organisation
Represents an organization entity with attributes such as id, description, creation and update timestamps. Many Users can belong to many organizations through UserOrganization.

### UserOrganisation
Represents the relationship between users and organizations, with attributes like id, user_id, or_id, and role.

### EmailTemplate
Represents an email template entity with attributes such as id, name, subject, body, and timestamps. One Template can have many messages.

### Contact
Represents a contact entity with attributes such as id, contact name, contact email, and contact message.

### Notification
Represents notifications associated with users, including id, user_id, message, read status, and creation timestamp.

### ActivityLog
Represents an activity log entry associated with users, including id, user_id, activity type, description, and timestamp.

### Blog
Represents a blog post entity with attributes such as id, title, content, author_id, and timestamps.

### Messages
Represents messages sent by users, including id, user_id, status, template_id, sent timestamp, and creation timestamp. Many messages to one template.

### Authentiation
Represents authentication details such as id, user_id, auth_type, auth_token, creation timestamp, and expiration timestamp.

### RandomData
Represents random data associated with users, including id, user_id, data name, and data value.

### ProfileSettings
Represents the profile settings of a user, including id, user_id, language, region, timezone, and timestamps.

### Payment
Represents a payment entity with attributes such as id, user_id, amount, currency, payment method, status, and transaction_id.

### Waitlist
Represents a waitlist entry with attributes such as id, email, and creation timestamp.

### Invite
Represents invitations sent to users or prospective users, with attributes like id, senders_id, receiver_email, status, and timestamps.

### Language
Represents the languages available or preferred by users, including id, language code, and language name.

### REGION
Represents the regions or geographical areas associated with users or organizations, including id, region code, and region name.

## API Endpoints

### Default

#### POST /api/organisation
- **Description**: Create a new organization
- **Consumes**: `application/json`
- **Request Body**: `CreateOrganisation` (required)

```json
{
  "status": "status",
  "message": "message"
}
```

- **Return Type**: `CreateOrganisationRes`
- **Responses**:
  - `201`: Organisation created

#### GET /api/organisations/{orgId}
- **Description**: Get organization by ID
- **Path Parameters**:
  - `orgId` (required)
- **Return Type**: `CreateOrganisation`
- **Example:**
```json
{
  "createdAt": "2000-01-23T04:56:07.000+00:00",
  "name": "John's Organisation",
  "description": "John's default organization",
  "orgId": "eada83aj3ae3"
}

```
- **Responses**:
  - `200`: Organisation details
  - `404`: Organisation not found

#### POST /api/organisations/{orgId}/users
- **Description**: Add user to an organisation
- **Path Parameters**:
  - `orgId` (required)
- **Consumes**: `application/json`
- **Request Body**: `OrganisationAddUserRequest` (required)
```json
{
  "message": "message",
  "status": "status"
}

```
- **Return Type**: `OrganisationAddUserRes`
- **Responses**:
  - `200`: User added to organisation

#### GET /api/users
- **Description**: Get all users
- **Return Type**: array of `RegisterRequest`
- **Example:**
```json
[ {
  "firstName" : "John",
  "lastName" : "cena",
  "createdAt" : "2000-01-23T04:56:07.000+00:00",
  "password" : "password",
  "role" : 0,
  "userName" : "johnCena",
  "userid" : "uuid37aeuau3ja",
  "email" : "user@gmail.com"
}, {
  "firstName" : "John",
  "lastName" : "cena",
  "createdAt" : "2000-01-23T04:56:07.000+00:00",
  "password" : "password",
  "role" : 0,
  "userName" : "johnCena",
  "userid" : "uuid37aeuau3ja",
  "email" : "user@gmail.com"
} ]
```
- **Responses**:
  - `200`: A list of users

#### GET /api/users/{userId}
- **Description**: Get a user by ID
- **Path Parameters**:
  - `userId` (required)
- **Return Type**: `RegisterRequest`
- **Example:**
```json
{
  "firstName" : "John",
  "lastName" : "cena",
  "createdAt" : "2000-01-23T04:56:07.000+00:00",
  "password" : "password",
  "role" : 0,
  "userName" : "johnCena",
  "userid" : "uuid37aeuau3ja",
  "email" : "user@gmail.com"
}
```
- **Responses**:
  - `200`: User details
  - `404`: User not found

#### POST /auth/login
- **Description**: User login
- **Consumes**: `application/json`
- **Request Body**: `LoginRequest` (required)
```json
{
  "user" : {
    "firstName" : "John",
    "lastName" : "cena",
    "createdAt" : "2000-01-23T04:56:07.000+00:00",
    "password" : "password",
    "role" : 0,
    "userName" : "johnCena",
    "userid" : "uuid37aeuau3ja",
    "email" : "user@gmail.com"
  },
  "token" : "token"
}
```
- **Return Type**: `LoginResponse`
- **Responses**:
  - `200`: Successful login

#### POST /auth/magic-link
- **Description**: Send magic link for authentication
- **Consumes**: `application/json`
- **Request Body**: `MagicLinkRequest` (required)

```json
{
  "email": "user@gmail.com"
}
```
- **Responses**:
  - `200`: Magic link sent
  - `400`: Invalid email

#### POST /auth/register
- **Description**: User sign up
- **Consumes**: `application/json`
- **Request Body**: `RegisterRequest` (required)
```json
{
  "firstName" : "John",
  "lastName" : "cena",
  "createdAt" : "2000-01-23T04:56:07.000+00:00",
  "password" : "password",
  "role" : 0,
  "userName" : "johnCena",
  "userid" : "uuid37aeuau3ja",
  "email" : "user@gmail.com"
}
  ```
- **Return Type**: `createUserResponse`
- **Responses**:
  - `200`: User registration successful

### For more detailed information:
## Link to Database Documentation - [https://dbdiagram.io/d/HNG-stage-3-Task-66925fed9939893daed48a64](https://dbdiagram.io/d/HNG-stage-3-Task-66925fed9939893daed48a64)
## Link to API Documentation - [https://app.swaggerhub.com/apis-docs/ELMUBY404/HnG_Stage_3/1.0.0](https://app.swaggerhub.com/apis-docs/ELMUBY404/HnG_Stage_3/1.0.0)
