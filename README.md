# Title
## Realizer 1.0 ##

# About the Project 

Realizer is a in-house web application of Hls-Global Japan which automates the process of manual Finance/Accounting related Excel calculations & manipulations. It also has a Data reporting & Data analysis features by which years of data can be analyzed. It mainly has the following modules.

1. Sales 
     - Sales Allocation
     - Sales Pivot Analysis
     - Sales Data Report
2. Cost 
     - Cost Allocation
     - Cost Pivot Analysis
3. Net-Profit 
     - Net-Profit Analysis
     - Net-Profit Pivot Analysis
4. User Master
5. Vendor Master
6. Service Master

# Technologies Used

1. Java 8
2. Spring Boot 2.0.4.RELEASE
3. Apache Tomcat 8.5 (Embedded)
3. Hibernate 5.2.8.Final
4. MySQL 5.1.6
5. HTML, Javascript, JQuery, Bootstrap, CSS

# Getting Started

Copy the project folder wherever you want & install the softwares below.

## Prerequisites

Please Install the below mentioned softwares.

1. Java 8
2. MySQL Database
3. Eclipse Neon
4. SQLyog or MySQL Workbench

** Please set System Path (Environment Variables) of JAVA_HOME, JDK bin directory , MAVEN_HOME & MAVEN bin directory once installed. **

## Project Setup

1. Go to the root directory of the project & open command line / Git bash & download all the required dependencies by running the Maven command below.

     - ** mvn eclipse:clean eclipse:eclipse **

2. Once the above process finishes, you need to install ** lombok ** dependency for Eclipse,Please go to path below in your system,
   _"C:\Users\user\.m2\repository\org\projectlombok\lombok\1.16.20"_ 

     - Open terminal & type command **java -jar lombok-1.16.20.jar**, Click on specify location button once Project lombok Installer GUI pop's up & provide Eclipse installation directory path by selecting eclipse.exe file.

Now your project is ready to be imported in Eclipse..HURRAY!!

3. Next thing you need to do is to set-up the MySQL Database.

    - Create a Database called ** hls_global ** in SQLyog or MySQL Workbench, don't forget to select character encoding as following while creating the DB.
         - ** Database charset -> utf-8 ** 
        - ** Database collation -> utf8_unicode_ci **
    - You don't need to create tables manually, Hibernate will do that thing for you once you Logged in to the Application.
    - Open the terminal & run this Maven command to start the server ** mvn clean spring-boot:run **
    - Hit this URL in ** Google Chrome ** when you're server is up __http://localhost:8080/hls_global__
    - Enter UserId - Admin & Password Admin when you redirect to the login page
    - You won't have access to other modules except ** Master Settings -> UserMaster **, for getting the access of other modules 
    go to ** Master Settings -> UserMaster ** & click on ** update ** hyperlink, In the ** Modules Accessibility ** section select 
    all modules & click on ** Update User ** button.
    - Logout once & re-login again & you should be able to access all the Modules...YaYY!!

Go back to your DB tool __SQLyog or MySQL Workbench__ & refresh the DB & you should be able to see all the tables are being created.

That's all you need to do for setting up the DB..huh Finally!!

## Data Insertion 

#### Inserting Data in DB through SQL dump file
1. This is the easiest way to insert data in the DB. Just go to the ** sample_data ** folder located in Project directory.
2. There you'll find **hls_global.sql** dump file. Just execute **hls_global.sql** script from the MYSQL tool of your choice (SQLyog or MySQL Workbench) & you'll see tables are being created & sample data have been inserted in the tables.

#### Inserting Data in DB through Application

1. Go to ** View Data -> View & Manipulate Sales Data **, initially table will be blank as there is no data available in DB.
   
     - Go to your Eclipse, I'll assume that you've imported the project..Open ** salesallocation.jsp ** & uncomment the code on 
     line no. 117 & 142, save the file & restart your server.
    - Re-Login to the application & go to the sales module again ** View Data -> View & Manipulate Sales Data **, this time you should
     see the ** Browse, Upload, Reset & Save Data buttons are being added to the form.
    - Click on the Browse File button..select ** Sales_Data_FY14-18.xlsx ** from the ** sample_data ** located in Project folder, Click on 
     ** Upload File ** button once selected the file, You'll get an alert message once the file gets uploaded, Click on ** Save Data**
     button & you should be able to see the data in table once the process finishes.
    - Please take a note that the table will always show you current ** Fiscal Year ** data, You can view the data by entering fiscal year at the
     of the URL ** E.g - http://localhost:8080/hls_global/salesallocation/FY18 **. The excel file you've uploaded has data from 
     ** FY14 - FY18** 

2. Go to ** View Data -> View Cost Data ** & you'll see the blank cost data table which is but obvious.

     - Go to ** costallocation.jsp ** & uncomment the code on line no. 82 & 100, save the file & restart 
      your server.
    - Rest all the steps you need to follow as above.

3. You can comment the code which you have uncommented because we need to upload old data into the system just once.

## Insert or Update Database schema without deleting

Using ** Liquibase ** you can add,modify & update DB schema without deleting. I've done all the required setup of liquibase by which you can modify the DB schema in future (If required). Please refer [liquibase](https://www.liquibase.org/) for more details & to know what other operations you can perform.

Below are the steps you need to follow for adding new column in an existing table.

1. create xml file with the databaseChangeLog information you can find a example i have put in ** liquibase ** 
   directory ** db-changelog-costallocationfunctionality1.0.xml  & updateDBschema.xml** 
  
     - ** db-changelog-costallocationfunctionality1.0.xml ** contains databaseChangeLog information.
    - ** updateDBschema.xml ** is a main liquibase file which calls ** db-changelog-costallocationfunctionality1.0.xml **
    when we run the command.
    -  Once you create above two files, you need to run below maven commands
      - ** mvn clean install -U **
      - ** mvn liquibase:update **
    - Once the above commands executes successfully, you should be able to see newly created fields in the table.

##### PS : Please view this file in GitHub OR Eclipse Markdown Preview Mode so as to get the proper formatting. 
