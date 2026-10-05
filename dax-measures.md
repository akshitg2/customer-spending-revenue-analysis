# DAX Measures & Calculated Columns

## Measures

### 1. Current Week Revenue

```DAX
Current_week_Revenue =
CALCULATE(
    SUM(credit_card[Revenue]),
    FILTER(
        ALL(credit_card),
        credit_card[week_num2] = MAX(credit_card[week_num2])
    )
)
```

### 2. Previous Week Revenue

```DAX
Previous_week_Revenue =
CALCULATE(
    SUM(credit_card[Revenue]),
    FILTER(
        ALL(credit_card),
        credit_card[week_num2] = MAX(credit_card[week_num2]) - 1
    )
)
```

### 3. Week-over-Week Revenue Growth

```DAX
wow_revenue =
DIVIDE(
    [Current_week_Revenue] - [Previous_week_Revenue],
    [Previous_week_Revenue]
)
```

## Calculated Columns

### 4. Revenue

```DAX
Revenue =
    credit_card[Annual_Fees]
    + credit_card[Total_Trans_Amt]
    + credit_card[Interest_Earned]
```

### 5. Age Group

```DAX
AgeGroup =
SWITCH(
    TRUE(),
    customer[Customer_Age] < 30, "20-30",
    customer[Customer_Age] >= 30 &&
        customer[Customer_Age] < 40, "30-40",
    customer[Customer_Age] >= 40 &&
        customer[Customer_Age] < 50, "40-50",
    customer[Customer_Age] >= 50 &&
        customer[Customer_Age] < 60, "50-60",
    customer[Customer_Age] >= 60, "60+",
    "unknown"
)
```

### 6. Income Group

```DAX
IncomeGroup =
SWITCH(
    TRUE(),
    customer[Income] < 35000, "Low",
    customer[Income] >= 35000 &&
        customer[Income] < 70000, "Med",
    customer[Income] >= 70000, "High",
    "unknown"
)
```
