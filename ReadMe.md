# Oracle Cloud Infrastructure Foundations – Resumo de Estudos

<div align="center"><img src="slides/SaaS.png" alt="SaaS" width="600" height="300" /></div>

## 1. OCI Architecture

### 🌐 Conceitos Fundamentais
<div align="center"><img src="slides/architecture.png" alt="architecture" width="600" height="300" /></div>

- **Tenancy** 🏢: Raiz lógica da sua presença na OCI (parecido com uma “organização”). Tudo — usuários, políticas, compartments e recursos — existe dentro dela.  
- **Region** 📍: Conjunto geograficamente isolado de infraestrutura (ex.: `sa-saopaulo-1`). Cada região é independente em energia, rede e capacidade.  
- **Availability Domain (AD)** 🏬🏬🏬: Data centers independentes dentro de uma região. Falha em um AD não impacta os outros → alta disponibilidade.  
- **Fault Domain (FD)** 🧩: Partições lógicas dentro de um AD (3 por AD). Distribuir instâncias entre FDs evita que manutenção ou falha de rack derrube todo o serviço.  
<div align="center"><img src="slides/schema.png" alt="schema" width="600" height="300" /></div>
- **VCN (Virtual Cloud Network)** 🔗: Rede virtual isolada (CIDR escolhido) onde vivem subnets, roteamento e segurança.  
  - **Subnet Regional** 🌍: Vale para todos os ADs, simplifica failover.  
  - **Subnet AD-Local** 📦: Fixa recursos em um AD específico.  
- **Redundância / Alta Disponibilidade** ♻️: Replicar entre ADs/FDs ou usar serviços multi‑AD (Load Balancer, Autonomous DB).  
- **Disaster Recovery (DR)** 🚨: Replicação entre regiões (Object Storage Cross-Region, Block Volume Replication, Autonomous Data Guard).  
- **Edge Services** 🌍⚡: POPs para DNS, WAF, Email Delivery diminuem latência até o usuário final.  
- **Armazenamento** 💾: Object Storage (standard/archival), Block Volume (replicação automática entre FDs), File Storage (NFS), Archive.  
- **Observabilidade** 👁️: Logging, Monitoring, Events e Alarms para detectar e responder a incidentes.  
- **Rede e Segurança** 🔐: Route Tables, Security Lists, Network Security Groups, Internet/NAT/Service Gateways, Local/Remote Peering.  

### 📦 Sintaxe / Identificação dos Serviços OCI

#### OCIDs (Oracle Cloud IDs)
Cada recurso possui um identificador global único:  
`ocid1.<resource_type>.<realm>.<region>.<id>`  
Exemplo: `ocid1.instance.oc1.sa-saopaulo-1.abcd...`  
`<resource_type>` exemplos: `instance`, `subnet`, `vcn`, `bucket`, `autonomousdatabase`, `user`, `compartment`.
<div align="center"><img src="slides/OCID.png" alt="OCID" width="600" height="300" /></div>

#### Tipos Agregados (Resource Families)
Usados para simplificar políticas de autorização:

| Família (`*-family`) | Abrange |
|----------------------|--------|
| `instance-family` | Instâncias, boot volumes, attach/detach |
| `volume-family` | Block Volumes e backups |
| `object-family` | Buckets e objetos (Object Storage) |
| `database-family` | DB Systems, Autonomous Databases |
| `virtual-network-family` | VCN, subnets, route tables, gateways |
| `functions-family` | Oracle Functions |
| `management-dashboard-family` | Dashboards de observabilidade |
| `logs-family` | Logging |
| `keys-family` | Vault Keys |
| `all-resources` | Todos os recursos (usar só para admins) |

(Existem outras famílias específicas, mas estas são as principais.)

#### Tipos de Acesso (Verbos / Ações)
Hierarquia – cada nível inclui os anteriores:  
`inspect < read < use < manage`

- **inspect**: Listar metadados (nomes, OCIDs) – sem conteúdo.  
- **read**: `inspect` + ler conteúdo (ex.: baixar objeto).  
- **use**: `read` + executar operações funcionais (start/stop instância, gerar tokens).  
- **manage**: Controle total (criar, atualizar, deletar, alterar políticas internas).  

Também existem permissões específicas usadas em condições ou instruções finas (ex.: `read keys`, `use buckets`, `manage object-family`).

### 🔑 Sintaxe de Policies (AuthZ)

Estrutura básica (uma linha por instrução):  
`Allow <principal-type> <principal-name> to <verb> <resource-type|family> in <scope> [where <conditions>]`

Componentes:
- **principal-type**: `group` | `dynamic-group` | `service`
- **principal-name**: nome do grupo/dynamic group
- **verb**: `inspect|read|use|manage` ou ação específica
- **resource-type|family**: `instance-family`, `buckets`, `all-resources` etc.
- **scope**: `tenancy` ou `compartment <nome|ocid>`
- **conditions (opcional)**: filtros com tags ou atributos

Exemplos de policies:
Allow group Admins to manage all-resources in tenancy
Allow group Devs to use instance-family in compartment Dev
Allow dynamic-group BatchInstances to use object-family in compartment Shared where any { request.permission='OBJECT_CREATE' }
Allow group Auditors to read audit-events in tenancy


Condições comuns:
- `request.permission = '<permissão>'`
- `target.compartment.id = 'ocid1.compartment...'`
- `target.resource.tag.<namespace>.<key> = 'valor'`

### 🧩 Comparação com Concorrentes
| Conceito OCI | AWS | Azure | GCP |
|--------------|-----|-------|-----|
| Tenancy 🏢 | Account | Subscription | Project |
| Region 📍 | Region | Region | Region |
| Availability Domain 🏬 | Availability Zone | Availability Zone | Zone |
| Fault Domain 🧩 | (Partition Placement) | Fault Domain | (Distribuir entre Zones) |
| Compartments 📂 | Accounts/OUs + Tags | Resource Groups | Folders/Projects |
| VCN 🔗 | VPC | VNet | VPC |
| Service Gateway 🛰️ | VPC Endpoint / PrivateLink | Private Link / Service Endpoint | Private Service Connect |
| Cross-Region DR 🚨 | S3 CRR / RDS Replicas | GRS Storage / Geo-Rep | Multi-/Dual-Region Storage |
| Edge DNS/WAF 🌍 | Route53 / CloudFront WAF | Azure DNS / Front Door | Cloud DNS / Cloud Armor |

---

## 2. Identity and Access Management (IAM)

<div align="center"><img src="slides/Indentity Concepts.png" alt="Identity Concepts" width="600" height="300" /></div>

### 🔐 IAM Introduction
Gerencia identidades (usuários, grupos, recursos) e permissões via policies legíveis. Integração com federação SAML/OAuth, MFA e identidades gerenciadas (Instance/Resource Principals).

### 📂 Compartments & 🪪 Identity Domains
<div align="center"><img src="slides/compartment.png" alt="compartment" width="600" height="300" /></div>
- **Compartments**: Hierarquia lógica para isolar recursos, delegar administração e facilitar billing/auditoria.  
- **Identity Domains**: Domínios de identidade independentes com usuários, grupos, provedores de autenticação, políticas de senha e MFA. Permitem separar identidades internas/externas.

### ✅ AuthN (Autenticação) & 🔓 AuthZ (Autorização)
**AuthN**: Verifica identidade. Métodos: senha + MFA, API Keys, Auth Tokens, Federation (SAML/OAuth), Instance Principals (VMs), Resource Principals (Functions/OKE), tokens de sessão.

**AuthZ**: Concedida por policies (sintaxe acima). Boas práticas:
<div align="center"><img src="slides/authZ.png" alt="authZ" width="600" height="300" /></div>
- Princípio do menor privilégio (`use` em vez de `manage` quando possível).
- Usar families (`instance-family`, `object-family`) reduz manutenção.
- Dynamic Groups: agrupam recursos por condições (ex.: tag ou compartment).  
  Exemplo de regra de dynamic group:  
  `ANY {instance.compartment.id = 'ocid1.compartment....'}`  
  Policy correspondente:  
  `Allow dynamic-group OKEPods to use object-family in compartment Dev`
- Condições refinam acesso (permissão específica ou tag exigida).

### 🏗️ Tenancy Setup (Passo a Passo)
1. Estrutura de compartments.  
2. Identity Domains / Federação.  
3. Grupos e Dynamic Groups.  
4. Policies (menor privilégio).  
5. MFA e rotação de chaves.  
6. Auditoria habilitada (Audit/Logging).  
7. Automatização com Instance/Resource Principals.  

### 🤝 Comparação (IAM)
| Recurso OCI | AWS | Azure | GCP |
|-------------|-----|-------|-----|
| Policies 📜 | IAM Policy JSON | RBAC Role Assignment | IAM Bindings |
| Dynamic Groups 🧠 | IAM Conditions + Tags | Dynamic Groups | IAM Conditions |
| Instance Principals 🖥️ | EC2 Instance Role | Managed Identity | Service Account |
| Resource Principals ⚙️ | Lambda Execution Role | Managed Identity | Service Account |
| Compartments 📂 | Accounts/OUs/Tags | Resource Groups | Folders/Projects |
| MFA 🔐 | MFA | MFA/Conditional Access | MFA |
| Audit Logs 🕵️ | CloudTrail | Activity Log | Cloud Audit Logs |

## Networking
<div align="center"><img src="slides/vcn.png" alt="vcn" width="600" height="300" /></div>


### 3.1 🔗 VCN Introduction
- **O que é**: Virtual Cloud Network (VCN) é sua rede virtual privada na OCI, completamente isolada e configurável (CIDR, subnets, roteamento).  
- **Componentes principais**:  
  - **CIDR block** (ex.: `10.0.0.0/16`)  
  - **Subnets** (regionais ou AD-local)  
  - **Route Tables**  
  - **Security Lists / Network Security Groups**  
  - **Gateways** (Internet, NAT, Service, DRG)  
- **Caso de uso**: Criar Zonas de DMZ, redes de front-end/back-end isoladas, interligar data centers on-premises.  

| OCI (VCN)           | AWS (VPC)         | Azure (VNet)      | GCP (VPC)        |
|---------------------|-------------------|-------------------|------------------|
| Rede global regional| Regional/global   | Regional          | Regional/global |
| Subnets regionais   | Subnets AZ        | Subnets Region/​AZ| Subnets Global  |
| Gateways nativos    | IGW, NAT, VGW     | Internet/NAT GW   | IGW, Cloud NAT  |

---

### 3.2 ➡️ VCN Routing
- **Route Tables**: definem para onde o tráfego sai da subnet.  
- **Tipos de rota**:  
  - `0.0.0.0/0` → Internet Gateway (tráfego público)  
  - `10.0.0.0/16` → Local (intra-VCN)  
  - `Service CIDR` → Service Gateway (p. ex., Object Storage)  
  - `DRG Attachment` → Dynamic Routing Gateway (VPN/DR)  
- **Propagação**: rotas estáticas configuradas manualmente; rota dinâmica via DRG opcional.  

| OCI (Route Tables)    | AWS (Route Tables)       | Azure (User Routes)         | GCP (Custom Routes)      |
|-----------------------|--------------------------|-----------------------------|--------------------------|
| Estático + DRG        | Estático + VGW BGP       | Estático + BGP ExpressRoute| Estático + Cloud Router |

---

### 3.3 🔐 VCN Security
- **Security Lists**: firewall em nível de subnet (stateless).  
- **Network Security Groups (NSG)**: firewall em nível de instância (stateful).  
- **Ingress/Egress Rules**: portas, protocolos, CIDRs.  
- **Private vs Public**:  
  - **Public Subnet** com Internet Gateway + regras abertas (somente o necessário).  
  - **Private Subnet** com NAT Gateway para saída sem entrada direta.  
- **Opcional**: Web Application Firewall (WAF) via Load Balancer; IPS através de parceiros no Marketplace.  

| OCI                   | AWS                      | Azure                         | GCP                         |
|-----------------------|--------------------------|-------------------------------|-----------------------------|
| Security Lists (SL)   | Network ACLs (stateless) | NSGs (stateful) + ASGs        | Firewall Rules (stateful)   |
| NSG (stateful)        | Security Groups          | Network Security Groups       | Firewall with Tags/Service  |
| WAF no LB             | AWS WAF + ALB/CLB        | WAF no Application Gateway    | Cloud Armor + LB           |

---

### 3.4 ⚖️ Load Balancer
- **Tipos**:  
  - **Public Load Balancer** (pública)  
  - **Private Load Balancer** (intra-VCN)  
  - **Opcional**: Network Load Balancer (L4) vs Application Load Balancer (L7) via partners.  
- **Componentes**:  
  - **Listener** (porta/protocolo)  
  - **Backend Set** (pool de instâncias ou IPs)  
  - **Health Checks** (HTTP, TCP)  
  - **SSL Offload** (certificados gerenciados)  
- **Use cases**: escalabilidade, alta disponibilidade, SSL termination, path-based routing.  

| OCI LB                 | AWS ELB                       | Azure Load Balancer / App GW | GCP Cloud Load Balancing     |
|------------------------|-------------------------------|------------------------------|------------------------------|
| Public / Private LB    | ALB / NLB / CLB               | Public LB / Internal LB      | HTTP(S) LB / TCP/UDP LB     |
| SSL offload integrada  | ACM + ELB                     | Managed Certificates         | Managed SSL Certs           |
| Health Checks nativos  | Health Checks definíveis      | Health Probes                | Health Checks               |

## Capítulo 5: Compute

### 5.1 Compute Introduction  
A família **Compute** da OCI oferece máquinas virtuais (VMs) elásticas e de alta performance para executar cargas de trabalho variadas — desde servidores web e bancos de dados até aplicações de inteligência artificial.  
- 🖥️ **VMs gerenciadas**: Templates imutáveis, alta disponibilidade e integração nativa com Block Storage, Networking e IAM.  
- ⚙️ **Shapes**: Configurações pré-definidas ou flexíveis de OCPU e memória, otimizadas para CPU-intensivo, memória-intensivo ou uso geral.  
- 🔄 **Integrado** com Auto Scaling, Compartments e Observability (Monitoring/Logging) para operações DevOps/SRE.  

### 5.2 Instance Basics  
- **Image & Boot Volume**  
  - Escolha de **imagem** (Oracle Linux, Ubuntu, Windows, custom) que define o SO e pacotes iniciais.  
  - **Boot Volume** persistente (Block Volume) que armazena SO e dados. Pode ser copiado, ampliado e replicado.  
- **Shapes**  
  - **Standard Shapes** (VM.Standard2.x, VM.Standard.E3.x): balanceados.  
  - **Dense I/O** (VM.DenseIO2.x): I/O intensivo.  
  - **GPU Shapes** (BM.GPU2.1): para ML e render.  
  - **Flex Shapes** (VM.Standard.E4.Flex): defina OCPUs/memória custom.  
- **Networking**  
  - Associação a uma **VCN + Subnet**: pública (Internet Gateway) ou privada (NAT).  
  - Configuração de **public IP**, **private IP** e **secondary VNICs**.  
- **Chaves SSH / Auth**  
  - Injeção de chave pública no momento do launch.  
  - Suporte a Instance Principals para automação sem credenciais.

### 5.3 Demo: Creating a Compute Instance  
1. **Console → Compute → Instances → Create Instance**  
2. **Define** nome, availability domain e compartment.  
3. **Escolher Image & Shape** (ex.: Oracle Linux 8 + VM.Standard2.1).  
4. **Configurar Networking**: VCN, subnet, atribuir Public IP.  
5. **Chave SSH**: colar key pública do cliente.  
6. **Avançar**: Tags, Metadata, Boot Volume size.  
7. **Create** → Instância provisionada em segundos.  
8. **Acessar via SSH** (`ssh opc@<public_ip>`), validar SO e montar Block Volumes adicionais.  

### 5.4 Scaling  
- **Vertical Scaling**  
  - **Resize** de shape (scale-up/down): requer shutdown ou live migration em determinados cases.  
  - Ajustar OCPU/memória sem reprovisionar disco.  
- **Horizontal Scaling**  
  - **Instance Pools** + **Autoscaling**:  
    - Cria grupo de instâncias idênticas (baseado em launch configuration).  
    - Regras de autoscale (CPU, Memory, Custom Metrics) que adicionam/removem instâncias automaticamente.  
- **Load Balancer Integration**: espalhar tráfego entre instâncias de um pool, garantindo alta disponibilidade.

### 5.5 Oracle Container Engine for Kubernetes (OKE)  
- **OKE** é o serviço gerenciado de Kubernetes da OCI:  
  - **Clusters** control plane redundante e upgrade automático.  
  - **Node Pools**: grupos de VMs gerenciados, usando shapes otimizados para pods.  
  - **Auto Repair & Auto Scaling** de nós.  
- **Integrações**:  
  - **IAM & RBAC** nativo;  
  - **VCN CNI** (cada pod recebe IP na VCN);  
  - **Service Mesh** (OCI Service Mesh) para observabilidade e segurança no tráfego entre microservices.  
- **Fluxo**:  
  1. Criar cluster OKE  
  2. Provisionar node pool  
  3. `kubectl` & `helm` deploy de workloads  
  4. Monitorar com OCI Monitoring / Prometheus  

### 5.6 Container workloads in OCI  
- **Container Instances** (Container Engine Light):  
  - Executar containers isolados sem gerenciar VMs ou Kubernetes.  
  - Ideal para jobs event-driven.  
- **Registry**: Oracle Container Registry (OCIR) ou Docker Hub integrado.  
- **DevOps Integration**: build/push automático de imagens via Code Repository + Pipelines.  
- **Networking**: containers recebem VNICs ou compartilham da VM hospedeira, com Security Lists/NSGs aplicados.

### 5.7 Serverless with Oracle Functions  
- **Oracle Functions** é uma plataforma FaaS baseada no projeto Fn:  
  - **Functions**: unidades leves de código (Java, Python, Go, Node.js, etc.).  
  - **Applications**: coleções de funções que compartilham configurações e VCN.  
  - **Triggers**: eventos que disparam funções — HTTP (API Gateway), Streaming, Object Storage, Vault.  
- **Escalonamento automático** e **cobrança por invocação**: sem gestão de infraestrutura.  
- **CLI & SDK**: `fn init`, `fn deploy`, integração com Terraform e Cloud Events.  
- **Casos de uso**: processamento de eventos, back-ends leves, orquestração de pipelines sem servidor.

---
