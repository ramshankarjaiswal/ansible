dyngroups
=========

This role creates dynamic groups.

Example usage - group_by: key={{ ec2_tag_env }}

When the above task is executed it will create groups based on the value of env tag on your ec2 instances. For example if your EC2 instances have been tagged with env=prod and env=stage then we can then specify variables for those groups in group_vars by creating corresponding files like group_vars/prod.yml group_vars/stage.yml

Variables specified in group_vars/sandbox.yml would have higher priority than group_vars/all.yml


Dependencies
------------

key={{ ec2_tag_env }} is dependent on EC2 dynamic inventory script.
