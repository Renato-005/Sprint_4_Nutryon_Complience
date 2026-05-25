# 4º Sprint – 2º Semestre: Compliance & Quality Assurance
## Projeto Nutryon (Backend API)

---

## Integrantes e RMs

| Nome | RM |
|---|---|
| Renato Silva Alexandre Bezerra | RM560928 |
| Victor Rodrigues de Lima Lourenço | RM560087 |
| Luan Noqueli Klochko | RM560313 |
| Lucas Higuti Fontanezi | RM561120 |

---

## 1. Objetivo da Sprint 4

A **Sprint 4** corresponde à entrega de **Compliance & Quality Assurance**. O foco desta sprint foi a criação e execução de um plano de testes completo para o projeto Nutryon, abrangendo:

- **Parte A (80%)** — Testes manuais documentados no Azure Boards (Test Plans), com Test Suites e Test Cases vinculados aos PBIs do backlog
- **Parte B (20%)** — Testes automatizados via Postman com assertions programáticas, executados contra a API em produção no Azure

---

## 2. Repositórios

| Componente | Repositório |
|---|---|
| Backend Java | https://github.com/VoyDcode/Nutryon |
| Frontend Angular | https://github.com/VoyDcode/Nutryon-angular |

---

## 3. Links importantes

| Recurso | Link |
|---|---|
| 🗂️ Azure DevOps / Boards | https://dev.azure.com/RM560087/Nutryon |
| 🎥 Vídeo dos testes automatizados (Postman) | https://youtu.be/XzRBeZ0HEXc |

---

## 4. Arquitetura em nuvem

```
Usuário
  ↓ HTTPS
Azure Static Web Apps
Frontend Angular (Nutryon-angular)
  ↓ HTTPS/JSON
Azure Web App
Backend Nutryon API — Java Spring Boot
  ↓ JDBC (Oracle Thin)
Oracle Cloud Autonomous Database (Always Free)
  ↓
Persistência dos Dados
```

| Camada | Serviço |
|---|---|
| Frontend | Azure Static Web Apps |
| Backend | Azure Web App (App Service) |
| Banco de Dados | Oracle Cloud Autonomous Database (Always Free) |
| CI/CD Backend | Azure DevOps Pipelines |
| CI/CD Frontend | Azure DevOps Pipelines |
| Documentação API | Swagger UI / SpringDoc OpenAPI |

---

## 5. Testes manuais — Azure Test Plans

Os testes manuais foram criados diretamente no Azure Boards, com Test Cases vinculados aos PBIs de cada sprint.

### Test Plans criados

| Test Plan | Sprint | Período | Suites | Resultado |
|---|---|---|---|---|
| Nutryon Team_Stories_Sprint 3 | Sprint 3 | 24/03 – 10/04/2026 | 6 suites | ✅ 100% Passed |
| Nutryon Team_Stories_Sprint 4 | Sprint 4 | 11/04 – 24/05/2026 | 5 suites | ✅ 100% Passed |

### Test Cases — Sprint 3

| Test Case | PBI Vinculado | Resultado |
|---|---|---|
| TC01 - Cadastro de usuário com dados válidos | 5 - Cadastro de Usuário | ✅ Passed |
| TC02 - Login com credenciais válidas | 6 - Login do usuário | ✅ Passed |
| TC08 - Validação de autenticação JWT | 21 - Autenticação JWT | ✅ Passed |
| TC09 - Cadastro e gestão de ingredientes | 23 - Gestão de ingredientes | ✅ Passed |
| TC05 - Registro manual de refeição | 14 - Registrar refeição manualmente | ✅ Passed |
| TC11 - Sugestão nutricional via IA | 27 - Componente de IA com Oracle ML | ✅ Passed |

### Test Cases — Sprint 4

| Test Case | PBI Vinculado | Resultado |
|---|---|---|
| TC07 - Atualização do perfil nutricional | 18 - Atualizar perfil nutricional | ✅ Passed |
| TC03 - Cálculo automático de macros nutricionais | 7 - Cálculo automático de macros | ✅ Passed |
| TC10 - Exclusão de refeição registrada | 24 - Exclusão de refeição | ✅ Passed |
| TC06 - Visualização do resumo diário e semanal | 16 - Resumo diário e semanal | ✅ Passed |
| TC04 - Definição de estratégia nutricional | 11 - Definição de estratégia nutricional | ✅ Passed |

---

## 6. Testes automatizados — Postman

Coleção: **Nutryon - Testes Automatizados**
URL base: `https://nutryon-f8h2e8bqa0d7gjbx.southafricanorth-01.azurewebsites.net`

### Resultado da execução

| Informação | Valor |
|---|---|
| Data de execução | 24/05/2026 |
| Total de assertions | 8 |
| Passed | ✅ 8 |
| Failed | ❌ 0 |
| Ambiente | Nuvem — Azure Web App (sem localhost) |

### Testes criados

| Teste | Método | Endpoint | Resultado |
|---|---|---|---|
| TC01 - Health Check | GET | `/health` | ✅ PASS |
| TC02 - Login JWT | POST | `/auth/login` | ✅ PASS |
| TC03 - Listar Ingredientes | GET | `/api/ingredientes` | ✅ PASS |
| TC04 - Acesso sem token | GET | `/api/refeicoes` | ✅ PASS |

🎥 **Vídeo da execução dos testes automatizados:** https://youtu.be/XzRBeZ0HEXc

---

## 7. Endpoints da API

### Autenticação (público)

| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/auth/register` | Registrar novo usuário |
| POST | `/auth/login` | Login — retorna Bearer Token JWT |

### Ingredientes

| Método | Endpoint | Acesso | Descrição |
|---|---|---|---|
| GET | `/api/ingredientes` | Autenticado | Listar todos os ingredientes |
| POST | `/api/ingredientes` | ADMIN | Criar ingrediente |

### Refeições

| Método | Endpoint | Acesso | Descrição |
|---|---|---|---|
| GET | `/api/refeicoes` | Autenticado | Listar refeições (filtro por data opcional) |
| POST | `/api/refeicoes` | Autenticado | Criar refeição com itens |
| DELETE | `/api/refeicoes/{id}` | Autenticado | Excluir refeição própria |
| GET | `/api/refeicoes/resumo-diario/{data}` | Autenticado | Totais de macros do dia |
| GET | `/api/refeicoes/resumo-semanal/{segunda}` | Autenticado | Resumo semanal de macros |

### Utilitários

| Método | Endpoint | Acesso | Descrição |
|---|---|---|---|
| GET | `/health` | Público | Health check da API |
| GET | `/swagger-ui/index.html` | Público | Documentação interativa |

---

## 8. Como usar a API (fluxo de autenticação)

1. `POST /auth/register` — criar usuário com os campos `nome`, `email`, `senha` e `role` (`ADMIN` ou `USER`)
2. `POST /auth/login` — receber token JWT
3. Usar o token no header `Authorization: Bearer <token>` nas demais requisições

---

## 9. Tecnologias

| Tecnologia | Versão | Função |
|---|---|---|
| Java | 17 | Linguagem do backend |
| Spring Boot | 3.5.6 | Framework principal |
| Spring Security | 6.x | Autenticação e autorização |
| JWT (Auth0) | 4.4.0 | Geração e validação de tokens |
| Spring Data JPA / Hibernate | 6.x | Camada de persistência |
| Oracle JDBC (ojdbc11) | 23.3.0 | Driver de banco de dados |
| SpringDoc OpenAPI | 2.8.13 | Documentação Swagger |
| Maven | 3.x | Gerenciador de build |
