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
