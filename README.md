
1. Descrição Técnica do Código Original (Tarefa 1)
O código main.tf define a criação de uma infraestrutura na AWS usando Terraform. Ele abrange os seguintes recursos:

Provedor AWS: Configurado para a região us-east-1.

Variáveis:

projeto: Nome do projeto para personalizar os recursos.
candidato: Nome do candidato que será utilizado para personalizar o nome dos recursos.
Chave Privada (TLS) e Key Pair:

Gera uma chave privada usando o algoritmo RSA com 2048 bits.
Cria um Key Pair na AWS para permitir acesso seguro via SSH à instância EC2.
VPC (Virtual Private Cloud):

Cria uma VPC com um CIDR de 10.0.0.0/16 e com suporte a DNS e resolução de nome.
Subnet:

Cria uma Subnet dentro da VPC com o bloco 10.0.1.0/24, localizada na zona de disponibilidade us-east-1a.
Internet Gateway:

Configura um Internet Gateway para permitir tráfego de saída da VPC.
Route Table:

Configura uma tabela de rotas que permite tráfego de saída para a internet através do Internet Gateway.
Security Group:

Cria um grupo de segurança que permite acesso SSH (porta 22) a partir de um IP específico (177.53.133.172/32).
Todo o tráfego de saída é liberado.
AMI Debian:

Utiliza a AMI mais recente do Debian 12 para criar a instância EC2.
Instância EC2:

Cria uma instância EC2 de tipo t2.micro associada à Subnet e ao Security Group criados.
Instala o Nginx automaticamente na instância através de um script user_data.
Outputs:

Exibe a chave privada gerada para o acesso SSH.
Exibe o IP público da instância EC2.
2. Melhorias de Segurança e Automação (Tarefa 2)
Melhorias de Segurança:

A segurança foi aprimorada ao restringir o acesso SSH à instância EC2 a um IP específico (177.53.133.172/32). Isso impede acessos indesejados de qualquer outro IP.
Automação da Instalação do Nginx:

Um script foi incluído no user_data da instância EC2 para instalar e iniciar o Nginx automaticamente. Isso garante que, após a criação da instância, o Nginx estará em execução e pronto para servir páginas web.

O código do script user_data é:
#!/bin/bash
apt-get update -y
apt-get upgrade -y
apt-get install nginx -y
systemctl start nginx

3. Instruções de Uso
Pré-requisitos:
AWS CLI configurado corretamente com as credenciais da AWS.
Terraform instalado no seu sistema.
Passos para Aplicar a Configuração:
Inicializar o Terraform:

Navegue até a pasta onde o arquivo main.tf está localizado e execute:

terraform init

Verificar o Plano:

Para ver o que o Terraform irá criar, execute o comando:

terraform plan

Aplicar a Configuração:

Se o plano estiver correto, aplique a configuração com o comando:

terraform apply

Confirme digitando yes quando solicitado.
Acesso à Instância EC2:

O IP público da instância EC2 será exibido após a aplicação da configuração. Utilize esse IP para acessar o servidor via SSH ou abrir a página do Nginx no navegador.

Para acessar via SSH:

ssh -i /caminho/para/sua-chave.pem ec2-user@ip-da-instancia

4. Resultados Esperados
Uma instância EC2 rodando Debian com o Nginx instalado e funcionando.
Segurança aprimorada com restrição de acesso SSH a um IP específico.
Outputs no terminal do Terraform mostrando a chave privada e o IP público da instância.


