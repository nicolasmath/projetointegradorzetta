![GitHub License](https://img.shields.io/github/license/nicolasmath/lab-redes-01)

# Projeto Integrador - Implantação de Infraestrutura de TI

**Empresa:** Zetta

**Slogan:** Soluções tecnológicas e suporte em TI.

<p align="center">
  <img src="Logotipo.png" alt="Zetta" width="450">
</p>

Alunos: Nicolas, Anna, Rafael, Sara, Gabriel M., Levy.

---

## 📝 Sobre a Empresa

### Missão
Nossa missão é alinhar processos, blindar servidores e garantir o fluxo contínuo de dados, entregando um suporte em TI tão fluido, inteligente e sob medida que se torna invisível no dia a dia dos nossos parceiros.

### Visão
Ser a principal referência em terceirização e infraestrutura de TI para empresas prestadoras de serviços, alcançando a marca de 100% de disponibilidade dos ambientes gerenciados e expandindo nossa operação com soluções automatizadas e alta retenção de clientes.

### Organograma Simplificado

* **Diretoria:** CEO e CTO
* **Administrativo / Financeiro:** RH e Faturamento
* **Recepção:** Atendimento Inicial e Triagem
* **Suporte Técnico / Operações:** Analistas de Infraestrutura, Redes e Helpdesk

**Quantidade de Funcionários:** 15 colaboradores.

### Planta Baixa do Escritório

<p align="center">
  <img src="PlantaescritórioTI.png" alt="Logo Hair Hi-Tech" width="700">
</p>

---

## 👥 Integrantes do Grupo e Funções (Kanban)

* **[Nicolas e Anna]** - Scrum Master & Sysadmin Windows (Active Directory, DNS, DHCP e GPOs).
* **[Gabriel Monteiro e Sara]** - Sysadmin Linux & DevOps (Servidor Web Apache/Nginx, Banco de Dados e GLPI).
* **[Rafael e Levy]** - Engenheiro de Redes (Topologias e Configurações no Cisco Packet Tracer).

---

## 🛠️ Projeto de Rede (Cisco Packet Tracer)

A rede está estruturada na subrede **192.168.20.0/24** para organizar os ativos de forma estática e as estações de trabalho via DHCP.

<h3 align="center">🌐 Topologia Lógica da Rede</h3>
<p align="center">
  <img src="Topologia.png" alt="Topologia da Rede - Cisco Packet Tracer" width="750">
</p>

### Plano de Endereçamento IP

| Equipamento / Serviço | Endereço IP | Interface | Função no Projeto |
| :--- | :--- | :--- | :--- |
| **Gateway / Firewall** | `192.168.20.1` | Gig0/0/1 | Roteamento de borda e segurança |
| **Windows Server (AD/DNS)** | `192.168.20.10` | FE0 | Controlador de Domínio e escopo DHCP |
| **Linux Server (GLPI)** | `192.168.20.20` | FE0 | Sistema de chamados técnicos |
| **Linux Server (Web/Wiki)** | `192.168.20.30` | FE0 | Aplicação Web Corporativa |
| **Impressora de Rede** | `192.168.20.50` | FE0 | Impressora compartilhada do escritório |
| **Access Point (Wi-Fi)** | `192.168.20.60` | Port 0 | Distribuição de sinal sem fio (SSID: Zetta) |
| **Estações de Trabalho** | DHCP | FE0 / Dynamic | IPs distribuídos do `.100` ao `.200` |

---

### Topologia Lógica do Cenário

<p align="center">
  <img src="cenário.png" alt="Logo Hair Hi-Tech" width="500">
</p>

---

## 📂 Estrutura de Pastas do Repositório

* `/packet-tracer`: Arquivos `Topologia Zetta.pkt` das topologias física e lógica.
* `/documentacao`: Planta baixa do escritório, relatórios e atas de reuniões.
* `/scripts`: Scripts de automação ou arquivos de configuração dos servidores (Windows/Linux).

---

## 📸 Galeria de Implementação Física e Fases do Projeto

Abaixo está o registro cronológico das etapas de montagem, configuração e testes da nossa infraestrutura real.

---

### 🧱 Fase 1: Infraestrutura Física e Cabeamento
*Nesta etapa, realizamos a identificação dos equipamentos de hardware, montagem dos racks e a confecção/crimpagem dos cabos de rede Cat.6 para interligar os computadores.*

<p align="center">
  <img src="Switch.jpg" alt="Montagem do Hardware e Racks" width="400" style="margin: 10px;">
  <img src="Crimpagem.jpg" alt="Crimpagem e Organização dos Cabos" width="400" style="margin: 10px;">
</p>

---

### 💿 Fase 2: Instalação de Sistemas e Provisionamento
*Instalação dos Sistemas Operacionais nas máquinas físicas. Configuração do ambiente de testes e carregamento de drivers específicos (como Intel RST) para o perfeito reconhecimento e desempenho dos SSDs e storages.*

<p align="center">
  <img src="Debian.jpg" alt="Instalação do SO nas Máquinas" width="400" style="margin: 10px;">
  <img src="Win.jpg" alt="Configuração de Hipervisores e Servidores" width="400" style="margin: 10px;">
</p>

---

### 🔑 Fase 3: Configuração dos Serviços de Rede
*Momento em que os Sysadmins e Engenheiros de Rede colocaram a inteligência do projeto para rodar: criação do Controlador de Domínio no Windows Server, subida das diretivas (GPOs), escopo DHCP ativo e inicialização dos servidores Linux (GLPI e Web).*

<p align="center">
  <img src="dhcp-active.jpg" alt="Painel do Active Directory e DHCP" width="400" style="margin: 10px;">
  <img src="documentacao/fotos/fase3_linux_glpi.jpg" alt="Servidores Linux e Tela de Chamados GLPI" width="400" style="margin: 10px;">
</p>

---

### 🧪 Fase 4: Testes de Conectividade e Homologação
*Validação final de que tudo funciona de verdade no mundo real. Telas comprovando o recebimento de IPs automáticos pelas estações de trabalho, testes de ping e o funcionamento do Firewall de borda isolando a rede.*

<p align="center">
  <img src="documentacao/fotos/fase4_testes_ping.jpg" alt="Testes de Conectividade com Ping" width="400" style="margin: 10px;">
  <img src="documentacao/fotos/fase4_homologacao.jpg" alt="Infraestrutura Pronta e Funcionando" width="400" style="margin: 10px;">
</p>
