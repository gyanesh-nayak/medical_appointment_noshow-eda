# Medical Appointment No-Show Exploratory Data Analysis

Missed appointments are expensive for clinics and disruptive for patients waiting behind them. This project digs into a dataset of over 110,000 medical appointments from Brazil to ask a simple question: which patient and appointment characteristics actually line up with a no-show?

Rather than jumping straight to a predictive model, this is a ground-up exploration. It inspects the data, checks its quality, and lets the patterns in demographics, health conditions, and appointment logistics tell their own story before drawing any conclusions.

## Tools

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## What's in the Analysis

- Dataset inspection and data quality checks
- Missing value, duplicate, and invalid value analysis
- Attendance rate overview (Positive/Negative style class balance)
- Demographic breakdowns (gender, age, age groups)
- Health and socioeconomic factors (hypertension, diabetes, alcoholism, handicap, scholarship)
- Appointment characteristics (waiting time, SMS reminders, day of week)
- Neighborhood level attendance patterns
- Visualizations throughout, built with Matplotlib and Seaborn

## Key Findings

- The dataset covers 110,527 appointments, with roughly 80% attended and 20% resulting in a no-show.
- Waiting time (the gap between scheduling and the appointment) showed the strongest association with attendance. Same-day appointments had a no-show rate of just 4.6%, climbing to over 30% once the wait passed a month.

![No-show rate by waiting time](images/waiting_time_noshow.png)

- Age had a real but moderate relationship with attendance. Patients aged 18 to 29 missed appointments noticeably more often than patients 45 and older.
- SMS reminders looked counterintuitive at first, since recipients had a higher raw no-show rate. That's because SMS is never sent for same-day bookings, the group with the lowest no-show rate to begin with. Once waiting time is accounted for, SMS recipients actually show lower no-show rates.

![SMS reminder effect reverses within waiting time bands](images/sms_reversal.png)

- Neighborhood mattered more than expected, with no-show rates ranging from roughly 16% to 29% across the city. These gaps held up even within similar waiting-time groups.

![No-show rate by neighborhood](images/neighborhood_comparison.png)

- Scholarship status showed a modest, consistent association that held up across age groups.
- Gender, day of week, and most individual health conditions (hypertension, diabetes, alcoholism) showed weak associations. This shows that a variable being present in the data doesn't guarantee it's predictive.

![Correlation heatmap of features against no-show](images/correlation_heatmap.png)

## Context Beyond the Dataset

While exploring this dataset, several questions came up that the data itself couldn't answer. I reviewed discussions with the dataset's creator on Kaggle, which confirmed some of these findings and flagged questions the dataset cannot answer.

**Confirmed by the dataset creator:**
- This data comes from Brazil's public healthcare sector (SUS), likely primary care. Healthcare is free at the point of use, meaning patients do not face a direct financial penalty for missing an appointment. This may help explain the relatively high no-show rate in this dataset (~20%).
- Appointment specialty, time of day, and whether it was a patient's first visit with a provider are not included in this dataset. The creator himself suspects first-time visits and early-morning slots may be more prone to no-shows, but this hasn't been tested here.

**Open questions raised by our own analysis:**
- Same-day appointments show a dramatically lower no-show rate (4.6%) than longer-wait appointments. It's tempting to read this as "shorter wait time causes better attendance," but patients who receive same-day appointments may differ systematically from patients scheduled weeks in advance. They may have more urgency or availability that day. The real driver could be patient circumstances, not wait time itself.
- Scholarship recipients (Bolsa Família, a government program for economically vulnerable families) show a consistent no-show gap. Since healthcare is already free, missing an appointment doesn't cost them money either. But these patients may face greater barriers, like commute, work schedules, or caregiving, that make it harder to show up. This variable might be picking up on accessibility issues, not a lack of intent to attend.

## Limitations
Please note that this is an association-based analysis, not a causal one. Several variables are intertwined, SMS receipt and waiting time in particular, so raw comparisons can be misleading until confounders are checked. Some subgroups (certain neighborhoods, higher handicap levels) have very small sample sizes and shouldn't be over-interpreted. And since this project stops at exploration, it doesn't test how well any of these features would actually hold up predicting outcomes for new patients.

A natural next step would be to take these findings and build out a classification model to see how well they generalize.

## Potential Implications
- Since longer wait times are associated with higher no-show rates, a second SMS reminder closer to the appointment date (especially for bookings made far in advance) could be worth testing.
- Patients aged 18 to 29 and patients enrolled in the scholarship program show higher no-show rates, making these groups potential targets for future outreach. Investigating the underlying reasons for these differences could also help create more targeted interventions.
- No-show rates vary by neighborhood even after accounting for wait time, suggesting that factors like transportation access or clinic proximity are worth investigating.
- Because appointment type/urgency isn't available in this dataset, the wait-time finding should be validated against appointment-type data before being used to justify scheduling changes.

## Dataset

This project uses the Medical Appointment No Shows dataset from Kaggle.

- Dataset: Medical Appointment No Shows
- Source: Kaggle
- Records: 110,527 appointments across 14 features, tied to appointment scheduling, patient demographics, and health/socioeconomic conditions

Used here strictly for educational and exploratory purposes.

## Project Structure

```
medical_appointment_noshow-eda/
├── medical_noshow_eda.ipynb
├── medical_noshow_data.csv
├── images/
│   ├── waiting_time_noshow.png
│   ├── sms_reversal.png
│   ├── neighborhood_comparison.png
│   └── correlation_heatmap.png
├── LICENSE
└── README.md
```
