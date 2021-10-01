# Only Office Docs Developer Edition

Developer Edition allows you to install ONLYOFFICE Docs on your local server and integrate online editors with your web application.

[Documentation](https://helpcenter.onlyoffice.com/installation/docs-developer-install-ubuntu.aspx)

## Requirements

* Ubuntu Server 20.04
* Ansible 2.9.6
* Community Postgresql

## Initial settings

Change `username` and `ansible_host` on `inventory/onlyoffice.yml` **hosts** and **vars** with your hostname and username
```bash
hosts:
  onlyoffice:
    ansible_host: '<hostname>'
vars:
  username: '<username>'
```

> hostname can be a name like localhost or an ip address

Install `ansible` in your system
```bash
sudo apt -y install ansible
```

> ansible version 2.9.6

Install postgresql community plugin
```bash
ansible-galaxy collection install community.postgresql
```

## Setup ssh config

Change ssh-key permissions
```bash
chmod 400 ~/.ssh/<ssh_key>
```

Configure ssh config file
```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

SSH config file sample
```bash
Host alias
  HostName <ip_address>
  User <username>
  Port 22
  IdentityFile ~/.ssh/<ssh_key>

```

## Usage and information

Install only office on ubuntu server 20.04, add **flag** `-K` in case the user has a password
```bash
ansible-playbook -i inventory/onlyoffice.yml playbook/onlyoffice.yml
```

### Run on localhost

Change on `inventory/onlyoffice.yml` the variables
```bash
hosts:
  onlyoffice:
    ansible_host: 'localhost'
vars:
  ansible_connection: 'local'
```

### Tags

Using tags helps to define which roles will be selected or skipped

Run only tags with tags `postgres` and `onlyoffice`

```bash
ansible-playbook -i inventory/onlyoffice.yml playbook/onlyoffice.yml --tags "postgres,onlyoffice"
```

Run all tasks except those with the tags `nginx` and `redis`

```bash
ansible-playbook -i inventory/onlyoffice.yml playbook/onlyoffice.yml --skip-tags "nginx,redis"
```

## Adding license

Copy the product license to Data folder
```bash
cp ./license.lic /var/www/onlyoffice/Data
```

## License

[MIT license](http://opensource.org/licenses/MIT).
