###### pipeline_devsecops-networkscan

# DevSecOps creation for network scan


#### Requirement
```
* This pipeline runs only in Linux environment (eg. MacOS, Kali Linux etc...).
* NMAP should be installed.
```

#### Downloads

1. [NMAP](https://nmap.org/) 
2. [Httpx](https://github.com/projectdiscovery/httpx)
3. [Nikto](https://github.com/sullo/nikto)
4. [Dirsearch](https://github.com/maurosoria/dirsearch)
5. [EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness)
6. [Nuclei](https://github.com/projectdiscovery/nuclei)

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
    - [ ] Httpx
    - [ ] Nikto
    - [ ] Dirsearch
    - [ ] EyeWitness
    - [ ] Nuclei
* Reporting
    - [x] TEXT
    - [ ] HTML
    - [ ] JSON
