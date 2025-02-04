# Bells Bank Loan Portfolio Analysis

## Problem Statement
Bells Bank, is a fictional bank in the USA and it is one of the top prioritized bank by people for borrowing loans. The stakeholders of the bank wants to gain insights about the health of banks's loan portfolio and asks the data anlytics team to analyze the historical data to find trends and patterns. These trends and pattern will help in data-driven decision making for the stakeholders and enhance the bank's loan portfolio.

## Requirements from the Stakeholders
1. **Key Performance Indicators**
    - Total Loan Applications (Month to Date, Month over Month)
    - Total Funded Amount (Month to Date, Month over Month)
    - Total Amount Received (Month to Date, Month over Month)
    - Average Interest Rate (Month to Date, Month over Month)
    - Average Debt-to-Income Ratio (Month to Date, Month over Month)
      
2. **Good/Bad Loan KPI's**
    - Good/Bad Loan Application Percentage
    - Good/Bad Loan Total Applications
    - Good/Bad Loan Total Funded Amount
    - good/Bad Loan Total Received Amount

3. **Loan-Related Metrics and Trends**
    - Monthly Trends by Issue Date
    - Regional Trends by State
    - Loan Term Analysis
    - Employee Length Analysis
    - Loan Purpose Breakdown
    - Home Ownership Analysis

## Dataset
**financial_loan.csv** : The dataset contains columns like id, address_state, application_type emp_length, emp_title, grade, home_ownership, home_ownership, issus_date, last_credit_pull_date, last_payment_date, loan_status, next_payment_date, member_id, purpose, sub_grade, term, verification_status, annual_income, dti, installment, int_rate, loan_amount, total_acc, total_payment. 

## Dashboard/Report Live here
https://public.tableau.com/views/BankLoanDashboard_17031803847860/SUMMARY?:language=en-GB&:display_count=n&:origin=viz_share_link

## Created Dashboard/Report
### SUMMARY VIEW
![dash1](https://github.com/guddushah/Bank-Loan-Analysis-Finance_Domain-Tableau/assets/40028193/782c5888-e245-4c7c-bde2-75d6728fa2fd)

### OVERVIEW VIEW
![dash2](https://github.com/guddushah/Bank-Loan-Analysis-Finance_Domain-Tableau/assets/40028193/ebcbe014-2857-4143-855f-2fa64cf173d1)

### DETAILS VIEW
![bells3](https://github.com/guddushah/Bank-Loan-Analysis-Finance_Domain-Tableau/assets/40028193/3cfd8502-ebc4-4f94-9230-ba65e07cd449)

## Key Insights Obtained from the Dashboard
1. Total Loan Application: 38.6K | MTD: 4.3K | MoM: 6.9%
2. Total Funded Amount: $435.8M | MTD: $54.0M | MoM: 13.0%
3. Total Amount Received: $473.1M | MTD: $58.1M | MoM: 13.7%
4. Average Interest Rate: 12.0% | MTD: 12.4% | MoM: 3.5%
5. Average DTI: 13.3% | MTD: 13.7% | MoM: 2.7%
6. Total Good Loan Applications: 33.2K | Good Loan %: 86.2% | Good Loan Funded Amount: $370.2M | Good Loan Amount Received: $435.8M
7. Total Bad Loan Applications: 5.3K | Bad Loan %: 13.8% | Bad Loan Funded Amount: $65.5M | Bad Loan Amount Received: $37.3M
8. Slight linear growth in number of loan applications every following month.
9. California recorded the highest number of loan applications
10. Nearly three quarters of the loans applications were for the term period of 36 Months.
11. People with more than 10 years of work history made the maximum loan applications.
12. Mostly the purpose loan was for debt consolidation purpose whilst lowest for renewable energy.
13.  The maximum number of applications was from people staying in rented home.
14.  Highest number of loan was issued to people staying in mortgage home.

## Implementing SQL for Stakeholders requirements
1. **Total Loan Applications (Month to Date, Month over Month)**                               
    - select count(*) as Total_Loan_Applications from financial_loan;                                 

    - select count(*) as MTD_Total_Loan_Applications from financial_loan                                              
      where MONTH(issue_date) = 12 and YEAR(issue_date)=2021;                                    

    - select                                        
	(select count(*) as MTD_Total_Loan_Applications from financial_loan                            
	where MONTH(issue_date) = 12 and YEAR(issue_date)=2021) -                               
	(select count(*) as PMTD_Total_Loan_Applications from financial_loan                                   
	where MONTH(issue_date) = 11 and YEAR(issue_date)=2021) as MoM;
                      
2. **Total Funded Amount (Month to Date, Month over Month)**                                
    - select SUM(loan_amount) as Total_Funded_Amount from financial_loan;                              

    - select sum(loan_amount) as MTD_Total_Funded_Amount from financial_loan                              
      where MONTH(issue_date) = 12 and YEAR(issue_date)=2021;                             

    - select                                  
	(select sum(loan_amount) as MTD_Total_Funded_Amount from financial_loan                                                             
        where MONTH(issue_date) = 12 and YEAR(issue_date)=2021) -                                 
	(select sum(loan_amount) as PMTD_Total_Funded_Amount from financial_loan                                                                     
        where MONTH(issue_date) = 11 and YEAR(issue_date)=2021) as MoM;                                   
                         
3. **Total Amount Received (Month to Date, Month over Month)**
    - select SUM(total_payment) as Total_Amount_Received from financial_loan;                                                 

    - select sum(total_payment) as MTD_Total_Amount_Received from financial_loan                                          
      where MONTH(issue_date) = 12 and YEAR(issue_date)=2021;                                           

    - select                                  
	(select sum(total_payment) as MTD_Total_Amount_Received from financial_loan                                          
        where MONTH(issue_date) = 12 and YEAR(issue_date)=2021) -                                 
	(select sum(total_payment) as PMTD_Total_Amount_Received from financial_loan                                          
      where MONTH(issue_date) = 11 and YEAR(issue_date)=2021) as MoM;
      								      
4. **Average Interest Rate (Month to Date, Month over Month)**                                                    
    - select round(SUM(int_rate)/COUNT(int_rate)*100,2) as Average_Interest_Rate from financial_loan;                                            

    - select round(sum(int_rate)/COUNT(int_rate)*100,2) as MTD_Average_Interest_Rate from financial_loan                                          
      where MONTH(issue_date) = 12 and YEAR(issue_date)=2021;
      
    - select                                  
	(select round(sum(int_rate)/COUNT(int_rate)*100,2) as MTD_Average_Interest_Rate from financial_loan                                          
        where MONTH(issue_date) = 12 and YEAR(issue_date)=2021) -                                 
	(select round(sum(int_rate)/COUNT(int_rate)*100,2) as MTD_Average_Interest_Rate from financial_loan                                          
        where MONTH(issue_date) = 11 and YEAR(issue_date)=2021) as MoM;
                                                                                
5. **Average Debt-to-Income Ratio (Month to Date, Month over Month)**
    - select Round(AVG(dti),4)*100 as AVG_DTI from financial_loan;                                      

    - select Round(AVG(dti),4)*100 as MTD_AVG_DTI from financial_loan                                            
      where MONTH(issue_date) = 12 and YEAR(issue_date)=2021;                                      

    - select                                  
	(select Round(AVG(dti),4)*100 as MTD_AVG_DTI from financial_loan                                            
        where MONTH(issue_date) = 12 and YEAR(issue_date)=2021) -                                 
	(select Round(AVG(dti),4)*100 as MTD_AVG_DTI from financial_loan                                            
        where MONTH(issue_date) = 11 and YEAR(issue_date)=2021) as MoM;
      
6. **Good/Bad Loan Application Percentage**
- Good Loan                             
    - select                                   
	  COUNT(CASE when loan_status='Fully Paid' or loan_status='Current' then id end)*100/COUNT(id) as Good_Load_Percentage                                   
      from financial_loan;
- Bad Loan                                                                             
    - select                                            
	COUNT(CASE when loan_status='Charged Off' then id end)*100/COUNT(id) as Bad_Load_Percentage                                             
      from financial_loan;
                                                                                                           
7. **Good/Bad Loan Total Applications**
- Good Loan  																	                           
    - select COUNT(CASE when loan_status='Fully Paid' or loan_status='Current' then id end) as Total_Good_Loan						
      from financial_loan;				
- Bad Loan                                                                             
    - select COUNT(CASE when loan_status='Charged Off' then id end) as Total_Bad_Load					
      from financial_loan;
      				                                           
8. **Good/Bad Loan Total Funded Amount**
- Good Loan  	                     																                          
    - select sum(loan_amount) as Good_Loan_Funded_Amt from financial_loan                                   
      where loan_status in ('Fully Paid','Current');	 														
- Bad Loan                                                                             
    - select sum(loan_amount) as Bad_Loan_Funded_Amt from financial_loan				
      where loan_status in ('Charged Off');
      
8. **Good/Bad Loan Total Received Amount**
- Good Loan  	                     																                          
    - select sum(total_payment) as Good_Loan_Amt_Received from financial_loan							
      where loan_status in ('Fully Paid','Current');                                                  	 										
- Bad Loan                                                                             
    - select sum(total_payment) as Bad_Loan_Amt_Received from financial_loan                                          
      where loan_status in ('Charged Off');
      
9. **Loan Status Grid View**
    - select                          
	loan_status,                         
	count(id) as Total_Loan_Applications,                                  
	sum(total_payment) as Total_Amount_Received,                           
	sum(loan_amount) as Total_Loan_Amount,                               
	AVG(int_rate)*100 as Interest_Rate,                              
	AVG(dti) *100 as DTI                                    
     from financial_loan                              
     group by loan_status;

10. **Monthly Trends by Issue Date**
    - select                                 
	MONTH(issue_date) as Month_Num,                               
	DATENAME(MONTH,issue_date) as Month_Name,                                
	COUNT(id) as Total_Loan_Applications,                              
	sum(total_payment) as Total_Amount_Received,                                   
	sum(loan_amount) as Total_Loan_Amount                             
	from financial_loan                              
	group by MONTH(issue_date), DATENAME(MONTH,issue_date)                                      
	order by MONTH(issue_date);                                         
                                               			                                                
11. **Regional Trends by State**
    - select                           
	address_state,                                  
	COUNT(id) as Total_Loan_Applications,                        
	sum(total_payment) as Total_Amount_Received,                       
	sum(loan_amount) as Total_Loan_Amount                               
	from financial_loan                             
	group by address_state                            
	order by sum(loan_amount) desc;                                     

12. **Loan Term Analysis**
    - select                                  
	term,                               
	COUNT(id) as Total_Loan_Applications,                         
	sum(total_payment) as Total_Amount_Received,                              
	sum(loan_amount) as Total_Loan_Amount                       
   	from financial_loan                             
	group by term                        
	order by term desc;

13. **Employee Length Analysis**
    - select                                  
	emp_length,                          
	COUNT(id) as Total_Loan_Applications,                             
	sum(total_payment) as Total_Amount_Received,                              
	sum(loan_amount) as Total_Loan_Amount                            
   	from financial_loan                        
	group by emp_length                          
	order by emp_length;

14. **Loan Purpose Breakdown**
    - select                            
	purpose,                              
	COUNT(id) as Total_Loan_Applications,                             
	sum(total_payment) as Total_Amount_Received,                              
	sum(loan_amount) as Total_Loan_Amount                         
 	from financial_loan                              
	group by purpose                             
	order by COUNT(id)DESC;

15. **Home Ownership Analysis**
    - select                        
	home_ownership,                                
	COUNT(id) as Total_Loan_Applications,                             
	sum(total_payment) as Total_Amount_Received,                           
	sum(loan_amount) as Total_Loan_Amount                                 
 	from financial_loan                                    
	group by home_ownership                                
	order by COUNT(id)DESC;

## Created Calculated Fields in Tableau Desktop
1. Total Loan Applications
   - COUNT([Id])
2. MTD Total Loan Applications
   - COUNT(IF (DATEDIFF('month',[Issue Date],{MAX([Issue Date])}))=0                              
     THEN                         
     [Id]                         
     END)
3. MoM Total Loan Applications
   - ([MTD Total Loan Applications]-[PMTD Loan Applications])/[PMTD Loan Applications]
4. Total Funded Amount
   - SUM([Loan Amount])                    
5. MTD Total Funded Amount
   - SUM(IF (DATEDIFF('month',[Issue Date],{MAX([Issue Date])}))=0                                      
     THEN                                   
     [Loan Amount]                                  
     END)
6. MoM Total Funded Amount
   - ([MTD Total Funded Amount] - [PMTD Funded Amount])/[PMTD Funded Amount]
7. Total Amount Received
   - SUM([Total Payment])
8. MTD Total Amount Received
   - SUM(IF (DATEDIFF('month',[Issue Date],{MAX([Issue Date])}))=0
     THEN                                      
     [Total Payment]                                       
     END)
9. MoM Total Amount Received
    - ([MTD Total Received Amount]-[PMTD Total Amount Received])/[MTD Total Received Amount]
10. Average Interest Rate
    - AVG([Int Rate])
11. MTD Average Interest Rate
    - AVG(IF (DATEDIFF('month',[Issue Date],{MAX([Issue Date])}))=0                                
     THEN                            
     [Int Rate]                                 
     END)
12. MoM Average Interest Rate
    - ([MTD Average Int Rate]-[PMTD Average Int Rate])/[PMTD Average Int Rate]
13. Average DTI
    - AVG([Dti])
14. MTD Average DTI
    - AVG(IF (DATEDIFF('month',[Issue Date],{MAX([Issue Date])}))=0                          
     THEN                                                                 
     [Dti]                           
     END)
15. MoM Average DTI
    - ([MTD Average DTI]-[PMTD Average DTI])/[PMTD Average DTI]
16. Good Loan %
    - COUNT(IF [Good vs Bad Loan]='Good Loan' THEN [Id] END)/COUNT([Id])
17. Good Loan
    - COUNT(IF [Good vs Bad Loan]='Good Loan' THEN [Id] END)
18. Good Loan Funded Amount
    - SUM(IF [Good vs Bad Loan]='Good Loan' THEN [Loan Amount] END)
19. Good Loan Amount Received
    - SUM(IF [Good vs Bad Loan]='Good Loan' THEN [Total Payment] END)
20. Bad Loan %
    - COUNT(IF [Good vs Bad Loan]='Bad Loan' THEN [Id] END)/COUNT([Id])
21. Bad Loan
    - COUNT(IF [Good vs Bad Loan]='Bad Loan' THEN [Id] END)/COUNT([Id])
22. Bad Loan Funded Amount
    - SUM(IF [Good vs Bad Loan]='Bad Loan' THEN [Loan Amount] END)
23. Bad Loan Amount Received
    - SUM(IF [Good vs Bad Loan]='Bad Loan' THEN [Total Payment] END)
24. Dynamic Measures
    - IF [Select Measures]='Total Loan Applications' THEN [Total Loan Applications]                                   
      ELSEIF [Select Measures]='Total Funded Amount' THEN [Total Funded Amount]                               
      ELSEIF [Select Measures]='Total Amount Received' THEN [Total Amount Received]                                  
      END                                    

    
                                 






















