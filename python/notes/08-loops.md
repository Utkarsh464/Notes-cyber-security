# Loops — Iterating Through Data with for and while

Process lists of IPs, read log lines, brute-force directories — loops make it repeatable.

## For Loop

```python
for i in range(5):
    print(i)          # 0 1 2 3 4

for i in range(2, 6):
    print(i)          # 2 3 4 5

for i in range(0, 10, 2):
    print(i)          # 0 2 4 6 8
```

## Looping Over Collections

```python
for char in "hello":
    print(char)

for item in [1, 2, 3]:
    print(item)

for key, val in {"a": 1, "b": 2}.items():
    print(f"{key}: {val}")
```

## While Loop

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

## Break and Continue

```python
for i in range(10):
    if i == 3:
        continue      # skip 3
    if i == 7:
        break         # stop at 7
    print(i)
```

## Else with Loops

`else` runs only if the loop completed without a `break`.

```python
def find_port(port, scanned):
    for p in scanned:
        if p == port:
            print("found")
            break
    else:
        print("not found — loop exhausted")

# Useful for search loops
```

## Enumerate and Zip

```python
ports = [22, 80, 443]
for i, port in enumerate(ports, start=1):
    print(f"{i}: {port}")

services = ["SSH", "HTTP", "HTTPS"]
for port, service in zip(ports, services):
    print(f"{service} -> {port}")

# zip stops at the shortest iterable
```

## Reversed and Sorted

```python
for item in reversed([1, 2, 3]):
    print(item)       # 3, 2, 1

for item in sorted([3, 1, 2]):
    print(item)       # 1, 2, 3
```

## Generator Expressions

Memory-efficient iteration without building a list.

```python
total = sum(x**2 for x in range(1000))
logs = (line.strip() for line in file if "ERROR" in line)

for log in logs:
    print(log)
```

## Itertools Overview

```python
from itertools import chain, product, count, cycle

# chain — iterate over multiple sequences as one
for item in chain([1, 2], [3, 4]):
    print(item)       # 1 2 3 4

# product — cartesian product (nested loop replacement)
for ip, port in product(["10.0.0.1", "10.0.0.2"], [22, 80]):
    print(f"{ip}:{port}")

# cycle — infinite repeater
for state in cycle(["up", "down"]):
    print(state)      # up down up down ...
```

## Loop Performance Note

```python
# Bad — attribute lookup on each iteration
for i in range(len(items)):
    process(items[i])

# Good — iterate directly
for item in items:
    process(item)

# Good — use enumerate when index needed
for i, item in enumerate(items):
    print(i, item)
```
