# Bitwarden On-Premice

Ansible role to install and configure Bitwarden on your own server with ansible.

## Platforms

Developed and test on Debian 10. Should work with any Linux platform with
docker and python3.

Ansible used is 2.8, but also lower versions could be sufficient.

## Updating

when updating the role doesn't check if new version has been downloaded and
therefore the tasks related to update always report changed state and restart
bitwarden.

## Notes

Google Chrome doesn't allow bitwarden to work without ssl (works in the extention).
If the installation script changes its behavior, the role will have to be updated.

## Role design choices

All design choices are made to reflect the way bitwarden installer works.

 - Path to ssl certificate is adjusted based on it being generated or not and the domain name of the instance
 - global.override.env is changed using lineinfile because of the passwords generated for docker container
 - {{" "}} is used for adding trailing white space wherever the installer leaves trailing white space

## Usage with SSL

Here is an example how to supply ssl key and certificate.

```
- name: Bitwarden server
  hosts: bitwarden
  roles:
    - docker
    - our-ssl
    - { role: bitwarden,
      vaulted_ssl_priv_key: "{{ our_ssl_private_key }}",
      vaulted_ssl_crt: "{{ our_ssl_crt }}" }
```

## License

GPLv3

## Author

Filip Široký
Ordbogen A/S
