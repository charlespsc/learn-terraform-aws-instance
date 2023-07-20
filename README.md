
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
Nós podemos com o Ansibe fazer instalações como no exemplo instalei python3, virtualenv e o django.
Segue abaixo alguns comandos: 
  ```
  $ venv/bin/activate
  $ pip freeze
  $ django-admin startprojet setup .
  $ python3 manage.py runserver 0.0.0.0:8000
  ```
  - rodar o django no IP:PORTA da máquina, mas precisamos permitir o IP no Django no arquivo settings.py dentro da pasta setup.
  - As configurações dos projetos Django ficam em um arquivo chamado settings.py e podemos pedir para o Ansible fazer isso da seguinte forma:
      
  ```
  path: /home/ubuntu/tcc/setup/settings.py
  regexp: 'ALLOWED_HOSTS'
  line: 'ALLOWED_HOSTS = ["*"]'
  backrefs: yes
  ```


### Ansible realizar tarefas em SHELL
- Vamos editar a tarefa no playbook.yml com o seguinte:
  ```
  - name: Iniciando o projeto
      shell: 'comando 1; comando 2; comando 3'
  ```
  Vamos colocar um parametro adicional para ele continuar a execução e ignorar os erros.
  <br>Exemplo: 
  ```
  - name: Iniciando o projeto
      shell: '. /home/ubuntu/tcc/venv/bin/activate; django-admin startproject setup /home/ubuntu/tcc/'
      ignore_errors: yes
  ```
  
