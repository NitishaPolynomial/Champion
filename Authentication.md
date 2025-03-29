```mermaid
graph TD;
  A[App Launch] --> B[Language Selection]
  B --> C[Proceed to Mobile Number
  Validations for Mobile Number -
    1. Only 10 digit numbers are allowed.
    2. Characters and Special characters are not allowed.
    3. Negative numbers are not allowed.]
  
  C -->|Enter Valid Number| D[Enable Proceed Button]
  C -->|"Invalid Number: Less than 10 digits, alphabets, special characters"| E[Show Error Message]
  C -->|"Empty Field"| F[Disable Proceed Button]

  D -->|Proceed Clicked| G[Terms of Use Check]
  G -->|"Checked"| H[Send OTP]
  G -->|"Not Checked"| I[Disable Proceed Button]

  H --> J[Enter OTP
 Validations for OTP -
    1. Only 4 digit numbers are acceptable.
    2. Characters and Special characters are not allowed.
    3. Negative numbers are not allowed.]
  J -->|"Valid OTP"| K[Login Success]
  J -->|"Invalid OTP"| L[Show Error Message]
  J -->|"Resend OTP Clicked"| H[Resend OTP]

 K --> M[Onboarding Screen 1: Earn First, Pay Later]
  M --> N[Onboarding Screen 2: Boost Earnings]
  N --> O[Onboarding Screen 3: No Suspensions, No Penalties]
  O -->|Proceed Clicked| T[User Type Selection]

  T -->|Select User Type| U[Enable Proceed Button]
  T -->|"No Selection"| V[Disable Proceed Button]

  U --> W[User Type Specific Details]
  
  W --> |"Rider"| RIDER_NAME[Enter Name
Validations for Name -
    1. Character limit should be 2-200 characters.
    2. Numbers and special characters other than space are not allowed.]
   RIDER_NAME --> |Invalid Input| ERROR3[Show Error Message]
  RIDER_NAME --> |Valid Input| X[Permission Screen]
 
  W --> |"Fleet Owner"| FO_NAME[Enter Name
Validations for Name -
    1. Character limit should be 2-200 characters.
    2. Numbers and special characters other than space are not allowed.]

  FO_NAME --> FO_VEHICLES[Number of Vehicles
Validation for Vehicle Number - 
  <li> Only characters and numbers are allowed.</li>
  <li> Vehicle number must be in proper format.</li>
  <li> Vehicle number must be registered.</li>
]

  FO_VEHICLES --> FO_GSTIN["GSTIN Option
Validations - 
    1. Must be 15 characters long.
    2. Must be in proper format.
    3. No special characters or spaces allowed.
    4. The PAN within GST should be valid."]
  FO_GSTIN -->|"Valid Input"| X
  FO_GSTIN -->|"Invalid Input"| ERROR1[Show Error Message]

  W -->|"Driver-Cum-Owner"| DCO_NAME[Enter Name
Validations for Name -
    1. Character limit should be 2-200 characters.
    2. Numbers and special characters other than space are not allowed.]

  DCO_NAME --> DCO_VEHICLES[Number of Vehicles
Validation for Vehicle Number - 
  <li> Only characters and numbers are allowed.</li>
  <li> Vehicle number must be in proper format.</li>
  <li> Vehicle number must be registered.</li>
]

  DCO_VEHICLES --> DCO_GSTIN["GSTIN Option
Validations - 
    1. Must be 15 characters long.
    2. Must be in proper format.
    3. No special characters or spaces allowed.
    4. The PAN within GST should be valid."]
  DCO_GSTIN -->|"Valid Input"| X
  DCO_GSTIN -->|"Invalid Input"| ERROR2[Show Error Message]

  X --> |Allow All| Y[Document Ready Screen]
  X --> |"Deny Permissions"| Z[Show Warning]

  Y --> WELCOME[Welcome Champion Screen]
  WELCOME -->|Continue| DONE[Profile Setup Complete]
