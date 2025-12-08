# Chamado-Pro 🚀

Sistema completo de gerenciamento de chamados, desenvolvido com **Java Spring Boot** no backend e **Angular** no frontend. O projeto foi criado para oferecer uma solução organizada, rápida e escalável para abertura, acompanhamento e fechamento de chamados, atendendo necessidades reais de suporte interno ou externo.

Este README descreve todo o funcionamento da aplicação, tecnologias utilizadas e a infraestrutura construída na AWS.

---

## 📌 Visão Geral do Projeto
O **Chamado-Pro** permite que usuários registrem chamados, acompanhem seu status, façam atualizações e finalizem atendimentos. Ele foi projetado pensando em **organização, desempenho e escalabilidade**, com backend robusto, frontend moderno e uma arquitetura em nuvem bem estruturada.

---

## 🧩 Tecnologias Utilizadas

### **Backend — Java / Spring Boot**
- Spring Boot 3+
- Spring Web
- Spring Data JPA
- Spring Security + JWT
- Lombok
- PostgreSQL
- Maven

**Principais recursos do backend:**
- API REST com endpoints protegidos por JWT
- Persistência com JPA e PostgreSQL
- Camadas organizadas (Controller, Service, Repository)
- Tratamento global de exceções
- Autenticação e autorização robustas

---

### **Frontend — Angular**
- Angular 17+
- TypeScript
- RxJS
- Angular Material (opcional)
- HTML & SCSS

**Principais recursos do frontend:**
- Interface responsiva
- Login e armazenamento seguro do token
- Formulários reativos
- Listagem, criação e edição de chamados
- Serviços integrados ao backend via HTTPClient

---

## ☁️ Arquitetura AWS Desenvolvida
A aplicação conta com uma infraestrutura sólida hospedada na AWS, garantindo alta disponibilidade, resiliência e desempenho.

### **Serviços Utilizados**

#### **EC2**
- Hospedagem do backend em uma instância Linux configurada com Java + Spring Boot
- NGINX como proxy reverso (quando necessário)

#### **Load Balancer (ALB)**
- Distribuição de tráfego
- Health Checks configurados
- Suporte a múltiplas instâncias

#### **Auto Scaling Group (ASG)**
- Criação automática de novas instâncias
- Baseado em métricas de uso da CPU / tráfego
- Utiliza Launch Templates versionados

#### **RDS — PostgreSQL**
- Banco de dados gerenciado
- Backup automático
- Alta durabilidade

#### **VPC personalizada**
- Sub-redes públicas e privadas
- Tabelas de roteamento configuradas
- Segurança via Security Groups

#### **IAM**
- Políticas seguras para acesso a EC2, ASG e RDS
- Usuários e permissões organizadas

#### **S3 (opcional)**
- Possibilidade de hospedar o frontend Angular
- Armazenamento de estáticos

### **Testes de Carga (K6 + Grafana)**
O sistema passou por testes de estresse utilizando **k6**:
```
k6 run --vus 200 --duration 3m stress.js
```
Script utilizado:
```javascript
const http = require("k6/http");

exports.default = function () {
  http.get("http://chamado-pro-alb-xxxxxxxxx.us-east-1.elb.amazonaws.com/");
};
```
Esses testes validaram o comportamento do ALB, ASG e EC2 sob carga real.

---

## 📐 Arquitetura Geral
A arquitetura final do Chamado-Pro funciona assim:

1. **O usuário acessa o frontend Angular** (hospedado em S3 ou EC2)
2. O frontend envia requisições para o **ALB**
3. O ALB encaminha para uma instância do **EC2** via ASG
4. O backend acessa o **RDS (PostgreSQL)**
5. O sistema responde com os dados ao usuário
6. Logs e monitoramento são feitos via CloudWatch

Essa arquitetura garante **alta disponibilidade**, capacidade de escalar e segurança.

---

## 🛠️ Como Rodar Localmente

### **Backend**
```bash
git clone https://github.com/guualonso/chamado-pro
cd backend
mvn spring-boot:run
```
O backend iniciará por padrão em:  
`http://localhost:8080`

---

### **Frontend**
```bash
cd frontend
npm install
npm start
```
O frontend iniciará em:  
`http://localhost:4200`

---

## 📄 Status do Projeto
✔ Backend funcional  
✔ Frontend Angular configurado  
✔ Autenticação JWT  
✔ Banco PostgreSQL integrado  
✔ Arquitetura AWS criada e validada  
✔ Testes de estresse realizados  

Próximos passos:
- Criar novas features (comentários, anexos, categorias)
- Adicionar gráficos e dashboards

---

## 👨‍💻 Autor
Desenvolvido por **Gustavo Alonso (@guualonso)**.

Sinta-se à vontade para contribuir, abrir issues e sugerir melhorias!

