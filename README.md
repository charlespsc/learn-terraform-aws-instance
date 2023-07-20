
# Treinamento de Terraform e Ansible usando AWS


## Principais arquivos: 
  - main.tf       - Para criar as máquinas na AWS com Terraform
  - hosts.yml     - Para permitir que o Ansible fale com o Terraform
  - playbook.yml  - Para criar as tarefas do Ansible


## Comandos Terraform:
```
$ terraform init
$ terraform plan
$ terraform apply
```
  Com esses comandos inicializamos o terraform e a instância na AWS 
    - Para acesso via SSH precisamos criar a chave (.PEM) e adicionar uma política de segurança (IN/OUT)

  Podemos testar criando um arquivo index.html na instância criada e chamar um servidor web de teste com o comando abaixo:
  ```
  $ nohup busybox httpd -f -p 8080 &
  ```

## Comandos Ansible:
```
$ ansible-playbook playbook.yml -u ubuntu --private-key=charlespscKey.pem -i hosts.yml
```
