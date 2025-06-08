# learning-ansible

On managment node (for add ssh-phase):

.bash_profile
```
if [ -z "$SSH_AUTH_SOCK" ]; then
    eval $(ssh-agent -s)
    ssh-add ~/.ssh/id_rsa
fi
```

# Prepare hosts

ansible ubuntu -m ansible.builtin.user -a "name=ansible state=present password=$(mkpasswd --method=sha-512 'password') groups=sudo" -u vagrant -k -K -b
ansible rocky -m ansible.builtin.user -a "name=ansible state=present password=$(mkpasswd --method=sha-512 'password') groups=wheel" -u vagrant -k -K -b

ssh-copy-id ansible@ubuntu-test-01
ssh-copy-id ansible@rocky-test-01

ansible learning -m ansible.builtin.copy -a "src=files/ansible dest=/etc/sudoers.d/" -k -K -b -u vagrant
