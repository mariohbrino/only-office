# Only Office Docs Developer Edition

Developer Edition allows you to install ONLYOFFICE Docs on your local server and integrate online editors with your web application.

[Documentation](https://helpcenter.onlyoffice.com/installation/docs-developer-install-ubuntu.aspx)

## Requirements

* Ubuntu Server 20.04
* Ansible 2.9.6
* Community Postgresql

## Initial settings

Define the variables on `inventory.yml` as per your needs

Change variables on `inventory.yml`
```bash
ansible_host: '<hostname>'
username: '<username>'
```

Ansible connection can be set as `local` or `ssh`
```bash
ansible_connection: '<connection>'
```

SSH private key file needs to be defined when using `ssh` connection
```bash
ansible_ssh_private_key_file: /path/to/your/ssh-key
```

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
chmod 400 ~/.ssh/<ssh-key>
```

Configure ssh config file
```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

SSH config file sample
```bash
Host alias
  HostName <ip-address>
  User <username>
  Port 22
  IdentityFile ~/.ssh/<ssh-key>

```

## Usage and information

Install only office on ubuntu server 20.04, add **flag** `-K` in case the user has a password
```bash
ansible-playbook -i inventory.yml onlyoffice.yml
```

> Access onlyoffice [localhost](http://localhost) or `hostname`

### Tags

Using tags helps to define which roles will be selected or skipped

Run only tags with tags `postgres` and `onlyoffice`

```bash
ansible-playbook -i inventory.yml onlyoffice.yml --tags "postgres,onlyoffice"
```

Run all tasks except those with the tags `nginx` and `redis`

```bash
ansible-playbook -i inventory.yml onlyoffice.yml --skip-tags "nginx,redis"
```

## Adding license

Copy the product license to Data folder
```bash
cp ./license.lic /var/www/onlyoffice/Data
```

## License

[MIT license](http://opensource.org/licenses/MIT).
