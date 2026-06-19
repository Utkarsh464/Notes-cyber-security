# Tuples, Sets, and Dictionaries — Immutable, Unique, and Key-Value Collections

Tuples for fixed data, sets for deduplication, dicts for lookups — essential for security tooling.

## Tuples

Tuples are ordered and immutable. Useful for data that shouldn't change.

```python
coords = (10, 20)
single = (5,)      # comma needed

x, y = coords      # unpacking
print(x)           # 10
```

### Tuple Methods

```python
t = (1, 2, 3, 2, 4)
t.count(2)         # 2
t.index(3)         # 2
```

### Named Tuples

```python
from collections import namedtuple

Port = namedtuple("Port", ["number", "service"])
p = Port(22, "SSH")
p.number           # 22
p.service          # "SSH"
```

---

## Sets

Sets are unordered collections of unique items.

```python
unique_ports = {22, 80, 443, 22}
# {80, 443, 22}  — duplicates removed

unique_ports.add(8080)
unique_ports.remove(80)
```

### Set Operations

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a | b   # union:          {1, 2, 3, 4, 5, 6}
a & b   # intersection:   {3, 4}
a - b   # difference:     {1, 2}
b - a   # difference:     {5, 6}
a ^ b   # sym diff:       {1, 2, 5, 6}

a.issubset({1, 2, 3, 4, 5})     # True
a.issuperset({1, 2})            # True
a.isdisjoint({7, 8})            # True
```

### Frozenset

Immutable set — usable as a dict key.

```python
fs = frozenset([1, 2, 3])
# fs.add(4)  — AttributeError
```

---

## Dictionaries

Dictionaries store key-value pairs.

```python
user = {
    "name": "alice",
    "role": "admin",
    "age": 30
}

user["name"]               # "alice"
user.get("email", "N/A")   # "N/A" (safe access)
user["email"] = "alice@hack.com"

user.keys()    # dict_keys(["name", "role", "age"])
user.values()  # dict_values(["alice", "admin", 30])
user.items()   # key-value pairs

for key, val in user.items():
    print(f"{key}: {val}")
```

### Dict Comprehensions

```python
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

ports = {s: n for n, s in [(22, "SSH"), (80, "HTTP")]}
# Warning: n and s are reversed — intentional swap
```

### Merging Dictionaries

```python
defaults = {"timeout": 30, "retries": 3}
config = {"timeout": 60}

merged = {**defaults, **config}       # Python 3.5+
merged = defaults | config            # Python 3.9+
```

### Nested Dicts

```python
users = {
    "alice": {"role": "admin", "mfa": True},
    "bob":   {"role": "user",  "mfa": False}
}

users["alice"]["role"]     # "admin"
```

---

## Specialized Collections

```python
from collections import defaultdict, Counter, OrderedDict

# defaultdict — auto-initializes missing keys
log_counts = defaultdict(int)
log_counts["ERROR"] += 1   # no KeyError

# Counter — frequency counting
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.1"]
Counter(ips)               # {"10.0.0.1": 2, "10.0.0.2": 1}

# OrderedDict — remembers insertion order (dict does too since 3.7)
OrderedDict([("a", 1), ("b", 2)])
```
