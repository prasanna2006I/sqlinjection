# Name: Hariharan M
# Reg.no: 212224100019
# EX 8
# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
<img width="1658" height="853" alt="437691967-12e11cd7-8c9c-45fb-9596-322abfc9016d" src="https://github.com/user-attachments/assets/ab0fcf22-8a12-4517-b73a-bb205643495e" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
<img width="1918" height="870" alt="437692086-bed9767b-5b11-41ba-9238-9a51e67ac4f4" src="https://github.com/user-attachments/assets/7768bb92-6001-4df0-8813-5feeb3202ffa" />

Click on the menu Login/Register and register for an account
<img width="1919" height="871" alt="437692090-34234ec5-55eb-4f58-b60d-bc8482009998" src="https://github.com/user-attachments/assets/23e591cf-89e1-492d-9cd2-b1e9900436f2" />

Click on the link “Please register here”
<img width="1918" height="868" alt="437692102-57157003-af0a-46f9-a49d-061d4ca8c946" src="https://github.com/user-attachments/assets/794a39e8-def3-4d9e-84ee-f7dd73cb478e" />

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
<img width="1919" height="848" alt="437692123-923055d7-a6a5-4c40-9530-12dcb9699afb" src="https://github.com/user-attachments/assets/f9b38b7e-3dc9-4acd-a618-a7ad9f61d0f0" />

Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”
After logging out, Now choose the menu as shown below:
<img width="1919" height="868" alt="437692171-e47b1a73-be7a-4c7c-84ca-dd1caa9eeaa2" src="https://github.com/user-attachments/assets/9f775e94-a269-4dca-a23e-243cc3599706" />
<img width="1655" height="854" alt="437692189-04d34c6f-665b-468f-9791-44ff11ac6b27" src="https://github.com/user-attachments/assets/b79f83d5-56d2-48d7-89b0-82ee0fed4914" />

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
<img width="1822" height="861" alt="437692212-afdbb2b3-2ed7-4373-b179-baaf1f436df5" src="https://github.com/user-attachments/assets/5ac7d631-e9f4-408c-b194-26689e331238" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
<img width="1917" height="395" alt="437692439-0b840f63-9cd1-4449-bbd7-46d6235e4394" src="https://github.com/user-attachments/assets/314fbc62-2fb8-4199-bd49-88a76e983e18" />

The browser url of this info page need to be modified with the url as below:
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
<img width="1919" height="868" alt="437692369-5a37df72-1140-4dea-9d7f-da1322803059" src="https://github.com/user-attachments/assets/b6e625d4-004e-4ef1-b175-6b99e418bef8" />

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.
Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
<img width="1884" height="867" alt="437692356-620d8d2b-bf26-45ac-981c-c09261906dff" src="https://github.com/user-attachments/assets/587c841c-9762-4b25-8675-36949eb99510" />

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
