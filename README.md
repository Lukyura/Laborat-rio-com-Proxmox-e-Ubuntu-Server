# Laboratório Proxmox VE + Ubuntu Server

Projeto prático de infraestrutura desenvolvido com o objetivo de estudar **virtualização, administração de servidores Linux, redes e acesso remoto**, utilizando o **Proxmox VE** como hypervisor e o **Ubuntu Server** como máquina virtual.

---

## Objetivo

O objetivo deste projeto foi montar um ambiente virtualizado utilizando o Proxmox VE e configurar uma máquina virtual com Ubuntu Server, aplicando na prática conceitos relacionados a:

* Virtualização
* Administração de servidores Linux
* Redes
* SSH
* Testes de conectividade
* Verificação de portas e serviços
* Troubleshooting

---

## Tecnologias utilizadas

* Proxmox VE
* Ubuntu Server
* Linux
* SSH
* TCP/IP
* Virtualização
* Interface Web
* Terminal Linux

---

## Arquitetura do ambiente

```text
Máquina Host
     │
     ▼
┌─────────────────┐
│   Proxmox VE    │
│   Hypervisor    │
└────────┬────────┘
         │
         │ Máquina Virtual
         ▼
┌─────────────────┐
│  Ubuntu Server  │
│                 │
│       SSH       │
│   Serviços      │
└─────────────────┘
```

---

## Implementação

### Instalação e configuração do Proxmox VE

Foi realizada a instalação do **Proxmox VE**, utilizado como plataforma de virtualização do laboratório.

Após a configuração inicial, o ambiente passou a ser administrado através da interface Web do Proxmox.

A interface pode ser acessada utilizando:

```text
https://IP_DO_PROXMOX:8006
```

Através do painel foi possível realizar tarefas como:

* Criação de máquinas virtuais
* Gerenciamento de CPU e memória
* Configuração de armazenamento
* Configuração de rede
* Acesso ao console das máquinas virtuais
* Gerenciamento do ambiente virtualizado

---

## Criação da máquina virtual

Dentro do Proxmox foi criada uma máquina virtual destinada ao **Ubuntu Server**.

Durante a criação da VM foram configurados recursos como:

* CPU
* Memória RAM
* Armazenamento
* Interface de rede
* Imagem ISO do Ubuntu Server

Após a configuração dos recursos, o sistema operacional foi instalado normalmente dentro da máquina virtual.

---

## Ubuntu Server

Após a instalação, o Ubuntu Server ficou operacional dentro do ambiente Proxmox.

A máquina virtual foi utilizada para praticar conceitos de administração Linux e redes, incluindo:

* Utilização do terminal
* Configuração de rede
* Identificação do endereço IP
* Comunicação entre dispositivos
* Administração remota
* Verificação de portas e serviços

---

## Testes realizados

### Teste de conectividade

Foi utilizado o comando `ping` para verificar a comunicação entre as máquinas do laboratório.

```bash
ping IP_DO_SERVIDOR
```

O teste confirmou que havia comunicação entre os dispositivos presentes na rede local.

**Resultado:** conectividade local funcionando.

---

### Acesso ao Proxmox pelo navegador

A interface administrativa do Proxmox foi acessada através do navegador utilizando a porta padrão:

```text
8006
```

Exemplo:

```text
https://192.168.x.x:8006
```

**Resultado:** painel Web acessível pela rede.

---

### Acesso remoto utilizando SSH

O Ubuntu Server foi acessado remotamente utilizando o protocolo SSH.

Exemplo:

```bash
ssh usuario@IP_DO_SERVIDOR
```

Esse teste permitiu administrar o servidor através de outra máquina da rede.

**Resultado:** acesso remoto via SSH funcionando.

---

### Verificação de portas

Também foram realizados testes para verificar quais portas estavam disponíveis no servidor.

Essa etapa foi utilizada para compreender melhor a relação entre:

```text
Serviço → Porta → Protocolo → Comunicação
```

A verificação das portas permitiu validar os serviços disponíveis na máquina virtual.

---

## Resultados

Durante o desenvolvimento do projeto foram concluídas as seguintes etapas:

* [x] Instalação do Proxmox VE
* [x] Configuração inicial do Proxmox
* [x] Acesso ao painel Web
* [x] Criação de máquina virtual
* [x] Instalação do Ubuntu Server
* [x] Inicialização e configuração básica do servidor
* [x] Comunicação entre as máquinas
* [x] Testes utilizando Ping
* [x] Acesso remoto utilizando SSH
* [x] Verificação de portas abertas
* [ ] Configuração de acesso à Internet no Ubuntu Server

---

## Problema encontrado

Durante a configuração do laboratório, a máquina virtual Ubuntu Server conseguiu estabelecer comunicação dentro da rede local, porém ainda não foi possível concluir o acesso à Internet.

A conectividade local funciona normalmente, inclusive permitindo acesso remoto por SSH.

O troubleshooting desse problema será realizado analisando principalmente:

* Configuração da interface de rede
* Endereço IP
* Gateway padrão
* DNS
* Bridge de rede do Proxmox
* Rotas de rede
* Configuração do Ubuntu Server

Alguns comandos que podem ser utilizados durante o diagnóstico:

```bash
ip addr
```

```bash
ip route
```

```bash
ping 8.8.8.8
```

```bash
ping google.com
```

```bash
resolvectl status
```

A solução encontrada será documentada futuramente neste repositório.

---

## Próximas etapas

Como evolução do laboratório, pretendo implementar:

* [ ] Resolver o acesso do Ubuntu Server à Internet
* [ ] Configurar endereço IP estático
* [ ] Configurar autenticação SSH utilizando chaves
* [ ] Desativar autenticação SSH por senha
* [ ] Configurar firewall utilizando UFW
* [ ] Implementar Fail2ban
* [ ] Analisar logs de autenticação
* [ ] Criar snapshots da máquina virtual
* [ ] Configurar backup da VM
* [ ] Realizar testes de restauração
* [ ] Implementar monitoramento básico do servidor

---

## Conhecimentos praticados

### Virtualização

* Conceito de hypervisor
* Criação de máquinas virtuais
* Configuração de recursos
* Administração através do Proxmox VE

### Linux

* Instalação do Ubuntu Server
* Administração pelo terminal
* Gerenciamento básico do sistema
* Administração remota

### Redes

* Endereçamento IP
* Comunicação entre dispositivos
* Testes de conectividade
* Portas e protocolos
* Gateway
* DNS
* Troubleshooting de rede

### Infraestrutura

* Administração de servidores
* Virtualização
* Acesso remoto
* Gerenciamento de máquinas virtuais
* Diagnóstico de problemas

---

## Status do projeto

🚧 **Em desenvolvimento**

O ambiente principal já está funcional, incluindo Proxmox VE, Ubuntu Server, comunicação local e acesso via SSH.

A próxima etapa do projeto será solucionar a conectividade externa da máquina virtual e adicionar novas configurações relacionadas à segurança, backup e administração do servidor.

---

## Autor

**Luiz Batista**

Estudante de Ciência da Computação e Técnico em Informática, com foco em **Infraestrutura, Redes, Linux e Segurança da Informação**.
