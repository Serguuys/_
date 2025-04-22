
/etc/bashrc
```shell
ssh() {
    if [[ $@ == "VDS"]]; then
        command ssh -p 2202 user@
    else 
        command ssh $@
    fi
}
```
**user@100.99.90.101**
