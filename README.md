This is the example of possible ansible vars bug.

Run it like this:
```bash
ansible-playbook -i inventory bug.yml
```

Expected output:

```
PLAY [all] ********************************************************************
127.0.0.1: importing .../ansible-bug/environments/development.yml

TASK: [debug msg="role message - this is development"] ********************************
ok: [127.0.0.1] => {"item": "", "msg": "role message - this is development"}

TASK: [debug msg="task message - this is development"] ********************************
ok: [127.0.0.1] => {"msg": "task message - this is development"}

PLAY RECAP ********************************************************************
127.0.0.1                  : ok=2    changed=0    unreachable=0    failed=0
```

Actual output:
```
PLAY [all] ********************************************************************
127.0.0.1: importing .../ansible-bug/environments/development.yml

TASK: [debug msg="role message - this is common"] *****************************
ok: [127.0.0.1] => {"item": "", "msg": "role message - this is common"}

TASK: [debug msg="task message - this is common"] *****************************
ok: [127.0.0.1] => {"msg": "task message - this is development"}

PLAY RECAP ********************************************************************
127.0.0.1                  : ok=2    changed=0    unreachable=0    failed=0
```

Tested with Ansible 1.3.1.
