- create an account
- generate an pair of ssh keys with an empty passphrase
```sh
ssh-keygen -f linode -N ""
mv linode* ~/.ssh/
```
- create a `linode`
- pw: `kormef-sycroN-fecwo9` | `mezjup-gorcic-6qiXfa`
- try to connect to ssh
- copy compose file
```
scp  docker-compose.yml root@<host>:/root/    
```
- compose the freshly copied docker
- check url now with generated host ip

