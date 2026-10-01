# IRCTC Power BI — Data Model & Analytics Architecture

## Model Structure

The Power BI report uses the `irctc_data` table as the primary booking-level dataset and a dedicated `Date` table for time-based analysis.

```text
                ┌──────────────┐
                │     Date     │
                │──────────────│
                │ Date         │
                │ Year         │
                │ Month        │
                │ Month Number │
                │ Quarter      │
                └──────┬───────┘
                       │ 1 : *
                       │
                ┌──────▼───────┐
                │  irctc_data  │
                │──────────────│
                │ Booking      │
                │ Train        │
                │ Route        │
                │ Revenue      │
                │ Passenger    │
                │ Occupancy    │
                │ Delay        │
                └──────────────┘
```

## Relationship

```text
Date[Date]  1 ───────── *  irctc_data[Booking_Date]
```

The Date table is used for:

- Monthly revenue analysis
- Monthly booking analysis
- Previous-month calculations
- MoM growth
- Time-based filtering

---

## Dashboard Pages

### 01 — Executive Overview

High-level KPIs and major business trends.

### 02 — Revenue Analysis

Revenue trends, travel-class contribution, train-type revenue, and revenue components.

### 03 — Booking & Demand

Booking trends, booking types, travel classes, channels, passengers, and route demand.

### 04 — Train Operations

Railway-zone performance, occupancy, delay, cancellations, and train-level operational metrics.

### 05 — Data & Methodology

Dataset description, model structure, DAX approach, and analytical workflow.

---

## Analytics Workflow

```text
Raw CSV Dataset
      ↓
Data Validation
      ↓
Power Query
      ↓
Date Table & Data Model
      ↓
DAX Measures
      ↓
Interactive Visualizations
      ↓
Business Insights
```

---

## Core KPIs

- Total Revenue
- Total Bookings
- Total Passengers
- Average Booking Value
- Average Occupancy
- Average Delay
- Average Distance
- Cancelled Bookings
- Cancellation Rate
- MoM Revenue Growth
- MoM Booking Growth

---

## Tools

- Power BI
- DAX
- Power Query
- SQL / MySQL
- Data Modeling
- Data Visualization
