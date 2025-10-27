# 🧠 AWS — Principais Serviços e Funcionamento Detalhado

## 📘 Descrição do Projeto
Este documento apresenta uma análise **profunda e didática** dos **principais serviços da Amazon Web Services (AWS)**, a plataforma de computação em nuvem mais utilizada do mundo.  
O objetivo é compreender como cada serviço funciona, suas **arquiteturas**, **casos de uso reais** e **vantagens técnicas**, fornecendo uma visão sólida para estudantes e profissionais de tecnologia.

---

## ☁️ Serviços Abordados

### 🔹 1. Amazon EC2 (Elastic Compute Cloud)
Serviço de **computação em nuvem** que permite criar e gerenciar **máquinas virtuais (instâncias)** sob demanda.  
É a base da infraestrutura da AWS, usada para hospedar sites, aplicações, bancos de dados e sistemas corporativos.

**Destaques:**
- Total controle do sistema operacional.  
- Tipos de instância otimizados (CPU, memória, GPU).  
- Escalabilidade automática via Auto Scaling.  
- Modelos de cobrança: On-Demand, Reserved e Spot.

---

### 🔹 2. Amazon S3 (Simple Storage Service)
Serviço de **armazenamento de objetos** que oferece **alta durabilidade (99,999999999%)**, segurança e escalabilidade automática.

**Destaques:**
- Armazenamento em **buckets** com controle de acesso via IAM.  
- Classes de armazenamento: Standard, Infrequent Access, Glacier e Intelligent-Tiering.  
- Suporte a versionamento, políticas de ciclo de vida e eventos automáticos.  
- Integração com outros serviços (CloudFront, Lambda, Athena).

---

### 🔹 3. Amazon RDS (Relational Database Service)
Serviço de **banco de dados relacional gerenciado**.  
Reduz o trabalho operacional (instalação, backup, patching e replicação).

**Destaques:**
- Suporte a **MySQL, PostgreSQL, MariaDB, Oracle, SQL Server e Aurora**.  
- **Multi-AZ** para alta disponibilidade e **read replicas** para escala.  
- Backups automáticos e snapshots manuais.  
- Segurança via VPC, TLS e criptografia KMS.

---

### 🔹 4. AWS Lambda
Serviço **serverless** que executa código **sem necessidade de servidores**.  
Ideal para automações, processamento em tempo real e APIs escaláveis.

**Destaques:**
- Suporte a múltiplas linguagens (Python, Node.js, Java, Go, C#, etc.).  
- Escalabilidade automática instantânea.  
- Custo baseado no tempo de execução (em milissegundos).  
- Integração com eventos do S3, DynamoDB, API Gateway e CloudWatch.

---

### 🔹 5. Amazon VPC (Virtual Private Cloud)
Serviço que permite criar uma **rede virtual privada e isolada** dentro da nuvem AWS.  
Proporciona controle total sobre IPs, sub-redes, gateways e regras de segurança.

**Destaques:**
- Sub-redes públicas e privadas.  
- Controle granular com **Security Groups** e **Network ACLs**.  
- Conexões seguras via **VPN** ou **AWS Direct Connect**.  
- Segmentação por ambientes (dev, teste, produção).

---

## ⚙️ Tabela Comparativa

| Serviço | Categoria | Escalabilidade | Modelo de Custo | Segurança | Casos de Uso |
|----------|------------|----------------|-----------------|------------|--------------|
| **EC2** | Computação | Manual / Auto Scaling | Por hora/segundo | IAM + VPC + SG | Hospedagem de apps e sistemas |
| **S3** | Armazenamento | Automática | Por GB/mês | IAM + KMS | Backups, data lakes, sites estáticos |
| **RDS** | Banco de Dados | Vertical + Réplicas | Por instância + storage | IAM + TLS + SG | E-commerce, BI, ERP |
| **Lambda** | Serverless | Automática | Por execução (ms) | IAM | APIs, ETL, automações |
| **VPC** | Rede | Manual | Gratuito (alguns componentes pagos) | SG + ACL + VPN | Isolamento e segurança de rede |

---

## 🏗️ Arquitetura Exemplo (Aplicação Completa)

**Fluxo típico:**
1. Usuários acessam a aplicação hospedada no **EC2**.  
2. Imagens e arquivos são salvos no **S3**.  
3. Dados transacionais são armazenados no **RDS**.  
4. Funções **Lambda** processam eventos automáticos (como uploads e logs).  
5. Toda a infraestrutura é isolada dentro de uma **VPC**, garantindo segurança e controle.

---

## 📚 Tecnologias Utilizadas
- **AWS EC2**
- **AWS S3**
- **AWS RDS**
- **AWS Lambda**
- **AWS VPC**
- **IAM** (Identity and Access Management)
- **CloudWatch** (Monitoramento)

---
