# Fedora Server Setup

### Firewall Configuration (firewalld)

- use `firewall-cmd` command to interact with firewall
- systemd manages the firewalld daemon `sudo systemctl status firewalld`
- on Fedora, the default firewall zone is called `FedoraServer` and is the only active zone
- to enable HTTP/HTTPS traffic, need to add them as services
- to check current services for FedoraServer zone `sudo firewall-cmd --zone FedoraServer --list-all`
- to add HTTP service `sudo firewall-cmd --zone FedoraServer --add-service http --permanent`
- to add HTTPS service `sudo firewall-cmd --zone FedoraServer --add-service https --permanent`
- restart firewalld `sudo systemctl restart firewalld`
- to check for only active zones `sudo firewall-cmd --get-active-zones`

### SELinux Configuration (

- check if semanage command is installed `semanage -h`
- if necessary, install semanage `sudo dnf install semanage`
- then make all the httpd stuff permissive, which resolves some 403 errors `sudo semanage permissive -a httpd_t`
- also, another precaution is to make sure all your nginx directories/files have 755 permissions set up
