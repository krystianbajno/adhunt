This tool was encrypted (https://github.com/krystianbajno/armory), but I decided to make it public.

# ADHUNT
ADHUNT is a polyglot file (Bash, PowerShell, Python, HTML) for domain information gathering, that works everywhere and needs no installation.

Just open the website, hit Save As and start your recon.

**Collectors**:
- PowerShell `New-Object DirectoryServices.DirectorySearcher`
- Bash `ldapsearch` 

**Converters**:
- Python converter crafting JSON files from ldapsearch LDIF.

**GUI**:
- HTML GUI that runs in your browser.

### It supports the following scenarios:

- Run the HTML file as a PowerShell script to dump domain information using the PowerShell, including all users, groups, computers, and group policies:
```bash
iex(gc -path adhunt.html -raw) # From local file
iwr https://adhunt.netlify.app | iex # Download and execute in memory
```

- Run the HTML file as a Bash script to dump domain information (requires ldapsearch), including all users, groups, computers, and group policies:
```bash
bash adhunt.html <server> <domain> <user> <password>
bash adhunt.html # You will be prompted for credentials
curl https://adhunt.netlify.app | bash # Download and execute in memory
```

The PowerShell will try to get current user credentials automatically, but you will be prompted if you want to use custom ones. Useful on hardened AD computers.

- Run the HTML file with Python to parse LDIF ldapsearch results into JSON for use in the HTML GUI:
```bash
python adhunt.html <ldif_results_directory>
curl https://adhunt.netlify.app | python # Download and execute in memory
```

- Run the HTML file in a browser to display and filter the results:
Upload the JSON files into ADHUNT. ADHUNT is hosted as a static file, and runs on your computer.
https://adhunt.netlify.app
If you feel extra paranoid, download it to your computer.

Use the global filter to search for entries. For example, if you want to find a computer associated with a user and the user's name is mentioned in the computer's description, enter the username. This will display both the user and the computer in the results.

The tool displays all the Active Directory attributes and you can query them.

- Run the HTML file in a browser to filter for entities and save .csv file.
Filter for users in a specific group, for example: "Managers". Now you have the list of all managers in the company.
If you want to send phishing e-mails, then just query for your target group and export .csv file. You will get all the e-mails to send e-mails to.

### Installation
```
curl https://adhunt.netlify.app > adhunt.html
wget https://adhunt.netlify.app
Browser -> right click -> Save as -> adhunt.html
```
The tool requires no installation however, as you can run it completely in memory in order to dump domain information, and then parse the results using your browser at https://adhunt.netlify.app.

### Todo
- Python domain information collector
- BloodHound data converter
