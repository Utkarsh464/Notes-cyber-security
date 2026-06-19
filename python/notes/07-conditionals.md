# Conditionals — Controlling Program Flow with if/elif/else

Every decision your tool makes — allow or block, scan or skip, alert or ignore — starts here.

## Basic Syntax

```python
age = 18

if age >= 18:
    print("you are an adult")
else:
    print("you are a minor")
```

## Multiple Conditions

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

## Nested Conditionals

```python
if user == "admin":
    if password == "secret":
        print("access granted")
    else:
        print("wrong password")
else:
    print("unknown user")
```

## Truthy and Falsy Values

```python
# Falsy values:
# False, None, 0, 0.0, "", [], {}, ()

if []:
    print("this won't run")

name = ""
if not name:
    print("name is empty")
```

## Ternary Operator

```python
status = "active" if logged_in else "inactive"
```

## Short-Circuit Evaluation

```python
# `and` stops at first False, `or` stops at first True
def check_ip(ip):
    return ip and is_trusted(ip)  # skips is_trusted if ip is None

def get_config(key):
    return cache.get(key) or load_config(key)  # falls back
```

## Walrus Operator (`:=`) — Python 3.8+

Assign and test in one expression.

```python
if (match := re.search(r"\d+", text)):
    print(f"found: {match.group()}")

while (chunk := file.read(1024)):
    process(chunk)
```

## Match/Case — Python 3.10+

Structural pattern matching for cleaner dispatch.

```python
def handle_status(code):
    match code:
        case 200:
            return "OK"
        case 301 | 302:
            return "redirect"
        case 401 | 403:
            return "auth error"
        case 500 | 502 | 503:
            return "server error"
        case _:
            return "unknown"

# Matching on structures
def analyze_packet(pkt):
    match pkt:
        case {"proto": "TCP", "port": p} if p < 1024:
            return f"privileged TCP port {p}"
        case {"proto": "UDP", "port": p}:
            return f"UDP port {p}"
        case _:
            return "unknown protocol"
```
