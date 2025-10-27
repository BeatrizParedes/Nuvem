# AWS — 5 Principais Serviços
**Serviços:** Amazon EC2, Amazon S3, Amazon RDS, AWS Lambda e Amazon VPC

---

## 1) Amazon EC2 (Elastic Compute Cloud)

### Visão Geral
O **EC2** oferece **máquinas virtuais sob demanda** (“instâncias”) para qualquer carga: sites, sistemas corporativos, IA/ML e Big Data.

### Arquitetura e Funcionamento
- **AMI (Amazon Machine Image):** define SO, bibliotecas e configs iniciais.
- **Tipos de Instância:** T (geral), C (CPU), M (misto), R (memória), P/G (GPU).
- **Rede:** roda dentro de uma **VPC** com IPs, **Security Groups** e sub-redes.
- **Disco:** **EBS** como armazenamento em bloco persistente.

### Recursos Avançados
- **Auto Scaling:** ajusta o nº de instâncias conforme a demanda.
- **Elastic Load Balancer (ELB):** distribui tráfego entre instâncias.
- **Elastic IPs:** IP público fixo.
- **Spot Instances:** capacidade ociosa com grande desconto.

### Casos de Uso
Hospedagem web (WordPress, Node.js), treinamento de ML com GPU, ERPs, ambientes de dev/teste.

### Vantagens
Controle total do SO, alta flexibilidade/escalabilidade, ecossistema integrado, modelos de custo (On-Demand, Reserved, Spot).

---

## 2) Amazon S3 (Simple Storage Service)

### Visão Geral
**Armazenamento de objetos** com **alta durabilidade (11 noves)**, segurança corporativa e **escala automática**.

### Funcionamento
- **Buckets** (contêineres) → **Objetos** (conteúdo + metadados + permissões).
- Replicação automática em **múltiplas AZs** na região.

### Classes de Armazenamento
- **Standard** (uso frequente)
- **Standard-IA** (acesso infrequente)
- **Glacier/Deep Archive** (arquivamento)
- **Intelligent-Tiering** (muda de classe conforme uso)

### Recursos
- **Versionamento**, **Lifecycle** (mover/apagar após X dias)
- **Eventos** (gatilhos para Lambda)
- **S3 Select** (consulta parcial em CSV/JSON/Parquet)

### Casos de Uso
Backups, logs, **sites estáticos**, lake de dados para Analytics/ML.

### Vantagens
Durabilidade extrema, escala ilimitada, custos por classe, segurança via IAM/Policies/KMS.

---

## 3) Amazon RDS (Relational Database Service)

### Visão Geral
**Banco relacional gerenciado** (menos operação: instalação, patch, backup, failover, replicação).

### Mecanismos Suportados
**Aurora** (compatível MySQL/PostgreSQL), **MySQL**, **PostgreSQL**, **MariaDB**, **Oracle**, **SQL Server**.

### Arquitetura & Recursos
- **Multi-AZ:** réplica síncrona para **failover automático**.
- **Read Replicas:** escalar leitura.
- **Backups automáticos** (S3) + **Snapshots** manuais.
- **Monitoramento** via CloudWatch; **manutenção** automatizada.

### Segurança
Execução em **VPC**, criptografia **em repouso** (KMS) e **em trânsito** (TLS), IAM + Security Groups.

### Casos de Uso
E-commerce, apps financeiros/corporativos, relatórios/BI (Aurora + Redshift).

### Vantagens
Alta disponibilidade, custo operacional menor, escala simples e segura.

---

## 4) AWS Lambda

### Visão Geral
**Serverless**: execute código em resposta a **eventos** sem gerenciar servidores; pague por **tempo de execução** (ms).

### Funcionamento
- Funções em **Python/Node.js/Java/Go/C#** ou **contêiner**.
- Disparos por S3, DynamoDB, **API Gateway**, EventBridge, etc.
- **Escala automática** e paralelismo por invocação.
- **Ambiente efêmero** e isolado por execução.

### Casos de Uso
Processamento de arquivos (S3), **APIs serverless**, automações/ETL, streams (logs, IoT).

### Vantagens
Escala instantânea, **custo ultrabaixo**, integração profunda na AWS, zero manutenção de infraestrutura.

---

## 5) Amazon VPC (Virtual Private Cloud)

### Visão Geral
**Rede virtual privada**: controle total de endereçamento, roteamento e perímetros de segurança.

### Componentes
- **Subnets** (pública/privada)
- **Route Tables** (rotas)
- **Internet Gateway (IGW)** (acesso público)
- **NAT Gateway** (saída à internet para sub-redes privadas)
- **Security Groups** (stateful) e **Network ACLs** (stateless)

### Integrações
EC2, RDS, Lambda, EKS, VPN site-to-site, **AWS Direct Connect**, múltiplas AZs.

### Casos de Uso
Ambientes corporativos isolados, cargas sensíveis (finanças/saúde), **híbrido** (nuvem + datacenter).

### Vantagens
Isolamento, segurança granular, segmentação por ambiente (dev/test/prod), resiliência nativa.

---

## Resumo Técnico

| Serviço | Tipo | Escalabilidade | Custo | Segurança | Casos Típicos |
|---|---|---|---|---|---|
| **EC2** | Computação | Manual/Auto Scaling | On-Demand/Reserved/Spot | IAM + VPC + SG | Servidores e apps |
| **S3** | Armazenamento | Automática | Por GB + requests | IAM + KMS + Policies | Backups, sites estáticos, data lake |
| **RDS** | Banco relacional | Vertical + Réplicas | Instância + storage | IAM + TLS + SG | E-commerce, sistemas críticos |
| **Lambda** | Serverless | Automática | Por execução (ms) | IAM | APIs, ETL, automações |
| **VPC** | Rede | Manual | (Componentes pagos) | SG + ACL + VPN | Isolamento/híbrido |

---
