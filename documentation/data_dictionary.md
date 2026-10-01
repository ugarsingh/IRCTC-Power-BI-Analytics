# IRCTC Dataset — Data Dictionary

## Dataset Overview

**Dataset:** `irctc_data`

**Rows:** 20,000

**Columns:** 28

**Booking Date Range:** January 1, 2025 – December 31, 2025

The dataset contains booking-level information covering customers, trains, routes, travel classes, booking channels, revenue components, booking status, occupancy, and delays.

---

## Data Fields

| Column | Type | Description |
|---|---|---|
| `Booking_ID` | Text | Identifier associated with a booking record |
| `User_ID` | Text | Identifier of the customer/user |
| `Booking_Date` | Date | Date on which the booking was made |
| `Booking_Time` | Time/Text | Time at which the booking was made |
| `Travel_Date` | Date | Scheduled travel date |
| `Train_Number` | Integer | Train number |
| `Train_Name` | Text | Name of the train |
| `Train_Type` | Text | Train category/type |
| `Railway_Zone` | Text | Railway zone associated with the booking |
| `Source_Station` | Text | Journey origin |
| `Destination_Station` | Text | Journey destination |
| `Route` | Text | Source-to-destination route |
| `Distance_KM` | Integer | Journey distance in kilometres |
| `Travel_Class` | Text | Travel class such as 1A, 2A, 3A, CC, EC, and SL |
| `Booking_Type` | Text | Reserved, Tatkal, or Premium Tatkal |
| `Booking_Channel` | Text | IRCTC Website, IRCTC App, or Authorised Partners |
| `Partner_Platform` | Text | Partner platform information where applicable |
| `Passenger_Count` | Integer | Number of passengers in the booking record |
| `Base_Fare_INR` | Integer | Base fare component in INR |
| `Surge_Tatkal_Charges_INR` | Integer | Surge/Tatkal charge component in INR |
| `Catering_Charges_INR` | Integer | Catering charge component in INR |
| `Taxes_And_Convenience_INR` | Integer | Taxes and convenience charges in INR |
| `Total_Revenue_INR` | Integer | Total revenue associated with the booking record |
| `Payment_Method` | Text | Payment method used for the booking |
| `Booking_Status` | Text | Booking status such as Confirmed, RAC, Waitlisted, or Cancelled |
| `Train_Capacity` | Integer | Train capacity used for the record |
| `Occupancy_Percentage` | Decimal | Occupancy percentage for the train/service |
| `On_Time_Delay_Mins` | Integer | Delay in minutes |

---

## Main Analytical Dimensions

### Time
- Booking Date
- Travel Date
- Booking Time

### Train
- Train Number
- Train Name
- Train Type
- Railway Zone

### Journey
- Source Station
- Destination Station
- Route
- Distance

### Booking
- Booking Type
- Booking Channel
- Partner Platform
- Booking Status
- Payment Method

### Travel
- Travel Class
- Passenger Count
- Train Capacity
- Occupancy

### Revenue
- Base Fare
- Surge Tatkal Charges
- Catering Charges
- Taxes & Convenience
- Total Revenue

### Operations
- Delay
- Occupancy
- Cancellation

---

## Key Dataset Statistics

| Metric | Value |
|---|---:|
| Records | 20,000 |
| Total Revenue | ₹53,055,565 |
| Total Passengers | 39,949 |
| Cancelled Records | 749 |
| Average Occupancy | 79.92% |
| Average Delay | 22.19 min |
| Average Distance | 803.98 km |

---

## Data Quality Notes

- `Booking_ID` is not unique across all rows in the supplied dataset, so the dashboard treats each dataset row as a booking record when using `COUNTROWS`.
- There is one exact duplicate row in the supplied CSV.
- `Occupancy_Percentage` is stored as values such as `79.92`, not as decimal fractions such as `0.7992`. DAX measures should account for this when formatting as a percentage.
- Revenue component columns reconcile exactly to `Total_Revenue_INR`.
