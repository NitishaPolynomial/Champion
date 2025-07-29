```mermaid
flowchart TD
    A[Start] --> B[Order Created by Loadster, Shiprocket, or Pidge]
    B --> C[Request sent to filtered champions]
    C --> D[Champion accepts and completes the ride]
    D --> E{Order Type: COD or Prepaid}
    E -- COD --> F[Show cash to be collected]
    F --> G[End]
    E -- Prepaid --> H[Show message - Payment in 3 to 5 hours - Add bank details]
    H --> I{Bank Details Exist?}
    I -- Yes --> J[Show Done button only]
    J --> K[Click Done to complete trip]
    K --> L[End]
    I -- No --> M[Disable Done until bank details are added]
    M --> N{Choose Bank Detail Type}
    %% Manual Bank Path
    N -- Bank Details --> B1[Enter Account Holder Name]
    B1 --> B2{Is Name Valid?}
    B2 -- No --> B2e[Error - Invalid Name]
    B2 -- Yes --> B3[Enter Account Number]
    B3 --> B4{Account Number Valid?}
     B4 -- Yes --> B5[Re-enter Account Number]
    B5 --> B6{Do Numbers Match?}
    B6 -- No --> B6e[Error - Mismatch]
    B6 -- Yes --> B7[Enter IFSC Code]
    B7 --> B8{IFSC Format Valid?}
    B8 -- No --> B8e[Error - Invalid IFSC]
    B8 -- Yes --> B9[Upload Passbook]
    B9 --> B10{Valid File Uploaded?}
    B10 -- No --> B10e[Error - Upload Required]
    B10 -- Yes --> Z
    B4 -- No --> B4e[Error - Invalid Account Number]
    %% UPI Path
    N -- UPI ID --> O[Enter or Select UPI ID]
    O --> P{UPI Format Valid?}
    P -- No --> P1[Show error - Invalid format]
    P -- Yes --> Q[Call UPI verification API]
    Q --> R{Verification Successful?}
    R -- No --> S[Show error - UPI not valid]
    R -- Yes --> T[Show name and checkmark]
    T --> Z[Enable Save - UPI details complete]

    Z --> AA[Bank Details Addition Completed]
    AA --> AB[Redirect to Complete Order Screen]
    AB --> AC[End]
