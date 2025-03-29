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
  PD -->|Click DL Details| DL[Driving License Details]

  %% KYC Flow (Aadhaar & PAN)
  KYC -->|Select Aadhaar or PAN| K1{KYC Selection}
  K1 -->|User Selects Aadhaar| K2[Enter Aadhaar Details]
  K1 -->|User Selects PAN| K3[Enter PAN Details]

  %% Aadhaar Upload Flow (All Fields Mandatory)
  K2 -->|Enter Aadhaar Number| K4["Aadhaar Number Entered <br> Validation: <br> 1. Must be 12 digits long. <br> 2. Digits only (0-9). <br> 3. No repetitive sequences."]
  K2 -->|Upload Aadhaar Front| K5[Aadhaar Front Uploaded]
  K5 -->|Upload Aadhaar Back| K6[Aadhaar Back Uploaded]

  K4 -->|"Invalid Aadhaar Format"| KA[Show Aadhaar Error Message]
  K4 --> K7{All Aadhaar Fields Provided?}
  K6 --> K7

  K7 --|No|--> K8[All Aadhaar Fields Required] 
  K7 --|Yes|--> K9[Submit Button Enabled]

  K9 -->|Click Submit| K10[Aadhaar Under Verification]
  K10 -->|"Failure"| K11[Retry Aadhaar Upload]
  K10 -->|"Success"| G[Back to Profile Screen]
  
  

    %% PAN Upload Flow
  K3 -->|Enter PAN Number| K12[PAN Entered]
  K12 -->|Click Submit| K13[PAN Under Verification]
  K13 -->|"Success"| G
  K13 -->|"Failure"| K14[Retry PAN Upload]
  K3 -->|"Invalid PAN Format"| KB[Show PAN Error Message]

  %% PAN Selection Alert
  K1 -->|"User Switches from Aadhaar to PAN"| KC[Show Data Reset Alert]
  KC -->|User Confirms| K3
  KC -->|User Cancels| K1

    %% DL Upload Flow
  DL -->|Upload DL Front| D13[DL Front Uploaded]
  D13 -->|Upload DL Back| D14[DL Back Uploaded]
  D14 -->|Click Submit| D15[DL Under Verification]
  D15 -->|"Success"| G
  D15 -->|"Failure"| D16[Retry DL Upload]

   %% Vehicle Details Flow (Updated)
  E -->|Enter Vehicle Number| E1[Vehicle Number Entered <br> Validation: <br> 1. Must start with Indian State code . <br> 2. Cannot be all zeros. <br> 3. Only uppercase letters and digits. <br> 4. Must be in standard format.]
  E -->|Upload RC Card| E2[RC Card Uploaded]

  %% Enable Submit Button Only If Both Fields Are Entered
  E1 --> E3{Are both vehicle number & RC uploaded?}
  E2 --> E3

  E3 --|No|--> E4[Show Required Fields Message]
  E3 --|Yes|--> E5[Enable Submit Button]

  E5 -->|Click Submit| E6[RC Card Under Verification]
  E6 -->|"Success"| E7[Select Vehicle Type]
  E6 -->|"Failure"| E8[Retry RC Upload]

  %% Vehicle Type Selection
  E7 -->|Select Petrol| E9[Enable Submit Button]
  E7 -->|Select Diesel| E9
  E7 -->|Select EV| E9

  E9 -->|Click Submit| G[Back to Profile Screen]

  %% Bank Details Flow
  F -->|Enter Account Holder's Name| F1[Enter Name <br> Validation: <br> 1. Must contain only letters . <br> 2. Length msut be 2-200 characters. <br> 3. Only uppercase letters and digits. <br> 4. No Consecutive Spaces or Special Characters. <br> 5. No Leading or Trailing Spaces.]
  F1 -->|Enter Account Number| F2[Enter Account Number <br> Validation: <br> 1. Length ramges from 6 to 18 digits. <br> 2. No alphabets or special characters allowed.]
  F2 -->|Re-enter Account Number| F3[Re-enter Account Number]
  F3 -->|Enter IFSC Code| F4[Enter IFSC Code <br> Validation: <br> 1. Must be exactly 11 characters long. <br> 2. No special characters allowed. <br> 3. The first 4 characters must match a valid bank code.]
  F4 -->|Enter UPI ID| F5[Enter UPI ID]
  F5 -->|Upload Passbook First Page| F6[Upload Passbook]
  F6 -->|Click Submit| F7[Bank Details Under Verification]
  F7 -->|"Success"| G
  F7 -->|"Failure"| F8[Retry Bank Details]

  %% Profile Completion Check
  G -->|All Sections Completed| H[Profile Completion 100%]
  G -->|Any Section Pending| I[Profile Still Incomplete - Show Pending Items]

  %% Edge Cases
  E4 -->|"Missing Vehicle Details"| L[Show Required Fields Message]
  E8 -->|"Invalid RC Upload"| M[Retry Upload]
  F2 -->|"Incorrect Bank Details Format"| N[Highlight Error Field]

%% Retry Mechanisms
  K11 -->|"User Clicks Retry"| K2
  K14 -->|"User Clicks Retry"| K3
  D16 -->|"User Clicks Retry"| DL
  E8 -->|"User Clicks Retry"| E
  F8 -->|"User Clicks Retry"| F

    H -->|"Click Profile Again"| C
  I -->|"User Clicks Pending Section: KYC"| KYC
  I -->|"User Clicks Pending Section: DL"| DL
  I -->|"User Clicks Pending Section: Vehicle Details"| E
  I -->|"User Clicks Pending Section: Bank Details"| F
