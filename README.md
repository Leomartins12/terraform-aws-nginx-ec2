# Terraform AWS – EC2 com Nginx e Infraestrutura Completa

Este projeto utiliza Terraform para provisionar uma infraestrutura completa na AWS com foco em segurança, automação e boas práticas de DevOps.

##Recursos criados

- VPC com CIDR `10.0.0.0/16`
- Subnet pública (`10.0.1.0/24`) na zona `us-east-1a`
- Internet Gateway + Tabela de Rotas
- Grupo de Segurança com acesso SSH (porta 22) restrito a IP específico
- Instância EC2 (Debian 12) com tipo `t2.micro`
- Instalação automatizada do Nginx via `user_data`
- Geração e saída de chave privada (para SSH)
- Exibição do IP público da instância

##Segurança

- Acesso SSH restrito a um único IP (ex: `177.53.133.172/32`)
- Tráfego de saída totalmente liberado
- AMI oficial do Debian 12
- Infraestrutura replicável com versionamento de código (IaC)

##Pré-requisitos

- Conta AWS com credenciais configuradas (`~/.aws/credentials`)
- Terraform instalado
- AWS CLI instalada (opcional)

##Como usar

```bash
# Inicialize o Terraform
terraform init

# Verifique o plano de execução
terraform plan

# Aplique a configuração
terraform apply
Confirme com yes quando solicitado.

Acesso à Instância
Após o terraform apply, serão exibidos:

A chave privada gerada
O IP público da instância

Conecte-se via SSH:
ssh -i ./minha-chave.pem ec2-user@<ip-público>

Acesse via navegador:
http://<ip-público>

Ferramentas utilizadas
Terraform
AWS EC2
Amazon VPC
Nginx
Debian 12 (AMI oficial)



