# 🚀 TeamFlow --- Sistema de Gestão de Equipes e Tarefas

## 📌 Visão Geral

O **TeamFlow** é uma aplicação web desenvolvida na plataforma **Bubble**
com o objetivo de facilitar a gestão de equipes e a organização de
tarefas colaborativas.

A aplicação permite: - criação e gerenciamento de equipes - convite de
novos membros - criação e atribuição de tarefas - notificações
automáticas quando tarefas são atribuídas

O projeto demonstra o uso de **No-Code / Low-Code** para desenvolvimento
de aplicações completas.

------------------------------------------------------------------------

# ❗ Problema

Equipes frequentemente enfrentam dificuldades como:

-   falta de organização das tarefas
-   dificuldade de acompanhar responsabilidades
-   ausência de notificações quando algo muda
-   dificuldade em gerenciar convites para novos membros

O **TeamFlow** resolve esses problemas centralizando o gerenciamento da
equipe e das tarefas.

------------------------------------------------------------------------

# 🎯 Objetivo do Projeto

Desenvolver uma aplicação que permita:

-   organização de tarefas em equipes
-   gerenciamento de membros
-   automação de notificações
-   controle de permissões por papel de usuário

------------------------------------------------------------------------

# 🛠 Tecnologias Utilizadas

  Tecnologia   Uso
  ------------ ------------------------------
  Bubble       Desenvolvimento da aplicação
  GitHub       Documentação do projeto
  Markdown     Estrutura da documentação

O **GitHub foi utilizado apenas para documentação**, enquanto o
desenvolvimento foi feito totalmente no Bubble.

------------------------------------------------------------------------

# ⚙️ Funcionalidades

## 👤 Gestão de Usuários

-   cadastro de usuários
-   login
-   recuperação de senha
-   edição de perfil
-   alteração de senha
-   atualização de foto de perfil

------------------------------------------------------------------------

## 👥 Gestão de Equipes

Dependendo do papel do usuário:

**Gestor** - criar equipe - editar equipe - excluir equipe

**Gestor e Líder** - convidar membros - remover membros

**Todos** - visualizar membros da equipe

------------------------------------------------------------------------

## ✅ Gestão de Tarefas

Todos os membros podem:

-   criar tarefas
-   visualizar tarefas
-   editar tarefas
-   excluir tarefas

Cada tarefa pode ser atribuída **apenas a um membro da equipe**.

Campos principais da tarefa: - título - descrição - prioridade - data de
vencimento - responsável

------------------------------------------------------------------------

## 📧 Sistema de Convites

Novos membros entram na equipe através de um **link de convite**.

Cada convite possui:

-   e-mail do convidado
-   papel do usuário
-   equipe
-   token único
-   data de expiração
-   status

------------------------------------------------------------------------

## 🔐 Validações Implementadas

-   verificação de link de convite válido
-   verificação de convite expirado
-   bloqueio de convite para usuários que já possuem equipe
-   validação de senha
-   validação de confirmação de senha
-   validação de campos obrigatórios

------------------------------------------------------------------------

# 👮 Sistema de Permissões

### 🧑‍💼 Gestor

-   criar equipes
-   editar equipes
-   excluir equipes
-   convidar membros
-   remover membros
-   criar tarefas
-   editar tarefas
-   excluir tarefas

### 👨‍💻 Líder

-   editar equipe
-   convidar membros
-   remover membros
-   criar tarefas
-   editar tarefas
-   excluir tarefas

### 👤 Membro

-   visualizar equipe
-   visualizar membros
-   criar tarefas
-   editar tarefas
-   excluir tarefas
-   visualizar notificações

------------------------------------------------------------------------

# 🔔 Sistema de Notificações

Quando uma tarefa é atribuída a um usuário:

1.  o sistema cria uma notificação
2.  a notificação aparece no **Dashboard**
3.  o usuário pode marcar como **lida**

------------------------------------------------------------------------

# 🖥 Interface da Aplicação

## Dashboard

Mostra: - notificações - tarefas da equipe - resumo da atividade

## Teams

Mostra: - equipe atual - membros da equipe - convites enviados

## Profile

Permite: - editar perfil - alterar senha - visualizar equipe -
visualizar membros

------------------------------------------------------------------------

# 🧠 Arquitetura do Sistema

## Fluxo visual da aplicação

``` mermaid
flowchart TD
    A[Usuário acessa a aplicação] --> B[Login]
    B --> C{Já pertence a uma equipe?}

    C -- Não --> D[Aguardar convite]
    C -- Sim --> E[Entrar no Dashboard]

    E --> F[Visualizar equipe]
    E --> G[Visualizar tarefas]
    E --> H[Visualizar notificações]

    F --> I[Gestor ou Líder convidam membro]
    I --> J[Enviar convite por e-mail]
    J --> K[Link com token de convite]

    K --> L[Usuário acessa o link]
    L --> M{Convite válido?}

    M -- Não --> N[Acesso bloqueado]
    M -- Sim --> O[Criar conta]

    O --> P[Usuário entra na equipe]

    P --> Q[Usuário cria tarefa]
    Q --> R[Tarefa atribuída a um membro]
    R --> S[Sistema gera notificação]
    S --> H
```

## Explicação do fluxo

1.  O usuário acessa a aplicação e realiza login.
2.  O sistema identifica se ele já pertence a uma equipe.
3.  Gestores ou líderes podem enviar convites para novos membros.
4.  O convite gera um link com token.
5.  Ao acessar o link, o sistema valida:
    -   token
    -   expiração
    -   status do convite
    -   se o usuário já está em uma equipe
6.  Após entrar na equipe, usuários podem criar tarefas.
7.  Quando uma tarefa é atribuída, o sistema gera uma notificação
    automática.

------------------------------------------------------------------------

# 🗄 Estrutura de Dados

## Diagrama visual das entidades

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

## Campos principais

**User** - name - email - role - profile_photo - team

**Team** - name - description - leader

**Task** - title - description - priority - due_date - assignee - team

**Invitation** - email - role - team - token - expires_at - status

**Notification** - message - is_read - recipient - task

------------------------------------------------------------------------

# 🌐 Link da Aplicação

A aplicação pode ser acessada através do seguinte link:

https://SEU-LINK-AQUI.bubbleapps.io

------------------------------------------------------------------------

# 🧪 Como Testar

## Login de demonstração

Email: admin@teamflow.com

Senha: admin123

## Fluxos que podem ser testados

### 1. Cadastro via convite

1.  Acesse **Teams**
2.  Clique em **Convidar membro**
3.  Envie um convite
4.  Use o link para criar uma nova conta

### 2. Recuperação de senha

1.  Clique em **Esqueci minha senha**
2.  Digite o e-mail
3.  Abra o link enviado
4.  Defina uma nova senha

### 3. Tarefas

-   criar
-   editar
-   excluir
-   atribuir responsável

### 4. Dashboard

-   visualizar notificações
-   marcar notificação como lida

### 5. Profile

-   editar perfil
-   alterar senha
-   visualizar equipe e membros

------------------------------------------------------------------------

# 📸 Evidências do Projeto



------------------------------------------------------------------------

# 👨‍💻 Autor

Kennedy Pereira Barra

------------------------------------------------------------------------

# 📚 Observação

Projeto desenvolvido para fins acadêmicos utilizando **Bubble (No-Code /
Low-Code)**.