## 📊 Workflow Overview

The script processes thousands of CSV/XLSX files, normalizes them, 
combines the data, splits outputs if necessary, and logs mismatches/failures.

```mermaid
flowchart LR
    A[Start: Load files from folder] --> B{File type?}
    B --> |CSV/XLSX| C[Read file]
    C --> D[Clean blank rows & Normalize headers]
    D --> |Matches schema| E[Tag with source info & add to combined]
    D --> |Wrong headers| F[Mismatched report]
    C --> |Error reading| G[Failed report]
    E --> H[Concatenate all good data]
    H --> I{Total rows > 500k?}
    I --> |Yes| J[Split into chunks -> Save multiple Excel files]
    I --> |No| K[Save as single Excel file]
    F & G --> L[Save mismatch and failure reports]
    K & J --> M[End: Summary printed]
