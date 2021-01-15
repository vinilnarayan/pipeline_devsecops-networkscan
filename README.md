###### pipeline_devsecops-networkscan

# DevSecOps creation for network scan



#### Requirement
```
☞ This pipeline runs only in Linux environment (eg. MacOS, Kali Linux etc...)
☞ Preinstall the below items...
    ☛ Python3
    ☛ NMAP
    ☛ Httpx
    ☛ Nikto
```

#### Downloads

➤ [Python](https://www.python.org/)\n
➤ [NMAP](https://nmap.org/) 
➤ [Httpx](https://github.com/projectdiscovery/httpx)
➤ [Nikto](https://github.com/sullo/nikto)
➤ [Dirsearch](https://github.com/maurosoria/dirsearch)
➤ [EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness)
➤ [Nuclei](https://github.com/projectdiscovery/nuclei)

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
