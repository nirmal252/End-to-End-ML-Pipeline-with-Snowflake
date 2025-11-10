# End-to-End-ML-Pipeline-with-Snowflake


# Overview
This README explains the complete workflow implemented using Snowflake and Python. It includes:
- Creating a student dataset in Snowflake
- Feature engineering using Snowpark
- Loading engineered data into Python
- Training a Random Forest model
- Uploading predictions back to Snowflake

---

# 1. Creating the Student Dataset
A simple student dataset is created in Snowflake containing:
- student_id  
- student_name  
- department  
- gpa  
- attendance  

It is stored in a table called `STUDENT_LOGS`.

---

#  2. Feature Engineering
Two new columns are generated:
- `gpa_level` → High / Medium / Low  
- `attendance_status` → Good / Average / Poor  

Final engineered dataset is stored as `STUDENT_FEATURES`.

---

#  3. Connecting Python to Snowflake
A Snowpark session is created using parameters:
- account  
- user  
- password  
- warehouse  
- database  
- schema  

The engineered table is loaded into a Pandas DataFrame using `to_pandas()`.

---

# 4. ML Model Training (Random Forest)
Steps performed:
- Convert `gpa_level` to numeric labels (2,1,0)
- Split the dataset into train/test
- Train RandomForestClassifier from scikit-learn
- Evaluate performance using classification report

---

# 5. Writing Predictions Back to Snowflake
The predictions are added as a new column and written back using:

```python
session.write_pandas(df, "STUDENT_PREDICTIONS", overwrite=True)
```

This completes the ML workflow.

---

# 6. Architecture Overview

```
Snowflake (STUDENT_LOGS)
       ↓
Feature Engineering → STUDENT_FEATURES
       ↓
Python Snowpark Session
       ↓
Pandas DataFrame → Random Forest ML
       ↓
Predictions → STUDENT_PREDICTIONS (Snowflake)
```

---

# 7. Summary
This project demonstrates:
- Data engineering inside Snowflake
- ML model development in Python
- End-to-end integration and prediction storage

---

