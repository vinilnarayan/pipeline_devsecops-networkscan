###### pipeline_devsecops-networkscan

# DevSecOps creation for network scan



#### Requirement
```
➤ This pipeline runs only in Linux environment (eg. MacOS, Kali Linux etc...).
➤ Preinstall the below items...
    ☛ Python3
    ☛ NMAP
    ☛ Httpx
    ☛ Nikto
```

#### Downloads

1. [Python](https://www.python.org/)
2. [NMAP](https://nmap.org/) 
3. [Httpx](https://github.com/projectdiscovery/httpx)
4. [Nikto](https://github.com/sullo/nikto)
5. [Dirsearch](https://github.com/maurosoria/dirsearch)
6. [EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness)
7. [Nuclei](https://github.com/projectdiscovery/nuclei)

## Jenkins Pipeline Setup

1. Click the 'New Item' menu within Jenkins.

2. Provide a name for your new item and select 'Pipeline'.

3. Scroll down to 'Pipeline' section and choose 'Pipeline script from SCM' in 'Definition'.

4. Choose 'git' from 'SCM' and give 'Repository URL' as `https://github.com/vinilnarayan/pipeline_devsecops-networkscan.git`.

5. Then give `*/main` in 'Branch Specifier'

6. Click Apply and Save button and watch your first Pipeline run!


### Road Map

 * Popular Tools support.
    - [x] Nmap
    - [x] Httpx
    - [x] Nikto
    - [ ] Dirsearch
    - [ ] EyeWitness
    - [ ] Nuclei
* Reporting
    - [x] TEXT
    - [x] HTML
    - [ ] JSON
