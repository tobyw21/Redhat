# Setting up the Control Node

`sudo dnf install ansible-core`

`pip install ansible-navigator`


# Set up Managed Nodes

```
cat >> inventory << EOF
ansible1 ansible_ssh_user=<user>
ansible2
EOF

ansible -i inventory all -u <user> -k -b -K -m user -a "name=ansible"

ansible -i inventory all -u <user> -k -b -K -m shell -a "echo <password> | passwd --stdin ansible"

ssh-keygen (control user and ansible user)

for i in ansible1 ansible2; do ssh-copy-id $i; done (control user and ansible user)

ansible -i inventory  all -u ansible -b -m command -a "ls -l /root" -K

ansible -i inventory all -u <user> -k -b -K -m shell -a 'echo "ansible ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ansible'
```