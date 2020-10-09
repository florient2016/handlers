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
If one or more tasks notify the handler, the handlers will run exactly once after all other tasks in the play have completed.
**Handlers** can be considered as inactive tasks that only get triggered when explicitly invoked
using **notify** statement.
Inthis snippet i will show you how to restart apache server when a configuration file is upload
```
# Restart apache server when configuration file is upload
tasks:
  - name: copy http.conf file to apache configuration file
    copy:
      src: httpd.conf
      dest: /etc/http/conf.d/httpd.conf
notify:
  - restart apache
handlers:
  - name: restart apache
    service:
      name: httpd
      state: restarted
```
- **notify** : indicates the task needs to trigger a handler
             the name of the handler to run
- **handlers** : indicates the handlers to start the list of handler tasks
### Benefits of using handlers
- handlers normally run after all other tasks in the play complete. A handlers called by a task in the tasks part of the playbook will not
run until all tasks under tasks have been processed.
- Even if more than one task notifies a handler, the handler only run once. if no tasks notify it, a handler will not run
- if a task that includes a notify statement does not report a changed result, the handler is not notified. the handler is skipped unless another task notifies it. 
ansible notifies handlers only if the task reports the changed status.
