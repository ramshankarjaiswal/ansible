# Ansible

**AWS Dynamic Inventory Dependencies** -
```
pip install --upgrade pip
pip install boto --user
chmod +x inventory/ec2.py

export AWS_ACCESS_KEY_ID='AK123'
export AWS_SECRET_ACCESS_KEY='abc123'
```
You can test the dynamic inventory script by itself to make sure your config is correct:
>./ec2.py --list

To verify that you are able to ssh to the hosts in your inventory.
>ansible all -m ping



#### Things you may want to change based on your environment.

##### inventory/ec2.ini

**Line 16** - You may only be using a few regions of AWS so limit it to them
>`regions = ap-southeast-1`

**Line 173** - You may want to apply filter based on tags to only fetch those resources from aws.
>instance_filters = tag:env=staging





Markdown Cheat Sheet
>https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#lines

Markdown preview in Atom text editor `Ctrl+Shift+M`
