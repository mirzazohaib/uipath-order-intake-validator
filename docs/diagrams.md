# Process diagrams

This file contains the workflow diagrams for the RPA Order Intake Validator project.

---

# Version 1 – Validator

## High-level automation flow

```mermaid
flowchart TD
    A[Start automation] --> B[Try Catch starts]
    B --> C[Read sample_orders.xlsx]
    C --> D[Load orders into ordersDt]
    D --> E[Create validOrdersDt and exceptionOrdersDt]
    E --> F[Loop through each order row]
    F --> G[Reset isValid and exceptionReason]
    G --> H[Apply validation rules]
    H --> I{Is row valid?}
    I -- Yes --> J[Add row to validOrdersDt]
    I -- No --> K[Add row to exceptionOrdersDt]
    J --> L{More rows?}
    K --> L
    L -- Yes --> F
    L -- No --> M[Calculate total, valid, and exception counts]
    M --> N[Build summaryDt]
    N --> O[Clear and write validated_orders.xlsx]
    O --> P[Clear and write exceptions.xlsx]
    P --> Q[Clear and write processing_summary.xlsx]
    Q --> R[Log successful completion]
    R --> S[End]
    B --> T[Catch unexpected exception]
    T --> U[Log failure message]
```

## Row validation flow

```mermaid
flowchart TD
    A[CurrentRow from ordersDt] --> B[Set isValid = True]
    B --> C[Set exceptionReason = empty]
    C --> D{Email blank or missing @?}
    D -- Yes --> D1[Append: Invalid or missing email;<br/>Set isValid = False]
    D -- No --> E
    D1 --> E{Country supported?}
    E -- No --> E1[Append: Country not supported;<br/>Set isValid = False]
    E -- Yes --> F
    E1 --> F{Quantity numeric and > 0?}
    F -- No --> F1[Append: Invalid quantity;<br/>Set isValid = False]
    F -- Yes --> G
    F1 --> G{Order value numeric and > 0?}
    G -- No --> G1[Append: Invalid order value;<br/>Set isValid = False]
    G -- Yes --> H
    G1 --> H{Priority blank?}
    H -- Yes --> H1[Set Priority = Normal]
    H -- No --> I
    H1 --> I{isValid = True?}
    I -- Yes --> J[Add to validOrdersDt]
    I -- No --> K[Add to exceptionOrdersDt]
```

## Input and output data flow

```mermaid
flowchart LR
    A[input/sample_orders.xlsx] --> B[UiPath Main.xaml]
    B --> C[validated_orders.xlsx]
    B --> D[exceptions.xlsx]
    B --> E[processing_summary.xlsx]
```

## Exception handling model

```mermaid
flowchart TD
    A[Run automation] --> B{Expected business-rule issue?}
    B -- Yes --> C[Add row to exceptions.xlsx]
    B -- No --> D{Unexpected runtime issue?}
    D -- Yes --> E[Catch System.Exception]
    E --> F[Log error message]
    D -- No --> G[Continue processing]
```

Business exceptions are expected validation failures, such as missing email or invalid quantity. Runtime exceptions are unexpected technical problems, such as a missing file, locked workbook, or corrupted Excel structure.

---

# Version 2 – Enterprise Solution

```mermaid
flowchart LR

Excel --> Dispatcher

Dispatcher --> Queue

Queue --> Performer

Performer --> Valid

Performer --> BusinessException

Performer --> SystemException
```

---

# REFramework Transaction Lifecycle

```mermaid
flowchart LR

Init

-->

GetTransactionData

-->

Process

-->

SetTransactionStatus

-->

GetTransactionData
```
