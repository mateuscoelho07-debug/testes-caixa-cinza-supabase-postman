# Testes Caixa Cinza em API de Autenticação (Supabase + Postman)

> **Aluno:** `<SEU NOME COMPLETO>` — **RA/Turma:** `<PREENCHER>`

> ⚠️ **Antes de entregar:** procure por `<PREENCHER>` / `TODO` neste arquivo e substitua pelos dados e prints reais produzidos por você. Nada aqui deve ser copiado de terceiros.

## Estrutura do repositório

```
/README.md
/postman/    -> collection e environment exportados do Postman
/prints/     -> evidências (prints reais)
/planilha/   -> registro_testes.csv (planilha de testes)
```

# Introdução

Este projeto documenta a execução de testes funcionais **caixa cinza** sobre a API de autenticação do **Supabase** (GoTrue), usando o **Postman Desktop**. No teste caixa cinza o testador conhece parcialmente o sistema (endpoint, headers, formato do body e respostas HTTP), mas não o código-fonte interno. Nenhuma interface gráfica foi implementada.

# Objetivo da Atividade

- Configurar um ambiente de autenticação por e-mail no Supabase e criar um usuário de teste.
- Configurar Workspace, Environment e variáveis no Postman.
- Criar e executar requisições HTTP de login e validar status, JSON, mensagens de erro e `access_token`.
- Registrar os testes em planilha e documentar todo o processo.

# Configuração do Supabase

**Como o projeto foi criado:** acessei https://supabase.com, criei minha conta, e em *New project* criei o projeto `<NOME DO PROJETO>` (região `<REGIÃO>`). `<PREENCHER com o seu relato>`

**Tipo de autenticação:** e-mail e senha (*Authentication → Providers → Email* habilitado). Para facilitar o teste, a confirmação de e-mail foi `<desativada / usuário confirmado manualmente>`.

**Como o usuário foi criado:** em *Authentication → Users → Add user → Create new user*, informando e-mail e senha de teste e marcando *Auto Confirm User*.

**Credenciais da API** (*Project Settings → API*): `Project URL` (→ `base_url`) e a chave `anon public` (→ `api_key`). Por segurança, a chave completa **não** está exposta neste README.

**Objetivo:** ter um backend de autenticação real, com usuário válido, para testar a API.

**Evidências (prints reais, com minha identificação visível):**

| Evidência | Arquivo |
|---|---|
| Projeto criado | `prints/01-projeto-criado.png` |
| Painel do Supabase | `prints/02-painel.png` |
| Autenticação habilitada | `prints/03-auth-habilitada.png` |
| Usuário criado | `prints/04-usuario-criado.png` |
| Credenciais da API (chave parcialmente oculta) | `prints/05-credenciais-api.png` |
| Identificação do aluno no ambiente | `prints/06-identificacao.png` |

<!-- TODO: após salvar os prints, descomente/adicione: ![Projeto criado](prints/01-projeto-criado.png) -->

# Configuração do Postman

- **Workspace:** criado em *Workspaces → Create Workspace* com o nome `<NOME>`.
- **Environment:** `Supabase Auth - Teste Caixa Cinza` (arquivo em `postman/`).
- **Variáveis:**

| Variável | Descrição |
|---|---|
| `base_url` | URL da API do Supabase (Project URL) |
| `api_key` | API KEY (anon public) |
| `email` | E-mail do usuário criado |
| `password` | Senha do usuário criado |

As variáveis evitam repetir valores e permitem trocar de projeto/usuário sem editar cada requisição. A collection `postman/supabase-auth.postman_collection.json` contém as 5 requisições, cada uma com testes automáticos (aba *Tests*).

**Evidências:** `prints/07-workspace.png`, `prints/08-environment.png`, `prints/09-variaveis.png`, `prints/10-organizacao-postman.png`.

# Configuração das Requisições

- **Método:** `POST`
- **Endpoint:** `{{base_url}}/auth/v1/token?grant_type=password`
- **Finalidade:** autenticar um usuário por e-mail/senha e obter o `access_token` (JWT).

| Header | Valor |
|---|---|
| apikey | `{{api_key}}` (XXXXX) |
| Authorization | `Bearer {{api_key}}` |
| Content-Type | application/json |

```json
{
  "email": "usuario@email.com",
  "password": "123456"
}
```

(No Postman o body usa `{{email}}` e `{{password}}`.)

**Evidências:** `prints/11-endpoint.png`, `prints/12-headers.png`, `prints/13-body.png`, `prints/14-requisicao.png`.

# Execução dos Testes

Cenários executados (collection `postman/`):

| ID | Cenário | Entrada Utilizada | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|
| CT01 | Login válido | e-mail e senha corretos | 200 + access_token | `<PREENCHER>` | `<OK/FALHA>` |
| CT02 | Senha incorreta | e-mail correto, senha errada | 400, erro de autenticação (`invalid_credentials`) | `<PREENCHER>` | `<OK/FALHA>` |
| CT03 | Usuário inexistente | `naoexiste.teste@email.com` | Acesso negado (4xx) | `<PREENCHER>` | `<OK/FALHA>` |
| CT04 | Campos vazios | email `""`, password `""` | Erro de validação (4xx) | `<PREENCHER>` | `<OK/FALHA>` |
| CT05 | Credenciais inválidas | `isso-nao-e-email` / `1` | Mensagem de erro (4xx) | `<PREENCHER>` | `<OK/FALHA>` |

**Erros encontrados:** `<PREENCHER>`

**Evidências:** `prints/15-ct01-valido.png` (com access_token), `prints/16-ct02-senha-incorreta.png`, `prints/17-ct03-inexistente.png`, `prints/18-ct04-vazios.png`, `prints/19-ct05-invalidas.png` — mostrando status HTTP, JSON e mensagem de erro.

# Registro dos Testes

Os testes foram registrados em [`planilha/registro_testes.csv`](planilha/registro_testes.csv) (campos: ID, cenário, entrada, resultado esperado, resultado obtido, status, observações), preenchida logo após cada execução. Documentar os testes garante rastreabilidade, repetibilidade e comparação entre versões. Falhas identificadas: `<PREENCHER>`.

**Evidências:** `prints/20-planilha.png`.

# Resultados Obtidos

`<PREENCHER após executar: resumo de quantos cenários passaram/falharam, status HTTP e mensagens reais retornadas.>`

# Conclusão

`<PREENCHER com suas palavras>` Pontos obrigatórios a comentar: se os testes foram executados corretamente; se a autenticação funcionou; dificuldades encontradas; falhas identificadas; melhorias possíveis (ex.: limite de tentativas, mensagens padronizadas, testes automatizados no CI via Newman); e a importância dos testes caixa cinza em APIs (validam contrato e segurança com conhecimento parcial, sem depender de interface).
