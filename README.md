# Linux-Audit-File-Monitoring

## Overview

This project demonstrates the use of Linux Audit (auditd) to monitor changes to a set of protected files. Custom audit rules are used to track modifications made by attack scripts, allowing us to identify which files were altered and by which attack.

## Set up Instructions
### 1. Download and extract project repo
```bash
wget https://github.com/codepath/project2/archive/main.zip
unzip main.zip
cd project2-main

```

<img width="815" height="292" alt="image" src="https://github.com/user-attachments/assets/3b20486f-c001-43bd-86db-7ba8fa2abbce" />

<img width="567" height="328" alt="image" src="https://github.com/user-attachments/assets/9923f669-2851-45bb-a51d-aedd34af4828" />

### 2. Make Attack Scripts Executable
```bash
chmod u+x attack-a attack-b attack-c

```
<img width="785" height="220" alt="image" src="https://github.com/user-attachments/assets/70785f03-9dae-4919-a832-1a89298b0c25" />

### 3. Ensure Audit Service is running
```bash
sudo systemctl status auditd
```
<img width="762" height="388" alt="image" src="https://github.com/user-attachments/assets/3f8fa29f-e980-40dd-b725-da457f30f0a7" />

### 4. Enter Rules 
- Add write-watch rules for the protected files in /etc/audit/rules.d/audit.rules
- Set out key to proj2.
- Save and quit afterwards (:wq)
```bash
sudo vi /etc/audit/rules.d/audit.rules
```
<img width="790" height="467" alt="image" src="https://github.com/user-attachments/assets/02734883-575f-426a-8bde-ee7ac99dd4f9" />

### 4. Restart Audit and Ensure rules have been saved

```bash
sudo systemctl restart auditd
sudo auditctl -l
```
<img width="733" height="215" alt="image" src="https://github.com/user-attachments/assets/e260f595-6c40-453a-97a8-cafd76c9d30c" />

## Execute Attack Files
```bash
./attack-a
./attack-b
./attack-c
```

<img width="791" height="187" alt="image" src="https://github.com/user-attachments/assets/4d1f2868-5a00-4ac4-8911-3b582a31c4cf" />

## Viewing Audit Logs
```bash
sudo ausearch -ts today -k proj2
```
<img width="909" height="219" alt="image" src="https://github.com/user-attachments/assets/2f76f629-356b-4edd-87e7-5fae05772113" />

- Those repeated blocks with comm="auditctl" and CONFIG_CHANGE op=add_rule key="proj2" are just the audit system logging that you added the rules (the -w lines). They aren’t the attacks — they’re the config change events when the rules were installed.

<img width="1029" height="270" alt="image" src="https://github.com/user-attachments/assets/ac5655d2-7a9a-4cdb-b21c-eae60b0e79f0" />

- Here is the information we want. Here we see `attack-a` executed and `cloudia.txt` was one of the path entries in that event. So attack-a -> cloudia.txt.
- Looking at the logs further we find that:
  - attack-b -> oakley.txt
  - attack b- > squeaky.txt

#### Looking at the “before” and “after” versions of cloudia.txt, here’s what changed:

##### Extra content added at the end:
- The “after attack” version includes a new paragraph about Harry Potter and the Avada Kedavra curse that was not present in the original file.

##### Everything else is identical:
- The story about Cloudia, her adventures, and her return to the sky is unchanged. Only the additional Harry Potter paragraph was appended to the file.


