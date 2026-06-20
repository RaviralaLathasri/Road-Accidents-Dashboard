# 📐 DAX Measures — India Road Accident Analytics Dashboard

All custom DAX measures used in the Power BI report, organized by category.

---

## 📊 Core KPI Measures

### Total Accidents
```dax
Total Accidents = COUNTROWS('Accidents')
```

### Total Fatalities
```dax
Total-Fatalities = SUM('accident_prediction_india'[Number of Fatalities])
```

### Fatality Rate (%)
```dax
Fatality Rate (%) = 
DIVIDE([Total-Fatalities], [Total Accidents], 0) * 100
```

### Average Speed Limit
```dax
Average Speed Limit = AVERAGE('accident_prediction_india'[Speed Limit (km/h)])
```

---

## 🚨 Cause-Based Measures

### Overspeeding Accidents
```dax
Overspeeding_Accidents = 
COUNTROWS(
    FILTER(
        Accidents,
        Accidents[Attribute] = "Overspeeding" &&
        Accidents[Value] = "Yes"
    )
)
```

### Alcohol-Involved Accidents
```dax
Alcohol_Accidents = 
COUNTROWS(
    FILTER(
        Accidents,
        Accidents[Attribute] = "Alcohol" &&
        Accidents[Value] = "Yes"
    )
)
```

### Total Cause Count
```dax
Cause_Count = 
COUNTROWS(
    FILTER(
        Accidents, 
        NOT(ISBLANK(Accidents[Value]))
    )
)
```

---

## 📝 Notes

- `Accidents[Attribute]` is an unpivoted column holding cause labels (e.g., `"Overspeeding"`, `"Alcohol"`)
- `Accidents[Value]` holds the corresponding flag (`"Yes"` / `"No"`)
- `DIVIDE()` is used instead of `/` to safely handle division-by-zero cases
- All measures reference the `Accidents` table unless otherwise specified
