## 1. OCI Architecture *(chatgpt0)*

### 🌐 Conceitos Fundamentais
- **Tenancy** 🏢: Raiz lógica da sua presença na OCI (parecido com uma “organização”). Tudo — usuários, políticas, compartments e recursos — existe dentro dela.
- **Region** 📍: Conjunto geograficamente isolado de infraestrutura (ex.: `sa-saopaulo-1`). Cada região é independente em energia, rede e capacidade. Permite *latency control* e conformidade regulatória.
- **Availability Domain (AD)** 🏬🏬🏬: Data centers independentes dentro de uma região (0–3). Falha em um AD não impacta os outros → alta disponibilidade horizontal.
- **Fault Domain (FD)** 🧩: Partições lógicas dentro de um AD (3 por AD). Distribuir instâncias entre FDs evita que manutenção programada ou falha de rack derrube todo o serviço.
- **VCN (Virtual Cloud Network)** 🔗: Rede virtual isolada (CIDR escolhido pelo cliente) onde vivem subnets, roteamento e segurança.
  - **Subnets Regionais** 🌍: Se estendem por todos os ADs → simplificam failover.
  - **Subnets AD-Local** 📦: Restringem recursos a um único AD quando necessário.
- **Redundância & Alta Disponibilidade** ♻️: Colocar recursos replicados em múltiplos ADs/Fault Domains ou usar serviços *multi-AD* (Autonomous DB, Load Balancer).
- **Disaster Recovery (DR)** 🚨: Replicação entre **regiões emparelhadas** (Cross-Region Object Storage, Block Volume Replication, Autonomous Data Guard) para recuperar após desastre regional.
- **Edge Services** 🌍⚡: Pontos de presença globais para DNS, Email Delivery e WAF diminuem latência até o usuário final.
- **Armazenamento** 💾: Object Storage (standard/archival), Block Volume (replicação automática entre domínios de falha), File Storage (NFS), Archive.
- **Observabilidade** 👁️: Logging, Monitoring, Events e Alarms integrados para detectar e agir sobre incidentes rapidamente.

### 🔁 Fluxos de Tráfego e Segurança
- **Route Tables** 🛣️: Determinam o próximo salto (Internet/NAT/Service Gateway).
- **Security Lists / Network Security Groups** 🔐: Controles de firewall em nível de subnet (SL) ou de instância (NSG).
- **Gateways**:
  - **Internet Gateway** 🌐: Acesso público.
  - **NAT Gateway** 🚪: Saída privada sem abrir portas de entrada.
  - **Service Gateway** 🛰️: Acesso privado a serviços OCI (Object Storage etc.).
  - **Local Peering / Remote Peering Gateway** 🔄: Conecta VCNs na mesma ou em outra região.

### 🧩 Comparação com Concorrentes
| Conceito OCI | AWS | Azure | GCP |
|--------------|-----|-------|-----|
| Tenancy 🏢 | Account | Subscription | Project |
| Region 📍 | Region | Region | Region |
| Availability Domain 🏬 | Availability Zone | Availability Zone | Zone |
| Fault Domain 🧩 | (Partition Placement Groups) | Fault Domain | (Distribuir entre Zones) |
| Compartments 📂 | Accounts/OUs + Tags | Resource Groups | Folders/Projects |
| VCN 🔗 | VPC | Virtual Network | VPC |
| Service Gateway 🛰️ | VPC Endpoint / PrivateLink | Private Link / Service Endpoint | Private Service Connect |
| Cross-Region DR 🚨 | S3 CRR / RDS Replicas | GRS Storage / Geo-Rep | Multi-/Dual-Region Storage |
| Edge DNS/WAF 🌍 | Route53 / CloudFront WAF | Azure DNS / Front Door | Cloud DNS / Cloud Armor |

---

## 2. Identity and Access Management (IAM)

### 🔐 IAM Introduction
O **OCI IAM** controla **quem** (usuários, grupos, recursos) pode fazer **o quê** (ações) em **quais recursos** e **onde** (tenancy ou compartment). Usa políticas legíveis:  
`Allow group Devs to use subnets in compartment Dev`.

### 📂 Compartments & 🪪 Identity Domains
- **Compartments** 📂: Pastas lógicas hierárquicas para isolar recursos, delegar administração e facilitar billing/auditoria. Políticas podem herdar escopo (política em nível de tenancy enxerga todos os filhos).
- **Identity Domains** 🪪: Contêm identidades (usuários, grupos, aplicativos), provedores de autenticação (SAML, Social), regras de senha/MFA. Permitem múltiplos domínios isolados dentro da mesma tenancy (ex.: *Employees*, *Partners*).
- **Boas Práticas**: Estruturar compartments por ambiente (Dev/Test/Prod) ou unidade de negócio; usar domínios distintos para separar identidade externa de interna.

### ✅ AuthN (Autenticação) & 🔓 AuthZ (Autorização)
- **AuthN**: Verifica identidade. Métodos: senha + MFA, API Keys (par de chaves), Tokens de Autenticação, Federation (SAML/OAuth), **Instance Principals** (VMs chamam API sem chaves estáticas), **Resource Principals** (Functions/OKE).
- **AuthZ**: Concedida via **Policies** usando níveis de permissão:  
  - `inspect` (listar metadados), `read` (ver conteúdo), `use` (operar sem gerenciar), `manage` (controle total).  
- **Principals** especiais:
  - **Instance Principal** 🖥️: Metadados da instância geram token temporário.
  - **Resource Principal** ⚙️: Funções, Streams, OKE etc. obtêm identidade gerenciada automaticamente.
- **Dynamic Groups** 🧠: Agrupam recursos com condições (ex.: todas instâncias com tag `Role=Batch`) para aplicar política sem intervenção manual.

### 🏗️ Tenancy Setup (Passo a Passo)
1. **Planejar Estrutura de Compartments** 📂 (ex.: `Root/Prod`, `Root/Dev`, `Root/Shared`).
2. **Criar Identity Domains / Federação** 🪪 (conectar Azure AD/Okta).
3. **Criar Grupos** 👥 (`Admins`, `Devs`, `Auditors`).
4. **Definir Policies** 📜:  
   - `Allow group Admins to manage all-resources in tenancy`  
   - `Allow group Devs to use instances in compartment Dev`  
   - `Allow dynamic-group BatchInstances to use object-family in compartment Shared`
5. **Configurar Segurança** 🔐: MFA obrigatório, rotação de chaves/API Keys.
6. **Ativar Audit & Logging** 🕵️: Monitorar mudanças e acessos.
7. **Automatizar** 🤖: Usar Instance/Resource Principals para pipelines sem credenciais fixas.

### 🤝 Comparação com Concorrentes
| Recurso OCI | AWS | Azure | GCP |
|-------------|-----|-------|-----|
| Usuários/Grupos 👥 | IAM Users/Groups | Azure AD Users/Groups | IAM Members |
| Policies 📜 | IAM Policy JSON | RBAC Role Assignment | IAM Policy (Bindings) |
| Compartments 📂 | Accounts/OUs/Tags | Resource Groups | Folders/Projects |
| Identity Domains 🪪 | IAM Identity Center (SSO) | Azure AD Tenants | Cloud Identity |
| Dynamic Groups 🧠 | IAM Conditions + Tags | Dynamic Groups (Preview) | IAM Conditions |
| Instance Principals 🖥️ | EC2 Instance Profile (IAM Role) | Managed Identity | Service Account |
| Resource Principals ⚙️ | Lambda Execution Role | Managed Identity | Service Account |
| MFA 🔐 | MFA | MFA/Conditional Access | MFA |
| Audit Logs 🕵️ | CloudTrail | Activity Log | Cloud Audit Logs |

---
