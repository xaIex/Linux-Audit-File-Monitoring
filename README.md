# Linux-Audit-File-Monitoring

## Overview

This project demonstrates the use of Linux Audit (auditd) to monitor changes to a set of protected files. Custom audit rules are used to track modifications made by attack scripts, allowing us to identify which files were altered and by which attack.

## Set up Instructions
### 1. Download and extract project repo
```
wget https://github.com/codepath/project2/archive/main.zip
unzip main.zip
cd project2-main

```

<img width="815" height="292" alt="image" src="https://github.com/user-attachments/assets/3b20486f-c001-43bd-86db-7ba8fa2abbce" />

<img width="567" height="328" alt="image" src="https://github.com/user-attachments/assets/9923f669-2851-45bb-a51d-aedd34af4828" />

### 2. Make Attack Scripts Executable
```
chmod u+x attack-a attack-b attack-c

```
<img width="785" height="220" alt="image" src="https://github.com/user-attachments/assets/70785f03-9dae-4919-a832-1a89298b0c25" />

### 3. Ensure Audit Service is running
```
sudo systemctl status auditd
```
<img width="762" height="388" alt="image" src="https://github.com/user-attachments/assets/3f8fa29f-e980-40dd-b725-da457f30f0a7" />

### 4. Enter Rules 
Add write-watch rules for the protected files in /etc/audit/rules.d/audit.rules
Also set out key to proj2
Save and quit (:wq)
```
sudo vi /etc/audit/rules.d/audit.rules
```
<img width="790" height="467" alt="image" src="https://github.com/user-attachments/assets/02734883-575f-426a-8bde-ee7ac99dd4f9" />

### 4. Restart Audit and Ensure rules have been saved

```
sudo systemctl restart auditd
sudo auditctl -l
```
<img width="733" height="215" alt="image" src="https://github.com/user-attachments/assets/e260f595-6c40-453a-97a8-cafd76c9d30c" />

## Execute Attack Files
```
./attack-a
./attack-b
./attack-c
```

<img width="791" height="187" alt="image" src="https://github.com/user-attachments/assets/4d1f2868-5a00-4ac4-8911-3b582a31c4cf" />




