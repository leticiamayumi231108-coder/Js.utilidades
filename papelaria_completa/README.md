# Sistema de Papelaria — Frontend + Backend

Este pacote reúne o backend Java/Spring Boot e o frontend Angular.

## Requisitos

- Docker Desktop (recomendado para iniciar PostgreSQL e API)
- Node.js compatível com Angular 22 (use Node.js 22.12 ou superior) e npm
- Navegador atualizado

## Estrutura

- `backend/`: API Java 21, Spring Boot e PostgreSQL
- `frontend/`: aplicação Angular 22

## Como executar no Windows

### 1. Iniciar banco de dados e backend

1. Instale e abra o Docker Desktop.
2. Abra o PowerShell na pasta `backend`.
3. Execute:

```powershell
docker compose up --build
```

4. Aguarde o PostgreSQL e a API iniciarem. A API ficará em `http://localhost:8080`.

Documentação Swagger:
`http://localhost:8080/swagger-ui/index.html`

Saúde da API:
`http://localhost:8080/actuator/health`

### 2. Iniciar o frontend Angular

1. Abra uma segunda janela do PowerShell.
2. Entre na pasta `frontend`.
3. Instale as dependências:

```powershell
npm ci
```

4. Inicie o Angular:

```powershell
npm start
```

5. Acesse `http://localhost:4200`.

O frontend está configurado para chamar a API em `http://localhost:8080`.

### 3. Encerrar

- No terminal do Angular: `Ctrl + C`.
- No terminal do Docker: `Ctrl + C` e depois `docker compose down`.
- Para apagar também os dados persistidos do PostgreSQL: `docker compose down -v` (ATENÇÃO: remove os dados do banco).

## Execução do backend sem Docker (alternativa)

Com JDK 21 e PostgreSQL instalado/configurado conforme `backend/src/main/resources/application.yaml`:

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

## Observações importantes

- O ZIP recebido do frontend contém Angular 22 e configura `apiUrl` como `http://localhost:8080`.
- O backend permite CORS para `http://localhost:4200` nos controllers analisados.
- O ZIP recebido do backend não inclui o frontend; por isso os projetos foram organizados em pastas separadas.
- O frontend depende de Node.js/npm; o backend depende de Java 21/Maven ou Docker.
- A análise do código não garante que a aplicação esteja validada em execução. A instalação de dependências/build do Angular não foi concluída neste ambiente devido ao tempo de espera do download. Faça `npm ci` e `npm run build` localmente para validar.
- Segurança: o login atual não implementa autenticação robusta por token e o backend armazena/compara senha sem hash. Não use dados ou senhas reais até corrigir esse ponto.
- Credenciais do PostgreSQL no Compose são padrões de desenvolvimento (`admin`/`postgres`); altere-as antes de qualquer implantação real.
