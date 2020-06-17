# AWS_Terraform_Ansible_HA_with_CFE_HTTPS_VS_with_WAF_Ansible_Vault


<H1>Preparing a Valid SSL Cert which will be used into AS3</H1>
Create a PFX/pkcs12 file which includes the cert and private key.
You can do it with openssl : openssl pkcs12 -export -in file.crt -inkey file.key -out file.pfx 
Upload the file.pfx to a repo. 
Replace the pkcs12 url with yours into the file AS3_Template.j2.


<H1>Ansible-Vault Setup</H1>

Create a file where you have your password in it : echo "default" > ~/.vault_pass.txt

create the ansible vault env variable export ANSIBLE_VAULT_PASSWORD_FILE=~/.vault_pass.txt 
OR
Add the line vault_password_file=~/.vault_pass.txt into the ansible.cfg file in case Terraform doesn't have access to the env variables of Ansible

Encrypt your bigip password: ansible-vault encrypt_string 'SanDiego123!' --name 'password'

Encrypt your PFX cert and key passphrase: ansible-vault encrypt_string 'default' --name 'passphrase'

Replace the vars password and passphrase with yours into the Playbooks.
