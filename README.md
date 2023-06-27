supporting conversation at https://github.com/ansible/ansible-rulebook/pull/539#discussion_r1240158903

given 3 items (vertical scroll in github):
https://github.com/tarilabs/demo20230626-ansible-playground/blob/504e0fc5937bfe6d71bed5e775d13620253f3b11/empiric1.playbook.yml#L6-L22

using:
https://github.com/tarilabs/demo20230626-ansible-playground/blob/504e0fc5937bfe6d71bed5e775d13620253f3b11/empiric1.playbook.yml#L38-L39

results in:
```
TASK [debug] **********************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        {
            "color": "red",
            "name": "apple",
            "nesting": {
                "alphabet": "vowel"
            },
            "nesting.alphabet": "none"
        },
        {
            "color": "red",
            "name": "cherry",
            "nesting": {
                "alphabet": "consonant"
            },
            "nesting.alphabet": "none"
        }
    ]
}
```

as expected.
