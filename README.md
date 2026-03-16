# TeamFlow

## Descrição do Projeto

O **TeamFlow** é uma aplicação web desenvolvida na plataforma **Bubble** com foco na **gestão de equipes, tarefas e notificações**. O sistema foi pensado para resolver dificuldades comuns na organização de times, como distribuição de tarefas, controle de membros, convites para equipe e acompanhamento das atividades.

A proposta do projeto é oferecer uma solução prática, intuitiva e funcional para ambientes colaborativos, utilizando abordagem **no-code/low-code**, reduzindo tempo de desenvolvimento e facilitando futuras manutenções.

---

## Problema que a aplicação resolve

Em muitos contextos acadêmicos e profissionais, equipes enfrentam problemas como:

- dificuldade em organizar tarefas entre os membros
- falta de visibilidade sobre responsáveis e andamento
- ausência de centralização das informações do time
- dificuldade para adicionar ou gerenciar membros
- falta de notificações sobre novas atribuições

O **TeamFlow** foi criado para centralizar essas operações em um único sistema, melhorando a organização, a comunicação interna e a produtividade.

---

## Público-alvo

A aplicação foi pensada para:

- equipes acadêmicas
- pequenos times de trabalho
- grupos de projeto
- usuários que precisam organizar tarefas de forma simples
- pessoas que buscam uma solução web funcional sem desenvolvimento tradicional

---

## Benefícios esperados

- melhor organização das tarefas
- definição clara de responsáveis
- controle de equipes e membros
- envio de convites para novos integrantes
- notificações para ações importantes
- interface simples e intuitiva
- redução de erros manuais na gestão do time

---

## Justificativa pelo uso de Bubble (No-Code/Low-Code)

A escolha do **Bubble** foi estratégica por permitir:

- criação rápida de aplicações web funcionais
- desenvolvimento visual sem necessidade de codificação tradicional
- modelagem de banco de dados integrada
- workflows automatizados com facilidade
- publicação e testes rápidos
- manutenção simplificada

### Vantagens do Bubble
- alta produtividade
- menor tempo de desenvolvimento
- menor custo inicial
- facilidade para prototipação e iteração
- interface visual para lógica e banco de dados

### Limitações
- menor flexibilidade do que programação tradicional em cenários muito complexos
- dependência da plataforma
- algumas validações avançadas podem exigir soluções alternativas

Mesmo com essas limitações, para a proposta do projeto o Bubble foi a escolha mais adequada, pois atendeu bem à necessidade de entregar uma aplicação funcional, organizada e documentada.

---

## Funcionalidades principais

O sistema conta com as seguintes funcionalidades:

- cadastro e login de usuários
- gerenciamento de perfil
- alteração de senha
- criação de equipes
- edição e exclusão de equipes
- convite de novos membros por e-mail
- aceitação de convite por link
- listagem de membros da equipe
- criação de tarefas
- atribuição de tarefa a um responsável
- painel com visão geral das tarefas
- notificações de tarefas atribuídas
- marcação de notificações como lidas

---

## Modelagem de Dados

A aplicação foi construída com base nas seguintes entidades principais:

### 1. User
Representa os usuários do sistema.

**Campos principais:**
- `name`
- `email`
- `profile_photo`
- `role`
- `team`

---

### 2. Team
Representa uma equipe dentro do sistema.

**Campos principais:**
- `name`
- `description`
- `leader`

---

### 3. Task
Representa as tarefas cadastradas no sistema.

**Campos principais:**
- `title`
- `description`
- `priority`
- `status`
- `due_date`
- `assignee`
- `team`

---

### 4. Invitation
Representa os convites enviados para ingresso em equipes.

**Campos principais:**
- `email`
- `role`
- `team`
- `token`
- `status`
- `expires_at`

---

### 5. Notification
Representa as notificações exibidas ao usuário.

**Campos principais:**
- `message`
- `recipient`
- `is_read`
- `task`

---

## Relacionamentos

Os principais relacionamentos do sistema são:

- um **usuário** pertence a uma **equipe**
- uma **equipe** possui vários **usuários**
- uma **tarefa** pertence a uma **equipe**
- uma **tarefa** pode ser atribuída a um **usuário**
- um **convite** pertence a uma **equipe**
- uma **notificação** pertence a um **usuário**
- uma **notificação** pode estar vinculada a uma **tarefa**

---

## Regras de Negócio

Algumas regras implementadas no sistema:

- apenas usuários autorizados podem visualizar determinados dados
- convites são enviados por e-mail com link de acesso
- convites possuem status e validade
- tarefas podem ser atribuídas a membros da equipe
- ao atribuir uma tarefa, o sistema cria uma notificação para o responsável
- notificações podem ser marcadas como lidas
- o sistema diferencia papéis como membro, líder e gestor
- a alteração de senha exige confirmação correta

---

## Workflows principais

### 1. Criação de equipe
Permite cadastrar uma nova equipe, validando campos obrigatórios antes da criação.

### 2. Envio de convite
Ao adicionar um membro, o sistema cria um convite com token, associação à equipe e envio por e-mail.

### 3. Aceitação de convite
O usuário acessa o link enviado por e-mail, cria sua conta e passa a integrar a equipe correspondente.

### 4. Criação de tarefa
O usuário pode cadastrar uma nova tarefa e definir informações como título, descrição, prioridade e responsável.

### 5. Atribuição de tarefa
Quando uma tarefa é atribuída a um usuário, o sistema cria automaticamente uma notificação.

### 6. Notificações
As notificações são listadas no sistema e o usuário pode marcá-las como lidas.

### 7. Edição de perfil
O usuário pode atualizar dados como nome, cargo e foto de perfil.

### 8. Alteração de senha
O sistema possui fluxo para mudança de senha e também recuperação via link de redefinição.

---

## Interface e Navegação

A aplicação foi organizada em telas principais para facilitar a usabilidade:

- **Dashboard**
  - visão geral das tarefas
  - indicadores e filtros

- **Equipes**
  - gerenciamento de equipes
  - visualização de membros
  - convites enviados

- **Perfil**
  - dados pessoais
  - foto de perfil
  - equipe atual
  - notificações

A navegação foi pensada para ser simples, com menu lateral e estrutura visual clara.

---

## Publicação e manutenção

### Publicação
A aplicação foi desenvolvida e testada no ambiente da plataforma Bubble, com possibilidade de publicação em link web.

### Estratégias de manutenção
- atualização dos workflows conforme necessidade
- revisão das regras de privacidade
- manutenção do banco de dados
- ajustes visuais e de usabilidade
- evolução de funcionalidades futuras

---

## Tecnologias utilizadas

- **Bubble** — desenvolvimento da aplicação web
- **GitHub** — versionamento e documentação
- **Markdown** — documentação do projeto
- **E-mail/fluxo de convite** — para ingresso em equipes

---

## Como acessar e testar

1. Acesse o link público da aplicação Bubble
2. Faça login ou cadastro
3. Crie ou visualize equipes
4. Cadastre tarefas
5. Atribua tarefas a membros
6. Verifique as notificações
7. Teste o fluxo de convite e perfil

> **Link da aplicação:** `ADICIONE_AQUI_O_LINK_DA_SUA_APLICACAO`

---

## Prints da aplicação

