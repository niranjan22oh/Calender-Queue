Certainly! Below is the **fully copyable Markdown** version for your `README.md` file:

````markdown
# 📅 Calendar Queue (CQ)

A **Calendar Queue** is a priority queue inspired by a physical desk calendar. Each bucket (day) holds scheduled events based on their timestamp (priority). Events with earlier times are dequeued first.

---

## 🛠️ How It Works

- Each "day" is represented as a **bucket**, implemented as a **sorted linked list**.
- An array of 365 pointers (e.g., `bucket[12]`) maps to each day's list of events.
- Events are scheduled using their **timestamp**, where **lower time = higher priority**.

---

## 📌 Core Concepts

### 1. Bucket Width & Resizing Policy

- **Bucket Width (`w`)** is the time interval covered by a bucket.
- Buckets dynamically resize for efficiency:
  - If `Ne > 2 * Nb`, double the number of buckets.
  - If `Ne < Nb / 2`, halve the number of buckets.
- New width is calculated by sampling average inter-event time gaps.
- Resizing involves creating a new Calendar Queue and copying all events.

> ℹ️ Optimal performance is achieved when `w` is close to the average event time gap.

### 2. Bucket Index Calculation

```python
index = int(time / width) % n_buckets
````

* This index determines the bucket in which the event is stored.

### 3. Other Key Attributes

* **Bucket Top**: Priority at the top of the last dequeued bucket.
* **LastBucket**: Index of the last bucket accessed.
* **LastPrio**: Priority of the last dequeued event.

---

## ⏱️ Time Complexity

| Operation       | Description                                                           | Time Complexity              |
| --------------- | --------------------------------------------------------------------- | ---------------------------- |
| **Insert**      | Uses hash to place the event in the correct bucket.                   | `O(1)` (average)             |
| **Pop Item**    | Scans to find the earliest available event.                           | `O(N)` (worst case)          |
| **Delete Item** | Finds the appropriate bucket and removes the event.                   | `O(m)` (m = items in bucket) |
| **Update Item** | Scans all buckets to locate and update an event by ID.                | `O(N)`                       |
| **Resize**      | Creates a new calendar with adjusted width and re-inserts all events. | `O(N)`                       |

---

## 🧪 Changes Made to Pre-existing Simulus

### 📁 `Event.py`

* Removed the old `PQDict` class and implemented the `CalendarQueue` class.
* Removed `sink()` and `swim()` operations.
* Added logic for **resizing buckets**: `Nb` must be a power of 2 and `w` in multiples of 3.
* Simplified event management by reducing dependence on event IDs.
* Rewrote event methods to work with the CalendarQueue structure.

### 📁 `Simulator.py`

* Updated logic to support **list of lists** instead of dict-based access.
* Preserved method names and outputs to match the original simulation flow.

---

## 🚀 How to Run Modified Simulus

1. **Unzip** the project files to a location (e.g., `Desktop` or `C:/`).
2. Run:

   ```bash
   pip install simulus
   ```
3. Navigate to:

   ```
   C:/Users/YourUsername/AppData/Local/Programs/Python/Python310/site-packages/simulus
   ```

   > ⚠️ `AppData` is a hidden folder.
4. **Backup** the original `event.py` and `simulator.py` files.
5. **Replace** them with the modified versions from the zip file.
6. Run the example scripts provided and compare results with the output files included.

---

## 📚 References

* [NS-3 Calendar Scheduler Class (Doxygen)](https://netdb.cis.upenn.edu/rapidnet/doxygen/html/classns3_1_1_calendar_scheduler.html#_details)
* [NS-3 Source Calendar Scheduler](https://www.nsnam.org/docs/release/3.18/doxygen/calendar-scheduler_8cc_source.html)
* Randy Brown, *Calendar Queues: A Fast O(1) Priority Queue Implementation for the Simulation Event Set Problem*, CACM, 31(10):1220–1227, October 1988.

```

Let me know if you'd like a version with badges, collapsible sections, or visuals for GitHub pages.
```
