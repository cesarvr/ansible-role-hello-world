# ansible-role-hello-world

Quick example of how to write reusable roles in Ansible. 


## How It Works 

This project has two roles ``x`` and ``p`` they both have the follow payload: 

```yml
---
- name: Print a message
  vars:
    message: Got P! 
  ansible.builtin.debug:
    msg: "Hello From P: {{ message }}" 
```

We then store both in the ``roles`` folder and we end up with this structure: 

```sh 
roles
├── p
│   └── tasks
│       └── main.yml
└── x
    └── tasks
        └── main.yml
```
> To initialize this structure we can run inside the ``roles`` folder the following command: ``ansible-galaxy init <name-of-the-role>``. 


Then we can reuse the roles in the main playbook: 

```yml 
---
- hosts: localhost
  tasks:
    - name: Printing From P
      include_role: 
        name: p 
      vars:
        message: Calling role P From A    
    - name: Printing From X
      include_role: 
        name: x 
      vars:
        message: Calling role X From A    
```

We should see this: 


```sh

TASK [Printing From P] ***************************************************************************************************************************************

TASK [p : Print a message] ***********************************************************************************************************************************
ok: [localhost] => {
    "msg": "Hello From P: Calling role P From A"
}

TASK [Printing From X] ***************************************************************************************************************************************

TASK [x : Print a message] ***********************************************************************************************************************************
ok: [localhost] => {
    "msg": "Hello From X: Calling role X From A"
}
```





