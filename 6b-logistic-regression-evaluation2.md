# 🎯 המשך הערכת מודל רגרסיה לוגיסטית

## ❗ פרדוקס הדיוק (Accuracy Paradox)

לפעמים מדד הדיוק **מטעה** – במיוחד כשיש **חוסר איזון בנתונים**.

### 🔍 דוגמה:
נניח שבמאגר שלנו:
- 95 מתוך 100 האנשים **לא חולים**
- רק 5 חולים

המודל "מתחכם" ומנבא שכולם לא חולים (כלומר תמיד 0).

#### 🎯 תוצאה:
- Accuracy = 95%
- אבל המודל **אף פעם לא מזהה חולה אמיתי**
- כלומר המודל חסר תועלת למרות דיוק גבוה

## 📢 Recall (שחזור)

מודד כמה מהמקרים **החיוביים האמיתיים** המודל הצליח לגלות.

$$
\text{Recall} = \frac{TP}{TP + FN}
$$

- TP = חיזוי חיובי נכון  
- FN = פספוס של חיובי

### 🧠 דוגמה:
אם יש 5 חולים, והמודל גילה 4 →  

$$
\text{Recall} = \frac{4}{5} = 0.8
$$

## 🎯 Precision (דיוק תחזיות חיוביות)

מודד כמה מהתחזיות שהמודל חזה כ"חיובי" הן באמת נכונות.

$$
\text{Precision} = \frac{TP}{TP + FP}
$$

- FP = חיזוי חיובי שגוי (False Alarm)

### 🧠 דוגמה:
אם המודל חזה 6 חיוביים, אבל רק 4 באמת חולים →  

$$
\text{Precision} = \frac{4}{6} \approx 0.666
$$

## ⚖️ F1 Score – ממוצע הרמוני של Precision ו-Recall

מאזן בין Precision ו-Recall. חשוב במיוחד כשיש חוסר איזון בין המקרים.

$$
\text{F1 Score} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
$$

### 🧠 דוגמה:
Precision = 0.666, Recall = 0.8

$$
\text{F1} = \frac{2 \cdot 0.666 \cdot 0.8}{0.666 + 0.8} \approx 0.72
$$

### למה לא מספיק **Precision** או **Recall** לבד

* ה- **Precision** אומר: מתוך כל מה שחזיתי כחיובי – כמה באמת חיוביים
* ה- **Recall** אומר: מתוך כל מה שבאמת חיובי – כמה הצלחתי לגלות

לעיתים הם מתנגשים: העלאת **Recall** בדרך כלל מורידה **Precision** ולהפך

### מהו **F1**

ה- **F1** הוא הממוצע ההרמוני של **Precision** ו־**Recall**

$$
F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}
$$

הממוצע ההרמוני מעניש מצבים לא מאוזנים: אם אחד מהמדדים נמוך מאוד, גם **F1** ירד

### למה זה חשוב

* נותן מדד יחיד שמאזן בין **Precision** ל־**Recall**
* שימושי במיוחד כשיש חוסר איזון בין המחלקות או כשהעלות של פספוס חיובי גבוהה אבל לא רוצים להציף חיוביים שגויים
* מאפשר להשוות מודלים או ספים שונים כשאי אפשר להסתפק בדיוק כללי

### מתי להשתמש

* כשיש מחלקה חיובית נדירה ורוצים גם לאתר אותה טוב **וגם** להיות אמינים כשאומרים "חיובי"
* כשמשחקים עם סף ההחלטה של מודל לוגיסטי ורוצים נקודת איזון בין איתור לאמינות

### תובנה מהירה

אם חשוב לך לזהות כמה שיותר חיוביים בלי להציף שגויים – הסתכל על **F1** כמדד מאוזן שמסכם את **Precision** ו־**Recall** יחד

**דוגמה בפייתון:**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
from sklearn.model_selection import train_test_split
import numpy as np

# Example data: study hours and exam result
X = np.array([[1], [2], [3], [4], [5], [6], [7], [8], [9]])
y = np.array([0, 0, 0, 0, 1, 1, 1, 1, 1])  # 0 = fail, 1 = pass

# Split into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Create and train the logistic regression model
model = LogisticRegression(solver='liblinear')
model.fit(X_train, y_train)

# Predict the test set
y_pred = model.predict(X_test)

# Calculate and print evaluation metrics
accuracy = accuracy_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)

print(f"Accuracy:  {accuracy:.2f}")
print(f"Recall:    {recall:.2f}")
print(f"Precision: {precision:.2f}")
print(f"F1 Score:  {f1:.2f}")
```

Output (using a small sample we will get 100%):

```
Accuracy:  1.00
Recall:    1.00
Precision: 1.00
F1 Score:  1.00
```
