# Analyzing Students' Mental Health

Does going to university in a different country affect your mental health? This project explores that question using data from a 2018 survey conducted at a Japanese international university. The study, approved by several ethical and regulatory boards, found that **international students have a higher risk of mental health difficulties** than the general population and that **social connectedness** and **acculturative stress** are predictive of depression.

Using SQL (PostgreSQL), we analyze the survey data to investigate whether international students' length of stay is a contributing factor to depression, social connectedness, and acculturative stress.

## Dataset

The dataset (`students.csv`) contains **285 records** collected from both international and domestic students. Key columns used in the analysis include:

| Field Name      | Description                                              |
| --------------- | -------------------------------------------------------- |
| `inter_dom`     | Type of student (international or domestic)              |
| `japanese_cate` | Japanese language proficiency                            |
| `english_cate`  | English language proficiency                             |
| `academic`      | Current academic level (undergraduate or graduate)       |
| `age`           | Current age of student                                   |
| `stay`          | Current length of stay in years                          |
| `todep`         | Total score of depression (PHQ-9 test)                   |
| `tosc`          | Total score of social connectedness (SCS test)           |
| `toas`          | Total score of acculturative stress (ASISS test)         |

## Analysis

The notebook (`notebook.ipynb`) uses PostgreSQL to query the data. The main query groups **international students by their length of stay** and calculates:

- **Average PHQ-9 score** (depression)
- **Average SCS score** (social connectedness)
- **Average ASISS score** (acculturative stress)

```sql
SELECT
    stay,
    COUNT(*) AS count_int,
    ROUND(AVG(todep), 2) AS average_phq,
    ROUND(AVG(tosc), 2) AS average_scs,
    ROUND(AVG(toas), 2) AS average_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC
LIMIT 9;
```

## Project Structure

```
├── notebook.ipynb                        # Jupyter notebook with SQL analysis
├── students.csv                          # Survey dataset
├── Analyzing Students' Mental Health.pdf # Project report
└── README.md                            # This file
```

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/EngMengeang/Analyzing-Students-Mental-Health.git
   ```
2. **Set up a PostgreSQL database** and import `students.csv`.
3. **Open `notebook.ipynb`** in Jupyter Notebook or JupyterLab and run the SQL cells.

## Tools & Technologies

- **PostgreSQL** — querying and aggregating the survey data
- **Jupyter Notebook** — interactive analysis environment
- **Python 3** — notebook runtime

## Acknowledgments

This project is based on a study conducted at a Japanese international university in 2018. The original research was approved by several ethical and regulatory boards.
