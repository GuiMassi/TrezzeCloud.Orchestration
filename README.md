# README - TrezzeCloud.Orchestration

````md
# TrezzeCloud.Orchestration

Repositório responsável pela orquestração da plataforma TrezzeCloud utilizando Docker Compose e Kubernetes.

## Objetivo

Centralizar toda a infraestrutura necessária para execução dos microsserviços da plataforma:

- RabbitMQ
- SQL Server
- UsersAPI
- CatalogAPI
- PaymentsAPI
- NotificationsAPI

Além disso, este repositório contém os manifestos Kubernetes utilizados para deploy local da aplicação.

---

# Arquitetura

A solução foi construída utilizando arquitetura de microsserviços orientada a eventos.

## Microsserviços

| Serviço | Responsabilidade |
|---|---|
| UsersAPI | Cadastro, autenticação JWT e autorização |
| CatalogAPI | CRUD de jogos e fluxo de compra |
| PaymentsAPI | Processamento de pagamentos |
| NotificationsAPI | Envio de notificações |

---

# Tecnologias

- .NET 10
- ASP.NET Core
- Entity Framework Core
- SQL Server
- RabbitMQ
- MassTransit
- Docker
- Docker Compose
- Kubernetes

---

# Repositórios

## Orchestration

https://github.com/GuiMassi/TrezzeCloud.Orchestration.git

## UsersAPI

https://github.com/GuiMassi/TrezzeCloud.UsersAPI.git

## CatalogAPI

https://github.com/GuiMassi/TrezzeCloud.CatalogAPI.git

## PaymentsAPI

https://github.com/GuiMassi/TrezzeCloud.PaymentsAPI.git

## NotificationsAPI

https://github.com/GuiMassi/TrezzeCloud.NotificationsAPI.git

---

# Docker Compose

## Executar aplicação completa

```bash
docker compose up --build
````

---

# Kubernetes

## Pré-requisitos

* Docker Desktop
* Kubernetes habilitado
* kubectl instalado

---

## Aplicar manifestos

```bash
kubectl apply -f .
```

---

## Verificar pods

```bash
kubectl get pods
```

---

# Estrutura Kubernetes

```txt
k8s/
 ├── rabbitmq
 ├── sqlserver
 ├── users-api
 ├── catalog-api
 ├── payments-api
 └── notifications-api
```

---

# Fluxos de Eventos

## Cadastro de usuário

1. UsersAPI cria usuário.
2. Publica UserCreatedEvent.
3. NotificationsAPI consome evento.
4. Simula envio de e-mail de boas-vindas.

---

## Compra de jogo

1. CatalogAPI inicia compra.
2. Publica OrderPlacedEvent.
3. PaymentsAPI processa pagamento.
4. Publica PaymentProcessedEvent.
5. CatalogAPI adiciona jogo à biblioteca.
6. NotificationsAPI envia confirmação.

---

# Deploy Local Kubernetes

## RabbitMQ

```bash
kubectl apply -f .\k8s\rabbitmq\rabbitmq.yaml
```

## SQL Server

```bash
kubectl apply -f .\k8s\sqlserver\sqlserver.yaml
```

## UsersAPI

```bash
kubectl apply -f .\k8s\users-api\users-api.yaml
```

## CatalogAPI

```bash
kubectl apply -f .\k8s\catalog-api\catalog-api.yaml
```

## PaymentsAPI

```bash
kubectl apply -f .\k8s\payments-api\payments-api.yaml
```

## NotificationsAPI

```bash
kubectl apply -f .\k8s\notifications-api\notifications-api.yaml
```

---

# Verificação Final

```bash
kubectl get pods
kubectl get svc
```

