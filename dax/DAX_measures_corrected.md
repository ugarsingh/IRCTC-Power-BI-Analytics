# IRCTC Power BI Dashboard — DAX Measures

Table used in the Power BI model: `irctc_data`

The measures below use the actual column names from the supplied CSV dataset.

> Important: The supplied dataset contains 20,000 rows. `Booking_ID` is not unique in the CSV, so `COUNTROWS(irctc_data)` is used for booking-record counts to match the row-level dashboard analysis.

---

## 1. Core KPI Measures

### Total Revenue

```DAX
Total Revenue =
SUM(irctc_data[Total_Revenue_INR])
```

### Total Bookings

```DAX
Total Bookings =
COUNTROWS(irctc_data)
```

### Total Passengers

```DAX
Total Passengers =
SUM(irctc_data[Passenger_Count])
```

### Average Booking Value

```DAX
Average Booking Value =
DIVIDE(
    [Total Revenue],
    [Total Bookings]
)
```

### Average Occupancy

Because `Occupancy_Percentage` is stored as values such as `79.92` rather than `0.7992`, divide by 100 if the measure is formatted as a percentage.

```DAX
Average Occupancy =
DIVIDE(
    AVERAGE(irctc_data[Occupancy_Percentage]),
    100
)
```

Format as Percentage with 2 decimal places.

### Average Delay

```DAX
Average Delay =
AVERAGE(irctc_data[On_Time_Delay_Mins])
```

### Average Distance

```DAX
Average Distance =
AVERAGE(irctc_data[Distance_KM])
```

---

## 2. Cancellation Measures

### Cancelled Bookings

```DAX
Cancelled Bookings =
CALCULATE(
    [Total Bookings],
    irctc_data[Booking_Status] = "Cancelled"
)
```

### Cancellation Rate

```DAX
Cancellation Rate =
DIVIDE(
    [Cancelled Bookings],
    [Total Bookings]
)
```

Format as Percentage with 2 decimal places.

---

## 3. Revenue Component Measures

### Base Fare Revenue

```DAX
Base Fare Revenue =
SUM(irctc_data[Base_Fare_INR])
```

### Surge Tatkal Revenue

```DAX
Surge Tatkal Revenue =
SUM(irctc_data[Surge_Tatkal_Charges_INR])
```

### Catering Revenue

```DAX
Catering Revenue =
SUM(irctc_data[Catering_Charges_INR])
```

### Taxes & Convenience Revenue

```DAX
Taxes & Convenience Revenue =
SUM(irctc_data[Taxes_And_Convenience_INR])
```

The four revenue components sum to the dataset's `Total_Revenue_INR`.

---

## 4. Time Intelligence

The model should contain a dedicated `Date` table related to the booking table:

```text
Date[Date]
    1
    |
    *
irctc_data[Booking_Date]
```

Recommended Date table columns:

- Date
- Year
- Month Number
- Month Name
- Quarter
- Year-Month

Sort `Month Name` by `Month Number`.

### Previous Month Revenue

This measure returns the revenue for the immediately preceding month in the current date context.

```DAX
Previous Month Revenue =
CALCULATE(
    [Total Revenue],
    DATEADD('Date'[Date], -1, MONTH)
)
```

### Previous Month Bookings

```DAX
Previous Month Bookings =
CALCULATE(
    [Total Bookings],
    DATEADD('Date'[Date], -1, MONTH)
)
```

### MoM Revenue Growth

```DAX
MoM Revenue Growth =
DIVIDE(
    [Total Revenue] - [Previous Month Revenue],
    [Previous Month Revenue]
)
```

### MoM Booking Growth

```DAX
MoM Booking Growth =
DIVIDE(
    [Total Bookings] - [Previous Month Bookings],
    [Previous Month Bookings]
)
```

Format both MoM measures as Percentage with 2 decimal places.

---

## 5. Revenue / Bookings Till Previous Month

If the dashboard needs the approximately ₹48M and 18K values shown in the current design, those are not "Previous Month Revenue" or "Previous Month Bookings". They represent cumulative values through the month before the current/latest month.

### Revenue Till Previous Month

```DAX
Revenue Till Previous Month =
CALCULATE(
    [Total Revenue],
    FILTER(
        ALL('Date'),
        'Date'[Date] <= EOMONTH(MAX('Date'[Date]), -1)
    )
)
```

### Bookings Till Previous Month

```DAX
Bookings Till Previous Month =
CALCULATE(
    [Total Bookings],
    FILTER(
        ALL('Date'),
        'Date'[Date] <= EOMONTH(MAX('Date'[Date]), -1)
    )
)
```

---

## 6. Current Month vs Prior Cumulative Value

The existing dashboard values of approximately 10.72% revenue and 10.31% bookings are mathematically:

Current month value ÷ cumulative value through the previous month.

This is NOT standard MoM growth. If you want to retain those values, use clearer labels such as `Current Month vs Prior Cumulative`.

### Current Month vs Prior Cumulative Revenue

```DAX
Current Month vs Prior Cumulative Revenue =
DIVIDE(
    [Total Revenue] - [Revenue Till Previous Month],
    [Revenue Till Previous Month]
)
```

### Current Month vs Prior Cumulative Bookings

```DAX
Current Month vs Prior Cumulative Bookings =
DIVIDE(
    [Total Bookings] - [Bookings Till Previous Month],
    [Bookings Till Previous Month]
)
```

For a professional BI dashboard, use the standard `MoM Revenue Growth` and `MoM Booking Growth` measures when the KPI is intended to mean month-over-month growth.

---

## 7. Recommended Measure Organization

Create a dedicated `_Measures` table and organize measures into display folders:

```text
_Measures
│
├── Revenue
│   ├── Total Revenue
│   ├── Previous Month Revenue
│   ├── Revenue Till Previous Month
│   ├── MoM Revenue Growth
│   ├── Base Fare Revenue
│   ├── Surge Tatkal Revenue
│   ├── Catering Revenue
│   └── Taxes & Convenience Revenue
│
├── Bookings
│   ├── Total Bookings
│   ├── Previous Month Bookings
│   ├── Bookings Till Previous Month
│   ├── MoM Booking Growth
│   ├── Total Passengers
│   ├── Cancelled Bookings
│   └── Cancellation Rate
│
└── Operations
    ├── Average Occupancy
    ├── Average Delay
    └── Average Distance
```

---

## 8. Formatting

| Measure | Format |
|---|---|
| Total Revenue | ₹M |
| Previous Month Revenue | ₹M |
| Revenue Till Previous Month | ₹M |
| Average Booking Value | ₹K |
| Total Bookings | #,##0 |
| Total Passengers | #,##0 |
| Average Occupancy | 0.00% |
| Cancellation Rate | 0.00% |
| MoM Revenue Growth | 0.00% |
| MoM Booking Growth | 0.00% |
| Average Delay | 0.00 min |
| Average Distance | #,##0.00 km |

---

## 9. Validation Against Supplied Dataset

The supplied CSV contains:

- 20,000 rows
- Booking dates from January 1, 2025 to December 31, 2025
- ₹53,055,565 total revenue
- 39,949 total passengers
- 79.9175 average occupancy
- 22.18735 minutes average delay
- 803.975 km average distance
- 749 cancelled booking records

Revenue components reconcile to total revenue:

```text
Base Fare                  ₹41,307,760
Surge Tatkal Charges        ₹4,044,402
Catering Charges            ₹6,217,255
Taxes & Convenience         ₹1,486,148
                           -----------
Total Revenue              ₹53,055,565
```
