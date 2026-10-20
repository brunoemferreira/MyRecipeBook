# <p align="center"><img src="./assets/icons/briefcase.svg" width="40" height="40" valign="middle" /> MyRecipeBook <img src="./assets/icons/activity.svg" width="40" height="40" valign="middle" /></p>

<p align="center">
  <strong>Catálogo e Gerenciador de Receitas desenvolvido com as melhores práticas de Clean Architecture e .NET moderno.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/.NET-10.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt=".NET 10" />
  <img src="https://img.shields.io/badge/C%23-13-239120?style=for-the-badge&logo=csharp&logoColor=white" alt="C#" />
  <img src="https://img.shields.io/badge/Architecture-Clean%20Architecture-007ACC?style=for-the-badge" alt="Clean Architecture" />
  <img src="https://img.shields.io/badge/OpenAPI-Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=black" alt="Swagger" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="MIT License" />
</p>

---

## <img src="./assets/icons/explore.svg" width="24" height="24" valign="middle" /> Sumário

- [Visão Geral](#-visão-geral)
- [Objetivos do Projeto](#-objetivos-do-projeto)
- [Plano Arquitetural](#-plano-arquitetural)
  - [Arquitetura Inicial](#1-arquitetura-inicial)
  - [Arquitetura Melhorada Final](#2-arquitetura-melhorada-final)
- [Detalhamento das Camadas](#-detalhamento-das-camadas)
- [Tecnologias e Ferramentas](#-tecnologias-e-ferramentas)
- [Estrutura da Solução](#-estrutura-da-solução)
- [Como Executar o Projeto](#-como-executar-o-projeto)
- [Contexto Educacional](#-contexto-educacional)
- [Licença](#-licença)

---

## <img src="./assets/icons/explore.svg" width="24" height="24" valign="middle" /> Visão Geral

O **MyRecipeBook** é uma aplicação completa para gerenciamento e catálogo de receitas culinárias desenvolvida em **.NET 10**. O foco primordial do projeto é a aplicação prática de padrões arquiteturais corporativos, com ênfase em:

- **Clean Architecture & DDD**: Separação rigorosa de responsabilidades e desacoplamento do domínio em relação a frameworks e banco de dados.
- **Manutenibilidade e Escalabilidade**: Estrutura modular pensada para facilitar a inclusão de novas features e regras de negócio.
- **Segurança e Padronização**: Contratos de comunicação bem definidos e tratamento de exceções global e resiliente.
- **Preparado para o Mercado**: Segue padrões reais exigidos em equipes de engenharia de software de alta performance.

---

## <img src="./assets/icons/target.svg" width="24" height="24" valign="middle" /> Objetivos do Projeto

- <img src="./assets/icons/code.svg" width="18" height="18" valign="middle" /> **Isolamento de Responsabilidades:** Cada projeto tem um propósito único e limites claros.
- <img src="./assets/icons/connect.svg" width="18" height="18" valign="middle" /> **Contratos Estáveis:** DTOs e ViewModels isolados na camada de comunicação, protegendo o modelo de domínio de exposições indevidas.
- <img src="./assets/icons/target.svg" width="18" height="18" valign="middle" /> **Tratamento de Exceções Padronizado:** Camada dedicada para gerenciar erros conhecidos e inesperados de forma elegante.
- <img src="./assets/icons/database.svg" width="18" height="18" valign="middle" /> **Persistência Desacoplada:** Acesso a dados via repositórios na camada de infraestrutura, com inversão de dependência (DIP).

---

## <img src="./assets/icons/architecture.svg" width="26" height="26" valign="middle" /> Plano Arquitetural

A arquitetura do projeto foi planejada em duas etapas evolutivas:

### 1. Arquitetura Inicial

Na fase inicial, a solução foi modelada no padrão clássico de 4 camadas:

<p align="center">
  <img src="./assets/desenhoArquitetural.png" alt="Arquitetura Inicial do MyRecipeBook" width="850" />
</p>

#### Camadas da Arquitetura Inicial:
- <img src="./assets/icons/backend.svg" width="20" height="20" valign="middle" /> **API Project (`MyRecipeBook.Api`)**: Ponto de entrada, controladores REST e injeção de dependências.
- <img src="./assets/icons/code.svg" width="20" height="20" valign="middle" /> **Application Project (`MyRecipeBook.Application`)**: Casos de uso, orquestração e regras de serviço.
- <img src="./assets/icons/architecture.svg" width="20" height="20" valign="middle" /> **Domain Project (`MyRecipeBook.Domain`)**: Entidades, contratos/interfaces e regras de negócio essenciais.
- <img src="./assets/icons/database.svg" width="20" height="20" valign="middle" /> **Infrastructure Project (`MyRecipeBook.Infrastructure`)**: Implementação de repositórios, persistência de dados e serviços externos.

---

### 2. Arquitetura Melhorada Final

Para suportar um ecossistema mais robusto e desacoplado, foram introduzidas duas camadas especializadas: **Exception** e **Communication**.

<p align="center">
  <img src="./assets/desenhoArquitetural2.png" alt="Arquitetura Melhorada do MyRecipeBook" width="850" />
</p>

#### Evolução e Benefícios:
1. **`MyRecipeBook.Communication`**: Desacopla as requisições (Requests) e respostas (Responses) da API, permitindo que clientes (web, mobile) consumam contratos padronizados sem acoplamento à lógica de aplicação.
2. **`MyRecipeBook.Exception`**: Centraliza a taxonomia de erros, filtros de exceção e mensagens customizadas, evitando repetição de código e mantendo as respostas HTTP consistentes.

---

## <img src="./assets/icons/tools.svg" width="24" height="24" valign="middle" /> Detalhamento das Camadas

A tabela a seguir resume as camadas da solução final e seus papéis:

| Ícone | Camada / Projeto | Responsabilidade Principal | Dependências Permitidas |
| :---: | :--- | :--- | :--- |
| <img src="./assets/icons/backend.svg" width="22" height="22" /> | **`MyRecipeBook.Api`** | Ponto de entrada HTTP, Swagger/OpenAPI, Middlewares e configuração de DI. | `Application`, `Communication`, `Exception` |
| <img src="./assets/icons/connect.svg" width="22" height="22" /> | **`MyRecipeBook.Communication`** | Contratos de troca de dados (DTOs, Requests, Responses). | *Nenhuma* (Independente) |
| <img src="./assets/icons/target.svg" width="22" height="22" /> | **`MyRecipeBook.Exception`** | Exceções de negócio, códigos de erro e catálogo de mensagens. | *Nenhuma* (Independente) |
| <img src="./assets/icons/code.svg" width="22" height="22" /> | **`MyRecipeBook.Application`** | Casos de uso (Use Cases), validadores e orquestração de regras. | `Domain`, `Communication`, `Exception` |
| <img src="./assets/icons/architecture.svg" width="22" height="22" /> | **`MyRecipeBook.Domain`** | Entidades de domínio, interfaces de repositório e regras centrais. | *Nenhuma* (Núcleo) |
| <img src="./assets/icons/database.svg" width="22" height="22" /> | **`MyRecipeBook.Infrastructure`** | Acesso ao banco de dados (EF Core), migrações e integrações externas. | `Domain` |

---

## <img src="./assets/icons/tools.svg" width="24" height="24" valign="middle" /> Tecnologias e Ferramentas

O projeto utiliza o estado da arte do ecossistema .NET:

- <img src="./assets/icons/backend.svg" width="18" height="18" valign="middle" /> **Framework:** [.NET 10](https://dotnet.microsoft.com/) / ASP.NET Core Web API
- <img src="./assets/icons/code.svg" width="18" height="18" valign="middle" /> **Linguagem:** C# 13
- <img src="./assets/icons/architecture.svg" width="18" height="18" valign="middle" /> **Padrão Arquitetural:** Clean Architecture & Domain-Driven Design (DDD)
- <img src="./assets/icons/database.svg" width="18" height="18" valign="middle" /> **Persistência / ORM:** Entity Framework Core
- <img src="./assets/icons/explore.svg" width="18" height="18" valign="middle" /> **Documentação da API:** OpenAPI & Swagger UI
- <img src="./assets/icons/bot.svg" width="18" height="18" valign="middle" /> **Testes:** xUnit, Moq, FluentAssertions *(camada de testes em evolução)*

---

## <img src="./assets/icons/code.svg" width="24" height="24" valign="middle" /> Estrutura da Solução

```text
MyRecipeBook/
├── assets/
│   ├── desenhoArquitetural.png        # Diagrama da arquitetura inicial
│   ├── desenhoArquitetural2.png       # Diagrama da arquitetura melhorada
│   └── icons/                         # Ícones visuais do projeto
│       ├── activity.svg
│       ├── architecture.svg
│       ├── backend.svg
│       ├── bot.svg
│       ├── briefcase.svg
│       ├── cloud.svg
│       ├── code.svg
│       ├── connect.svg
│       ├── database.svg
│       ├── education.svg
│       ├── explore.svg
│       ├── frontend.svg
│       ├── target.svg
│       ├── tools.svg
│       └── user.svg
├── src/
│   ├── Backend/
│   │   ├── MyRecipeBook.Api/              # Camada de apresentação e controladores
│   │   ├── MyRecipeBook.Application/      # Casos de uso e lógica de negócio
│   │   ├── MyRecipeBook.Domain/           # Entidades e interfaces
│   │   └── MyRecipeBook.Infrastructure/   # Persistência e serviços externos
│   └── Shared/
│       ├── MyRecipeBook.Communication/    # DTOs, Requests e Responses
│       └── MyRecipeBook.Exception/        # Tratamento centralizado de erros
├── tests/                             # Testes unitários e de integração
├── MyRecipeBook.slnx                  # Arquivo da solução .NET
├── LICENSE.txt                        # Licença MIT
└── README.md                          # Documentação do projeto
```

---

## <img src="./assets/icons/activity.svg" width="24" height="24" valign="middle" /> Como Executar o Projeto

### Pré-requisitos

- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) instalado.
- IDE recomendada: [Visual Studio 2026](https://visualstudio.microsoft.com/), [VS Code](https://code.visualstudio.com/) com a extensão C# Dev Kit, ou [JetBrains Rider](https://www.jetbrains.com/rider/).
- Git para clonar o repositório.

### Passo a Passo

1. **Clonar o repositório:**
   ```bash
   git clone https://github.com/brunoemferreira/MyRecipeBook.git
   cd MyRecipeBook
   ```

2. **Restaurar as dependências:**
   ```bash
   dotnet restore
   ```

3. **Compilar a solução:**
   ```bash
   dotnet build
   ```

4. **Executar a API:**
   ```bash
   dotnet run --project src/Backend/MyRecipeBook.Api
   ```

5. **Acessar a documentação Swagger:**
   - Abra o navegador e navegue até: `https://localhost:5001/swagger` (ou a porta configurada no terminal).

---

## <img src="./assets/icons/education.svg" width="24" height="24" valign="middle" /> Contexto Educacional

Este repositório foi concebido como parte do curso **".NET: Um Curso Orientado para o Mercado de Trabalho"** na plataforma **Udemy**. 

O curso é direcionado à capacitação de desenvolvedores com foco nas exigências práticas do mercado:
- Arquitetura corporativa desacoplada;
- Escrever código legível, testável e manutenível;
- Boas práticas de design de software e governança de APIs.

---

## <img src="./assets/icons/briefcase.svg" width="24" height="24" valign="middle" /> Licença

Este projeto está distribuído sob a licença **MIT**. Consulte o arquivo [LICENSE.txt](LICENSE.txt) para mais detalhes.

---

<p align="center">
  Desenvolvido com dedicação por <strong>Bruno Ferreira</strong> 🚀
</p>
