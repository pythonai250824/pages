## 🧪 תרגיל: מימוש המחלקה `RubberDuck` לפי ה-UML

### ⚖️ מטרה

לממש את המחלקה `RubberDuck` לפי התרשים שלמטה

### 🦆 UML: RubberDuck

```
+---------------------------------------------------------------+
|                        RubberDuck                             |
+---------------------------------------------------------------+
| - __color: str = "yellow"               @class-variable       |
| - __quack_volume: int                                         |
+---------------------------------------------------------------+
| + __init__(quack_volume=5)                                    |
| + squeak(): None                         [@static-method]     |
| + get_default_color(): str               [@class-method]      |
| + boost_volume(): None                   [instance-method]    |
| + quack_volume: int                      [@property]          |
| + quack_volume(value: int): None         [@setter]            |
| + __str__(): str                         [@instance-method]   |
+---------------------------------------------------------------+
```

```python
RubberDuck quack_volume=5 color='yellow'  # __str__ output
```

### 🥉 משימה

1. לממש את המחלקה `RubberDuck` לפי ה-UML שלמעלה.
2. לבדוק את המחלקה עם הקוד שלמטה:

### 🧪 קוד בדיקה

```python
# main.py

duck = RubberDuck()
print(duck)  # שימוש ב-__str__

RubberDuck.squeak()

duck.quack_volume = 10
print("🔊 New volume:", duck.quack_volume)

duck.boost_volume()
print("🚀 Boosted volume:", duck.quack_volume)

print("🎨 Default color:", RubberDuck.get_default_color())
```

---

### 💡 טיפים

* הפונקציה boost_volume מכפילה את ה- volume פי 2

* יש להגיש את התרגיל ל- pythonai250824+HWOOP3@gmail.com
