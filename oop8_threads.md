# 🧵 Python Multithreading - Final Exercise

## 🌟 Exercise Goal
Deepen your understanding of working with threads in Python, including the use of `threading.Thread`, argument passing, waiting for completion, resource pools (`ThreadPoolExecutor`), and synchronized output.

## ✅ Step 1 – Create a Printing Function

1. Write a function called `print_sequence(name, count)`:
   - The function should accept a thread name and a number of repetitions.
   - In each iteration, it should print: `Thread <name>: i=<number>`
   - After each print, pause for `time.sleep(0.3)`

2. Create 3 separate threads that run the function with different names and values:
   - Example: `("Alpha", 5)`, `("Beta", 3)`, `("Gamma", 4)`

3. Start all threads and wait for them to finish (`join`)

## 🔄 Step 2 – Thread Pool

4. Reuse the same `print_sequence` function, but this time use `ThreadPoolExecutor`:
   - Define a pool with `max_workers=2`.
   - Run the function for each name+count from the previous step using `executor.submit`

## 🌟 Bonus – Dynamic Version

5. In your main script:
   - Create a list of `5 to 10` tuples with random names and values between 2 and 6
   - Run them all using `ThreadPoolExecutor`, and at the end print:
     - `"All threads completed!"`

## 🧪 Example Expected Output

```
Thread Alpha: i=0
Thread Beta: i=0
Thread Alpha: i=1
Thread Beta: i=1
Thread Gamma: i=0
...
All threads completed!
```

Good luck! 🎉


הגשה למייל: pythonai250824+OOP8@gmail.com

