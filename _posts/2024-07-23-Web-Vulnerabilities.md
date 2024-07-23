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

    I am not sure why I need to install `gorm.io`. Because, according to the video, there is only instruction command with no reason...

    However `gorm.io` is one of go lan library package.

    ![installGowitness2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.35.50.png)

    ![installGowitness3](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.35.56.png)

    run `gowitenss`

    ![runGowitness1](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.36.12.png)

    ![runGowitness2](../assets/img/webRevisited/Screenshot%202024-07-23%20at%2014.36.48.png)

5.  Multi-tasking bash script

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

1. SQL injection

2. XSS

3. Command injection

4. Insecure File Upload

5. Attacking Authentication

6. XXE

7. IDOR

8. Capstone

# Wireless penetration testing

# Reporting

Sample report

https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report
