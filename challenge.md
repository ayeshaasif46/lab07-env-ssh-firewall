# Challenge: Environment Audit and Ping Block

### Job 1: Environment Audit
Commands:
printenv | grep SHELL
printenv | grep HOME
printenv | grep USER

Values:
SHELL=/bin/bash
HOME=/home/ayeshaasif46
USER=ayeshaasif46

### Job 2: Temporary Student Variables
Commands:
export STUDENT_NAME="Ayesha Asif"
export STUDENT_ROLL_NUMBER="123456"
export STUDENT_SEMESTER="5"
printenv | grep '^STUDENT_'

Proof of disappearance:
Logged out and re-logged in; `printenv | grep '^STUDENT_'` returned empty output.

### Job 3: Permanent Student Variables
Added to ~/.bashrc:
export STUDENT_NAME="Ayesha Asif"
export STUDENT_ROLL_NUMBER="123456"
export STUDENT_SEMESTER="5"

Proof of permanence:
Logged out and re-logged in; `printenv | grep '^STUDENT_'` output:
STUDENT_NAME=Ayesha Asif
STUDENT_ROLL_NUMBER=123456
STUDENT_SEMESTER=5

### Job 4: Ping Block via UFW
Commands used:
sudo cp /etc/ufw/before.rules ~/before.rules.backup
sudo vim /etc/ufw/before.rules
# Changed ACCEPT to DROP on echo-request line
sudo ufw reload

Proof of block:
`sudo iptables -S ufw-before-input | grep "icmp-type 8"` ends with `-j DROP`.

Restored rule:
# Changed DROP back to ACCEPT in /etc/ufw/before.rules
sudo ufw reload
`sudo iptables -S ufw-before-input | grep "icmp-type 8"` ends with `-j ACCEPT`.
