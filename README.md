# Proxmox VE + Ubuntu Server Lab

Laboratório prático de **virtualização e infraestrutura**, desenvolvido para estudar a instalação e administração do **Proxmox VE**, criação de máquinas virtuais, configuração de rede e instalação de um servidor Linux.

O ambiente foi construído utilizando **virtualização aninhada**, com o Proxmox VE executado dentro do VirtualBox e uma máquina virtual Ubuntu Server criada posteriormente dentro do próprio Proxmox.

> 🚧 **Projeto em desenvolvimento:** o ambiente virtualizado está funcional, porém a conectividade do Ubuntu Server com a Internet ainda está pendente de configuração.

---

## Objetivo

O objetivo deste projeto foi sair da parte puramente teórica e montar um pequeno laboratório para praticar conceitos relacionados a:

* Virtualização
* Hypervisores
* Proxmox VE
* Linux
* Ubuntu Server
* Redes
* Bridges de rede
* Administração de máquinas virtuais
* Troubleshooting

Além da instalação do ambiente, o projeto também envolveu a resolução de problemas encontrados durante a configuração.

---

## Arquitetura do laboratório

O laboratório utiliza virtualização aninhada:

```text
Windows Host
    │
    ▼
VirtualBox
    │
    ▼
Proxmox VE 9.2
    │
    └── VM 100
         │
         ▼
    Ubuntu Server
```

Ou seja, o **Proxmox VE não está instalado diretamente em hardware físico**.

Ele funciona como uma máquina virtual dentro do VirtualBox exclusivamente para fins de estudo e laboratório.

---

## Tecnologias utilizadas

* Proxmox VE 9.2
* VirtualBox
* Ubuntu Server
* Linux
* Virtualização aninhada
* Bridge de rede
* VirtIO
* TCP/IP
* Interface Web do Proxmox

---

# Desenvolvimento do laboratório

## 1. Criação da VM do Proxmox

Inicialmente foi criada uma máquina virtual no VirtualBox para receber a instalação do Proxmox VE.

Durante essa etapa foi necessário configurar recursos como:

* CPU
* Memória RAM
* Disco virtual
* Interface de rede
* ISO do Proxmox VE
* Virtualização aninhada

---

## 2. Instalação do Proxmox VE

Após a criação da máquina virtual, foi realizada a instalação do **Proxmox VE 9.2**.

Depois da instalação, o Proxmox passou a ser administrado principalmente através de sua interface Web.

O endereço configurado no laboratório foi:

```text
https://192.168.1.200:8006
```

Configuração utilizada:

```text
IP:      192.168.1.200
Gateway: 192.168.1.1
Porta:   8006
```

---

## 3. Configuração da rede

Uma das principais etapas do laboratório foi a configuração de rede.

Inicialmente, o Proxmox estava utilizando uma interface configurada em **NAT pelo VirtualBox**, recebendo um endereço da rede:

```text
10.0.2.x
```

Essa configuração limitava a comunicação desejada entre o laboratório e a rede local.

Posteriormente, a configuração do VirtualBox foi alterada para utilizar **Bridge**, permitindo que o Proxmox participasse diretamente da mesma rede do computador host.

Após a alteração, foi utilizado:

```text
192.168.1.200
```

como endereço do Proxmox.

---

## Bridge do Proxmox

Dentro do Proxmox, a bridge utilizada pelas máquinas virtuais foi:

```text
vmbr0
```

Ela permite conectar as interfaces virtuais das VMs à infraestrutura de rede configurada no host Proxmox.

A VM Ubuntu Server também foi associada à:

```text
vmbr0
```

---

# Problemas encontrados e troubleshooting

Uma parte importante deste laboratório foi justamente lidar com erros reais durante a configuração.

---

## Problema 1 — Proxmox inacessível pela rede

### Situação

Inicialmente, o Proxmox estava utilizando NAT no VirtualBox e recebeu um endereço semelhante a:

```text
10.0.2.15
```

Isso dificultava o acesso ao ambiente a partir da rede local.

### Solução

A interface de rede da VM no VirtualBox foi alterada de:

```text
NAT
```

para:

```text
Bridge
```

Depois disso, o Proxmox passou a utilizar um endereço da mesma rede do computador host:

```text
192.168.1.200
```

Com isso, a interface Web passou a ser acessível através do navegador.

---

## Problema 2 — Referências ao endereço IP antigo

Após a alteração da configuração de rede, algumas referências ao endereço anterior ainda permaneceram no sistema.

Foram verificadas configurações como:

```bash
/etc/hosts
```

e:

```bash
/etc/issue
```

para remover ou atualizar referências relacionadas ao endereço antigo.

Essa etapa ajudou a manter a configuração do ambiente consistente com o novo endereço IP.

---

## Problema 3 — KVM indisponível

Durante a criação da máquina virtual dentro do Proxmox, foi encontrado um problema relacionado ao **KVM**.

Como o Proxmox já estava sendo executado dentro do VirtualBox, era necessário permitir que ele tivesse acesso aos recursos de virtualização do processador físico.

### Solução

Foi habilitado o recurso de **Nested VT-x/AMD-V** no VirtualBox.

Isso permitiu utilizar virtualização aninhada:

```text
CPU física
    ↓
VirtualBox
    ↓
Proxmox
    ↓
Ubuntu Server
```

Depois dessa alteração, foi possível continuar a criação e inicialização da VM.

---

## Problema 4 — VM bloqueada

Durante os testes com a máquina virtual, ocorreu uma situação em que a VM ficou bloqueada.

Foi utilizado o comando:

```bash
qm unlock 100
```

onde:

```text
100
```

corresponde ao ID da máquina virtual Ubuntu Server.

Isso permitiu desbloquear a VM e continuar sua administração pelo Proxmox.

---

## Problema 5 — Boot utilizando a ISO

Após concluir a instalação do Ubuntu Server, foi necessário ajustar o boot da máquina virtual.

A ISO utilizada durante a instalação ainda estava associada à VM.

Ela foi removida/desconectada para que a máquina passasse a iniciar diretamente pelo disco virtual onde o Ubuntu Server havia sido instalado.

---

## Problema 6 — Layout do teclado

Durante a utilização do terminal foi necessário ajustar o layout do teclado.

Foi utilizado:

```bash
setupcon
```

para aplicar a configuração apropriada no console Linux.

---

# Máquina virtual Ubuntu Server

Depois da configuração do Proxmox foi criada uma máquina virtual para instalação do **Ubuntu Server**.

Informações do laboratório:

```text
VM ID: 100
Sistema: Ubuntu Server
Bridge: vmbr0
Interface virtual: VirtIO
```

O hostname utilizado durante os testes foi:

```text
lab-1
```

---

## Recursos configurados

Durante a criação da VM foram configurados:

* CPU virtual
* Memória RAM
* Disco virtual
* ISO do Ubuntu Server
* Interface de rede VirtIO
* Bridge `vmbr0`

Após a instalação, o Ubuntu Server conseguiu inicializar normalmente dentro do Proxmox.

---

# Estado atual

Atualmente o ambiente possui:

* [x] VirtualBox configurado
* [x] Proxmox VE instalado
* [x] Virtualização aninhada funcionando
* [x] Interface Web do Proxmox acessível
* [x] Proxmox conectado à rede utilizando Bridge
* [x] Bridge `vmbr0` configurada
* [x] Máquina virtual criada
* [x] Ubuntu Server instalado
* [x] Ubuntu Server inicializando pelo disco virtual
* [x] Interface VirtIO configurada na VM
* [ ] Acesso do Ubuntu Server à Internet

---

# Pendência atual — conectividade do Ubuntu Server

A principal pendência do projeto atualmente está relacionada à rede da máquina virtual Ubuntu Server.

O Proxmox possui acesso pela rede e sua interface Web funciona normalmente, porém a conectividade externa da VM ainda precisa ser solucionada.

O próximo troubleshooting será realizado verificando diferentes camadas da configuração.

---

## Verificar a interface de rede

```bash
ip a
```

Esse comando permite verificar:

* interfaces existentes;
* endereço IP;
* estado da interface;
* máscara de rede.

---

## Verificar as rotas

```bash
ip route
```

O objetivo é confirmar principalmente a existência de uma rota padrão:

```text
default via GATEWAY
```

---

## Testar comunicação com o gateway

```bash
ping 192.168.1.1
```

Se funcionar, significa que a VM consegue alcançar o gateway da rede local.

---

## Testar acesso externo sem DNS

```bash
ping 8.8.8.8
```

Se esse teste funcionar, mas nomes de domínio não funcionarem, o problema provavelmente estará relacionado ao DNS.

---

## Testar DNS

```bash
ping google.com
```

Também podem ser verificadas as configurações utilizando:

```bash
resolvectl status
```

---

## Pontos que ainda serão analisados

* Endereço IP do Ubuntu Server
* Máscara de rede
* Gateway
* DNS
* Configuração da `vmbr0`
* Interface VirtIO
* Netplan do Ubuntu
* Rotas de rede
* Configuração da bridge no VirtualBox
* Comunicação VM → Proxmox → rede física

---

# Próximas etapas

Depois de solucionar a conectividade, pretendo continuar evoluindo o laboratório.

### Rede

* [ ] Resolver acesso à Internet
* [ ] Configurar IP estático
* [ ] Validar gateway
* [ ] Configurar DNS
* [ ] Documentar a solução do problema

### Administração Linux

* [ ] Criar usuário administrativo
* [ ] Configurar acesso SSH
* [ ] Configurar autenticação utilizando chave SSH
* [ ] Revisar permissões e usuários

### Segurança

* [ ] Configurar UFW
* [ ] Liberar apenas portas necessárias
* [ ] Configurar Fail2ban
* [ ] Analisar logs de autenticação

### Proxmox

* [ ] Criar snapshots
* [ ] Configurar backup da VM
* [ ] Testar restauração
* [ ] Monitorar utilização de CPU, memória e armazenamento

---

# Conhecimentos praticados

Durante o projeto foram praticados conceitos relacionados a:

## Virtualização

* Hypervisores
* Máquinas virtuais
* Virtualização aninhada
* KVM
* Alocação de recursos
* VirtIO

## Proxmox

* Instalação do Proxmox VE
* Interface administrativa Web
* Criação e gerenciamento de VMs
* Configuração de bridge
* Gerenciamento de discos e ISOs
* Console de máquinas virtuais
* Troubleshooting de VMs

## Linux

* Ubuntu Server
* Terminal Linux
* Configuração básica do sistema
* Interfaces de rede
* Rotas
* Diagnóstico de conectividade

## Redes

* NAT
* Bridge
* Endereçamento IPv4
* Gateway
* DNS
* Interfaces virtuais
* Troubleshooting de conectividade

---

# O que aprendi com o projeto

Além da instalação das ferramentas, o laboratório permitiu entender melhor como diferentes camadas de virtualização e rede se relacionam.

Um dos principais aprendizados foi a diferença prática entre utilizar **NAT e Bridge** em uma máquina virtual.

Também foi possível entender melhor como funciona a virtualização aninhada, já que o ambiente utiliza:

```text
VirtualBox
    ↓
Proxmox VE
    ↓
Ubuntu Server
```

Os problemas encontrados durante a configuração também foram importantes para praticar troubleshooting em vez de simplesmente seguir uma instalação pronta.

O projeto ainda não está finalizado e continuará sendo atualizado conforme novas configurações forem implementadas e os problemas restantes forem solucionados.

---

## Status

🚧 **Em desenvolvimento**

### Próximo objetivo

> Resolver a conectividade com a Internet da VM Ubuntu Server e documentar a causa e a solução encontrada.

---

## Autor

**Luiz Batista**

Estudante de Ciência da Computação e Técnico em Informática, com foco em infraestrutura, redes, Linux e segurança da informação.
