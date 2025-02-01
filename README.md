

# 📞 Call Center Performance Report - Power BI  

This Power BI report provides a comprehensive analysis of call center operations, helping managers track agent performance, call handling efficiency, and customer satisfaction.  

### Dashboard Link : https://github.com/Kaviya152/Call-Center-Performance-Report/blob/bfa79e4e0c06706153f4e0fb1c261b47d97b0f52/call%20center%20report.pbix

## Problem Statement

Call centers play a critical role in maintaining customer satisfaction and operational efficiency. However, they often encounter challenges such as high call abandonment rates, inconsistent agent performance, resource misallocation during peak hours, and low customer satisfaction due to unresolved issues.

This dashboard aims to provide actionable insights into key metrics like call volume trends, agent performance, customer satisfaction, and call handling efficiency. By addressing these challenges, the dashboard helps drive data-informed decisions to enhance overall call center performance and customer experience.

---

### Steps followed 
- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4.1 :Data Preparation: 
             - Imported dataset into Power BI  
             - Cleaned missing values and formatted columns for analysis as ,"Removing the duplicates","Checking for Null Values","Data type checking"
- Step 4.2:Renamed calls[Avg Talk Duration] as Talk Duration.
- Step 4.3:Table is renamed as Calls.                
- Step 5 : Layout colour & Design:
colour was selected based on the pwc logo .

![Image](https://github.com/user-attachments/assets/a4d797f4-cdc6-4e66-a84b-d9490856523c)
 
- Step 6 : In the report view, under the view tab, customise theme was selected.And based on the above figure my layout is designed with similar square and rectangle property,square shape is used to show 5 kpi's horizontaly in card visuals and also recatngle is for data visualizations charts with rounded edges.


- Step 7 : Since the data contains Call ID,Agents,Date,Time,Topic,Call answers,resolved,abandoned,Talk duration,Satisfaction Rating(1 to 5) thus in order to represent the Dashboard certain icons are used from www.Icons8.com.

- Step 8 : A new column "date time" is added in to the Calls table formated as date time data type.
          
- Step 18.1 : To add a column as Date Time,
        
          Date Time = [date]&[time]

- Step 9 : A table is created to add measures for calculations as "Measure_table".
      
        
        Measure_table=GENERATE(-1,1,1)


- Step 10 : new visual was added using the three ellipses in the visualizations pane in report view. 5 card visuals were added to the canvas, to representing 5 KPI'S of the data set.

  Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into  calculation.
           
  Although, by default, while calculating average, blank values are ignored.

- Step 10 : To find Total Calls     
   Following DAX expression was written for the same,

        Total Calls = DISTINCTCOUNT(Calls[Call Id]) 
   
   ->This is used to obtain the total number of calls.thus this measure is visualised by card as Call Volume.
   ![Image](https://github.com/user-attachments/assets/3b202672-ad4d-49a5-b016-f6b47177758f)

- Step 11 : To find Total Call Answered
   Following DAX expression was written for the same,
       
        Total Call Answered = CALCULATE(COUNT(Calls[Call Id]),Calls[Answered (Y/N)]="Y")

     ->this is used to do measures simple calculations in easy manner.     

- Step 12 : To find CUSTOMER SATISFACTION RATING,
Following DAX expression was written for the same,
        
        CSAT = 
           //TOTAL RATINGS//(TOTAL NO OF RATINGS * 5)*100

           VAR Totalratings = SUM(Calls[Satisfaction Rating])
           VAR Noofratings=COUNT(Calls[Satisfaction Rating])
           RETURN FORMAT(DIVIDE(Totalratings,Noofratings*5,0),"0.00%")
        
   ->This measure is represented in card visual   


- Step 13 : To find Call Resolved % 
   
    
        Call Resolved % = 
                VAR totalresolvedcalls = CALCULATE(COUNTA(Calls[Call Id]),Calls[Resolved]="Y") 
                VAR totalcalls = CALCULATE(COUNT(Calls[Call Id]),Calls[Answered (Y/N)]="Y")
                RETURN FORMAT(DIVIDE(totalresolvedcalls,totalcalls,0),"0.00%")
   
   ->this measure is visualised as card to visual the call resolved % measure. 

- Step 14 : To find Call abandoned % 
  Following DAX expression was written for the same,
        
        Call Abandonded % = 
                VAR callsnotanswered = CALCULATE(COUNT(Calls [Call Id]),Calls[Answered (Y/N)]="N")
                RETURN FORMAT(DIVIDE(callsnotanswered,[Total Calls],0),"0.00%")

    
     ->the card visual is used for call abandoned % measure            
  
- Step 15 : To find Speed Of Call
   Following DAX expression was written for the same,
        
        Speed Of Answer = 
                //total call picked/total answered
                VAR totalCallSpeedDuration=SUM(Calls[Speed Of Answer In Seconds])
                RETURN DIVIDE(totalCallSpeedDuration,[Total Call Answered],0)

     
     ->the 4th card visual is used to visual the  speed of answers (in sec) measure.         

- Step 16 : To find Average call handling time 
  Following DAX expression was written for the same,
          
        Avg Call Handling Time = 
                //totalcallduration/total answered
                VAR totalcalduration=SUM(Calls[Talk Duration])
                RETURN
                  DIVIDE(totalcalduration,[Total Call Answered],0)

      -> AS 5th card visual this is visualised as Average call handling time measure (in sec)

 ![Image](https://github.com/user-attachments/assets/4465a1a6-02e7-449d-91cc-35ea6306522f)   



- Step 17 : A Matrix Visual was added to the report design area that represents the "AGENT PERFORMANCE".
these are the measures used to show it.

   ->Agent

   ->Total callls

   ->Speed of answers
 
   ->Call abandoned %
 
   ->Call resolved %

![Image](https://github.com/user-attachments/assets/030b58b2-93b4-4433-bb19-333d1abf84a6)



- Step 18 : new columns were added for CALL VOLUME BY HOUR [LINE AREA CHART]


 for creating new columns following steps have DAX expressions ,


  - Step 18.1 : To add a column as "Hour",
        
             Hour = FORMAT(Calls[time],"HH" & ":00")      
  - Step 18.2 : new column added as "HOUR BY ORDER",

             HOUR BY ORDER = Hour(Calls[time])

       this new column is created to sort the hour column by this column.
       
       ->steps to be followed are,
       
        1) Hour -> Sort by column ->(cick) hour by order

        2) SORT BY :-  in  Call Volume chart, click sort axis as  " Hour by order".


![Image](https://github.com/user-attachments/assets/563e6cbd-d97f-42a3-86c9-b0afb36c736a)        

- Step 19 : new columns were added for CALL VOLUME BY DAY [LINE AREA CHART]        

 
 for creating new columns following steps have DAX expressions ,

  - Step 19.1 : To add a column as "Day Name",
      
             Day Name = Format(Calls[date],"Ddd")
  - Step 19.2 : To add a new column as "WeekDay Number",
             
             Weekday Number = WEEKDAY(Calls[date],2)
      //this function consider the monday number to starts from 1.

  - Step 19.3 : CALL VOLUME BY DAY CHART-
        X-axis= Day Name
        y-Axis= Total Calls        
  - Step 19.4 : sort the "DAY Name" column by Weekday Number as follows:
        
            Day Name->Sort by->Column Weekday Number then go for CALL VOLUME BY DAY chart ->sort axis (by)-> total axis .

  
![Image](https://github.com/user-attachments/assets/8ad6234e-f4e0-46f1-bbd1-c1148f9bd3f0)

In this visual the titles of x and y axis are removed.

- Step 20  :  new columns were added for COUNT OF CALLS BY SATISFACTION LEVELS [CLUSTERED BAR CHART]
- Step 20.1 : To add a column as " Satisfaction Levels ",
        
             Satisfaction Levels = SWITCH(
                     TRUE(),
                     ISBLANK(Calls[Satisfaction rating]),"Not    Served",
                     Calls[Satisfaction rating]=1,"Very Dissatisfied",
                     Calls[Satisfaction rating]=2,"Dissatisfied",
                     Calls[Satisfaction rating]=3,"Normal",
                     Calls[Satisfaction rating]=4,"satisfied",
                     Calls[Satisfaction rating]=5,"very satisfied"
             )

          
- Step 20.2 : To add a column as " Rating by order ",
        
             Rating by order = IF(ISBLANK(Calls[Satisfaction Rating]),0,Calls[Satisfaction rating])

- Step 20.3 : sort the "Satisfaction Levels" column by "Rating by order" as follows:
         Satisfaction Levels->sort by column -> Rating by order
- Step 20.4 : Create the clustered bar chart as,
        x-axis = Satisfaction Levels
        y-axis = Total Calls 

  thus sort the chart by ( sort axis -> ascending order)

  
![Image](https://github.com/user-attachments/assets/c6fb59e0-f9b5-48eb-ae51-f7d6ce08cf20)

A Clustered bar chart visual was used to "Count of calls by satisfaction " as differrent ratings.

  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating satisfaction rating,in slicers for each of the parameters mentioned above.


- Step 21 : To find Last Call,
  Following DAX expression was written for the same,

         Last Call =   MAX(Calls[Date Time])

- Step 22 : 
  
  A text box is used to to denote as " Agent Analysis" 

  Card visual is usedd for this measure to show  Last Call Recieved.
  
  ![Image](https://github.com/user-attachments/assets/d368bc45-1b62-4999-8c74-484c9b1c56e0)

- Step 23 : Creating group of four slicers for end user's analysis.
     
      //Slicer is same as filters for end users.these slicers have same property as 
      #Height = 75
      #width = 144
      # FORMAT = Dropdown 
      //THESE ARE ALIGNED AND GROUPED AS SLICERS.


    Slicers :
     
     -> Agents
        the Agents column is used.
     
     -> Topics
        the topic column is used as field.
     
     -> Month
        the "MONTH YY "is used as field here.

     -> WeekDay
        the weekday column is used as field.
    
    
    ![Image](https://github.com/user-attachments/assets/bde150db-ca84-41e3-9912-320270c2285f)


- Step 23.1 : To add a column as "Month YY",
        
             Month YY = Format(Calls[date],"Mmm YY") 
        

- Step 24 : Clear filter is used to BOOKMARK the unfiltered page view ,thus the filter image is formated to [action] on book mark.
        
        // this helps to return the unfiltered page, when the image is clicked.  

  ![Image](https://github.com/user-attachments/assets/08744de7-b05a-4a93-a271-e968967b3ca2)

- Step 25 : In the report view, under the insert tab,using image option pwc company's logo was added to the report design area.
text box is used to show the name as "call center data analysis." 


THE SNAP OF NEW MEASURES :-
     
   ![Image](https://github.com/user-attachments/assets/ab673a00-ce02-40d0-aac0-3ff740d260bd)

THE SNAP OF NEW COLUMNS :- 

  ![Image](https://github.com/user-attachments/assets/d89c5f4b-a833-4ee9-bf03-c6e0b8d6fbb7)      


 
 # Report Snapshot (Power BI DESKTOP)


![Image](https://github.com/user-attachments/assets/bb8b10c8-937c-442d-aa99-46860275a2a7)

# Insights

Got it! Let me provide the **insights observed from your dashboard** in the **format you requested**.

---

### Insights Observed from the Dashboard

---

### [1] **Call Volume**  
   - Total call volume handled: **5000 calls**.  
   - Significant call volume during specific hours (e.g., 9:00 AM–3:00 PM).  
   - Call volumes peak on **weekends**, especially **Saturday**.  

   - **Observation**: Staffing levels should be optimized to handle peak call volumes during busy hours and weekends.

---

### [2] **Customer Satisfaction Levels (CSAT)**  
   - Overall CSAT: **68.07%**.  
   - A significant proportion of customers are dissatisfied or not served.  
   - Majority of calls are resolved, but dissatisfaction highlights underlying service gaps.

   - **Observation**: Targeted measures are needed to enhance CSAT and address dissatisfaction.

---

### [3] **Agent Performance**  
   - **Best-performing agents** (e.g., Stewart and Dan) show balanced metrics of **speed of answer**, high **call resolution percentage**, and good **CSAT scores**.  
   - **Underperforming agents** (e.g., Diane) exhibit higher call abandonment rates (20.85%) and lower resolution efficiency.  

   - **Observation**: Focused training for underperforming agents and recognizing high-performing agents can improve overall performance.

---

### [4] **Call Handling Metrics**  
   - **Call Resolved Percentage**: **89.94%**.  
   - **Call Abandonment Rate**: **18.92%**, which is relatively high.  
   - Average **Speed of Answer**: **67.52 seconds**.  
   - Average **Call Handling Time**: **224.92 seconds**.  

   - **Observation**: Strategies to reduce call abandonment (e.g., reducing wait times) and improving handling times can enhance overall efficiency.

---

### [5] **Customer Satisfaction Trends**  
   - Higher customer satisfaction levels are observed among calls that are resolved faster.  
   - "Very Satisfied" and "Satisfied" customers form the majority.  
   - Dissatisfied customers are distributed across specific dissatisfaction areas.

   - **Observation**: Analyzing dissatisfaction reasons (e.g., long hold times, unresolved queries) can identify key improvement areas.

---
