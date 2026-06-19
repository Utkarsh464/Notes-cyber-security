# Newer Python Features — 3.10, 3.11, and Beyond

> **Utkarsh Solanki** — Cybersecurity & AI Student  
> [LinkedIn](https://linkedin.com/in/utkarsh-solanki-337806252) · [GitHub](https://github.com/Utkarsh464)

---

Features you will encounter in modern codebases and security tools.

## Match/Case — Python 3.10+

Structural pattern matching.

```python
def classify_response(status):
    match status:
        case 200:
            return "OK"
        case 301 | 302 | 307:
            return "redirect"
        case 401:
            return "unauthorized"
        case 403:
            return "forbidden"
        case 404:
            return "not found"
        case 500 | 502 | 503:
            return "server error"
        case _:
            return "unknown"

# Pattern matching on dicts
def handle_event(event):
    match event:
        case {"type": "login", "user": u}:
            return f"login by {u}"
        case {"type": "scan", "target": t, "ports": ps}:
            return f"scan of {t} on {len(ps)} ports"
        case _:
            return "unhandled event"
```

## str.removeprefix / str.removesuffix — Python 3.9+

Cleaner than slicing or `startswith`.

```python
url = "https://example.com"
url.removeprefix("https://")    # "example.com"

filename = "data.csv"
filename.removesuffix(".csv")   # "data"
```

## Zoneinfo — Python 3.9+

Timezone support without third-party libraries.

```python
from zoneinfo import ZoneInfo
from datetime import datetime

utc = datetime.now(ZoneInfo("UTC"))
ist = utc.astimezone(ZoneInfo("Asia/Kolkata"))
```

## Improved Type Hints

```python
# Python 3.9+ — use built-in generics
def parse(data: list[str]) -> dict[str, int]: ...

# Python 3.10+ — union with |
def lookup(key: str | int) -> str | None: ...

# Python 3.11+ — Self type
from typing import Self
class Parser:
    def clone(self) -> Self: ...
```

## Math Additions

```python
import math

math.comb(5, 2)    # 10  — combinations
math.perm(5, 2)    # 20  — permutations
math.isclose(0.1 + 0.2, 0.3)  # True  — safe float compare
```

## Exception Groups — Python 3.11+

Handle multiple unrelated exceptions at once.

```python
try:
    raise ExceptionGroup("scan errors",
        [ConnectionError("timeout"),
         PermissionError("denied")])
except* ConnectionError as e:
    print(f"network: {e.exceptions}")
except* PermissionError as e:
    print(f"auth: {e.exceptions}")
```
