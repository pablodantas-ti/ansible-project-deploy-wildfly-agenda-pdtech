# 📅 Agenda WildFly com Ansible

Automação de um ambiente de estudo para uma agenda de tarefas em Java, publicada no WildFly.

## ✨ O que foi configurado

- 🚀 WildFly executando como serviço `systemd`;
- 🌐 Nginx como proxy reverso;
- 🐘 PostgreSQL para usuários e tarefas persistentes;
- 🧰 Adminer protegido por autenticação no Nginx;
- 📦 Deploy automático de arquivos `.war`;
- 💾 Backup automático da versão anterior antes do deploy;
- 🔐 Ansible Vault para senhas do banco, administrador e Adminer.

## 🗂️ Estrutura

```text
inventory/     Inventário e variáveis
playbooks/     Execução das automações
roles/
  tarefas/     Build, backup e deploy da aplicação
  postgresql/  Instalação e banco da agenda
  adminer/     Interface web do PostgreSQL
```

## 🔒 Segurança

As senhas não devem ser enviadas ao GitHub.

O arquivo real abaixo é ignorado pelo Git:

```text
inventory/group_vars/all/vault.yml
```

Use o modelo `vault.example.yml` para criar seu Vault local:

```bash
ansible-vault create inventory/group_vars/all/vault.yml
```

## ▶️ Playbooks

### 🐘 Preparar o PostgreSQL

```bash
ansible-playbook -i inventory/hosts.yml playbooks/postgresql.yml \
  --ask-pass --ask-become-pass --ask-vault-pass
```

### 🧰 Instalar o Adminer

```bash
ansible-playbook -i inventory/hosts.yml playbooks/adminer.yml \
  --ask-pass --ask-become-pass --ask-vault-pass
```

### 🚀 Publicar a agenda

Compila a aplicação, salva backup da versão anterior e publica o novo `.war`.

```bash
ansible-playbook -i inventory/hosts.yml playbooks/tarefas.yml \
  --ask-pass --ask-become-pass --ask-vault-pass
```

## 🔗 Acessos

```text
📅 Agenda:  http://SERVIDOR/tarefas/
🧰 Adminer: http://SERVIDOR/adminer/
```

## ℹ️ Observação

O console administrativo do WildFly permanece restrito ao servidor e deve ser acessado por túnel SSH.

Este repositório contém somente a automação Ansible. O código Java da agenda permanece em um repositório separado.


👨‍💻 Autor
Pablo Dantas
Infraestrutura | Cloud | DevOps
