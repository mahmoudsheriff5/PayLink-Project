# PayLink — Phase 1 Requirements Pack 

Digital Bill-Payment and Wallet Backend System 

## 1. Problem Summary 

PayLink is a digital payment system that allows customers in Egypt to pay their electricity, water, mobile, and internet bills using a digital wallet. Instead of going to payment offices and waiting in lines, customers can pay their bills directly through the system or through local agents. 

One of the main challenges PayLink faces is making sure that payments are handled correctly, especially when dealing with different billers. For example, a payment might be sent twice because of a network problem, or a biller might take too long to respond. In these situations, the system needs to make sure customers aren't charged twice or lose money because of a failed payment. 

To solve these problems, PayLink will provide a backend system that manages customer accounts, wallets, bill payments, service fees, and agent commissions. It will also keep track of transactions, handle payment failures, and check payment records against billers' records to make sure everything is accurate. 

The system should also be easy to maintain and expand, so new billers can be added without having to make major changes to the existing system. 

## 2. Stakeholder Analysis 

PayLink involves several stakeholders who either use the system, manage its operations, or provide external services needed to complete payments. Understanding their roles helps us identify the system's requirements and make sure each stakeholder's needs are considered during development. 

### 2.1 Stakeholder Categories 

We can divide them into three main categories: 

#### 1. Primary Stakeholders: 

These are the people who directly use PayLink to perform payment-related activities. 

1. Customers: Use the system to manage their wallets and pay bills. 

2. Agents: Help customers complete payments and earn commissions. 

#### 2. Internal Stakeholders: 

These are the people within PayLink who manage the system, support its users, and oversee business operations. 

Page 1 of 25 

PayLink — Phase 1 Requirements Pack 

1. Admins: Manage billers, services, fees, and payment limits. 

2. Support Employees: Handle customer issues and investigate payment problems. 

3. PayLink Management: Oversees the platform's operations and business performance. 

#### 3. External Stakeholders: 

These are organizations or services outside PayLink that interact with the platform to support payment processing and communication. 

1. Billers: Electricity, water, mobile, and internet service providers that receive payments. 

2. Notification Providers: External services that deliver SMS, email, and push notifications. 

### 2.2 Stakeholder Responsibilities 

The following table summarizes the main responsibilities of each stakeholder. 

|Stakeholder|Description and Responsibilities|
|---|---|
|Customer|Uses PayLink to manage a digital wallet, check bills, make payments, and view<br>transaction history.|
|Agent|Helps customers pay bills through PayLink and earns commissions on<br>successful payments.|
|Admin|Manages billers, available services, fees, and payment limits.|
|Support Employee|Helps resolve payment issues, checks transaction details, and manages blocked<br>accounts.|
|PayLink Management|Oversees business operations and expects the system to be reliable, secure,<br>and easy to expand.|
|Billers|External service providers, such as ElectroCo, AquaCo, and TopUpNet, that<br>provide billing information and process payments.|
|Notification Providers|External services responsible for delivering payment confirmations and failure<br>notifications to customers.|



These stakeholders have different responsibilities, but they all depend on PayLink handling payments correctly and keeping financial records accurate. 

## 3. Functional Requirements (User Stories) 

User Stories related to functional requirements: 

### US-01: Customer Registration 

#### Priority: Must  |  User Story: 

Page 2 of 25 

PayLink — Phase 1 Requirements Pack 

As a new customer, I want to create a PayLink account so that I can access the system and use its wallet and bill payment services. 

#### Acceptance Criteria: 

- Given a new customer provides all required registration information, 

- When the customer submits valid details, 

- Then the system creates a new customer account with a basic verification level. 

#### Exceptional Scenarios: 

#### Scenario 1: Registration with Missing Information 

- Given a customer leaves one or more required fields empty, 

- When the customer submits the registration form, 

- Then the system rejects the registration and displays a clear message explaining which information is missing. 

#### Scenario 2: Duplicate Registration 

Given a customer account already exists with the same unique registration identifier, 

- When another registration is attempted using that identifier, 

- Then the system rejects the request and informs the customer that an account already exists. 

### US-02: Customer Verification Upgrade 

Priority: Should  |  User Story: 

As a customer with a basic account, I want to upgrade my verification level so that I can make payments with a higher daily limit. 

#### Acceptance Criteria: 

- Given a customer has a basic account and meets the verification requirements, 

- When the customer's verification upgrade is approved, 

- Then the system changes the account level to verified and increases the daily payment limit from 5,000 EGP to 30,000 EGP. 

#### Exceptional Scenarios: 

#### Scenario 1: Verification Requirements Not Met 

- Given a customer has not met the required verification conditions, 

- When the customer requests an upgrade, 

- Then the system does not upgrade the account and provides a clear reason. 

Page 3 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Account Already Verified 

- Given a customer already has a verified account, 

- When the customer attempts to upgrade the verification level again, 

- Then the system informs the customer that the account is already verified and leaves the verification level unchanged. 

### US-03: View Wallet Balance and Transaction History 

Priority: Must  |  User Story: 

As a customer, I want to view my wallet balance and transaction history so that I can track my money and know how much I have available for payments. 

#### Acceptance Criteria: 

- Given a customer is logged into PayLink and has an active wallet, 

- When the customer requests their wallet details, 

- Then the system displays the available balance, held balance, and transaction history. 

#### Exceptional Scenarios: 

Scenario 1: Customer Has No Transaction History 

- Given a customer has an active wallet but has not made any transactions, 

- When the customer views their wallet details, 

- Then the system displays the wallet balances and an empty transaction history. 

#### Scenario 2: Unauthorized Wallet Access 

- Given a user is not authenticated or attempts to access another customer's wallet without permission, 

- When the user requests wallet details, 

- Then the system denies access and does not reveal the wallet information. 

### US-04: Wallet Top-Up 

Priority: Must  |  User Story: 

As a customer, I want to add money to my PayLink wallet using a simulated card payment or an agent cash payment so that I have enough balance to pay my bills. 

#### Acceptance Criteria: 

Page 4 of 25 

PayLink — Phase 1 Requirements Pack 

- Given a customer has an active wallet and provides a valid top-up amount and payment method, 

- When the simulated card payment or agent cash payment is confirmed as successful, 

- Then the system credits the wallet with the top-up amount and records the transaction. 

#### Exceptional Scenarios: 

#### Scenario 1: Invalid Top-Up Amount 

- Given a customer enters a zero or negative top-up amount, 

- When the customer submits the top-up request, 

- Then the system rejects the request and displays an appropriate error message. 

#### Scenario 2: Failed Top-Up Payment 

- Given a customer attempts to top up their wallet using a simulated card payment, 

- When the payment is declined, 

Then the system does not credit the wallet and informs the customer that the top-up failed. 

### US-05: Record Wallet Transactions in the Ledger 

Priority: Must  |  User Story: 

As a customer, I want every money movement in my wallet to be recorded accurately so that my balance and transaction history remain correct and traceable. 

#### Acceptance Criteria: 

- Given a wallet transaction changes the customer's available or held balance, 

- When the transaction is successfully processed, 

- Then the system creates the corresponding ledger entries and calculates wallet balances from the recorded entries rather than directly overwriting them. 

#### Exceptional Scenarios: 

#### Scenario 1: Ledger Recording Failure 

- Given a wallet transaction requires one or more ledger entries, 

- When the system cannot save the required entries, 

- Then the transaction is not committed and the wallet's financial records remain unchanged. 

#### Scenario 2: Duplicate Transaction Processing 

- Given a wallet transaction has already been processed and recorded, 

- When the same logical transaction is submitted again, 

- Then the system prevents duplicate financial entries and preserves the correct wallet balance. 

Page 5 of 25 

PayLink — Phase 1 Requirements Pack 

### US-06: Manage Billers and Services 

Priority: Must  |  User Story: 

As an admin, I want to add, edit, and disable billers and their services so that PayLink can keep its available payment options up to date. 

#### Acceptance Criteria: 

- Given an authenticated admin provides valid information for a new biller or service, 

- When the admin saves the information, 

- Then the system adds the new biller or service to the catalog. 

- Given an existing biller or service needs to be updated, 

- When the admin submits valid changes, 

- Then the system saves the updated information. 

- Given an admin selects an active biller or service, 

- When the admin disables it, 

- Then the system marks it as inactive and prevents customers from initiating new payments through it. 

#### Exceptional Scenarios: 

#### Scenario 1: Missing or Invalid Information 

- Given an admin enters incomplete or invalid biller information, 

- When the admin attempts to save it, 

- Then the system rejects the request and displays a clear error message. 

#### Scenario 2: Unauthorized Access 

- Given a user does not have admin permissions, 

- When the user attempts to add, edit, or disable a biller or service, 

- Then the system denies the action and leaves the existing information unchanged. 

### US-07: View Available Billers and Services 

Priority: Must  |  User Story: 

As a customer, I want to view the available billers and their required information so that I can choose the service I need and know what details to provide before making a payment. 

#### Acceptance Criteria: 

Page 6 of 25 

PayLink — Phase 1 Requirements Pack 

- Given a customer accesses the bill payment section, 

- When the customer requests the list of available billers, 

- Then the system displays the active billers and their available services. 

- Given a customer selects a biller service, 

- When the customer views its details, 

- Then the system displays the required input fields, such as a meter number or phone number. 

#### Exceptional Scenarios: 

#### Scenario 1: No Available Billers 

- Given there are no active billers or services available, 

- When a customer opens the bill payment section, 

- Then the system displays a message indicating that no payment services are currently available. 

#### Scenario 2: Disabled Service 

- Given a biller service has been disabled by an admin, 

- When a customer requests the available services, 

- Then the system excludes the disabled service from the list of payment options. 

### US-08: Bill Inquiry 

Priority: Must  |  User Story: 

As a customer, I want to check my bill details and the total amount I need to pay so that I can review the charges before confirming a payment. 

#### Acceptance Criteria: 

- Given a customer selects an active biller and provides valid account information, 

- When the customer requests a bill inquiry, 

- Then the system retrieves the bill information and displays the amount due, service fee, and total payment amount. 

#### Exceptional Scenarios: 

#### Scenario 1: Invalid Account Information 

- Given a customer enters an invalid meter number or other required identifier, 

- When the customer requests a bill inquiry, 

- Then the system rejects the inquiry or displays the biller's error response in a clear and understandable way. 

Page 7 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Biller Unavailable 

- Given the selected biller's service is unavailable, 

- When the customer attempts to check a bill, 

- Then the system informs the customer that the inquiry could not be completed and does not display an unverified amount as confirmed. 

#### Scenario 3: No Outstanding Bill 

- Given the biller confirms that the customer has no outstanding amount, 

- When the inquiry result is received, 

- Then the system informs the customer that there is no bill currently due. 

### US-09: Pay a Bill Using the Wallet 

Priority: Must  |  User Story: 

As a customer, I want to pay my bills using my PayLink wallet so that I can complete payments without visiting a payment office. 

#### Acceptance Criteria: 

- Given a customer has sufficient available funds, passes the required payment checks, and has reviewed the bill details and total amount, 

- When the customer confirms the payment, 

- Then the system reserves the required amount, sends the payment to the selected biller, and records the transaction. 

- Given the biller confirms that the payment was successful, 

- When the system receives the confirmation, 

- Then the payment is marked as Completed, the held funds are settled, and the customer receives a payment confirmation. 

#### Exceptional Scenarios: 

#### Scenario 1: Insufficient Wallet Balance 

- Given a customer's available wallet balance is less than the total payment amount, 

- When the customer attempts to pay the bill, 

- Then the system rejects the payment and displays a message explaining that the balance is insufficient. 

Page 8 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Payment Rejected by the Biller 

- Given the customer's funds have been held and the payment request has been sent, 

- When the biller refuses the payment, 

- Then the system marks the payment as Failed, releases the held funds, and records the payment as Refunded after the release is completed. 

#### Scenario 3: Biller Response Timeout 

- Given the payment has been sent to a live biller, 

- When no response is received within the configured 10-second timeout, 

- Then the system marks the payment as Unknown, keeps the funds held, and informs the customer that the payment is still being processed. 

### US-10: Prevent Duplicate Payments 

Priority: Must  |  User Story: 

As a customer, I want PayLink to recognize repeated payment requests so that I am not charged more than once for the same payment. 

#### Acceptance Criteria: 

- Given a payment request has already been received with a specific idempotency key, 

- When the customer submits the same payment request again using that key, 

- Then the system returns the original payment result without creating another payment or charging the wallet again. 

#### Exceptional Scenarios: 

#### Scenario 1: Repeated Request While Payment Is Processing 

- Given a payment has already been initiated and is still being processed, 

- When another request arrives with the same idempotency key, 

- Then the system identifies the existing payment and returns its current status without starting a new payment. 

#### Scenario 2: Same Key Used for Different Payment Details 

- Given an idempotency key has already been associated with a payment request, 

- When the same key is submitted with different payment information, 

- Then the system rejects the conflicting request and does not create another payment. 

Page 9 of 25 

PayLink — Phase 1 Requirements Pack 

### US-11: Payment Status Management 

Priority: Must  |  User Story: 

As a customer, I want my payment status to be updated correctly throughout the payment process so that I can track its progress and know whether it was successful, failed, or is still being processed. 

#### Acceptance Criteria: 

- Given a customer initiates a payment, 

- When the payment moves through its processing stages, 

- Then the system updates its status according to the allowed payment life cycle: Initiated, FundsHeld, Sent-To-Biller, Completed, Rejected, Failed, Unknown, or Refunded. 

- Given a payment is in a particular state, 

- When an event requires a status change, 

- Then the system allows the change only if it follows one of the defined state transitions. 

#### Exceptional Scenarios: 

Scenario 1: Invalid Status Transition 

- Given a payment is in a state that does not allow the requested transition, 

- When the system attempts to change its status, 

- Then the system rejects the transition and keeps the current status unchanged. 

#### Scenario 2: Changing a Final Payment Status 

Given a payment has reached Completed, Rejected, or Refunded, 

- When another process attempts to change its status, 

Then the system prevents the change because these are final states. 

### US-12: Hold and Release Wallet Funds 

Priority: Must  |  User Story: 

As a customer, I want the required payment amount to be reserved in my wallet until the payment is confirmed so that my money is handled safely if the transaction succeeds or fails. 

#### Acceptance Criteria: 

Page 10 of 25 

PayLink — Phase 1 Requirements Pack 

- Given a customer has sufficient available balance and passes the required payment checks, When the customer initiates a valid payment, 

- Then the system transfers the total payment amount from the available balance to the held balance before contacting the biller. 

- Given a payment has been confirmed as successful, 

- When the system completes the transaction, 

- Then the held amount is settled as a final charge and the wallet records are updated. 

#### Exceptional Scenarios: 

#### Scenario 1: Insufficient Available Balance 

- Given a customer's available balance is less than the total payment amount, 

- When the system attempts to reserve the funds, 

- Then the payment is rejected and no funds are held. 

#### Scenario 2: Payment Failure 

- Given funds have already been held for a payment, 

- When the biller confirms that the payment has failed, 

- Then the system releases the held amount to the available balance and records the refund. 

### US-13: Handle Payment Timeouts and Retries 

Related-Requirement: FR-13  |  Priority: Must  |  User Story: 

As a customer, I want PayLink to handle delayed payment responses safely so that my money remains protected while the system checks whether the payment was completed. 

#### Acceptance Criteria: 

- Given a payment request has been sent to a live biller, 

- When the biller does not respond within 10 seconds, 

- Then the system marks the payment as Unknown and keeps the payment amount held. 

- Given a payment remains Unknown, 

- When the configured retry times are reached, 

- Then the system re-queries the payment status up to three times, after 1, 5, and 15 minutes. Given the payment remains unresolved after all three retries, 

- When no confirmed result is available, 

- Then the system keeps the payment pending for reconciliation without automatically refunding the money. 

#### Exceptional Scenarios: 

Page 11 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 1: Payment Confirmed During Retry 

- Given a payment is Unknown, 

- When a retry confirms that the biller successfully processed the payment, 

- Then the system marks the payment as Completed and settles the held funds. 

#### Scenario 2: Payment Confirmed as Failed 

- Given a payment is Unknown, 

- When a reliable biller response confirms that the payment failed, 

- Then the system marks the payment as Failed and releases the held funds, completing the refund process. 

### US-14: Handle Asynchronous Payment Callbacks 

Priority: Must  |  User Story: 

As a customer, I want PayLink to update my mobile payment status when the mobile operator sends its final confirmation so that I can know the actual result even if the payment was not completed immediately. 

#### Acceptance Criteria: 

- Given TopUpNet has accepted a payment and is processing it asynchronously, 

- When TopUpNet sends a valid callback confirming success, 

- Then the system marks the payment as Completed and finalizes the transaction once. 

- Given TopUpNet sends a valid callback confirming failure, 

- When the system processes the callback, 

- Then the payment is marked as Failed and its held funds are released. 

#### Exceptional Scenarios: 

#### Scenario 1: Duplicate Callback 

- Given a callback has already been processed, 

- When TopUpNet sends the same callback again, 

- Then the system ignores the duplicate, logs the event, and avoids repeating any financial operations. 

Page 12 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Invalid Callback 

- Given the system receives a callback with invalid information or an unknown payment reference, 

- When it attempts to process the callback, 

- Then the system rejects the callback and records the issue without changing any payment or wallet balances. 

### US-15: Support Different Biller Integrations 

Priority: Must  |  User Story: 

As a customer, I want to pay bills from different service providers through PayLink so that I can manage multiple types of payments using the same platform. 

#### Acceptance Criteria: 

- Given a customer selects a supported biller, 

- When the customer requests a bill inquiry or initiates a payment, 

- Then the system communicates with the selected biller using its required protocol and data format. 

- Given PayLink supports ElectroCo, AquaCo, and TopUpNet, 

- When a payment is processed through any of these billers, 

- Then the system handles the biller's response correctly without requiring the customer to understand the differences between their integrations. 

#### Exceptional Scenarios: 

#### Scenario 1: Biller Communication Failure 

- Given a selected biller is unavailable or experiences a communication failure, 

- When PayLink attempts to communicate with it, 

- Then the system handles the failure safely and prevents it from affecting payments to other billers. 

#### Scenario 2: Unexpected Biller Response 

- Given a biller returns an unexpected response format or error code, 

- When PayLink processes the response, 

- Then the system records the error and handles the affected operation without incorrectly confirming a payment. 

### US-16: Calculate Service Fees and Promotions 

Priority: Must  |  User Story: 

Page 13 of 25 

PayLink — Phase 1 Requirements Pack 

As a customer, I want PayLink to calculate service fees correctly and apply available promotions so that I know the total amount I will be charged before making a payment. 

#### Acceptance Criteria: 

- Given a customer requests a payment for electricity or water, 

- When the system calculates the service fee, 

- Then it applies a fixed fee of 2.50 EGP. 

- Given a customer requests a mobile top-up, 

- When the system calculates the service fee, 

- Then it applies 1.5% of the payment amount, with a minimum fee of 1 EGP. 

- Given a customer requests an internet bill payment, 

- When the system calculates the fee, 

- Then it applies 2 EGP for amounts up to 200 EGP and 4 EGP for amounts above 200 EGP. 

- Given an active promotion applies to the selected biller, 

- When the system calculates the fee during the configured promotion period, 

- Then the service fee is set to zero. 

#### Exceptional Scenarios: 

#### Scenario 1: Promotion Not Applicable 

- Given a promotion has expired, has not started, or applies to another biller, 

- When the system calculates the payment fee, 

- Then the normal fee rules are applied. 

#### Scenario 2: Missing or Invalid Fee Configuration 

- Given the fee configuration for a payment service is missing or invalid, 

- When the system attempts to calculate the payment total, 

- Then it prevents the payment from proceeding with an unverified fee and reports the configuration problem. 

### US-17: Agent Payments and Commissions 

#### Priority: Should  |  User Story: 

As a PayLink agent, I want to make bill payments on behalf of customers and receive commissions so that I can provide payment services and earn money from successful transactions. 

#### Acceptance Criteria: 

Page 14 of 25 

PayLink — Phase 1 Requirements Pack 

- Given an authorized agent initiates a valid payment on behalf of a customer, 

- When the biller confirms the payment as successful, 

- Then the system completes the payment and calculates the agent's commission as 40% of the service fee. 

- Given the agent's commission has been calculated, 

- When the payment is successfully completed, 

- Then the system credits the commission to the agent's wallet and records the transaction. 

#### Exceptional Scenarios: 

#### Scenario 1: Payment Failure 

- Given an agent initiates a payment on behalf of a customer, 

- When the payment fails, 

- Then the system does not award a commission for the failed payment. 

#### Scenario 2: Duplicate Commission Processing 

Given the commission for a completed payment has already been credited, 

- When the same completion event is processed again, 

- Then the system prevents the commission from being credited a second time. 

### US-18: Enforce Payment Limits 

Priority: Must  |  User Story: 

As a customer, I want PayLink to check payment limits before processing my transactions so that I can make payments within the allowed limits for my account. 

#### Acceptance Criteria: 

- Given a customer submits a payment within the allowed single-payment and daily limits, 

- When the system validates the payment amount and account verification level, 

- Then the payment is allowed to proceed to the remaining required checks. 

- Given a customer has a basic account, 

- When the system checks the daily payment limit, 

- Then it applies the configured limit of 5,000 EGP. 

- Given a customer has a verified account, 

- When the system checks the daily payment limit, 

- Then it applies the configured limit of 30,000 EGP. 

#### Exceptional Scenarios: 

Page 15 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 1: Single-Payment Limit Exceeded 

- Given a customer requests a payment below 5 EGP or above 10,000 EGP, 

- When the system validates the payment amount, 

- Then it rejects the payment and displays a clear reason. 

#### Scenario 2: Daily Payment Limit Exceeded 

- Given a customer's new payment would exceed the daily limit for their verification level, 

- When the system checks the daily total, 

- Then it rejects the payment and informs the customer that the daily limit would be exceeded. 

### US-19: Detect Excessive Payment Activity 

Priority: Should  |  User Story: 

As a customer, I want PayLink to detect unusual payment activity on my account so that repeated payment attempts can be restricted when they exceed the allowed frequency. 

#### Acceptance Criteria: 

- Given a customer makes no more than five qualifying payments within 60 seconds, 

- When the system checks the payment frequency, 

- Then the customer is allowed to continue if all other payment conditions are satisfied. 

- Given an account exceeds five qualifying payments within 60 seconds, 

- When the system detects the excessive activity, 

- Then the account is blocked from making payments for 10 minutes. 

#### Exceptional Scenarios: 

#### Scenario 1: Payment Attempt During Temporary Block 

- Given a customer's account is temporarily blocked by the velocity rule, 

- When the customer attempts another payment before the block expires, 

- Then the system rejects the attempt and informs the customer that the account is temporarily restricted. 

#### Scenario 2: Temporary Block Expires 

- Given the account's 10-minute velocity block has expired, 

- When the customer attempts another valid payment, 

- Then the system no longer applies the expired block and allows the payment to proceed through normal validation. 

Page 16 of 25 

PayLink — Phase 1 Requirements Pack 

### US-20: Search and View Payment History 

Priority: Must  |  User Story: 

As a support employee, I want to search for a payment using its reference number and view its complete history so that I can investigate customer complaints and understand what happened during the transaction. 

#### Acceptance Criteria: 

- Given an authorized support employee has a valid payment reference, 

- When the employee searches for the payment, 

- Then the system displays its details, current status, and recorded payment history. 

- Given a payment has gone through multiple processing stages, 

- When the support employee views its history, 

- Then the system displays the recorded status changes and relevant transaction details in chronological order. 

#### Exceptional Scenarios: 

Scenario 1: Payment Not Found 

- Given a support employee enters a payment reference that does not exist, 

- When the system performs the search, 

- Then it displays a clear message indicating that no matching payment was found. 

#### Scenario 2: Unauthorized Access 

- Given a user does not have permission to access support operations, 

- When the user attempts to search payment records, 

- Then the system denies access and does not reveal payment information. 

### US-21: Block and Unblock Customer Accounts 

Priority: Should  |  User Story: 

As a support employee, I want to block or unblock customer accounts so that I can restrict suspicious accounts and restore access when the issue has been resolved. 

#### Acceptance Criteria: 

Page 17 of 25 

PayLink — Phase 1 Requirements Pack 

- Given an authorized support employee identifies an account that needs to be restricted, 

- When the employee blocks the account, 

- Then the system updates the account status and prevents new payments from being initiated. 

- Given a previously blocked account has been cleared for use, 

- When an authorized support employee unblocks it, 

- Then the system removes the manual block and allows payments to proceed through the normal checks. 

#### Exceptional Scenarios: 

#### Scenario 1: Account Not Found 

- Given a support employee provides an account identifier that does not exist, 

- When the employee attempts to block or unblock the account, 

- Then the system rejects the request and displays an appropriate message. 

#### Scenario 2: Unauthorized Account Management 

- Given a user does not have permission to manage account restrictions, 

- When the user attempts to block or unblock an account, 

- Then the system denies the action and leaves the account unchanged. 

### US-22: Receive Payment Notifications 

Priority: Must  |  User Story: 

As a customer, I want to receive notifications when my payment is completed or fails so that I can stay informed about my transactions without having to check the system manually. 

#### Acceptance Criteria: 

- Given a customer's payment has been successfully completed, 

- When the system records the successful payment, 

- Then it triggers an SMS and push notification informing the customer of the successful transaction. 

- Given a customer's payment has failed, 

- When the failure is confirmed, 

- Then the system triggers an SMS and push notification explaining the payment result. 

#### Exceptional Scenarios: 

Page 18 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 1: Notification Provider Unavailable 

- Given a payment is completed or fails, 

- When the notification provider is unavailable, 

- Then the system records the notification delivery failure and handles it separately without changing the payment result. 

#### Scenario 2: Notification Delivery Delayed 

- Given a payment notification has been created but has not yet been delivered, 

- When the customer checks the payment status, 

- Then the system continues to display the correct payment status regardless of the notification delay. 

### US-23: Retry Failed Notifications 

Priority: Should  |  User Story: 

As a customer, I want PayLink to retry failed payment notifications so that temporary delivery problems do not prevent me from receiving important updates. 

#### Acceptance Criteria: 

- Given a payment notification could not be delivered, 

- When the notification delivery fails, 

- Then the system schedules the notification for retry. 

- Given a notification has failed to reach the customer, 

- When the configured retry process runs, 

- Then the system attempts delivery up to three retries. 

- Given the notification is delivered during one of the retries, 

- When the provider confirms successful delivery, 

- Then the system records the notification as delivered and stops retrying. 

#### Exceptional Scenarios: 

#### Scenario 1: All Retry Attempts Fail 

- Given a notification has failed during its initial delivery and all three retry attempts, 

- When the final retry also fails, 

- Then the system marks the notification as Undelivered and records the failure. 

Page 19 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Duplicate Retry Execution 

- Given a notification has already been successfully delivered, 

- When a previously scheduled retry attempts to run, 

- Then the system prevents unnecessary redelivery and keeps the notification marked as delivered. 

### US-24: Manage Fees and Limits Through Configuration 

Priority: Should  |  User Story: 

As an admin, I want to update service fees and payment limits through system configuration so that PayLink can adjust its business rules without needing to redeploy the application. 

#### Acceptance Criteria: 

- Given an authorized admin accesses the system's fee and limit settings, 

- When the admin submits valid updated values, 

- Then the system saves the new configuration and applies it to subsequent relevant operations without redeployment. 

#### Exceptional Scenarios: 

Scenario 1: Invalid Configuration Values 

- Given an admin enters an invalid fee or payment limit, 

- When the admin attempts to save the changes, 

- Then the system rejects the update and keeps the previous configuration unchanged. 

#### Scenario 2: Unauthorized Configuration Change 

- Given a user does not have admin permissions, 

- When the user attempts to modify fees or limits, 

- Then the system denies the request and preserves the existing configuration. 

### US-25: Maintain Audit Logs 

Priority: Must  |  User Story: 

As a support employee, I want PayLink to keep a record of financial transactions and administrative actions so that important activities can be traced and investigated when needed. 

Acceptance Criteria: 

Page 20 of 25 

PayLink — Phase 1 Requirements Pack 

- Given a money movement occurs in the system, 

- When the financial operation is recorded, 

- Then the system creates an audit record containing the responsible actor or process, timestamp, action, and reason. 

- Given an admin performs an action that changes system information or settings, 

- When the action is successfully processed, 

- Then the system records the administrative activity in the audit log. 

#### Exceptional Scenarios: 

#### Scenario 1: Audit Logging Failure 

- Given a financial operation requires an audit record, 

- When the system cannot persist the required audit information, 

- Then it prevents the financial operation from being committed without its required audit record. 

#### Scenario 2: Unauthorized Audit Log Access 

- Given a user does not have permission to view audit records, 

- When the user attempts to access the audit log, 

- Then the system denies access and protects the recorded information. 

### US-26: Generate Daily Reconciliation Reports 

Priority: Should  |  User Story: 

As a support employee, I want PayLink to compare its payment records with billers' settlement files so that missing, incorrect, or inconsistent payments can be identified and investigated. 

#### Acceptance Criteria: 

- Given a biller provides a valid daily settlement file, 

- When the system processes the file, 

- Then it compares the biller's payment records with PayLink's internal payment records and generates a reconciliation report. 

- Given the records match correctly, 

- When the reconciliation process finishes, 

- Then the matching transactions are identified as reconciled. 

#### Exceptional Scenarios: 

Page 21 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 1: Payment Record Mismatch 

- Given a settlement file contains a payment that PayLink records as Failed, 

- When the system compares the records, 

- Then it flags the difference in the reconciliation report for support review without silently changing the payment status. 

#### Scenario 2: Invalid Settlement File 

- Given a settlement file is missing required information or contains invalid data, 

- When PayLink attempts to process the file, 

- Then the system records the problem and reports that reconciliation could not be completed for the affected records. 

### US-27: Request a Refund for a Completed Payment 

Priority: Could  |  User Story: 

As a customer, I want to request a refund for a completed payment so that I can ask for my money back when there is a valid reason for reversing the transaction. 

#### Acceptance Criteria: 

- Given a customer has a completed payment, 

- When the customer submits a refund request for that payment, 

- Then the system records the request and makes it available for support review. 

- Given a support employee has reviewed a valid refund request, 

- When the employee approves the refund, 

- Then the system processes the refund according to the approved refund rules and records the related financial movements. 

#### Exceptional Scenarios: 

#### Scenario 1: Refund Request Rejected 

- Given a customer submits a refund request that does not meet the required conditions, 

- When a support employee rejects the request, 

- Then the system records the rejection and does not return any money. 

Page 22 of 25 

PayLink — Phase 1 Requirements Pack 

#### Scenario 2: Duplicate Refund Request 

- Given a completed payment already has a processed refund, 

- When another refund request is submitted for the same amount and transaction, 

- Then the system prevents an unintended duplicate refund and informs the customer that the payment has already been refunded. 

### US-28: View Daily Payment Statistics 

#### Priority: Could  |  User Story: 

As an admin, I want to view daily payment statistics so that I can monitor PayLink's financial activity and identify services that may be experiencing problems. 

#### Acceptance Criteria: 

- Given an authorized admin accesses the daily statistics, 

- When the admin selects a reporting day, 

- Then the system displays the daily payment totals, service fees earned, agent commissions paid, and failures grouped by biller. 

#### Exceptional Scenarios: 

#### Scenario 1: No Transactions for the Selected Day 

- Given no transactions were recorded on the selected day, 

- When the admin requests the statistics, 

- Then the system displays zero totals and indicates that no payment activity was recorded. 

#### Scenario 2: Unauthorized Access 

- Given a user does not have permission to view administrative reports, 

- When the user attempts to access the daily statistics, 

- Then the system denies access and does not reveal the financial information. 

## 3.3 Non-Functional Requirements (NFRs) 

Non-functional requirements describe how well the system should work, rather than what features it provides. 

For PayLink, the six required quality attributes are: 

Page 23 of 25 

PayLink — Phase 1 Requirements Pack 

|ID|Quality<br>attribute|Non-functional requirement|How to measure it|
|---|---|---|---|
|NFR-<br>01|Correctness|The system must prevent duplicate<br>charges and negative wallet balances,<br>even when duplicate or simultaneous<br>payment requests occur.|Run duplicate-request and<br>concurrent-payment tests. The<br>expected result iszero double<br>charges and zero negative<br>balances.|
|NFR-<br>02|Performance|The system must support at least100<br>payments per second continuously for<br>1 minutewhen tested against mock<br>billers.|Run a load test and verify that the<br>system sustains 100 payments per<br>second for 60 seconds.|
|NFR-<br>03|Resilience|An outage or failure in one biller must not<br>prevent customers from making payments<br>through other billers.|Simulate one biller going offline and<br>verify that payments to the other<br>billers still work.|
|NFR-<br>04|Modifiability|Adding a new biller must require changes<br>only to the Biller Integration module and<br>its configuration. Existing modules must<br>remain unchanged.|Add a new mock biller and inspect<br>the code changes to verify that no<br>other modules were modified.|
|NFR-<br>05|Auditability|Every money movement must have an<br>audit record containing who performed it,<br>when it happened, and why it happened.|Check the audit records and verify<br>that100% of money movements<br>have the required information.|
|NFR-<br>06|Testability|The domain logic must achieve at least<br>70% line coverage, measured through<br>the CI pipeline.|Generate a test coverage report in<br>GitHub Actions and verify that<br>domain logic coverage is at least<br>70%.|



### Understanding each one (so you can explain it to your TA) 

1. Correctness: Money must always be handled accurately. For example, if Sara clicks Pay twice because the internet is slow, she must only be charged once. 

2. Performance: The system should handle a large number of payments without becoming too slow. The required target is 100 payments every second for one minute. 

3. Resilience: If ElectroCo goes offline, customers should still be able to pay their water or mobile bills through other working billers. 

4. Modifiability: If the company adds a new electricity or water provider, we should only need to add its integration and configuration. We shouldn't have to rewrite the payment-processing or wallet modules. 

5. Auditability: Every time money moves, the system must record who caused the movement, when it happened, and why. This helps investigate mistakes and suspicious transactions. 

6. Testability: We need enough automated tests to cover at least 70% of the domain logic. This helps us detect bugs before deploying changes. 

Page 24 of 25 

PayLink — Phase 1 Requirements Pack 

## 4. Ambiguities & Resolved Decisions 

During requirements analysis, the following ambiguities were identified and resolved: 

1. Refunding a Completed payment ( US-27 ) vs. final state rules (Section 2.5) 

   - Ambiguity: Section 2.5 marks Completed as a final state, whereas US-27 ( Could ) allows a customer to request a refund of a completed payment and support to approve it. It is unclear whether approving a US-27 refund changes the original Payment status or creates a separate refund record/adjustment. 

   - Decision: Keep the core Payment lifecycle states ( Completed , Rejected , Refunded ) aligned with Section 2.5 for payment execution/failed-payment hold releases, and track US-27 customer refund requests via a RefundRequest workflow with explicit ledger entries when approved rather than mutating a Completed payment's lifecycle outside its rules. 

2. Promotion precedence and rounding when multiple fee rules or discounts apply ( US-16 , Section 2.6) 

   - Ambiguity: When a biller has an active promotion (0 fee) or when mobile top-up (1.5%, min 1 EGP) or tiered internet fees are computed, rounding rules ( BigDecimal half-up vs. floor) and promotion scope (service-level vs. biller-level) need an explicit rule. 

   - Decision: Use exact BigDecimal arithmetic with HALF_UP rounding to 2 decimal places (piasters/cents), and apply a zero fee when an active promotion covers the biller at the time of calculation. 

3. Which payments count toward the 5-in-60-seconds velocity rule ( US-19 , Section 2.6) 

   - Ambiguity: The brief specifies "More than 5 payments in 60 seconds from one account is blocked for 10 minutes," without clarifying whether rejected/failed attempts or only initiated/held payments count toward the threshold. 

   - Decision: Count payment attempts initiated for the customer account within the rolling 60-second window; once the threshold is exceeded, block new payment initiations for 10 minutes. 

4. Reconciling a Failed payment in PayLink that appears in a biller's settlement file ( US-26 , Hard Case #7) 

   - Ambiguity: When a settlement file includes a payment PayLink marked as Failed (or already refunded), should reconciliation automatically flip the payment to Completed and re-charge the wallet? 

   - Decision: Do not automatically alter payment status or wallet balances during batch reconciliation; flag the mismatch in the daily reconciliation report ( discrepancyFlag ) so support can investigate and resolve it deliberately. 

Page 25 of 25 

PayLink — Phase 1 Requirements Pack 

