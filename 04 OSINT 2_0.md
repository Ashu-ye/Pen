# OSINT
Open source Intelligence


### Extra 
            Attacker Surfact
LFI                            || ===> Google
RFI                            ||
XSS                            ||
SQLi        ====>   OSINT  === ||
BCA                            ||
IDOR                           || ===> Shodan

-----------------XOX-------------------------

# Google Dorking

## Google Advance Operators

1. Operators are used to refine the results and to maximize the search value. they are your tools as well as Hacker's weapon

2. Basic Operators
+, -, ~, ., *, "", |, OR


Example:- 
target :- cdac.in
* subdomains:- 
1. site:cdac.in
2. site:\*.*.cdac.in
3. site:\*.*.cdac.in -www

subdomains:
site:*.*.cdac.in
site:cdac.in
site:cdac.in -www

Login:
intitle:Login
site:*.sindhpolice.gov.pk intitle:Login

Login URL:
```````````
site:*.gov.pk inurl:admin

site:*.gov.pk inurl:"*.php?file="

Indexing:
``````````
site:edu.pk "index of /"

File Type:
```````````
site:edu.pk filetype:pdf

site:edu.pk filetype:db

site:edu.pk filetype:txt

site:edu.pk filetype:xlsx

site:edu.pk filetype:sql

site:edu.pk filetype:zip

site:edu.pk filetype:tar

https://dheerajmadhukar.github.io/oh-my-dorks/



# Shodan

* shodan gives you real ip address

dev shodan: KEY

hostname:*.cdac.in

org:cdac

http.title:"Jenkins"

http.title:"Jenkins" hostname:"cdac"

http.title:"Jenkins" port:8080
http.title:"Jenkins" status:200
os:"windows7"
country:cn
city: pune




# Internet Archiv


GO SETUP:

$ cd ~
$ wget https://go.dev/dl/go1.26.4.linux-amd64.tar.gz

$ sudo tar -C /usr/local -xzf go1.26.0.linux-amd64.tar.gz

SHELL:
$ echo $SHELL
$ sudo vim ~/.zshrc
$ sudo vim ~/.bashrc
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin

$ source ~/.zshrc
$ go version
go version go1.26.4 linux/amd64

__________________________
Install HTTPX:
$ sudo mv /usr/bin/httpx /usr/bin/_httpx
$ go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest

-------------------------
SUBFINDER:

go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

$ subfinder -d target.tld -all -recursive -silent | tee subs.txt
$ cat subs.txt | rev | cut -d'.' -f1-3 | rev | sort -u | tee l1.txt
$ subfinder -dL l1.txt -all -recursive -silent | tee -a subs.txt

$ cat subs.txt | sort -u | httpx -silent | tee alive.txt



WAYBACKURLS:

$ go install github.com/tomnomnom/waybackurls@latest

$ cat alive.txt | waybackurls | tee wayback.txt


GF-PATTERNS:

$ go install github.com/tomnomnom/gf@latest
$ echo 'source $GOPATH/pkg/mod/github.com/tomnomnom/gf@v0.0.0-20200618134122-dcd4c361f9f5/gf-completion.bash' >> ~/.zshrc

$ mkdir .gf
$ cp -r $GOPATH/pkg/mod/github.com/tomnomnom/gf@v0.0.0-20200618134122-dcd4c361f9f5/examples ~/.gf
$  git clone https://github.com/1ndianl33t/Gf-Patterns
$ sudo mv Gf-Patterns/*.json ~/.gf/

Example: LFI:

$ cat wayback.txt | gf lfi | httpx -silent | tee lfi.txt
$ cat wayback.txt | gf interestingEXT | httpx -silent | tee interestingEXT.txt
