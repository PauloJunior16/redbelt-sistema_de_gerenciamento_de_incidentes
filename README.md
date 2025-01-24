# Redbelt - Sistema de Gerenciamento de Incidentes
Um sistema para gerenciamento de incidentes de segurança, construído com Laravel (backend) e React (frontend).

## Estrutura do Projeto
O projeto é dividido em dois módulos principais:
- [`backend/`](https://github.com/PauloJunior16/backend): API RESTful em Laravel integrado com banco de dados MySQL
- [`frontend/`](https://github.com/PauloJunior16/frontend): Interface de usuário em React

## Configuração e Execução
### Requisitos
- Docker e Docker Compose
- Node.js 18+
- PHP 8.2+
- Composer

> [!IMPORTANT]
> ### Configuração inicial
> Clone este repositorio da forma que preferir, seja via SSH ou HTTPS, após isso acesse a pasta do projeto e rode o seguinte comando:
> 
> `git submodule update --init --recursive`
> 
> Esse comando ira realizar a conexão e atualização com os submodulos do projeto.
> 
> Após isso poderá seguir com as configuração do backend e frontend.

### Backend (Laravel)
 Após clonar o projeto navegue até a pasta do backend:

`cd backend`

1. Configure o ambiente copiando o criando uma copia do arquivo de váriaveis de ambiente e preencha conforme o ambiente de desenvolvimento:

`cp .env.example .env`

Em seguida rode o comando do composer para instalar as dependencias:

`composer install`

2. Faça a build do Dockerfile e inicie os containers Docker:

`docker-compose build && docker-compose up -d`

3. Caso necessario execute as migrações:

`docker-compose exec app php artisan migrate`

> [!NOTE]
> A API estará disponível em `http://localhost:8000/api`

#### Documentação Da API (Swagger)
A documentação estará disponivel em `http://localhost:8000/api/documentation`

* Endpoints Principais

  * POST  - `/api/register` - Registro de usuário
  * POST  - `/api/login` - Login de usuário
  * GET   - `/api/incidents` - Listar incidentes
  * POST  - `/api/incidents` - Criar incidente
  * PUT   - `/api/incidents/{id}` - Atualizar incidente
  * DELETE - `/api/incidents/{id}` - Deletar incidente
  * POST   - `/api/logout` - Logout de usuário


### Frontend (React)
Após clonar o projeto navegue até a pasta do frontend:

`cd frontend`

1. Instale as dependências:

`npm install`

2. Inicie o servidor de desenvolvimento:

`npm run dev`

> [!NOTE]
> O frontend estará disponível em `http://localhost:5173`

## Decisões de Design e Arquitetura
### Backend
- Autenticação: Implementada usando Laravel Sanctum para tokens de API
- Arquitetura: Seguindo os princípios REST e utilizando recursos do Laravel
- Controllers para lógica de negócios
- Models para interação com banco de dados
- Migrations para versionamento do banco
- Middleware para autenticação e autorização

#### Principios SOLID implementados
- Single Responsability (SRP): Controllers focados em responsabilidades espeficicas, o AuthController para autenticação e o IncidentCOntroller para gestão dos incidentes
- Interface Segregation (ISP): Uso das interfaces HasApiTokens e Notifiable através dos traits do Laravel
- Dependency Inversion (DIP): Dependência de abstrações através do service container do Laravel

### Frontend
- Estado: Gerenciamento local de estado com React Hooks
- Roteamento: React Router para navegação
- Componentes: Arquitetura baseada em componentes reutilizáveis

#### Design Patterns
- Container/Presentational Pattern: Separação entre componentes de lógica (Dashboard) e componentes de apresentação (IncidentForm)
- Provider Pattern: Implementado através do React Context para gerenciamento de estado global
- Custom Hook Pattern: Encapsulamento de lógica reutilizável (useEffect para carregar incidentes)

#### Princípios SOLID Implementados
- Single Responsibility (SRP): Cada componente tem uma única responsabilidade
  - Dashboard: Gerenciamento de incidentes
  - IncidentForm: Formulário de criação/edição/exclusão de incidentes
  - Auth: Autenticação do usuário (login e registro)

#### Arquitetura de Componentes
- Composição: Componentes menores e reutilizáveis formando interfaces maiores
- Prop Drilling: Minimizado através de gerenciamento de estado local
- Stateful/Stateless: Distinção clara entre componentes com e sem estado

### Esta arquitetura promove:
- Manutenibilidade através de componentes isolados
- Testabilidade por meio de responsabilidades bem definidas
- Escalabilidade através de padrões estabelecidos
- Reutilização de código com componentes modulares

