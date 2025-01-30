> **URL PARA EXEMPLOS E MAIS INFORMAÇÕES:** https://docs.ansible.com/ansible/2.8/user_guide/vault.html
{.is-info}

> O Ansible Vault é um recurso do Ansible que permite que você mantenha dados sensíveis, como senhas ou chaves, em arquivos criptografados, em vez de texto simples em playbooks ou funções. Esses arquivos do vault podem então ser distribuídos ou colocados no controle de origem.
  Para habilitar esse recurso, uma ferramenta de linha de comando - ansible-vault - é usada para editar arquivos, e um sinalizador de linha de comando ( --ask-vault-pass, --vault-password-fileou --vault-id) é usado. Como alternativa, você pode especificar o local de um arquivo de senha ou comandar o Ansible para sempre solicitar a senha no seu arquivo ansible.cfg. Essas opções não exigem o uso de sinalizador de linha de comando.
{.is-info}

# PARA CONFIGURAR O VAULT NO HOST.YAML CRIE UM DIRETORIO NO /ETC/ANSIBLE.

# COM O NOME "group_vars" DENTRO CRIE OUTRO DIRETORIO COM O NOME DO GRUPO DE HOST QUE VC DESEJA ADICIONAR O VAULT. NO MEU AQUIVO HOST.YAML O GRUPO QUE QUERO ADICIONAR É O "myhosts". 

```
sudo mkdir group_vars
cd group_vars
sudo mkdir <nome do grupo de hosts>
```

# FEITO ISSO VAI FICAR ASSIM "/etc/ansible/group_vars/myhosts" AGORA CRIE UM ARQUIVO "vars.yaml"

```
sudo vi vars.yaml
```

# NO ARQUIVO ADICIONE:

```
ansible_user: <nome do usuario que o ansible vai usar>
ansible_ssh_pass: <senha do usuario>
ansible_become_pass: <senha para o usuario virar sudo>
ansible_connection: ssh
ansible_python_interpreter: /usr/bin/python3
```

# SAIA SALVANDO O ARQUIVO, AGORA ENCRIPTOGRAFA O ARQUIVO

```
sudo ansible-vault encrypt vars.yaml
```

# MUDE A PERMISSÃO DO ARQUIVO PARA 664
```
ansible_user: <nome do usuario que o ansible vai usar>
ansible_ssh_pass: <senha do usuario>
ansible_become_pass: <senha para o usuario virar sudo>
ansible_connection: ssh
ansible_python_interpreter: /usr/bin/python3
```

# SAIA SALVANDO O
```
sudo chmod 664 vars.yaml
```

# CRIE UM ARQUIVO VAULT.PWD SO COM A SENHA DENTRO  

```
sudo vi vault.pwd
```

# FEITO ISSO SAIA DO ARQUIVO SALVANDO E CRIPTOGRAFA

```
sudo ansible-vault encrypt vault.pwd
```

# ABRA O ANSIBLE.CFG E ADICIONE:

```
VAULT_PASSWORD_FILE = <O CAMINHO DO ARQUIVO VAULT.PWD>
```
