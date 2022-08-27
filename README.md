# Finals-BankAccount
Final exam for the Introduction to Database course. Demonstrates ability in using SELECT, FROM, WHERE, JOIN, GROUP BY, and COUNT.

## Table of Contents  
  * [Case](#case)
  * [Normalization](#normalization)
  * [ERD](#erd)
  * [Solution](#solution)
  
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
  
## ERD
<p>
    <img src="https://github.com/zahraprivias/Finals-BankAccount/blob/0df58ac7e6b0671df3e387be65c76484ad2fb6da/ERD.png" width="400" height="355"/>
</p>

## Solution
1. All account details of Surabaya branch  
   ```sql
   SELECT  
     a.CustomerCIF, c.CustomerName, a.CardNumber, a.DateOpen, a.DateClose, a.CurrentBalance, ad.Nisbah, ad.ProfitDisAccNo, ad.PrincipalDisAccNo, ad.DepositTerm, ad.ProfitDistributionTerm, ad.ARO, ad.IslamicContract, ad.Zakat  
   FROM  
     Branch b JOIN Customer c ON b.BranchID = c.BranchID JOIN  
     Account a ON c.CustomerCIF = a.CustomerCIF JOIN  
     AccountDetail ad ON a.CardNumber = ad.CardNumber  
   WHERE  
     b.BranchAddress LIKE 'Surabaya'
   ```
2. CIF and name of customer who has more than three accounts  
   ```sql
   SELECT
     c.CustomerCIF, c.CustomerName,  
     [Account] = COUNT(a.CustomerCIF)
   FROM
     Customer c JOIN Account a ON c.CustomerCIF = a.CustomerCIF
   GROUP BY
     c.CustomerCIF, c.CustomerName
   HAVING
     COUNT(a.CustomerCIF) > 3
   ```
3. All customers exclude Jakarta branch  
   ```sql
   SELECT *
   FROM Customer
   WHERE BranchID IN(
     SELECT BranchID
     FROM Branch
     WHERE BranchAddress NOT LIKE 'Jakarta'
   )
   ```
4. All accounts of Jakarta and Tangerang branches  
   ```sql
   SELECT *
   FROM Account
   WHERE CustomerCIF IN(
     SELECT CustomerCIF
     FROM Customer
     WHERE BranchID IN(
       SELECT BranchID
       FROM Branch
       WHERE BranchID LIKE 'Jakarta' OR BranchAddress LIKE 'Tangerang'
     )
   )
   ```
