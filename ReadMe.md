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


