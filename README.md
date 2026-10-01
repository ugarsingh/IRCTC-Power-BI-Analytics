# 🚆 IRCTC Business Intelligence & Operations Analytics

An interactive **Power BI Business Intelligence dashboard** built to analyze railway booking performance, revenue, passenger demand, booking behavior, and train operations.

The project transforms the `irctc_data` booking dataset into an interactive analytical solution using **Power BI, DAX, Power Query, data modeling, and time-intelligence analysis**.

---

## 📊 Dashboard Overview

The report is organized into four analytical dashboards:

### 01 — Executive Overview

Provides a high-level view of overall business performance.

**Key metrics:**

- Total Revenue
- Total Bookings
- Total Passengers
- Average Booking Value
- Revenue Growth
- Booking Growth
- Average Occupancy
- Cancellation Rate
- Average Delay
- Top Routes
- Revenue by Booking Channel

---

### 02 — Revenue Analysis

Analyzes revenue generation and its major contributing factors.

**Analysis includes:**

- Monthly Revenue Trends
- Revenue by Travel Class
- Revenue by Train Type
- Base Fare Revenue
- Surge/Tatkal Charges
- Catering Revenue
- Taxes & Convenience Revenue
- Revenue Contribution
- Previous-period Revenue Analysis

---

### 03 — Booking & Demand Analysis

Analyzes passenger demand and booking behavior.

**Analysis includes:**

- Monthly Booking Trends
- Booking Type Distribution
- Travel Class Demand
- Booking Channel Performance
- Passenger Volume
- Route-level Demand
- Tatkal / Premium Tatkal Analysis
- Booking Status Distribution

---

### 04 — Train Operations

Analyzes operational performance across trains and railway zones.

**Analysis includes:**

- Average Occupancy
- Average Delay
- Average Distance
- Cancellation Rate
- Railway Zone Performance
- Train-level Occupancy
- Train-level Delay
- Train-level Cancellation
- Revenue and Booking Performance by Railway Zone

---

## 📈 Key Metrics

Based on the supplied `irctc_data` dataset:

| Metric | Value |
|---|---:|
| Dataset Records | 20,000 |
| Total Revenue | ₹53.06M |
| Total Passengers | 39,949 |
| Average Booking Value | ~₹2.65K |
| Average Occupancy | 79.92% |
| Cancelled Records | 749 |
| Cancellation Rate | ~3.75% |
| Average Delay | 22.19 min |
| Average Distance | 803.98 km |

> **Note:** Booking records are counted using the dataset rows because `Booking_ID` is not unique across all records.

---

## 🔍 Key Business Insights

The dashboard enables analysis of:

- Revenue performance across different months, train types, and travel classes.
- Contribution of base fare, Tatkal charges, catering, and taxes/convenience charges to total revenue.
- Booking demand across routes, travel classes, and booking types.
- Performance of different booking channels.
- Passenger volume and train utilization.
- Operational performance using occupancy, delay, and cancellation metrics.
- Railway-zone and train-level performance.

---

## 🧮 DAX & Time Intelligence

The project uses DAX measures to create reusable business metrics such as:

- Total Revenue
- Total Bookings
- Total Passengers
- Average Booking Value
- Average Occupancy
- Average Delay
- Average Distance
- Cancelled Bookings
- Cancellation Rate
- Previous Month Revenue
- Previous Month Bookings
- MoM Revenue Growth
- MoM Booking Growth

A dedicated Date table is used for time-intelligence calculations.

### Date Relationship

```text
Date[Date]
    1
    |
    *
irctc_data[Booking_Date]
```

---

## 🔄 Data Analysis Workflow

```text
Raw Booking Dataset
        ↓
Data Validation
        ↓
Power Query
        ↓
Data Transformation
        ↓
Data Modeling
        ↓
DAX Measures
        ↓
Interactive Visualizations
        ↓
Business Insights
```

---

## 🗂️ Dataset

The primary dataset is stored in the Power BI model as:

```text
irctc_data
```

The dataset contains **20,000 booking-level records** and **28 fields** covering:

### Booking Information

- Booking ID
- User ID
- Booking Date
- Booking Time
- Travel Date
- Booking Type
- Booking Channel
- Booking Status

### Train Information

- Train Number
- Train Name
- Train Type
- Railway Zone
- Train Capacity

### Journey Information

- Source Station
- Destination Station
- Route
- Distance

### Passenger & Travel Information

- Passenger Count
- Travel Class
- Occupancy Percentage
- Delay

### Revenue Information

- Base Fare
- Surge/Tatkal Charges
- Catering Charges
- Taxes & Convenience Charges
- Total Revenue

### Payment Information

- Payment Method
- Partner Platform

---

## 🏗️ Data Model

The report uses a dedicated Date table connected to the booking-level fact table.

```text
              ┌───────────────┐
              │     Date      │
              │───────────────│
              │ Date          │
              │ Year          │
              │ Month         │
              │ Month Number  │
              │ Quarter       │
              └───────┬───────┘
                      │
                    1 : *
                      │
              ┌───────▼───────┐
              │   irctc_data  │
              │───────────────│
              │ Booking       │
              │ Train         │
              │ Route         │
              │ Passenger     │
              │ Revenue       │
              │ Occupancy     │
              │ Delay         │
              └───────────────┘
```

---

## 🛠️ Tools & Technologies

| Technology | Purpose |
|---|---|
| **Power BI** | Dashboard development and visualization |
| **DAX** | Measures, KPIs and time intelligence |
| **Power Query** | Data cleaning and transformation |
| **Data Modeling** | Relationships and analytical model |
| **SQL / MySQL** | Data analysis knowledge applied to the project workflow |

---

## 📁 Repository Structure

```text
IRCTC-Power-BI-Analytics/
│
├── README.md
│
├── Dashboard/
│   └── IRCTC_Business_Insights.pbix
│
├── Screenshots/
│   ├── 01-executive-overview.png
│   ├── 02-revenue-analysis.png
│   ├── 03-booking-demand.png
│   └── 04-train-operations.png
│
├── DAX/
│   └── DAX_measures_corrected.md
│
└── Documentation/
    ├── data_dictionary.md
    └── data_model.md
```

---

## 📷 Dashboard Preview

### Executive Overview

![Executive Overview](Screenshots/01-executive-overview.png)

### Revenue Analysis

![Revenue Analysis](Screenshots/02-revenue-analysis.png)

### Booking & Demand

![Booking & Demand](Screenshots/03-booking-demand.png)

### Train Operations

![Train Operations](Screenshots/04-train-operations.png)

---

## 📚 Documentation

Additional project documentation is available in the repository:

- [DAX Measures](DAX/DAX_measures_corrected.md)
- [Data Dictionary](Documentation/data_dictionary.md)
- [Data Model & Analytics Architecture](Documentation/data_model.md)

---

## 🎯 Project Objective

The objective of this project is to demonstrate how a booking-level railway dataset can be transformed into an interactive Business Intelligence solution for analyzing:

- Revenue performance
- Passenger demand
- Booking behavior
- Booking channels
- Route performance
- Train utilization
- Operational efficiency
- Delays
- Cancellations

The project focuses on **data modeling, DAX, visualization, and business-oriented analytical storytelling**.

---

## 👨‍💻 Author

**Sukalyan Manna**

B.Tech — Electronics & Communication Engineering

Interested in **Software Engineering, Backend Development, Cloud, Data Analytics and Business Intelligence**.

---

## 📌 Disclaimer

This project is created for **educational and portfolio purposes**. The analysis represents the supplied dataset and should not be interpreted as official IRCTC operational or financial reporting.
