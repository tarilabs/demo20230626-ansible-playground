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

using:
https://github.com/tarilabs/demo20230626-ansible-playground/blob/817600a703748fe3bb1571110db901005afb584f/empiric1.playbook.yml#L42-L44

results in `has no attribute \"nesting['alphabet']\".` see:
```
TASK [debug] **********************************************************************************************************************************************************************
fatal: [localhost]: FAILED! => {"msg": "The task includes an option with an undefined variable. The error was: 'dict object' has no attribute \"nesting['alphabet']\". 'dict object' has no attribute \"nesting['alphabet']\"\n\nThe error appears to be in '/Users/mmortari/git/demo20230626-ansible-playground/empiric1.playbook.yml': line 43, column 7, but may\nbe elsewhere in the file depending on the exact syntax problem.\n\nThe offending line appears to be:\n\n    # has no attribute \\\"nesting['alphabet']\\\". :\n    - debug:\n      ^ here\n"}
```

so it would seems like, empirically, squared accessor is not supported in `selectattr`.

using:
https://github.com/tarilabs/demo20230626-ansible-playground/blob/87cd7e55221974641da6eabb12ec3517cd67237e/empiric1.playbook.yml#L47-L49

results in ` has no attribute \"nesting['alph\".` see:
```
TASK [debug] **********************************************************************************************************************************************************************
fatal: [localhost]: FAILED! => {"msg": "The task includes an option with an undefined variable. The error was: 'dict object' has no attribute \"nesting['alph\". 'dict object' has no attribute \"nesting['alph\"\n\nThe error appears to be in '/Users/mmortari/git/demo20230626-ansible-playground/empiric1.playbook.yml': line 48, column 7, but may\nbe elsewhere in the file depending on the exact syntax problem.\n\nThe offending line appears to be:\n\n    # has no attribute \\\"nesting['alph\\\". :\n    - debug:\n      ^ here\n"}
```

so it would seems like, empirically, squared accessor is completely ignored and just raw/brutally splitted on `.` for the 1st argument in `selectattr`.
