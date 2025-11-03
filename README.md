<!-- Badge Simulado: Indica que o projeto é um laboratório de redes -->
![Status](https://img.shields.io/badge/Tipo_de_Projeto-Laboratório_de_Redes-blue)
![Tecnologia](https://img.shields.io/badge/Ferramenta-Cisco_Packet_Tracer-orange)

# Projeto de Interconexão de Redes WAN (Rio de Janeiro - São Paulo)

---

## 1. Visão Geral do Projeto

Este projeto acadêmico, desenvolvido no **Cisco Packet Tracer**, simula a interconexão de duas redes locais (**LANs**) geograficamente distintas, representando filiais de uma empresa nas cidades de **Rio de Janeiro** e **São Paulo**.

O objetivo principal é demonstrar a configuração de conectividade de ponta a ponta, permitindo que todos os dispositivos (**PCs**) em ambas as filiais se comuniquem entre si, utilizando protocolos de **roteamento dinâmico** para a troca de informações de rede.

---

## 2. Topologia da Rede

A topologia é dividida em duas áreas principais, interligadas por um **link serial** (representado pela linha vermelha no Packet Tracer), simulando uma conexão **WAN (Wide Area Network)**.

### 2.1. Dispositivos Utilizados

| Filial | Dispositivo | Modelo | Função |
| :--- | :--- | :--- | :--- |
| **Rio de Janeiro** | Roteador 1 | Cisco 1841 | Roteamento interno (LAN) e externo (WAN) |
| | Switch 1 | Cisco 2950-24 | Conectividade e segmentação da LAN |
| | PCs (0, 1, 2) | PC-PT | Estações de trabalho da filial |
| **São Paulo** | Roteador 0 | Cisco 1841 | Roteamento interno (LAN) e externo (WAN) |
| | Switch 0 | Cisco 2950-24 | Conectividade e segmentação da LAN |
| | PCs (3, 4, 5) | PC-PT | Estações de trabalho da filial |

### 2.2. Diagrama da Topologia

A topologia é composta por:

*   **Duas LANs:** Uma em cada cidade, conectadas a um switch e a um roteador.
*   **Conexão WAN:** Um link serial conectando o Roteador 1 (Rio de Janeiro) ao Roteador 0 (São Paulo).

> **Nota:** O diagrama visual da topologia é crucial para a compreensão do projeto e pode ser encontrado no arquivo `aula31-10-2.pkt`. Recomenda-se incluir uma imagem da topologia neste README.

---

## 3. Configurações e Protocolos (Inferidos)

Com base na topologia padrão de laboratório, as seguintes configurações e protocolos são inferidos como necessários para o funcionamento do projeto:

### 3.1. Endereçamento IP

É essencial que cada segmento de rede (LAN e WAN) utilize uma sub-rede IP distinta.

| Segmento | Localização | Exemplo de Sub-rede (Sugestão) |
| :--- | :--- | :--- |
| **LAN 1** | Rio de Janeiro | `192.168.1.0/24` |
| **LAN 2** | São Paulo | `192.168.2.0/24` |
| **WAN** | Interconexão | `10.0.0.0/30` (Link Ponto-a-Ponto) |

### 3.2. Roteamento

Para que os PCs de uma filial se comuniquem com os PCs da outra, os roteadores devem conhecer as redes remotas. O protocolo de **roteamento dinâmico** mais provável para um projeto acadêmico como este é o **OSPF (Open Shortest Path First)** ou **EIGRP (Enhanced Interior Gateway Routing Protocol)**.

*   **Configuração de Roteamento:** Os roteadores 1 e 0 devem ser configurados para anunciar suas respectivas redes LAN e a rede WAN.
*   **Protocolo:** O protocolo de roteamento dinâmico (ex: **OSPF**) deve ser ativado em ambas as interfaces (LAN e WAN) de cada roteador.

### 3.3. Configuração de Dispositivos

| Dispositivo | Configurações Chave |
| :--- | :--- |
| **Roteadores (1841)** | Configuração de endereços IP nas interfaces LAN (**FastEthernet**) e WAN (**Serial**). Ativação do protocolo de roteamento dinâmico. Configuração de **clock rate** na interface serial do **DCE (Data Communications Equipment)**. |
| **Switches (2950-24)** | Configuração básica (hostname, senhas). As portas devem estar no modo *access* e pertencer à VLAN padrão (**VLAN 1**), a menos que haja segmentação por VLANs. |
| **PCs (PC-PT)** | Configuração de endereço IP estático ou via **DHCP** (se configurado no roteador), máscara de sub-rede e **Gateway Padrão** (o endereço IP da interface LAN do roteador). |

---

## 4. Instruções de Uso

Para utilizar e testar este projeto no Cisco Packet Tracer:

1.  **Requisito:** Instale o **Cisco Packet Tracer** (versão 7.0 ou superior).
2.  **Abrir o Arquivo:** Abra o arquivo `aula31-10-2.pkt` no software.
3.  **Verificação de Conectividade:**
    *   Aguarde até que todos os indicadores de *link* fiquem verdes (pode levar alguns segundos para o **Spanning Tree Protocol** convergir nos switches).
    *   Utilize a ferramenta **PDU Simples** (ícone de envelope fechado) para enviar um pacote de um PC em Rio de Janeiro (ex: PC0) para um PC em São Paulo (ex: PC3). O resultado deve ser **Successful**.
    *   Alternativamente, acesse o **Prompt de Comando** de qualquer PC e execute o comando:
        ```bash
        ping [Endereço IP do PC remoto]
        ```

### 4.1. Comandos de Verificação Úteis

Para verificar as configurações nos roteadores (via CLI):

| Comando | Descrição |
| :--- | :--- |
| `show ip interface brief` | Exibe o status e o endereço IP das interfaces. |
| `show ip route` | Exibe a tabela de roteamento para verificar se as redes remotas foram aprendidas. |
| `show running-config` | Exibe a configuração atual do dispositivo. |
| `show cdp neighbors` | Exibe informações sobre dispositivos Cisco vizinhos. |

---

## 5. Contexto Acadêmico

Este laboratório é ideal para a prática e demonstração dos seguintes conceitos de redes de computadores:

*   **Roteamento Inter-Redes:** Como roteadores conectam diferentes sub-redes.
*   **Protocolos de Roteamento Dinâmico:** Implementação e verificação de **OSPF** ou **EIGRP**.
*   **Configuração de Interfaces WAN:** Uso de interfaces seriais e o conceito de **clock rate**.
*   **Conectividade de Camada 2 e 3:** Diferença entre o papel do Switch (LAN) e do Roteador (WAN).

