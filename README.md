# Ansible sample

Sample for https://github.com/ansible/ansible/pull/6958

Run it via `ansible-playbook -i inventory-local sample-play.yml`

Output:

```
PLAY [local] ******************************************************************

GATHERING FACTS ***************************************************************
ok: [localhost]

TASK: [sample ] ***************************************************************
failed: [localhost] => (item={'sample_val': True, 'sample_path': '/tmp/yes'}) => {"failed": true, "item": {"sample_path": "/tmp/yes", "sample_val": true}}
msg: value of sample_val must be one of: yes,on,1,true,1,no,off,0,false,0, got: True
failed: [localhost] => (item={'sample_val': True, 'sample_path': '/tmp/no'}) => {"failed": true, "item": {"sample_path": "/tmp/no", "sample_val": true}}
msg: value of sample_val must be one of: yes,on,1,true,1,no,off,0,false,0, got: True
failed: [localhost] => (item={'sample_val': True, 'sample_path': '/tmp/true'}) => {"failed": true, "item": {"sample_path": "/tmp/true", "sample_val": true}}
msg: value of sample_val must be one of: yes,on,1,true,1,no,off,0,false,0, got: True
failed: [localhost] => (item={'sample_val': False, 'sample_path': '/tmp/false'}) => {"failed": true, "item": {"sample_path": "/tmp/false", "sample_val": false}}
msg: value of sample_val must be one of: yes,on,1,true,1,no,off,0,false,0, got: False

FATAL: all hosts have already failed -- aborting

PLAY RECAP ********************************************************************
           to retry, use: --limit @/Users/ngoyal/sample-play.retry

localhost                  : ok=1    changed=0    unreachable=0    failed=1
```

Change library/sample/sample choices parameter to `BOOLEANS+['True', True, 'False', False]`

Run again and works.
