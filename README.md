# Desafio Instâncias EC2 - Arquiteturas AWS

Este projeto foi desenvolvido como parte do curso de **Computação em Nuvem**, com o objetivo de explorar e comparar duas abordagens de arquitetura na **Amazon Web Services (AWS)**: uma **Serverless** e outra baseada em **instâncias EC2**.

Ambas têm como foco hospedar e executar uma aplicação web moderna utilizando os principais serviços da AWS.

---

## Arquitetura Serverless (Lambda + API Gateway + DynamoDB)

### Descrição
Nesta arquitetura, todo o backend da aplicação é **sem servidor**, utilizando funções **AWS Lambda** para executar a lógica sob demanda. O front-end é hospedado em um bucket **S3** e distribuído globalmente via **CloudFront**.

### Fluxo de Funcionamento
1. **Usuário** acessa a aplicação via **HTTPS**
2. **CloudFront (CDN)** entrega os arquivos estáticos armazenados no **Amazon S3**
3. **API Gateway** recebe as requisições do front-end e as direciona para as funções **AWS Lambda**
4. As funções **Lambda** processam, autenticam e armazenam dados no **DynamoDB**

### Tecnologias Utilizadas
- **Amazon CloudFront** – Rede de distribuição de conteúdo (CDN)
- **Amazon S3** – Armazenamento de arquivos estáticos
- **Amazon API Gateway** – Roteamento e gerenciamento de APIs
- **AWS Lambda** – Execução de código sob demanda
- **Amazon DynamoDB** – Banco de dados NoSQL escalável

### Diagrama da Arquitetura Serverless
<img width="590" height="626" alt="Arquitetura Serverless AWS" src="https://github.com/user-attachments/assets/9f810cd3-ec17-4481-86ab-ef253589db34" />

---

## Arquitetura com EC2 (Load Balancer + RDS)

### Descrição
Nesta abordagem, o backend é executado em **instâncias EC2** que atuam como servidores de aplicação. O tráfego é distribuído por um **Application Load Balancer**, garantindo disponibilidade e balanceamento de carga. O banco de dados é mantido no **Amazon RDS**.

### Fluxo de Funcionamento
1. **Usuário** acessa a aplicação via **HTTPS** pelo **CloudFront**
2. **CloudFront** entrega o front-end hospedado no **S3**
3. As requisições de API são enviadas ao **Application Load Balancer**, que distribui entre múltiplas instâncias **EC2**
4. Cada instância **EC2** executa o servidor de aplicação e se comunica com o **RDS**, onde ficam armazenados os dados

### Tecnologias Utilizadas
- **Amazon CloudFront** – CDN para distribuição do front-end
- **Amazon S3** – Armazenamento estático do site
- **Application Load Balancer** – Balanceamento de carga entre instâncias EC2
- **Amazon EC2** – Servidores de aplicação
- **Amazon EBS** – Volumes de armazenamento persistente
- **Amazon RDS** – Banco de dados relacional (MySQL, PostgreSQL, etc.)

### Diagrama da Arquitetura EC2
<img width="571" height="962" alt="Arquitetura EC2 AWS" src="https://github.com/user-attachments/assets/d48323fe-6574-4aaf-a98b-a312020ab936" />

---

## Comparação de Tecnologias

| Componente | Arquitetura Serverless | Arquitetura EC2 |
|------------|----------------------|----------------|
| **Computação** | AWS Lambda | Amazon EC2 |
| **Armazenamento** | Amazon S3 + DynamoDB | Amazon EBS + RDS |
| **Rede** | API Gateway + CloudFront | ALB + CloudFront |
| **Escalabilidade** | Automática e granular | Manual/Auto Scaling Groups |
| **Custo** | Pay-per-use | Custos fixos por instância |

---

## Conclusão

As duas arquiteturas atendem a diferentes necessidades de negócio:

- **Serverless**: Ideal para aplicações dinâmicas, escaláveis e com demanda variável, reduzindo custos e manutenção. Perfeita para startups e aplicações com tráfego imprevisível.

- **EC2**: Mais adequada para aplicações que exigem controle total do ambiente, sistemas legados ou alto processamento contínuo. Ideal para empresas com necessidades específicas de configuração e performance previsível.

---

## Contato

Desenvolvido como parte do curso de **Computação em Nuvem** na **DIO**. 

Para mais informações sobre a implementação ou dúvidas sobre as arquiteturas, sinta-se à vontade para abrir uma **issue** neste repositório.
