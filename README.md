# Daisy's Dog Groomers Database Project

## Overview
This project involves creating a relational database for Daisy's Dog Groomers to efficiently manage client information, appointments, and services. It also supports advanced reporting and insights into business operations.

## Features
1. **Database Design**:
   - A schema was developed based on an Entity-Relationship Diagram (ERD).
   - Tables include:
     - **Owner**: Stores owner details (name, email, phone).
     - **Dog**: Captures dog details (name, breed, notes).
     - **Groomer**: Stores groomer details (name, phone, email).
     - **Appointment**: Links dogs and groomers, capturing services and statuses.
     - **Billing**: Tracks payment details for completed appointments.

2. **Data Import**:
   - Data was imported from CSV files using SQL commands:
     - `dog.csv`
     - `groomer.csv`
     - `owner.csv`
     - `appointment.csv`

3. **Data Manipulation and Queries**:
   - Custom SQL queries were written to:
     - Show all appointments, sorted by date and time, with owner and dog details.
     - Show appointments with groomer and dog details.
     - Rank most popular dog breeds.
     - Rank dog breeds with the most notes or baths.
     - Rank groomers by haircut appointments.

4. **Analysis**:
   - Generated insights for Daisy's management, including:
     - Popular dog breeds.
     - Groomer efficiency and service rankings.
     - Trends in service demands.

## Technologies Used
- **SQL**: Core database language for schema creation, data import, and querying.
- **CSV Files**: Data source for importing dog, groomer, owner, and appointment details.
- **Database Management System**: MySQL
  

## Database Schema
- **Owner Table**:
  - `owner_id` (Primary Key)
  - `name`
  - `email`
  - `phone`
- **Dog Table**:
  - `dog_id` (Primary Key)
  - `owner_id` (Foreign Key)
  - `name`
  - `breed`
  - `notes`
- **Groomer Table**:
  - `groomer_id` (Primary Key)
  - `name`
  - `email`
  - `phone`
- **Appointment Table**:
  - `appointment_id` (Primary Key)
  - `dog_id` (Foreign Key)
  - `groomer_id` (Foreign Key)
  - `date`
  - `time`
  - `bath` (Boolean)
  - `haircut` (Boolean)
  - `works` (Boolean)
  - `status` (Enum: `pending` or `complete`)
- **Billing Table**:
  - `bill_id` (Primary Key)
  - `appointment_id` (Foreign Key)
  - `date`
  - `price`

## SQL Queries Highlights
1. **Show All Appointments with Owner and Dog Details**:
   ```sql
   SELECT a.date, a.time, o.name AS owner_name, d.name AS dog_name
   FROM appointment a
   JOIN dog d ON a.dog_id = d.dog_id
   JOIN owner o ON d.owner_id = o.owner_id
   ORDER BY a.date, a.time;
   ```

2. **Rank Popular Dog Breeds**:
   ```sql
   SELECT breed, COUNT(*) AS count
   FROM dog
   GROUP BY breed
   ORDER BY count DESC;
   ```

3. **Rank Groomers by Haircut Appointments**:
   ```sql
   SELECT g.name AS groomer_name, COUNT(*) AS haircut_count
   FROM appointment a
   JOIN groomer g ON a.groomer_id = g.groomer_id
   WHERE a.haircut = TRUE
   GROUP BY g.name
   ORDER BY haircut_count DESC;
   ```




