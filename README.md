# JetBrains Data Engineering & Analysis Test Assignment Instructions

This test assignment will familiarize you with JetBrains Data Engineering & Analysis daily tasks. Also, it is designed to make you aware of our database structure. Both tasks are real business cases that our team has solved. The database structure was reduced, nevertheless, table and column names are identical. Some sensitive facts were changed, and data were randomly generated to protect our internal information.

Feel free to use any software, programming language, database, and approach you prefer. Send us your solution along with all steps (source code and files) via email - if the attachment is too big, feel free to use GDrive or a similar service to share your files. We will provide our detailed feedback by email.

The most important is the correctness and fullness of the answer. In addition, we will evaluate the following aspects:
* the way how the test assignment was solved
* code readability
* used technology

## Issue: Data quality – the difference between NetSuite ERP and payment gateway
### Business description
JetBrains company provides different payment methods to customers. The most convenient way is an online card payment via the payment gateway Adyen. The great advantage of online payment is speed, the software license key can be activated and used immediately after the payment.

According to accounting principles and rules, we must properly and fully book all transactions. In our case, it means processing several CSV settlement files every month. Settlement processing is fully automated now, but previous CSV files were processed manually by an external tool. Unfortunately, there were several unknown and not logged errors during settlement processing. As a result, there are differences between our accounting software NetSuite, and settlement reports, which must be identified and fixed asap.

The accounting department provided an overall comparison by a batch number and a merchant account. 

|Merchant Account|Batch Number|NetSuite|Payment Gateway|Difference|
| ------------- | ------ | ------ | ------ | ------ |
|JetBrainsAmericasUSD||11,923,212|0|11,923,212|
|JetBrainsAmericasUSD|350|4,934,528|4,934,528|0|
|JetBrainsAmericasUSD|351|0|6,035,690|-6,035,690|
|JetBrainsAmericasUSD|352|5,943,286|5,943,286|0|
|JetBrainsAmericasUSD|353|0|5,887,522|-5,887,522|
|JetBrainsAmericasUSD|354|4,058,426|4,058,426|0|
|JetBrainsEUR|350|6,109,910|6,109,910|0|
|JetBrainsEUR|351|7,424,453|7,424,453|0|
|JetBrainsEUR|352|7,243,839|7,279,531|-35,692|
|JetBrainsEUR|353|7,142,144|7,142,144|0|
|JetBrainsEUR|354|4,929,912|4,924,707|5,205|
|JetBrainsGBP|350|503,614|503,614|0|
|JetBrainsGBP|351|0|598,793|-598,793|
|JetBrainsGBP|352|623,783|623,783|0|
|JetBrainsGBP|353|589,691|589,691|0|
|JetBrainsGBP|354|429,932|429,932|0|
|JetBrainsUSD|350|1,052,225|1,052,225|0|
|JetBrainsUSD|351|1,265,153|1,265,153|0|
|JetBrainsUSD|352|1,194,395|1,194,395|0|
|JetBrainsUSD|353|1,217,387|1,217,387|0|
|JetBrainsUSD|354|848,437|848,437|0|

Column *NetSuite* – a sum of all Payments and Customer Deposits foreign amounts on accounts:
* 315700 JBCZ: Receivables against ADYEN-EUR
* 315710 JBCZ: Receivables against ADYEN-USD
* 315720 JBCZ: Receivables against ADYEN-GBP
* 315800 JBA: Receivable from Adyen - USD
* 548201 Other operating costs

Column *Payment gateway* – a sum of Adyen settlement overview, equal to the content of CSV settlement files.
### Task
Analyze and provide a list of all differences on transaction level between NetSuite and payment gateway. Do not forget to compare all accounting-relevant columns.

### Technical information
CSV settlement files are stored in the settlement folder.

All relevant data is stored on SQL Server, database `dea`, schema `netsuite`.
