# Solution Architecture

## Version 1

Local Excel validation workflow.

```
Excel
↓

Validator

↓

Excel
```

---

## Version 2

Enterprise Dispatcher–Performer architecture.

```
Excel
↓

Dispatcher

↓

Queue

↓

Performer

↓

Business Result
```

The Dispatcher creates work.

The Performer processes work.

The two are completely independent.
