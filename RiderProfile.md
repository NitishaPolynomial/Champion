```mermaid
graph TD;
  A[Welcome Champion Screen] -->|Click Continue| B[Upload Document to go Online]
  B -->|Click Profile| C[Profile Screen - 40% Completion]

  %% Profile Screen Navigation
  C -->|Click Personal Details| PD[Personal Details]
  C -->|Click Vehicle Details| E[Vehicle Details Screen]
  C -->|Click Bank Details| F[Bank Details Screen]

  %% Personal Details Flow
  PD -->|Click KYC| KYC[Know Your Customer]
  KYC --> K1[Enter Aadhaar Details]

  %% Aadhaar Flow
  K1 -->|Enter Aadhaar Number| K2["Aadhaar Number Entered<br>Validation:<br>1. 12 digits<br>2. Digits only<br>3. No repetitive sequences"]
  K1 -->|Upload Aadhaar Front| K3[Aadhaar Front Uploaded]
  K3 -->|Upload Aadhaar Back| K4[Aadhaar Back Uploaded]

  K2 -->|"Invalid Aadhaar Format"| KA[Show Aadhaar Error]
  K2 --> K5{All Aadhaar Fields Provided?}
  K4 --> K5
  K5 --|No|--> K6[Show Aadhaar Fields Required]
  K5 --|Yes|--> K7[Submit Aadhaar]

  K7 --> K8[Aadhaar Under Verification]
  K8 -->|"Failure"| K9[Retry Aadhaar Upload]
  K8 -->|"Success"| K10[Proceed to PAN Upload]

  %% PAN Flow (Always follows Aadhaar)
  K10 --> K11[Enter PAN Details]
  K11 -->|Enter PAN Number| K12[PAN Number Entered]
  K12 -->|Upload PAN Card| K12A[PAN Card Uploaded]
  K12A -->|Click Submit| K13[PAN Under Verification]
  K13 -->|"Failure"| K14[Retry PAN Upload]
  K13 -->|"Success"| K15[Proceed to DL Upload]
  K11 -->|"Invalid PAN Format"| KB[Show PAN Error]

  %% DL Flow (Always follows PAN)
  K15 --> DL[Driving License Upload]
  DL -->|Upload DL Front| D13[DL Front Uploaded]
  D13 -->|Upload DL Back| D14[DL Back Uploaded]
  D14 -->|Click Submit| D15[DL Under Verification]
  D15 -->|"Success"| G[Back to Profile Screen]
  D15 -->|"Failure"| D16[Retry DL Upload]

  %% Retry Mechanisms
  K9 -->|"User Clicks Retry"| K1
  K14 -->|"User Clicks Retry"| K11
  D16 -->|"User Clicks Retry"| DL

  %% Vehicle Details Flow
  E -->|Enter Vehicle Number| E1[Vehicle Number Entered<br>Validation:<br>1. Starts with state code<br>2. No all zeros<br>3. Uppercase only<br>4. Valid format]
  E -->|Upload RC Card| E2[RC Card Uploaded]

  E1 --> E3{Both Vehicle Number & RC Uploaded?}
  E2 --> E3

  E3 --|No|--> E4[Show Required Fields Message]
  E3 --|Yes|--> E5[Enable Submit Button]
  E5 -->|Click Submit| E6[RC Card Under Verification]
  E6 -->|"Success"| E7[Select Vehicle Type]
  E6 -->|"Failure"| E8[Retry RC Upload]

  %% Vehicle Type Selection
  E7 -->|Select Fuel Type| E9[Enable Submit Button]
  E9 -->|Click Submit| G

  %% Bank Details Flow
  F -->|Enter Account Holder's Name| F1[Enter Name<br>Validation:<br>1. Only letters<br>2. 2-200 characters<br>3. No special characters<br>4. No leading/trailing spaces]
  F1 -->|Enter Account Number| F2[Account Number<br>6-18 digits only]
  F2 -->|Re-enter Account Number| F3[Re-enter Account Number]
  F3 -->|Enter IFSC Code| F4[IFSC Code<br>Exactly 11 characters]
  F4 -->|Enter UPI ID| F5[Enter UPI ID]
  F5 -->|Upload Passbook| F6[Upload Passbook]
  F6 -->|Click Submit| F7[Bank Details Under Verification]
  F7 -->|"Success"| G
  F7 -->|"Failure"| F8[Retry Bank Details]
  F2 -->|"Invalid Format"| N[Highlight Error Field]

  %% Completion Checks
  G -->|All Sections Completed| H[Profile Completion 100%]
  G -->|Any Section Pending| I[Profile Incomplete - Show Pending Items]
  H --> J[Buy Plan & Start]

  %% Retry Uploads
  E8 -->|"User Clicks Retry"| E
  F8 -->|"User Clicks Retry"| F

  %% Pending Sections Navigation
  H -->|"Click Profile Again"| C
  I -->|"Click KYC"| KYC
  I -->|"Click DL"| DL
  I -->|"Click Vehicle Details"| E
  I -->|"Click Bank Details"| F
