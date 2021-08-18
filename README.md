Ansible playbook to retrieve letsencrypt wildcard certificate from a public facing webserver and deploy it to LAN devices/applications on the same root domain.

Published for educational/reference purposes.

NOTE: You will need to configure local DNS so that the devices can be accessed via a subdomain of the root to which the certificate was issued against. Accessing the device via IP address will still result in a certificate warning.

Configures valid SSL for the following devices:
- UniFi Security Gateway
- UniFi CloudKey

Configures SSL certificates following applications/services on Debian 10 based VMs:
- Plex (the python-lxml package must be installed on the host for the plex configuration file to be managed)

Allows for configuring of and persistent mounting of additional QCOW2 disk images

Example Inventory
-
```
---
public:
  hosts:
    web-a:
      ansible_become_pass: # FILLIFSUDOING
      cert_path: /etc/letsencrypt/live/yourpublicwebserver.tld

usg:
  hosts:
    router: {}

cloudkey:
  hosts:
    unifi-cloudkey:
      cert_path: /etc/ssl/private

plex:
  hosts:
    media:
      ansible_become_pass: # FILLIFSUDOING
      cert_path: /etc/ssl/private
      plex_user: plex
      plex_group: plex
      plex_preferences_file: /var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Preferences.xml
      plex_certificate_location: /var/lib/plexmediaserver/plex.p12
      plex_certificate_encryption_key: password

```

License
-

BSD-3-Clause
