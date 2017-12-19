# Ansible Role: OpenSSL self signed certificates

An Ansible role that generates and installs OpenSSL cerificates which can be used
with Apache HTTP server or Nginx on RHEL/Centos.

## Requirements

There aren't any requirements for this role.

## Role variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

##### Workdir for the role. Inside there will be created some files required for the certificates.

    ssl_workdir: /opt/ansible-ssl-workdir
    
##### If set to true, role will add certificate authority to list of trusted certificates of managed instance.

    ssl_update_server_ca: true
    
##### If you want to provide your own certificate authority, you need to pass both private key and certificate.
##### Otherwise role will generate a new certificate authority.

    ssl_ca_key_path: ""
    ssl_ca_pem_path: ""

##### Default values for certificate authority created by this role. Used if `ssl_ca_key_path` and `ssl_ca_pem_path` are empty.

    ssl_ca_country: PL
    ssl_ca_province: warminsko-mazurskie
    ssl_ca_city: Klewki
    ssl_ca_organization: CIA
    ssl_ca_domain: ca.localhost

##### List of domains which you would like to create certificates for.

    ssl_domains: []

##### An example how to set all certificate for one domain:

    ssl_domains:
      - domain: example.com
        keyDestination: /var/www/certs/example.com.key
        crtDestination: /var/www/certs/example.com.crt
        countryCode: PL
        province: Neverland Province
        city: Neverland
        companyName: Acme inc.
        companyDepartment: IT
        email: root@example.com

##### An example for wildcard domain:

    ssl_domains:
      - domain: "*.example.com"
        domainFilename: STAR_fexample.com
        keyDestination: /var/www/certs/STAR_example.com.key
        crtDestination: /var/www/certs/STAR_example.com.crt
        countryCode: PL
        province: Neverland Province
        city: Neverland
        companyName: Acme inc.
        companyDepartment: IT
        email: root@example.com

##### Minimal example of domain configuration (rest of details will be taken from CA settings except department and email):

    ssl_domains:
      - domain: test.example.com
        keyDestination: /var/www/certs/test.example.com.key
        crtDestination: /var/www/certs/test.example.com.crt

## Dependencies

None.

## Example Playbook

    - hosts: webservers
      vars_files:
        - vars/main.yml
      roles:
        - { role: MWojtowicz.openssl }
        
## License

MIT / BSD

## Author Information

This role was created in 2017 by [Michal Wojtowicz](https://mwojtowicz.it/).
