# 🛡️ Packet Tracer - Examine NAT on a Wireless Router

> **Cisco Packet Tracer Lab**
>
> **Autor:** Jordão Paulo  
> **Categoria:** Redes de Computadores • Cisco Packet Tracer • Cisco Networking Academy (NetAcad)  
> **Nível:** Iniciante

---

# 📖 Descrição

Este laboratório apresenta uma atividade prática no **Cisco Packet Tracer** destinada à compreensão do funcionamento do **Network Address Translation (NAT)** em um **Wireless Router**.

O cenário permite observar como dispositivos de uma rede interna utilizam **endereços IPv4 privados** para se comunicar com uma rede externa, enquanto o Wireless Router realiza a tradução desses endereços para permitir o acesso a recursos localizados na Internet.

Durante o laboratório, serão configurados quatro computadores para obter endereços IP automaticamente através do **DHCP** disponibilizado pelo Wireless Router. Em seguida, será analisado o tráfego gerado pelos dispositivos e o processo de tradução realizado pelo NAT.

A atividade também utiliza o **Simulation Mode** do Cisco Packet Tracer para permitir a análise detalhada dos pacotes, incluindo os endereços IP de origem e destino antes e depois da passagem pelo roteador.

---

# 🎯 Objectives

Ao concluir este laboratório, o estudante será capaz de:

- Examinar a configuração de NAT em um Wireless Router;
- Configurar quatro PCs para obter endereços IP através de DHCP;
- Compreender a utilização de endereços IPv4 privados em uma rede interna;
- Examinar o tráfego que atravessa a rede;
- Observar o processo de tradução de endereços realizado pelo NAT;
- Analisar os cabeçalhos dos pacotes antes e depois da tradução.

---

# 🏗️ Topologia do Laboratório

```mermaid
flowchart LR
    PC0["PC0"]
    PC1["PC1"]
    PC2["PC2"]
    PC3["PC3"]

    WR["Wireless Router<br/>DHCP • NAT"]

    ISP["Internet / ISP"]
    SERVER["Web Server<br/>ciscolearn.nat.com"]

    PC0 -->|Ethernet| WR
    PC1 -->|Ethernet| WR
    PC2 -->|Ethernet| WR
    PC3 -->|Ethernet| WR

    WR -->|NAT / Internet| ISP
    ISP --> SERVER

    subgraph LAN["Rede Interna • Endereços Privados"]
        PC0
        PC1
        PC2
        PC3
        WR
    end

    subgraph WAN["Rede Externa"]
        ISP
        SERVER
    end
````

## 🚀 Como Executar o Laboratório

Para praticar, você precisa ter o **Cisco Packet Tracer** instalado. Clique no botão abaixo para baixar o arquivo do projeto:

[![Baixar Laboratório](https://img.shields.io/badge/Download-Clique%20Aqui-green?style=for-the-badge&logo=cisco)](https://raw.githubusercontent.com/unknown-code7/configure-wireless-router-and-client/main/Configure%20a%20Wireless%20Router%20and%20Client.pka)

[![Assistir Tutorial](https://img.shields.io/badge/Assistir_Tutorial-Clique_Aqui-blue?style=for-the-badge&logo=facebook)](https://www.facebook.com/share/v/18rSKRXpVg/)

---

# 🧪 Part 1: Examine the configuration for accessing external network

### a. Conectar o primeiro PC

Adicione **1 PC** e conecte-o ao **Wireless Router** utilizando um **cabo Copper Straight-Through**.

Aguarde até que todos os indicadores das interfaces fiquem verdes antes de continuar ou utilize a opção **Fast Forward**.

### b. Configurar o PC via DHCP

No PC:

**Desktop → IP Configuration → DHCP**

A opção **DHCP** permitirá que o dispositivo receba automaticamente um endereço IP disponibilizado pelo servidor DHCP do Wireless Router.

### c. Identificar o Default Gateway

Observe o endereço IP apresentado no campo **Default Gateway**.

Esse endereço corresponde ao gateway utilizado pelo PC para alcançar redes externas.

Feche a janela **IP Configuration** após verificar as informações.

### d. Acessar a interface do Wireless Router

Abra o **Web Browser** do PC e introduza o endereço IP do **Default Gateway** no campo de URL.

Quando solicitado, utilize:

* **Username:** `admin`
* **Password:** `admin`

### e. Acessar o Status do roteador

Na interface Web do Wireless Router, selecione a opção **Status**, localizada no canto superior direito.

Essa opção apresenta as informações de estado e configuração do roteador.

### f. Examinar a conexão com a Internet

Na página do roteador, localize a seção referente à **Internet Connection**.

O endereço IP apresentado nessa seção corresponde ao endereço atribuído pelo **ISP** à interface de Internet do Wireless Router.

Caso apareça:

```text
0.0.0.0
```

aguarde alguns segundos e atualize ou reabra a página. O Wireless Router pode ainda estar obtendo um endereço IP através do servidor DHCP do ISP.

### ❓ Question

**O endereço IP atribuído à interface de Internet é um endereço privado ou público?**

---

# 🌐 Part 2: Examine the configurations for accessing the internal network

### a. Acessar Local Network

Na barra do submenu **Status**, selecione:

**Local Network**

### b. Examinar a rede interna

Role a página para baixo e examine as informações referentes à **Local Network**.

O endereço apresentado corresponde ao endereço utilizado pela rede interna do Wireless Router.

### c. Examinar o servidor DHCP

Continue descendo a página para visualizar as informações do **DHCP Server**.

Observe:

* Endereço da rede interna;
* Endereço do gateway;
* Servidor DHCP;
* Faixa de endereços IP disponibilizados aos hosts conectados.

### ❓ Question

**Os endereços utilizados na rede interna são privados ou públicos?**

### d. Encerrar a configuração

Após concluir a análise, feche a janela de configuração do Wireless Router.

---

# 💻 Part 3: Connect 3 PCs to the wireless router

### a. Adicionar os computadores

Adicione **3 PCs adicionais** ao cenário.

Conecte cada PC ao Wireless Router utilizando **cabos Copper Straight-Through**.

Aguarde até que todos os indicadores das interfaces fiquem verdes ou utilize **Fast Forward**.

### b. Configurar os PCs via DHCP

Em cada PC:

**Desktop → IP Configuration → DHCP**

Cada dispositivo deverá receber automaticamente um endereço IP através do servidor DHCP configurado no Wireless Router.

Feche a janela **IP Configuration** após a configuração.

### c. Verificar a configuração IP

Em cada PC, abra:

**Desktop → Command Prompt**

Execute:

```text
ipconfig /all
```

Utilize o comando para verificar:

* Endereço IPv4;
* Máscara de sub-rede;
* Default Gateway;
* Informações relacionadas ao DHCP.

> **Nota:** Os computadores receberão endereços IPv4 privados. Esses endereços não podem ser utilizados diretamente para atravessar a Internet. Por isso, o Wireless Router precisa realizar uma **tradução NAT** antes que o tráfego alcance a rede externa.

---

# 🔄 Part 4: View NAT translation across the wireless router

Nesta etapa será utilizado o **Simulation Mode** do Cisco Packet Tracer para observar o tráfego atravessando o Wireless Router.

### a. Entrar no Simulation Mode

Clique na aba:

**Simulation**

A aba está localizada no canto inferior direito da interface do Cisco Packet Tracer, ao lado de **Realtime**, e possui o símbolo de um cronômetro.

### b. Criar um Complex PDU

No **Simulation Panel**:

1. Clique em **Show All/None** para remover os eventos atualmente selecionados;
2. Clique em **Edit Filters**;
3. Na aba **Misc**, marque:

   * **TCP**
   * **HTTP**
4. Feche a janela de filtros;
5. Clique no ícone de **Complex PDU** representado pelo envelope aberto;
6. Selecione um dos PCs como dispositivo de origem.

### c. Configurar o Complex PDU

Na janela **Create Complex PDU**, configure:

**PDU Settings**

* **Application:** `HTTP`

**Destination**

* Selecione o servidor **ciscolearn.nat.com**.

**Source Port**

```text
1000
```

**Simulation Settings**

* **Periodic:** selecionado;
* **Interval:** `120` segundos.

Após configurar os parâmetros, clique em:

**Create PDU**

### d. Expandir o Simulation Panel

Clique duas vezes no **Simulation Panel** para desbloqueá-lo da janela principal do Packet Tracer.

Isso permitirá movimentar o painel e visualizar toda a topologia da rede.

### e. Observar o tráfego

Clique em:

**Play**

no Simulation Panel para iniciar a simulação.

O controle de velocidade pode ser deslocado para a direita para acelerar a animação.

> **Nota:** Caso apareça a mensagem **Buffer Full**, utilize a opção **View Previous Events** para continuar examinando os eventos anteriores.

---

# 📦 Part 5: View the header information of the packets

Nesta etapa será realizada uma análise dos cabeçalhos dos pacotes que percorrem a rede entre um PC e o servidor Web.

### a. Examinar os pacotes

No **Simulation Panel**:

1. Localize a lista de eventos;
2. Dê duplo clique na **3ª linha** da lista de eventos;
3. Um envelope representando o evento será apresentado na área de trabalho;
4. Clique no envelope para visualizar as informações do pacote.

### b. Examinar o Inbound PDU

Selecione a aba:

**Inbound PDU Details**

Examine as informações do pacote, principalmente:

* **SRC IP Address**
* **Destination IP Address**

Registre o endereço IP de origem apresentado.

### c. Examinar o Outbound PDU

Agora selecione:

**Outbound PDU Details**

Compare novamente:

* **SRC IP Address**
* **Destination IP Address**

Observe especialmente a alteração no **SRC IP Address**.

Essa alteração demonstra o processo de **NAT**, no qual o endereço IP privado utilizado pelo dispositivo interno é traduzido pelo Wireless Router antes que o pacote seja encaminhado para a rede externa.

### d. Examinar outros eventos

Clique em diferentes linhas da lista de eventos para acompanhar os cabeçalhos dos pacotes durante as diferentes etapas da comunicação.

Observe como as informações dos pacotes podem mudar conforme eles atravessam os dispositivos da topologia.

### e. Verificar o resultado

Após concluir a atividade, clique em:

**Check Results**

para verificar o resultado do laboratório.

---

# 🧠 Conceitos Abordados

* Network Address Translation (NAT)
* IPv4
* Endereços IP privados
* Endereços IP públicos
* DHCP
* Default Gateway
* Wireless Router
* LAN
* WAN
* TCP
* HTTP
* Complex PDU
* Simulation Mode
* Packet Headers
* Source IP
* Destination IP
* Cisco Packet Tracer

---

# 🔍 O que observar durante o laboratório

O principal objetivo desta atividade é compreender a diferença entre o endereço utilizado pelo dispositivo dentro da **LAN** e o endereço utilizado pelo Wireless Router ao acessar a **rede externa**.

O fluxo básico pode ser representado da seguinte forma:

```text
PC
│
│ IP Privado
▼
Wireless Router
│
│ NAT
│
│ IP Público
▼
Internet
│
▼
ciscolearn.nat.com
```

Antes do NAT, o pacote utiliza o endereço IP privado do PC como origem.

Após atravessar o Wireless Router, o endereço de origem é traduzido para o endereço utilizado na interface externa do roteador.

---

# 🎓 Competências Desenvolvidas

Ao concluir este laboratório, o estudante será capaz de:

* Identificar endereços IPv4 privados e públicos;
* Compreender a função do DHCP em uma rede doméstica;
* Identificar o Default Gateway de um host;
* Compreender o funcionamento básico do NAT;
* Analisar alterações nos cabeçalhos dos pacotes;
* Utilizar o Simulation Mode do Cisco Packet Tracer;
* Analisar tráfego TCP/HTTP;
* Interpretar o processo de comunicação entre uma LAN e uma rede externa.

---

# 📌 Resultado Esperado

Ao final do laboratório, os quatro PCs deverão estar conectados ao Wireless Router e obter automaticamente seus endereços IPv4 através do **DHCP**.

Os computadores deverão utilizar endereços privados na rede interna, enquanto o Wireless Router realizará a tradução **NAT** para permitir a comunicação com o servidor Web externo.

A análise realizada no **Simulation Mode** deverá permitir identificar a alteração do endereço IP de origem dos pacotes durante a passagem pelo Wireless Router.

---

# 🛠️ Tecnologias e Ferramentas

* Cisco Packet Tracer
* IPv4
* DHCP
* NAT
* TCP
* HTTP
* Ethernet
* Wireless Router
* Simulation Mode
* Complex PDU

---

# 👨‍💻 Autor

**Jordão Paulo**

**Analista de Cibersegurança** • **Analista de Redes** • **Infraestrutura de TI**

Criador da série **Laboratórios Cisco NetAcad**, dedicada ao ensino prático de Redes de Computadores, Infraestrutura de TI e Cibersegurança utilizando o Cisco Packet Tracer.

---

© 2026 Jordão Paulo. Todos os direitos reservados.

```
```
