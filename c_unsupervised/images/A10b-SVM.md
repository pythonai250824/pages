# הגדרות SVM, Kernel, Kernel Function, ו-Kernel Trick

## Support Vector Machine (SVM)
זהו אלגוריתם למידה מונחית המשמש לסיווג (classification) ורגרסיה (regression). האלגוריתם מחפש היפרפלן אופטימלי (מישור הפרדה) שיפריד בין קבוצות שונות של נתונים. היפרפלן אופטימלי הוא זה שיוצר את המרווח (margin) המרבי בין הנקודות הקרובות ביותר מכל קבוצה, הידועות כווקטורי תמיכה (support vectors).

מתמטית, עבור נתונים לינאריים, המודל מיוצג על ידי:
- $f(x) = w^T x + b$
- כאשר $w$ הוא וקטור המשקלות
- x הוא וקטור תכונות הקלט
- b הוא ערך ההסטה (bias)
- הנוסחא מתאימה להרבה מימדים ולא רק לדו-מימד

# איך מוצאים את וקטור המשקלים \( w \) ב־SVM

## 🎯 המטרה של SVM
למצוא את הקו (או ההיפר־פליין) שמפריד הכי טוב בין שתי קבוצות, כך שהמרחק מהנקודות הקרובות ביותר מכל צד (ה־**support vectors**) אל הקו יהיה **הכי גדול שאפשר**


## 🔢 איך מוצאים את \( w \)?
המודל מגדיר בעיה מתמטית של **אופטימיזציה** (מציאת מקסימום/מינימום)

### 1. נוסחת ההיפר־פליין:
$$
f(x) = w^T x + b
$$

אם:

$$f(x) \geq 1$$

→ הדגימה שייכת למחלקה החיובית (label = +1)

$$f(x) \leq -1$$ 

→ הדגימה שייכת למחלקה השלילית (label = -1)

### 2. תנאי ההפרדה:
לכל דוגמה Xi Yi:

$$
y_i (w^T x_i + b) \geq 1
$$

**מה זה Yi**

ה- Yi זה התווית (label) של הדוגמה ה־ i

כל Xi הוא וקטור

כל Yi הוא מספר שאומר לאיזה קבוצה שייכת הדוגמא, לקבוצה החיובית או לקבוצה השלילית

### 3. פונקציית המטרה (Objective Function):
כדי למקסם את המרחק בין הקבוצות, נמזער את גודל \( w \):

$$
\min \left( \frac{1}{2} \||w\||^2 \right)
$$

$$
\|w\| = \sqrt{w_1^2 + w_2^2 + \dots + w_n^2}
$$

תחת ההגבלה:

$$
y_i (w^T x_i + b) \geq 1 \quad \forall i
$$


❓ למה צריך להקטין את \||w\||  ב־SVM?

✨ ההסבר: כל הסוד נמצא ב־**Margin** – המרווח בין הקבוצות

**המרחק של נקודה מהמישור:**
לפי הנוסחה:

$$
\text{Distance from hyperplane} = \frac{|w^T xi + b|}{\||w\||}
$$

**המטרה של SVM:**
למצוא מישור שמפריד בין הקבוצות עם **המרחק הכי גדול מהנקודות הקרובות ביותר** — כלומר, מרווח (margin) מקסימלי

**תנאי ההפרדה:**

$$
y_i(w^T x_i + b) \geq 1
$$

הנקודות הכי קרובות למישור הן ה־**Support Vectors**, שמקיימות:

$$
y_i(w^T x_i + b) = 1
$$

**המרחק שלהן מהמישור:**

$$
\text{margin} = \frac{1}{\||w\||}
$$


### ולכן:
- ככל ש־ ||w||  **קטן יותר**, המרווח **גדול יותר**.
- כלומר: אם נקטין את ||w\||, אנחנו **מרחיקים** את המישור מהנקודות הקרובות ביותר — וזה בדיוק מה שאנחנו רוצים!

**ולכן בפונקציית המטרה של SVM:
אנחנו **ממזערים** את:**

$$
\frac{1}{2} \||w\||^2
$$


כדי למצוא את ההיפר־פליין עם **margin מקסימלי** ולוודא הפרדה טובה בין הקבוצות.

**למה ממזערים את**

$$ 
\frac{1}{2} \||w\||^2 
$$

ולא פשוט את 

$$ 
\||w\||
$$

ב־SVM?

**המטרה המקורית:**
אנחנו רוצים למקסם את המרווח (**margin**) בין שתי הקבוצות.

**המרווח מוגדר כ:**

$$
\text{margin} = \frac{1}{\|w\|}
$$

כדי **למקסם** את המרווח — צריך **למזער** את:

$$
\|w\|
$$

אז למה ממזערים דווקא את 

$$ 
\frac{1}{2} \|w\|^2 
$$

?

**סיבות מתמטיות:**

**נגזרות פשוטות יותר**:

אם נגדיר את פונקציית המטרה כך:

$$
\frac{1}{2} \|w\|^2
$$

אז הנגזרת שלה היא פשוט 

$$ 
w 
$$

ואין צורך בשורשים או נגזרות מורכבות

---



## 🤖 איך פותרים את זה בפועל?

🔁 מה זה ה־Dual Problem ב־SVM?

ב־SVM מנסים למצוא את הקו הכי טוב שמפריד בין קבוצות
יש שתי דרכים לפתור את הבעיה:

✨ Primal Problem (בעיה מקורית):
- מוצאים ישירות את: `w`, `b`, ו־ `ξ` (שגיאות)
- מתאימה בעיקר למקרים פשוטים או לינאריים

✨ Dual Problem (בעיה כפולה):
- פותרים דרך משתנים חדשים: `αᵢ`
- מאפשר שימוש ב־**Kernel Trick**
- מדגישה רק את **וקטורי התמיכה** (support vectors)
- αᵢ ≥ 0  
- Σ αᵢ yᵢ = 0

💡 למה זה טוב?
- מאפשר שימוש בקרנלים (גם אם הדאטה לא לינארי)
- מדגיש רק דוגמאות חשובות
- יעיל יותר כשיש הרבה ממדים

**פתרון:**

1. משתמשים בשיטה מתמטית בשם **Lagrange Multipliers**
2. פותרים את הבעיה הכפולה (Dual Problem)
3. הפתרון מבוסס רק על ה־**Support Vectors** (הנקודות הכי קרובות להיפר־פליין)
4. מהם מחשבים את \( w \) כך:

$$
w = \sum_i \alpha_i y_i x_i
$$


כאשר:

$$
\alpha_i
$$

-  הם פרמטרים שקובעים את חשיבות כל דוגמה
- רק עבור ה־support vectors יש alpha שונה מאפס

**💡 סיכום**
- אנחנו לא מחשבים את \( w \) ישירות, אלא פותרים בעיית אופטימיזציה.
- המטרה היא למצוא את הקו שמפריד הכי טוב בין הקבוצות עם **margin** מקסימלי.
- התוצאה: משוואה שמבוססת רק על ה־support vectors.


## 🧠 איך SVM מתמודד עם יותר משתי קבוצות?

### 🎯 הבעיה:
המודל ה- "קלאסי" נועד לבעיה של **שני סוגים בלבד**:
- מחלקה חיובית: \( +1 \)
- מחלקה שלילית: \( -1 \)

אבל מה עושים כשיש **שלוש קבוצות או יותר**? (למשל A, B, C)

**✅ פתרונות נפוצים:**

**1. One-vs-Rest (OvR) – "אחד מול כל השאר"**

- אם יש 3 קבוצות (A, B, C) → נבנה 3 מודלים:
  - מודל 1: A מול (B ו־C)
  - מודל 2: B מול (A ו־C)
  - מודל 3: C מול (A ו־B)

- כל מודל מאמן SVM בינארי
- כשבודקים דוגמה חדשה:
  - מריצים את שלושת המודלים
  - בוחרים את הקבוצה עם הציון הגבוה ביותר

**2. One-vs-One (OvO) – "כל זוג מול זוג"**

- נבנה SVM עבור כל **זוג קבוצות**
- לדוגמה, עבור קבוצות A, B, C → נבנה:
  - A מול B
  - A מול C
  - B מול C
- עבור \( k \) קבוצות יש:


$$
\frac{k(k - 1)}{2}
$$

  מודלים שונים

- כשבודקים דוגמה חדשה:
  - כל מודל נותן "הצבעה"
  - הקבוצה שזוכה בהכי הרבה הצבעות היא הזוכה

**🤖 בפועל – עם Scikit-learn:**

- אם תשתמש ב־`SVC` (ספריית `sklearn.svm`) — אין צורך לטפל בזה ידנית!
- כברירת מחדל, האלגוריתם מפעיל **One-vs-One** באופן אוטומטי

**💡 סיכום:**

| מס' קבוצות | פתרון SVM               |
|------------|-------------------------|
| 2          | SVM רגיל                |
| >2         | One-vs-Rest או One-vs-One |



## דוגמא בפייתון עבור 3 קבוצות

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import svm
from sklearn.preprocessing import StandardScaler
from itertools import combinations

# Create a dataset for apples, bananas, and oranges
# Features: sweetness (x-axis) and weight (y-axis)
apples = np.array([[3, 150], [4, 130], [2, 160], [3, 140], [3.5, 145]])
bananas = np.array([[7, 120], [6, 110], [8, 115], [7.5, 125], [6.5, 118]])
oranges = np.array([[5, 180], [4.5, 195], [5.5, 185], [6, 175], [4.8, 190]])

# Combine features and create labels (0 for apples, 1 for bananas, 2 for oranges)
X = np.vstack([apples, bananas, oranges])
y = np.array([0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2])

# Scale the features (important for SVM)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Create and train the SVM model
# For multiclass problems, SVM creates multiple binary classifiers (one-vs-one by default)
clf = svm.SVC(kernel='linear', C=1000, decision_function_shape='ovr')
clf.fit(X_scaled, y)

# Create a test point
test_point = np.array([[5, 150]])  # A point with sweetness=5, weight=150
test_point_scaled = scaler.transform(test_point)
prediction = clf.predict(test_point_scaled)[0]
class_names = ["Apple", "Banana", "Orange"]
predicted_class = class_names[prediction]

print(f"Test point: Sweetness={test_point[0][0]}, Weight={test_point[0][1]}")
print(f"Predicted class: {predicted_class}")
```

<img src="svm8.png" style="width: 80%" />

Output:
```
Test point: Sweetness=5, Weight=150
Predicted class: Apple

Decision function values for test point:
Apple: 2.15989923461655
Banana: -0.18143598271709815
Orange: 1.071382786408734

the negative value for Banana simply indicates that the binary classifier for 
  "Banana vs. not-Banana" believes your test point is in the "not-Banana" category (rest)
  because we are using One-vs-Rest (OvR)
```