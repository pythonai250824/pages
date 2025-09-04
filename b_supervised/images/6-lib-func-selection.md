# 🧠 השוואה בין פונקציות רגרסיה בפייתון (Linear / Polynomial)

מטרת המסמך: להבין מתי להשתמש באיזו פונקציית רגרסיה בפייתון עבור מודלים לינאריים ופולינומיאליים

מושגים:

**ה- p-value**
 
 פרמטר סטטיסטי שאומר לנו מה הסיכוי שהקשר בין משתנה X לבין Y קרה במקרה, בלי קשר אמיתי ביניהם. אם הוא גדול מ־0.05: ייתכן שאין קשר אמיתי בין המשתנה לתוצאה. הסיכוי שזה קרה במקרה גבוה מדי, ולכן לא ניתן להסיק שזה משתנה חשוב

**ה- Multicollinearity**

קורה כששני משתנים או יותר מתוך המשתנים המסבירים (X) קשורים מאוד אחד לשני. במילים פשוטות – אם יש לך כמה עמודות (פיצ'רים), וחלק מהן אומרות כמעט את אותו הדבר – זה בעיה

**ה- interactions**

יצירת עמודות חדשות שמייצגות אינטראקציה בין פיצ’רים קיימים, כלומר מכפלות בין משתנים. לדוגמא- עמודה חדשה שמייצגת את המכפלה בין שני הפיצ'רים – כלומר את האינטראקציה שלהם  x1 * x2



---

## 📘 1. `sklearn.linear_model.LinearRegression`

```python
from sklearn.linear_model import LinearRegression
```

- ✅ מתאימה לרגרסיה לינארית (פיצ'ר אחד או יותר)
- ✅ תומכת בהכשרה נוחה עם `fit(X, y)`
- ✅ מספקת `predict(X)`, וגם `coef_`, `intercept_`
- ❌ לא תומכת ישירות ב־p-values או סטטיסטיקה מתקדמת

💡 **מעולה אם אתה רוצה מודל מהיר לעבודה פרקטית ולשימוש ב- PIPELINE**

---

## 📘 2. `sklearn.preprocessing.PolynomialFeatures` + `LinearRegression`

```python
from sklearn.preprocessing import PolynomialFeatures
```

- ✅ מאפשר הרחבת X ל־x, x², x³ וכן הלאה
- ✅ תומך ב־multivariate + interactions
- ❌ דורש עבודה עם `Pipeline` או `fit_transform` על X
- ❌ לא נותן סטטיסטיקה כמו R² Adjusted או p-values

💡 **טוב מאוד כשאתה רוצה פולינום מסודר, עם תמיכה ב־train_test_split ושאר כלים**

---

## 📘 3. `numpy.polyfit` / `numpy.poly1d`

```python
import numpy as np
np.polyfit(x, y, deg=3)  # calc Beta 0..n
np.poly1d(...)  # generate the function in order to predict
```

- ✅ הכי קל ופשוט לשימוש עם וקטורים
- ✅ מחזיר מקדמים של הפולינום
- ❌ לא תומך ביותר מפיצ’ר אחד
- ❌ לא נותן R², סטטיסטיקה או תכונות מתקדמות

💡 **מושלם לגרפים פשוטים ומהירים – כמו גרף נתוני עקומה**

---

## 📘 4. `statsmodels.api.OLS`

```python
import statsmodels.api as sm
model = sm.OLS(y, X).fit()
```

- ✅ נותן לך פלט שלם: p-values, R², Adjusted R², סטיות תקן
- ✅ תומך גם בפולינום (אם אתה מוסיף ידנית עמודות X², X³ וכו')
- ❌ דורש ממך להוסיף bias (עמודת 1) בעצמך עם `sm.add_constant`
- ❌ פחות אינטואיטיבי כשמשתמשים בפיצ’רים מרובים

💡 **בחירה מושלמת אם אתה רוצה ניתוח סטטיסטי מפורט ומדויק, כמו מאמר מדעי**

---

## 📘 5. `sns.regplot` (Seaborn Visual Regression)

```python
import seaborn as sns
sns.regplot(x=X, y=Y)
```

- ✅ **מבצע רגרסיה לינארית בפועל** ומצייר את קו הרגרסיה על הדאטה
- ✅ מאפשר הוספת תחום סמך (confidence interval)
- ✅ תומך בפולינום עם `order=2` ומעלה
- ❌ לא מחזיר מודל שניתן להשתמש בו אחר כך (כמו `fit`), אלא רק ציור ויזואלי
- ❌ אין תמיכה ישירה בסטטיסטיקה כמו `coef_`, `intercept_`, `p-values` או `R^2`

💡 **שימושי מאוד לניתוח ויזואלי מהיר של קשרים בין משתנים**.
---

## 📊 סיכום השוואתי

| Library                  | Supports Polynomial? | Supports R²? | Supports p-values? | Best Suited For                        |
|--------------------------|----------------------|--------------|--------------------|----------------------------------------|
| `sklearn.linear_model`   | ✅ (עם `PolynomialFeatures`) | ✅ | ❌ | Machine learning ו־pipeline             |
| `numpy.polyfit`          | ✅ (פיצ’ר אחד בלבד)         | ❌ (צריך לחשב בנפרד) | ❌ | גרפים פשוטים ומהירים                  |
| `statsmodels.OLS`        | ✅ (ידנית)                  | ✅ | ✅ | ניתוח סטטיסטי מתקדם (כמו מאמרים)       |
| `sns.regplot`            | ✅ (`order=2`)               | ❌ (ויזואלי בלבד)     | ❌ | ויזואליזציה מהירה של קשרים             |
---

## 📘 6. `Ridge` (Regularized Linear Regression - L2)

```python
from sklearn.linear_model import Ridge
```

- ✅ מבצעת רגרסיה לינארית עם רגולריזציה מסוג L2 (עונש על סכום ריבועי המקדמים)
- ✅ טובה למקרים עם הרבה פיצ'רים או קולינאריות גבוהה
- ❌ מקטינה את המקדמים אבל לא מבטלת אותם לגמרי

💡 **מעולה כשיש הרבה משתנים והקשר ביניהם בעייתי או חופף**

---

## 📘 7. `Lasso` (Regularized Linear Regression - L1)

```python
from sklearn.linear_model import Lasso
```

- ✅ רגולריזציה מסוג L1 (עונש על סכום ערכי מוחלט של המקדמים)
- ✅ מבטלת משתנים פחות חשובים – אפקט של feature selection
- ❌ עלולה לאבד מידע חשוב אם הנתונים רועשים מדי

💡 **בחירה נהדרת כשאתה רוצה גם רגרסיה וגם לבחור משתנים רלוונטיים**

---

## 📊 סיכום מעודכן:

| Library                | Supports Polynomial?             | Supports R²?                    | Supports p-values? | Regularization | Best Suited For                                      |
|------------------------|----------------------------------|----------------------------------|---------------------|----------------|------------------------------------------------------|
| `sklearn.linear_model` | ✅ (with `PolynomialFeatures`)   | ✅                                | ❌                  | ❌             | ML workflows and pipelines                          |
| `numpy.polyfit`        | ✅ (single feature only)         | ❌ (manual calculation needed)   | ❌                  | ❌             | Simple and quick curve fitting                      |
| `statsmodels.OLS`      | ✅ (manual expansion)            | ✅                                | ✅                  | ❌             | Advanced statistical analysis                       |
| `sns.regplot`          | ✅ (`order=2`)                   | ❌ (visual only)                | ❌                  | ❌             | Fast visual regression and exploration              |
| `Ridge`                | ✅ (with `PolynomialFeatures`)   | ✅                                | ❌                  | ✅ (L2)        | Handles multicollinearity and improves generalization |
| `Lasso`                | ✅ (with `PolynomialFeatures`)   | ✅                                | ❌                  | ✅ (L1)        | Automatic feature selection and sparsity            |
