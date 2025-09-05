
# 🚀 AWSarchitecture

Projeto desenvolvido para o desafio do **Bootcamp Santander Code Girls**.  
O objetivo é demonstrar duas soluções de arquitetura AWS para armazenamento e processamento de dados, utilizando **EBS**, **Lambda Function**, **EC2** e **S3**.

---

## 🌐 Visão Geral

Este projeto apresenta **duas arquiteturas**:

1. 🗂️ **Processamento de arquivos CSV via Lambda e DynamoDB**
2. 🖥️ **Servidor Web em EC2 com armazenamento persistente em EBS**

---

## 1️⃣ Processamento de Arquivos CSV (Lambda + S3 + DynamoDB)

### 🔄 Fluxo Resumido

1. O usuário gera ou possui um arquivo `.csv` localmente.
2. Utiliza o **AWS CLI** para fazer upload do arquivo para um bucket **S3**.
3. O **S3** dispara um evento ao receber o arquivo.
4. Uma **função Lambda** é acionada, lê o arquivo, processa os dados e salva no **DynamoDB**.

### 📊 Diagrama Mermaid

```mermaid
%% Diagrama: Processamento de CSV via Lambda
graph TD
	subgraph subGraph0["Ambiente Local"]
		A@{ label: "<i class='fas fa-user' style='color:#FF9900'></i> Usuário / Sistema de Arquivos" }
		B("Arquivo.csv")
		C@{ label: "<i class='fas fa-terminal' style='color:#4A5568'></i> AWS CLI" }
	end
	subgraph subGraph1["Nuvem AWS"]
		D@{ label: "<i class='fab fa-aws' style='color:#232F3E'></i> Amazon S3 Bucket" }
		E@{ label: "<i class='fab fa-aws' style='color:#FF9900'></i> AWS Lambda Function" }
		F@{ label: "<i class='fas fa-database' style='color:#2E73B8'></i> Amazon DynamoDB" }
	end
		A -- Gera/Possui --> B
		B -- "aws s3 cp arquivo.csv s3://meu-bucket/" --> C
		C -- Upload --> D
		D -- Evento (s3:ObjectCreated:*) --> E
		E -- Lê o arquivo, processa<br>e salva os dados --> F
		A@{ shape: rect}
		C@{ shape: rect}
		D@{ shape: rect}
		E@{ shape: rect}
		F@{ shape: rect}
```

---

## 2️⃣ Servidor Web com EC2 + EBS

### 🔄 Fluxo Resumido

1. Usuários da internet acessam o servidor web hospedado em uma instância **EC2**.
2. O **EC2** está conectado a um volume **EBS**, garantindo armazenamento persistente para dados do servidor.

### 📊 Diagrama Mermaid

```mermaid
%% Diagrama: EC2 + EBS
graph TD
	subgraph "AWS Cloud"
		B[<i class='fab fa-aws' style='color:#FF9900'></i> Amazon EC2 <br> Instância / Servidor Web]
		C[<i class='fab fa-aws' style='color:#5D6D7E'></i> Amazon EBS <br> Volume / Disco Persistente]
	end

	A[<i class='fas fa-globe-americas' style='color:#3498DB'></i> Usuário da Internet]

	A -- Requisição HTTP/S --> B
	B -- Anexado a --> C
```

---

## 💡 Observações

- Os diagramas foram criados no [draw.io](https://draw.io) e também estão disponíveis em código Mermaid para facilitar visualização em Markdown.
- O projeto demonstra boas práticas de arquitetura AWS, separando processamento **serverless** (Lambda) e infraestrutura tradicional (**EC2 + EBS**).

---

## 👀 Como visualizar os diagramas

Você pode visualizar os diagramas Mermaid diretamente em plataformas que suportam esse formato, como o **GitHub** ou extensões do **VS Code**.

---

## 📚 Referências

- [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Amazon EC2](https://docs.aws.amazon.com/ec2/)
- [Amazon EBS](https://docs.aws.amazon.com/ebs/)
- [Amazon S3](https://docs.aws.amazon.com/s3/)
- [Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/)

---
