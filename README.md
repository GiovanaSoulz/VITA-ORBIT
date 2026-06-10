# VITA-ORBIT

## Integrantes

* Giovana Souza Vieira – RM 564430
* Beatriz Franco - RM 563686
* Maria Fernanda Santos RM 565277
* Natan Freitas De Moraes RM 564992

---

# Sobre o Projeto

O VITA ORBIT é uma API REST desenvolvida em Java com Spring Boot para monitoramento remoto da saúde de pessoas em ambientes extremos, astronautas em missões espaciais, rurais ou afetadas por eventos extremos.

A solução permite o cadastro de pessoas monitoradas, registro de indicadores clínicos, controle de medicamentos, gerenciamento de alertas de risco e autenticação segura utilizando JWT.

O objetivo é apoiar ações preventivas e fornecer informações em tempo real para tomada de decisão em cenários de emergência sanitária.

---

# Tecnologias Utilizadas

* Java 23
* Spring Boot 3
* Spring Data JPA
* Spring Security
* JWT Authentication
* PostgreSQL
* Swagger / OpenAPI
* Maven
* Lombok
* HATEOAS
* Hibernate

---

# Arquitetura da Aplicação

A aplicação segue o padrão de arquitetura em camadas:

Controller
↓
Service
↓
Repository
↓
PostgreSQL

Cada camada possui responsabilidade específica:

### Controller

Responsável por expor os endpoints REST.

### Service

Responsável pelas regras de negócio.

### Repository

Responsável pela persistência dos dados.

### Entity

Representação das tabelas do banco de dados.

### DTO

Objetos de transferência utilizados entre cliente e servidor.

---

# Funcionalidades

## Autenticação

* Cadastro de usuários
* Login
* Geração de Token JWT
* Proteção de endpoints

## Pessoas Monitoradas

* Cadastrar pessoa
* Listar pessoas
* Buscar por ID
* Atualizar dados
* Excluir cadastro

## Registros de Saúde

* Cadastro de indicadores clínicos
* Atualização de registros
* Exclusão
* Consulta por ID
* Listagem geral

### Indicadores monitorados

* Temperatura
* Frequência cardíaca
* Pressão arterial
* Oxigenação
* Nível de dor
* Hidratação
* Horas de sono
* Sintomas

## Medicamentos

* Cadastro
* Consulta
* Atualização
* Exclusão

## Associação Pessoa x Medicamento

Implementação utilizando chave composta:

MedicamentoPacienteId

Relacionamento:

PessoaMonitorada ↔ Medicamento

---

# Classificação de Risco

O sistema calcula automaticamente o nível de risco clínico.

### BAIXO

Paciente estável.

### MODERADO

Temperatura acima de 37,5°C.

### ALTO

* Temperatura ≥ 39°C
* Frequência cardíaca > 120 bpm
* Dor ≥ 8

### CRÍTICO

Oxigenação abaixo de 90%.

---

# Herança Implementada

Foi utilizado o conceito de herança do JPA através da estratégia JOINED.

Classe Pai:

Alerta

Classes Filhas:

* AlertaModerado
* AlertaCritico

Estratégia:

```java
@Inheritance(strategy = InheritanceType.JOINED)
```

---

# Chave Composta

Foi implementada através da entidade:

```java
MedicamentoPacienteId
```

Utilizando:

```java
@Embeddable
@EmbeddedId
@MapsId
```

Relacionando:

* PessoaMonitorada
* Medicamento

---

# Segurança

A aplicação utiliza:

* Spring Security
* JWT Token
* PasswordEncoder BCrypt

Fluxo:

1. Usuário realiza cadastro.
2. Usuário realiza login.
3. Sistema gera Token JWT.
4. Token é enviado no Header Authorization.
5. Endpoints protegidos validam o token.

Exemplo:

```http
Authorization: Bearer eyJhbGciOiJIUzI1Ni...
```

---

# Endpoints Principais

## Autenticação

POST /auth/register

POST /auth/login

---

## Pessoas

GET /pessoas

GET /pessoas/{id}

POST /pessoas

PUT /pessoas/{id}

DELETE /pessoas/{id}

---

## Registros

GET /registros

GET /registros/{id}

POST /registros

PUT /registros/{id}

DELETE /registros/{id}

---

## Medicamentos

GET /medicamentos

GET /medicamentos/{id}

POST /medicamentos

PUT /medicamentos/{id}

DELETE /medicamentos/{id}

---

# Swagger

Documentação disponível em:

http://localhost:9090/swagger-ui/index.html

---

# Banco de Dados

PostgreSQL

Principais tabelas:

* tb_usuario
* tb_pessoa_monitorada
* tb_endereco
* tb_registro_saude
* tb_medicamento
* tb_medicamento_paciente
* tb_alerta
* tb_alerta_moderado
* tb_alerta_critico

---

# Como Executar

## Clonar Projeto

```bash
git clone <repositorio>
```

## Instalar Dependências

```bash
mvn clean install
```

## Executar

```bash
mvn spring-boot:run
```

Aplicação disponível em:

```bash
http://localhost:9090
```

---

# Diferenciais Implementados

✔ Spring Security

✔ JWT Authentication

✔ Swagger/OpenAPI

✔ HATEOAS

✔ Herança JPA

✔ Chave Composta

✔ Tratamento Global de Exceções

✔ DTO Pattern

✔ Arquitetura em Camadas

✔ PostgreSQL

✔ Classificação Automática de Risco

---
Deploy da API 

https://orbital-health-monitor.onrender.com 

Documentação Swagger 

https://orbital-health-monitor.onrender.com/swagger-ui/index.html 

Link do Postman 

https://giovana-vieiras1302-3216039.postman.co/workspace/Giovana-Souza's-Workspace~71849833-8bbb-44ef-86ab-68a5a6d1328e/collection/49645015-b476a9a7-c21f-4a17-a199-38ad63ff86af?action=share&creator=49645015 

Vídeo de Apresentação 

https://youtu.be/HhdrqEq1c-o?si=r57dTLEvm_KXnQ9b 
https://youtu.be/Lhs25gQ5Yoo?si=fa5m3GXzWCATPhh4 


