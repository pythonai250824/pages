# 🥵 Python Multithreading - תרגיל מסכם

## 🌟 מטרת התרגיל
להעמיק את ההבנה בעבודה עם threads בפייתון, כלל שימוש ב‎`threading.Thread`, העברת ארגומנטים, המתנה לסיום, בריכת משאבים (`ThreadPoolExecutor`) והדפסה מסונכרנת  

## ✅ שלב ראשון – יצירת פונקציית הדפסה

1. כתוב פונקציה בשם `print_sequence(name, count)`:
   - הפונקציה תקבל שם של thread ומספר חזרות.
   - בכל חזרה היא תדפיס: `Thread <name>: i=<number>`
   - לאחר כל הדפסה – `time.sleep(0.3)`

2. צור 3 threads שונים שמריצים את הפונקציה עם שמות וערכים שונים:
   - לדוגמה: `("Alpha", 5)`, `("Beta", 3)`, `("Gamma", 4)`

3. הפעל את שלושת השחבות והמתן שכלם יסיימו (`join`)

## 🔄 שלב שני – בריכת משאבים

4. כתוב את אותה פונקציית `print_sequence`, אבל הפעם השתמש בפעם `ThreadPoolExecutor`:
   - הגדר בריכה עם `max_workers=2`.
   - הרץ את הפונקציה עבור כל אחד מהשלב הקודם, עם `executor.submit`

## 🌟 בונוס – גרסה דינמית

5. בקובץ הראשי:
   - צור רשימה של `5 עד 10` tuples עם שמות רנדומליים וערכים בין 2 לַ׳ 6  
   - הרץ את כלם עם `ThreadPoolExecutor`, ובסיום הדפס:
     - `"All threads completed!"`

6. ודא שכל התפוקות מוגדות ממספרים נכונות, לפי כל thread, בלי ערבוב ששורות.

## 🧪 דוגמת תפוקה מצופה

```
Thread Alpha: i=0
Thread Beta: i=0
Thread Alpha: i=1
Thread Beta: i=1
Thread Gamma: i=0
...
All threads completed!
```

הגשה למייל: pythonai250824+OOP8@gmail.com

בהצלחה! 🎉
