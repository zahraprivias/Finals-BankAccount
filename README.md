# Finals-BankAccount
Final exam for the Introduction to Database course. Demonstrates ability in using SELECT, FROM, WHERE, JOIN, GROUP BY, and COUNT.

## Table of Contents  
- [Case] (#case)
- [Normalization] (#normalization)
- ERD
- Solution

## Case
<img src="https://github.com/zahraprivias/Finals-BankAccount/blob/d266e1faa5efc4e1cc450282ebb5726baff67fab/soal.png" alt="Image" width="490" height="320">

Write DML based on your ERD in prior question to show:  
1. All account details of Surabaya branch  
2. CIF and name of customer who has more than three accounts  
3. All customers exclude Jakarta branch  
4. All accounts of Jakarta and Tangerang branches  

## Normalization
### 3NF Normalization  
- Customer
  | **Customer**     |               |              |              |
  | ---------------- |:-------------:| :-----------:| ------------ |
  | CustomerCIF (PK) | BranchID (FK) | CustomerName | CustomerType |  
- Branch
  | **Branch**    |               |            |
  | ------------- |:-------------:| ---------- |
  | BranchID (PK) | BranchAddress | BranchType |
- Account
  | **Account**         |                    |          |           |                |
  | ------------------- |:------------------:|:--------:|:---------:| -------------- |
  | CustomerCIF (PK FK) | CardNumber (PK FK) | DateOpen | DateClose | CurrentBalance |
- AccountDetail
  | **AccountDetail** |        |                |                   |             |                        |     |                 |       |
  | ----------------- |:------:|:--------------:|:-----------------:|:-----------:|:----------------------:|:---:|:---------------:| ----- |
  | CardNumber (PK)   | Nisbah | ProfitDisAccNo | PrincipalDisAccNo | DepositTerm | ProfitDistributionTerm | ARO | IslamicContract | Zakat |
  
