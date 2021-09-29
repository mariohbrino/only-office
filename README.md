# Only Office Docs Development installation

Developer Edition allows you to install ONLYOFFICE Docs on your local server and integrate online editors with your web application.

[Documentation](https://helpcenter.onlyoffice.com/installation/docs-developer-install-ubuntu.aspx)

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

Install only office in your ubuntu server 20.04, add **flag** `-K` in case the user has a password
```bash
ansible-playbook -i inventory/onlyoffice.yml playbooks/onlyoffice.yml
```

## License

Copy the product license to Data folder
```bash
cp ./license.lic /var/www/onlyoffice/Data
```
