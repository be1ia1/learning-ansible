# learning-ansible

# Prepare hosts

ansible ubuntu -m ansible.builtin.user -a "name=ansible state=present password=$(mkpasswd --method=sha-512 'password') groups=sudo" -u hula -k -K -b
ansible rocky -m ansible.builtin.user -a "name=ansible state=present password=$(mkpasswd --method=sha-512 'password') groups=wheel" -u hula -k -K -b

ssh-copy-id ansible@ls-test-01
ssh-copy-id ansible@ls-test-02

ansible all -m ansible.builtin.copy -a "src=files/ansible dest=/etc/sudoers.d/" -k -K -b
