# handlers
inplemement tasks on ansible playbook that run only when some condition are define
## Overview of ansible handlers
Ansible module are designed to be idempotent. This mean the playbook and 
the task can be run multiple time without changing the managed host unless they
the need to make a change to get the managed host to the desired state.
Ansible module handlers are tasks that respond to a notification triggered by other tasks.
Task only notify when something change on a manage host.Each handlers has a unique name 
and is triggered at the end of a block of task in a playbook.
if any name notify the handlers then the handlers will not run.

