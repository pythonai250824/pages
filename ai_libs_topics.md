
# נושאים למבחן - Python Libraries

## תאוריה
- מה זה Data Science
- Structured Data vs Unstructured Data
- תפקידי מפתח בארגון:
  - Data Scientist
  - Data Analyst
  - Data Engineer
  - AI Developer
  - DevOps Engineer
  - Product Manager
- מבוא לספריות פייתון
- מבוא ל-Anaconda ול-Jupyter Notebook

---

## Jupyter Notebook
- הפעלת Jupyter דרך Anaconda או CMD
- שני מצבים: Edit Mode (ירוק) ו־Command Mode (כחול)
- הרצת תאים עם Ctrl+Enter
- הוספה/מחיקה של תאים (Insert Cell Above/Below, DD למחיקה)
- Cells מסוג Markdown והצגתם
- חשיבות סדר ההרצה ולא מיקום התאים
- שינוי סוג תא (Code / Markdown)
- קיצורים חשובים: Enter, Esc, B, A, DD

---

## NumPy
- התקנה: `pip install numpy`
- ייבוא: `import numpy as np`
- יצירת מערכים עם `np.array()`
- הבדל בין NumPy Arrays ל־Python Lists
- פעולות מתמטיות על מערכים: `+`, `*`, `sum()`, `mean()`
- פונקציות: `reshape()`, `max()`, `min()`, `argmax()`, `argmin()`, `shape`
- סינון עם תנאים (`array[array > 10]`)
- גישה למשתני מערך עם סלייסים
- העתקה עמוקה עם `copy()`
- שימוש ב־axis=0 ו־axis=1 בפעולות על מטריצות

---

## Pandas

### בסיס
- התקנה: `pip install pandas`
- ייבוא: `import pandas as pd`
- Series: מבנה חד־ממדי
- DataFrame: מבנה דו־ממדי

### פעולות על DataFrame
- טעינת CSV: `pd.read_csv("path")`
- הצגת מידע: `head()`, `tail()`, `info()`, `describe()`
- גישה לעמודות: `df['col']`, `df[['col1', 'col2']]`
- יצירת עמודה חדשה או חיבור עמודות
- מחיקת שורה/עמודה עם `drop()` (כולל inplace, axis)

### סינון תנאי (Boolean Filtering)
- `df[df['col'] > 100]`
- תנאים מרובים עם `&`, `|`

### פונקציות מתקדמות
- `apply()` עם פונקציות מותאמות אישית
- `np.vectorize()` לעבודה על מספר עמודות

### סטטיסטיקות
- `value_counts()`, `unique()`, `nunique()`
- `replace()`, `map()`, `duplicated()`, `drop_duplicates()`
- `nlargest()`, `nsmallest()`, `sample()`

### טיפול בערכים חסרים
- השארה עם NaN
- מחיקה עם `dropna()`
- השלמה עם `fillna(value)`
- מחיקה לפי שורות או עמודות לפי אחוזי חוסר

### קיבוץ (`groupby`)
- `df.groupby('column').mean()`
- קיבוץ לפי מספר עמודות → MultiIndex
- שליפת שורה עם `loc[]`
- שליפת ערכים לפי רמת אינדקס עם `xs()`
- `agg()` לביצוע מספר פעולות שונות

### קיבוץ לפי זמן
```python
df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)
df.groupby(df.index.year)['sales'].sum()
df.groupby(df.index.month)['visits'].mean()
```

### מיזוג טבלאות (Merge)
- `pd.merge(left, right, how='inner', on='id')`
- אפשרויות: `inner`, `left`, `right`, `outer`
- שימוש ב־`left_on`, `right_on` או `left_index`, `right_index`
- מיזוג לפי אינדקס ועמודה משולב

### חיבור טבלאות (Concatenation)
- `pd.concat([df1, df2], axis=0)`  # שורות
- `pd.concat([df1, df2], axis=1)`  # עמודות

---

## Matplotlib
- התקנה: `pip install matplotlib`
- ייבוא: `import matplotlib.pyplot as plt`
- `plt.plot(x, y)`, `title`, `xlabel`, `ylabel`, `xlim()`, `ylim()`
- שמירת גרף עם `savefig()`
- עבודה עם Figure ו־Axes
- `subplot()`, `tight_layout()`, `legend()`, `style`, `marker`
- סוגי גרפים:
  - Line
  - Bar
  - Pie
  - Histogram
  - Scatter

---

## Seaborn
- התקנה: `pip install seaborn`
- ייבוא: `import seaborn as sns`
- גרפים:
  - `sns.scatterplot()`
  - `sns.displot()` / `sns.histplot()`
  - `sns.countplot()`
  - `sns.barplot()`
  - `sns.boxplot()`
- פרמטרים חשובים: `hue`, `palette`, `style`, `size`, `alpha`
- KDE: `kde=True` או `sns.kdeplot()`
- שמירת גרף עם `plt.savefig()`
