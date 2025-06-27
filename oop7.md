# 🐍 תרגול : *args ו־**kwargs בפייתון

## ✳️ תרגיל 1: סכום מספרים עם *args

כתוב פונקציה בשם `sum_numbers` שמקבלת כמות לא ידועה של מספרים ומחזירה את סכומם.

```python
def sum_numbers(*args):
    pass  # כתוב כאן את הפתרון
```

קלט לדוגמה:
```python
sum_numbers(1, 2, 3, 4)
```

פלט צפוי:
```python
10
```

## ✳️ תרגיל 2: הדפסת מידע על משתמשים עם **kwargs

כתוב פונקציה בשם `print_user_info` שמקבלת מילות מפתח כמו `name`, `age`, `city` ומדפיסה את המידע בשורה אחת.

```python
def print_user_info(**kwargs):
    pass  # כתוב כאן את הפתרון
```

קלט לדוגמה:
```python
print_user_info(name="Dana", age=30, city="Tel Aviv")
```

פלט צפוי:
```python
name: Dana, age: 30, city: Tel Aviv
```

## ✳️ תרגיל 3: חיבור ערכים עם *args ו־**kwargs יחד

כתוב פונקציה בשם `combine_values` שמדפיסה:
- סכום כל המספרים שהועברו דרך `*args`
- כל זוגות המפתחות והערכים שהועברו דרך `**kwargs`

```python
def combine_values(*args, **kwargs):
    pass  # כתוב כאן את הפתרון
```

קלט לדוגמה:
```python
combine_values(2, 4, 6, name="Tom", job="Dev")
```

פלט צפוי:
```
Sum: 12
name: Tom
job: Dev
```

## ✳️ תרגיל 4: ברירת מחדל עם **kwargs

כתוב פונקציה `greet_user` שמדפיסה:
- "Hello [name]" if `name` was given
- if not, print "Hello guest"

```python
def greet_user(**kwargs):
    pass  # כתוב כאן את הפתרון
```

קלט לדוגמה:
```python
greet_user(name="Lior")
greet_user()
```

פלט צפוי:
```
Hello Lior
Hello guest
```
הגשה למייל: pythonai250824+OOP7@gmail.com


