# Criação de Instância EC2 Gratuita (Free Tier AWS)

Este documento contém **todo o guia completo** para criação de uma instância gratuita **EC2 na AWS**, configuração de servidor web, teste de funcionamento, encerramento seguro, benefícios, dificuldades e aprendizados.

---

##  Objetivo
Ensinar, passo a passo, como **criar uma instância EC2 gratuita (Free Tier)** na **Amazon Web Services (AWS)**, configurando um **servidor Apache**, de forma **segura, funcional e sem custos adicionais** (dentro dos limites do Free Tier).

---

##  Pré-requisitos
- Conta AWS ativa (**o Free Tier exige cartão** para verificação; não há cobrança se usar dentro dos limites).
- Acesso ao Console AWS: https://aws.amazon.com/console
- Região recomendada: **US East (N. Virginia)**.
- Permissões para criar EC2, Security Groups e EBS.
- Noções básicas de rede e Linux (opcional, mas ajudam).

---

##  Avisos Importantes
- Free Tier: **750 horas/mês** para **1** instância `t2.micro` ou `t3.micro`.
- O limite é por **conta**. Duas instâncias ligadas 24/7 excedem o limite.
- Evite **Elastic IP parado** e **NAT Gateway** (cobram à parte).
- Ao terminar, **encerre (terminate)** a instância e remova volumes para evitar custos.

---

##  Passo a Passo

### 1. Acessar o EC2
1. Faça login no **Console AWS**.  
2. Pesquise por **EC2**.  
3. Vá em **Instances** e clique em **Launch instances**.

---

### 2. Configurar a instância

| Campo | Configuração |
|---|---|
| **Name** | `web-free-tier` |
| **Application and OS Image (AMI)** | `Amazon Linux 2023 (Free tier eligible)` **ou** `Ubuntu 22.04 LTS` |
| **Instance type** | `t2.micro` ou `t3.micro` (Free Tier) |
| **Key pair (login)** | Criar nova chave, ex.: `web-key.pem` (baixe e guarde) |
| **Network settings** | VPC padrão + Subnet padrão |
| **Auto-assign Public IP** | **Enable** |
| **Security group** | Novo SG com **SSH(22)=My IP** e **HTTP(80)=Anywhere (0.0.0.0/0)** |
| **Storage (EBS)** | **8 GiB gp3** (elegível ao Free Tier) |

> Dicas de segurança: mantenha **SSH(22)** restrito a **My IP**. Deixe **HTTP(80)** público para teste do site. Ative **Delete on termination** no volume.

---

### 3. Instalar automaticamente o servidor web (User Data)

No formulário de criação, expanda **Advanced details → User data** e cole **um** dos scripts:

**Amazon Linux 2023**
```bash
#!/bin/bash
dnf update -y
dnf install -y httpd
systemctl enable --now httpd
echo "<h1>Hello AWS Free Tier!</h1>" > /var/www/html/index.html
```

**Ubuntu 22.04 LTS**
```bash
#!/bin/bash
apt-get update -y
apt-get install -y apache2
systemctl enable --now apache2
echo "<h1>Hello AWS Free Tier!</h1>" > /var/www/html/index.html
```

---

### 4. Lançar a instância
1. Clique em **Launch instance**.  
2. Aguarde o status **running**.  
3. Anote o **IPv4 Public Address**.

---

### 5. Testar no navegador
Abra no navegador:
```
http://SEU_IP_PUBLICO
```
Você deve ver:
```
Hello AWS Free Tier!
```

---

### 6. Conectar via SSH (opcional)

**Amazon Linux**
```bash
chmod 400 ~/Downloads/web-key.pem
ssh -i ~/Downloads/web-key.pem ec2-user@SEU_IP_PUBLICO
```

**Ubuntu**
```bash
chmod 400 ~/Downloads/web-key.pem
ssh -i ~/Downloads/web-key.pem ubuntu@SEU_IP_PUBLICO
```

---

### 7. Encerrar a instância
1. Em **EC2 → Instances**, selecione a instância.  
2. **Instance state → Terminate instance**.  
3. Confirme.  
4. Garanta que o volume **EBS** seja removido (Delete on termination) ou apague manualmente em **Volumes**.

> Encerrar evita cobranças após o uso.

---

##  Benefícios
- **Custo zero** dentro do Free Tier (1x `t2.micro`/`t3.micro` + 8 GiB `gp3`).  
- **Aprendizado prático**: EC2, VPC padrão, Security Groups, EBS, User Data.  
- **Automação simples**: servidor web sobe automaticamente no 1º boot.  
- **Flexibilidade de acesso**: HTTP público e SSH opcional para admin.  
- **Reprodutibilidade** e documentação clara para trabalhos e estudos.  
- **Controle total** do ambiente (SO, pacotes, portas, logs).

---

##  Dificuldades 

| Problema | Possível causa | Solução |
|---|---|---|
| Não conecta via SSH | Regra de SG não libera **SSH(22)** para seu IP | Ajuste o Security Group para **SSH(22)=My IP** |
| Página não abre | Porta **80** bloqueada ou serviço não iniciado | Libere **HTTP(80)**; verifique `systemctl status httpd/apache2` |
| IP mudou após stop/start | IP público dinâmico muda ao reiniciar | Verifique o novo **IPv4 Public Address** no console EC2 |
| Script User Data não rodou | Sintaxe incorreta ou AMI diferente | Revise script; cheque `/var/log/cloud-init-output.log` |
| Cobrança inesperada | 2ª instância, EIP parado, NAT GW | Use **1** instância; evite EIP ocioso e **NAT Gateway** |
| Perdeu a chave `.pem` | Arquivo não é recuperável | Crie nova instância (ou recrie via AMI/volume para trocar `authorized_keys`) |

---

##  Aprendizados
- **IaaS**: lançar, configurar e administrar servidores na nuvem.  
- **Rede e segurança**: VPC padrão, Subnets, Security Groups, portas mínimas abertas.  
- **Automação**: **User Data** para provisionamento no boot.  
- **Custos**: como operar **dentro do Free Tier** e evitar cobranças.  
- **Operação**: checagem de serviços com `systemctl`, leitura de logs de inicialização.  
- **Boas práticas**: princípio do menor privilégio, limpeza de recursos, versionamento seguro (não subir `.pem`).

---

##  Instalação manual (sem User Data)

**Amazon Linux**
```bash
sudo dnf update -y
sudo dnf install -y httpd
sudo systemctl enable --now httpd
echo "Hello AWS Free Tier! $(hostname)" | sudo tee /var/www/html/index.html
```

**Ubuntu**
```bash
sudo apt-get update -y
sudo apt-get install -y apache2
sudo systemctl enable --now apache2
echo "Hello AWS Free Tier! $(hostname)" | sudo tee /var/www/html/index.html
```
