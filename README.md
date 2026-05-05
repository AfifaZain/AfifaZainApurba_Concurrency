# Concurrency Assignment

Name: Afifa Zain Apurba  
ID: 1912310642
Course: 425.8 (Concepts of Programming Language Assignment) 

---

## Folder Structure

```text
AfifaZainApurba_Concurrency/
├── README.md
├── part1_race_condition.py
├── part2_producer_consumer.py
├── part3_dining_philosophers.py
├── part4_thread_pool.py
└── screenshots/
    ├── part1_output.png
    ├── part2_output.png
    ├── part3_output.png
    └── part4_output.png
```

---

## How to Run

Open a terminal in the project folder:

```bash
cd AfifaZainApurba_Concurrency
```

Then run each Python file:

```bash
python part1_race_condition.py
python part2_producer_consumer.py
python part3_dining_philosophers.py
python part4_thread_pool.py
```

If your system uses `python3`, run:

```bash
python3 part1_race_condition.py
python3 part2_producer_consumer.py
python3 part3_dining_philosophers.py
python3 part4_thread_pool.py
```

---

## Running in Kaggle Notebook

This assignment can also be run in a Kaggle Notebook.

To create the folder structure in Kaggle:

```python
!mkdir -p AfifaZainApurba_Concurrency/screenshots
```

Files can be created using `%%writefile`.

Example:

```python
%%writefile AfifaZainApurba_Concurrency/part1_race_condition.py
# Paste the Python code here
```

Run the file using:

```python
!python AfifaZainApurba_Concurrency/part1_race_condition.py
```

To zip the final submission folder:

```python
!zip -r AfifaZainApurba_Concurrency.zip AfifaZainApurba_Concurrency
```

---

# Part 1: Race Condition

## Description

This part demonstrates a race condition using multiple threads.

A shared counter starts at 0. Three threads increase the counter 1000 times each.

Expected final result:

```text
3000
```

The program runs in two ways:

1. Without using a lock
2. Using a lock

---

## Without Lock

When the program runs without a lock, multiple threads can access and change the counter at the same time.

For example:

```text
Thread 1 reads counter = 5
Thread 2 reads counter = 5
Thread 1 writes counter = 6
Thread 2 writes counter = 6
```

The counter should have increased twice, but it only increased once.

Because of this, the final value may be wrong, such as:

```text
2847
```

instead of:

```text
3000
```

---

## With Lock

The program uses:

```python
threading.Lock()
```

A lock allows only one thread to update the shared counter at a time.

So, when one thread is updating the counter, the other threads must wait.

This prevents interference between threads.

Final correct result:

```text
3000
```

---

## What I Learned

I learned that a race condition happens when multiple threads access shared data at the same time. Using a lock protects the shared data and gives the correct result.

---

# Part 2: Producer-Consumer

## Description

This part demonstrates the Producer-Consumer problem.

In this program:

- Producer = Baker
- Consumer = Customer
- Queue = Bread basket

The basket has a maximum size of 5.

```python
queue.Queue(maxsize=5)
```

---

## How It Works

Bakers produce bread and place it into the basket.

Customers take bread from the basket and eat it.

There are:

- 1 or 2 bakers
- 1 or 2 customers
- A shared basket with maximum size 5

---

## Full Basket

If the basket is full, the baker cannot add more bread.

The baker waits until a customer takes bread from the basket.

This prevents overflow.

---

## Empty Basket

If the basket is empty, the customer cannot take bread.

The customer waits until a baker adds bread to the basket.

This prevents underflow.

---

## Why Queue Is Used

The program uses Python’s `queue.Queue`.

`queue.Queue` is thread-safe.

It automatically handles waiting when:

- The basket is full
- The basket is empty

This means producers and consumers can safely work together.

---

## What I Learned

I learned how producers and consumers can communicate safely using a queue. I also learned that `queue.Queue` prevents adding too many items or removing items when none exist.

---

# Part 3: Dining Philosophers

## Description

This part demonstrates the Dining Philosophers problem.

There are:

- 3 philosophers
- 3 forks

Each philosopher needs two forks to eat.

Each philosopher repeats these steps:

1. Thinks
2. Picks up forks
3. Eats
4. Puts down forks

---

## Deadlock Problem

Deadlock means all threads wait forever and the program cannot continue.

In Dining Philosophers, deadlock can happen if every philosopher picks up one fork and waits for another fork.

Example:

```text
Philosopher 0 picks fork 0
Philosopher 1 picks fork 1
Philosopher 2 picks fork 2
```

Now each philosopher is waiting for the next fork, but no one releases their fork.

So everyone waits forever.

---

## Deadlock Prevention Method Used

The method used in this program is:

```text
Always pick the lower-numbered fork first.
```

For example, if a philosopher needs fork 0 and fork 2, the philosopher picks fork 0 first, then fork 2.

---

## Why Deadlock Does Not Happen

Deadlock requires circular waiting.

By making all philosophers pick forks in the same order, circular waiting is removed.

Because there is no circular waiting, deadlock does not happen.

The philosophers can continue thinking and eating normally.

---

## What I Learned

I learned that deadlock happens when threads wait on each other forever. I also learned that using a fixed order when taking locks can prevent deadlock.

---

# Part 4: Thread Pool

## Description

This part compares sequential execution with parallel execution.

There are 10 tasks.

Each task sleeps for a short time to simulate work.

The program runs the tasks in two ways:

1. Sequential execution
2. Parallel execution using `ThreadPoolExecutor`

---

## Sequential Execution

In sequential execution, tasks run one after another.

Only one task runs at a time.

If there are 10 tasks and each task takes about 1 second, the total time is around 10 seconds.

---

## Parallel Execution

In parallel execution, multiple tasks can run at the same time.

The program uses:

```python
ThreadPoolExecutor(max_workers=4)
```

This means up to 4 tasks can run at the same time.

Because of this, the total time is much shorter, usually around 3 seconds.

---

## Output

The output shows:

- Time for sequential execution
- Time for parallel execution
- Speedup
- Number of threads used

Example:

```text
Sequential time: 10.00 seconds
Parallel time:   3.00 seconds
Speedup:         3.33x faster
Threads used:    4
```

---

## Why Parallel Is Faster

Parallel execution is faster because several tasks run at the same time.

In this assignment, the tasks use `sleep`, so while one thread is waiting, another thread can also run.

This reduces the total time.

---

## What I Learned

I learned that a thread pool helps run many tasks using a limited number of worker threads. This makes the program faster for tasks that wait or sleep.

---

# Screenshots

The screenshots of the outputs are saved in the `screenshots` folder.

```text
screenshots/part1_output.png
screenshots/part2_output.png
screenshots/part3_output.png
screenshots/part4_output.png
```

Each screenshot shows the output of one part.

---

# Overall Learning

From this assignment, I learned:

- How to create threads in Python
- How multiple threads can run at the same time
- What a race condition is
- How locks prevent race conditions
- How the Producer-Consumer problem works
- How queues help producers and consumers communicate safely
- What deadlock is
- How to prevent deadlock
- How thread pools improve performance
- Why parallel execution can be faster than sequential execution

---

# Conclusion

This assignment helped me understand important concurrency concepts in Python. I learned that threads are useful, but they must be controlled carefully when they share data or resources.
