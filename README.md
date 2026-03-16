# 🚀 TeamFlow --- Sistema de Gestão de Equipes e Tarefas

## 📌 Visão Geral

O **TeamFlow** é uma aplicação web desenvolvida utilizando a plataforma
**Bubble (No‑Code / Low‑Code)** com o objetivo de facilitar a gestão de
equipes e a organização de tarefas colaborativas.

A aplicação permite:

-   criação e gerenciamento de equipes
-   convite de novos membros
-   criação, edição e exclusão de tarefas
-   atribuição de tarefas a membros
-   notificações automáticas
-   controle de permissões por papel do usuário

O projeto demonstra como aplicações completas podem ser desenvolvidas
utilizando ferramentas **No‑Code**, mantendo arquitetura clara, controle
de acesso e fluxos automatizados.

------------------------------------------------------------------------

# ❗ Problema

Equipes frequentemente enfrentam dificuldades relacionadas à organização
do trabalho, como:

-   falta de visibilidade sobre tarefas
-   dificuldade em distribuir responsabilidades
-   ausência de notificações sobre novas tarefas
-   dificuldade em gerenciar membros da equipe
-   processos manuais de convite para novos integrantes

O **TeamFlow** resolve esses problemas centralizando o gerenciamento de
equipes e tarefas em uma única plataforma.

------------------------------------------------------------------------

# 🎯 Objetivo do Projeto

Desenvolver uma aplicação que permita:

-   organizar tarefas dentro de equipes
-   gerenciar membros da equipe
-   automatizar notificações de tarefas
-   controlar permissões de usuários
-   facilitar colaboração entre membros

------------------------------------------------------------------------

# 🛠 Tecnologias Utilizadas

  Tecnologia   Utilização
  ------------ ------------------------------
  Bubble       Desenvolvimento da aplicação
  GitHub       Documentação do projeto
  Markdown     Estrutura da documentação

📌 O **GitHub foi utilizado exclusivamente para documentação**, enquanto
toda a aplicação foi construída dentro do Bubble.

------------------------------------------------------------------------

# 👥 Sistema de Permissões

O sistema possui três papéis principais de usuário.

## 🧑‍💼 Gestor

Permissões:

-   criar equipes
-   editar equipes
-   excluir equipes
-   convidar membros
-   remover membros
-   visualizar convites enviados
-   criar tarefas
-   editar tarefas
-   excluir tarefas

------------------------------------------------------------------------

## 👨‍💻 Líder

Permissões:

-   editar equipes
-   convidar membros
-   remover membros
-   visualizar convites enviados
-   criar tarefas
-   editar tarefas
-   excluir tarefas

------------------------------------------------------------------------

## 👤 Membro

Permissões:

-   visualizar equipe atual
-   visualizar membros da equipe
-   criar tarefas
-   visualizar tarefas
-   editar tarefas
-   excluir tarefas
-   receber notificações

------------------------------------------------------------------------

# ⚙️ Funcionalidades da Aplicação

## Gestão de Usuários

-   cadastro de usuários
-   login
-   recuperação de senha
-   edição de perfil
-   alteração de senha
-   atualização de foto de perfil

------------------------------------------------------------------------

## Gestão de Equipes

Dependendo do papel do usuário:

Gestor: - criar equipe - editar equipe - excluir equipe

Gestor e Líder: - convidar membros - remover membros

Todos: - visualizar membros da equipe

------------------------------------------------------------------------

## Gestão de Tarefas

Usuários podem:

-   criar tarefas
-   editar tarefas
-   excluir tarefas
-   visualizar tarefas

Cada tarefa pode ser atribuída a **apenas um membro da equipe**.

Campos principais da tarefa:

-   título
-   descrição
-   prioridade
-   data de vencimento
-   responsável

------------------------------------------------------------------------

## Sistema de Convites

Novos membros entram na equipe através de **convites enviados por
e‑mail**.

Cada convite possui:

-   e‑mail do convidado
-   papel do usuário
-   equipe associada
-   token único
-   data de expiração
-   status do convite

------------------------------------------------------------------------

# 🔐 Validações Implementadas

Para garantir consistência e segurança do sistema, foram implementadas
validações como:

-   verificação se o link de convite é válido
-   verificação se o convite está expirado
-   verificação se o convite já foi aceito
-   bloqueio de convite para usuários que já possuem equipe
-   validação de senha e confirmação de senha
-   validação de campos obrigatórios

------------------------------------------------------------------------

# 🔔 Sistema de Notificações

Quando uma tarefa é atribuída a um usuário:

1.  o sistema cria um registro de **Notification**
2.  a notificação aparece no **Dashboard**
3.  o usuário pode marcar a notificação como **lida**

------------------------------------------------------------------------

# 🧠 Arquitetura do Sistema

## Fluxo Geral da Aplicação

``` mermaid
flowchart TD

A[Usuário acessa aplicação] --> B[Login]

B --> C{Usuário pertence a uma equipe?}

C -- Não --> D[Aguardar convite]
C -- Sim --> E[Entrar no Dashboard]

E --> F[Visualizar tarefas]
E --> G[Visualizar equipe]
E --> H[Visualizar notificações]

G --> I[Gestor ou Líder convidam membro]
I --> J[Enviar convite por e-mail]
J --> K[Usuário acessa link]

K --> L{Convite válido?}

L -- Não --> M[Acesso bloqueado]
L -- Sim --> N[Cadastro]

N --> O[Usuário entra na equipe]

O --> P[Usuário cria tarefa]

P --> Q[Tarefa atribuída]

Q --> R[Notificação criada]

R --> H
```

------------------------------------------------------------------------

# 🗄 Estrutura de Dados

``` mermaid
erDiagram

USER {
string name
string email
string role
string profile_photo
Team team
}

TEAM {
string name
string description
User leader
}

TASK {
string title
string description
string priority
date due_date
User assignee
Team team
}

INVITATION {
string email
string role
string token
date expires_at
string status
Team team
}

NOTIFICATION {
string message
boolean is_read
User recipient
Task task
}

USER }o--|| TEAM : pertence
TEAM ||--o{ TASK : possui
TEAM ||--o{ INVITATION : gera
USER ||--o{ TASK : responsavel
USER ||--o{ NOTIFICATION : recebe
TASK ||--o{ NOTIFICATION : gera
```

------------------------------------------------------------------------

# ⚙️ Explicação dos Workflows Principais

## Workflow: Criação de Tarefa



Fluxo:

1.  Usuário preenche formulário
2.  Sistema valida campos obrigatórios
3.  Bubble cria novo registro **Task**
4.  Se houver responsável definido:
5.  Sistema cria **Notification**

------------------------------------------------------------------------

## Workflow: Edição de Tarefa



Fluxo:

1.  Sistema carrega dados da tarefa
2.  Usuário altera informações
3.  Workflow atualiza registro no banco

------------------------------------------------------------------------

## Workflow: Exclusão de Tarefa



Fluxo:

1.  Usuário seleciona tarefa
2.  Sistema exibe popup de confirmação
3.  Bubble remove registro da base

------------------------------------------------------------------------

## Workflow: Convite para Equipe



Fluxo:

1.  Gestor ou líder informa e-mail
2.  Sistema valida convite
3.  Bubble cria registro **Invitation**
4.  Sistema envia e-mail com token

------------------------------------------------------------------------

## Workflow: Cadastro via Convite



Fluxo:

1.  Usuário acessa link de convite
2.  Sistema lê token da URL
3.  Bubble valida convite
4.  Usuário cria conta
5.  Usuário entra na equipe

------------------------------------------------------------------------

## Workflow: Recuperação de Senha



Fluxo:

1.  Usuário solicita redefinição
2.  Bubble envia e-mail seguro
3.  Usuário acessa link
4.  Sistema valida token
5.  Usuário define nova senha

------------------------------------------------------------------------

# 🖥 Interface da Aplicação

## Tela de Login

![login](images/login.png)

------------------------------------------------------------------------

## Tela de Cadastro

![signup](images/signup.png)

------------------------------------------------------------------------

## Recuperação de Senha

![reset](images/reset_password.png)

------------------------------------------------------------------------

## Dashboard

![dashboard](images/dashboard.png)

------------------------------------------------------------------------

## Tela Teams (Gerenciamento de Equipe)

![teams](images/teams.png)

------------------------------------------------------------------------

## Tela Profile

![profile](images/profile.png)

------------------------------------------------------------------------

# 🧪 Como Testar a Aplicação

### 1. Acessar a aplicação

Abra o link da aplicação.

Link: https://teamflow-26022.bubbleapps.io/version-test/login

------------------------------------------------------------------------

### 2. Login de demonstração

Email: teste@gmail.com

Senha: 123456

------------------------------------------------------------------------

### 3. Fluxos que podem ser testados

-   criação de tarefas
-   edição de tarefas
-   exclusão de tarefas
-   convite de membros
-   cadastro via convite
-   recuperação de senha
-   notificações no dashboard

------------------------------------------------------------------------

# 🎥 Vídeo Pitch do Projeto

🎬 Pitch:

------------------------------------------------------------------------

# 👨‍💻 Autor

Kennedy Pereira Barra

------------------------------------------------------------------------

# 📚 Observação

Projeto desenvolvido para fins acadêmicos utilizando **Bubble (No‑Code /
Low‑Code)**.
