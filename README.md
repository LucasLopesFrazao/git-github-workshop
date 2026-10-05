# Oficina de Git e GitHub

Oficina prática de introdução ao Git e GitHub, abordando os principais conceitos e fluxos de desenvolvimento colaborativo.

O objetivo é compreender o funcionamento do controle de versão e praticar o fluxo de trabalho com branches, commits, Pull Requests, code review e merge.

## Conteúdo

* Fundamentos do Git e GitHub
* Repositórios e branches
* Commits e staging
* Push e pull
* Pull Requests (PR)
* Code review
* Merge e resolução de conflitos

## Pré-requisitos e configuração inicial

Antes de iniciar a oficina, certifique-se de que você possui:

* [Git](https://git-scm.com/downloads) instalado.
* Uma conta no [GitHub](https://github.com/).
* Acesso ao repositório da oficina.
* Um editor de código de sua preferência (VS Code recomendado)
* Um Personal Access Token (PAT) para autenticação via HTTPS.

### 1. Verificar a instalação do Git

Verifique se o Git está instalado:

```bash
git --version
```

### 2. Configurar a identidade do Git

Configure seu nome e e-mail, que serão associados aos seus commits:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

Para conferir as configurações:

```bash
git config --global --list
```

> Essas configurações identificam o autor dos commits e são independentes da autenticação no GitHub.

### 3. Criar um Personal Access Token (PAT)

O GitHub não permite mais utilizar a senha da conta para autenticar operações Git via HTTPS. Para isso, é necessário utilizar um Personal Access Token (PAT) ou outro método de autenticação compatível.

Para esta oficina, utilizaremos um **Personal Access Token clássico (classic)**.

Siga as etapas:

1. Acesse [GitHub](https://github.com/) e faça login.
2. Clique na sua foto de perfil e acesse **Settings**.
3. No menu lateral, entre em **Developer settings**.
4. Acesse **Personal access tokens** e, em seguida, **Tokens (classic)**.
5. Clique em **Generate new token** e selecione **Generate new token (classic)**.
6. Preencha os campos:

   * **Note:** `Oficina Git e GitHub`.
   * **Expiration:** selecione um prazo de validade adequado, preferencialmente curto para esta atividade.
   * **Scopes:** selecione as permissões necessárias.

Para a oficina, vamos selecionar todas:

7. Clique em **Generate token**.
8. Copie o token gerado e guarde-o em um local seguro.

**Atenção:** o token é exibido integralmente apenas no momento da criação. Trate-o como uma senha: não o compartilhe com outras pessoas, não o envie pelo chat e nunca o inclua em arquivos do projeto.


### 4. Autenticar via HTTPS

Clone o repositório utilizando sua URL HTTPS:

```bash
git clone https://github.com/LucasLopesFrazao/git-github-workshop.git
```

Ao realizar uma operação que exija autenticação, como um `git push`, o Git poderá solicitar suas credenciais:

```text
Username for 'https://github.com': seu-usuario
Password for 'https://seu-usuario@github.com':
```

Preencha da seguinte forma:

* **Username:** seu nome de usuário do GitHub.
* **Password:** cole o Personal Access Token criado anteriormente, em vez da senha da sua conta.

Ao colar o token no terminal, é normal que nenhum caractere seja exibido. Basta pressionar `Enter` para confirmar.

Dependendo do gerenciador de credenciais configurado, o Git poderá armazenar o token de forma segura para evitar solicitações repetidas.

---

# Atividade prática

Durante a atividade, cada participante deverá criar sua própria branch, adicionar um arquivo ao repositório, realizar um commit e abrir um Pull Request para revisão.

## 1. Clonar o repositório

O primeiro passo é obter uma cópia local do repositório remoto.

```bash
git clone https://github.com/LucasLopesFrazao/git-github-workshop.git
```

Verifique o estado atual do repositório:

```bash
git status
```

O comando `git clone` cria uma cópia local do repositório, incluindo seu histórico. O comando `git status` permite verificar a situação atual dos arquivos e da branch.

## 2. Atualizar a branch principal

Antes de iniciar uma nova atividade, é importante trabalhar com a versão mais recente da branch principal.

```bash
git checkout main
```

Atualize a branch local com as alterações do repositório remoto:

```bash
git pull origin main
```

* `git checkout`: alterna entre branches.
* `git pull`: busca e integra as alterações do repositório remoto.
* `origin`: nome padrão do repositório remoto.
* `main`: branch principal do projeto.

## 3. Criar uma branch

Cada participante deverá trabalhar em sua própria branch, evitando realizar alterações diretamente na `main`.

Crie uma branch com um nome único:

```bash
git checkout -b feat/participante-seu-nome
```

Exemplo:

```bash
git checkout -b feat/participante-lucas
```

O comando `git checkout -b` cria uma nova branch e muda automaticamente para ela.

Para listar as branches locais:

```bash
git branch
```

A branch marcada com `*` é aquela que está ativa no momento.

## 4. Realizar uma alteração

Cada participante deverá criar um arquivo próprio na pasta `participantes/`, utilizando seu nome para identificá-lo.

Crie o arquivo `participantes/participante-seu-nome.md` e adicione algumas informações sobre você (em algum lugar do texto, coloque uma palavra errada).

Após salvar o arquivo, verifique as alterações:

```bash
git status
```

Você pode visualizar as diferenças nos arquivos modificados diretamente no VSCode.

## 5. Preparar as alterações (staging)

Antes de criar um commit, precisamos selecionar quais alterações farão parte dele.

Adicione seu arquivo ao staging:

```bash
git add participantes/participante-seu-nome.md
```

Para adicionar todas as alterações do diretório:

```bash
git add .
```

O staging permite selecionar as alterações que serão incluídas em um commit. Você pode verificar o que está preparado diretamente no VSCode.

## 6. Criar um commit

Um commit registra um conjunto de alterações no histórico do Git.

Crie um commit com uma mensagem que descreva o que foi realizado:

```bash
git commit -m "docs: adiciona participante seu-nome"
```

Boas práticas para mensagens de commit:

* Utilize mensagens objetivas e descritivas.
* Prefira indicar o que foi realizado.
* Evite mensagens genéricas, como `ajustes`, `alterações` ou `teste`.

Exemplos:

```bash
git commit -m "feat: adiciona autenticação"
git commit -m "fix: corrige validação do formulário"
git commit -m "docs: atualiza documentação"
```

## 7. Enviar a branch para o GitHub (push)

Após criar o commit, envie sua branch para o repositório remoto.

```bash
git push -u origin feat/participante-seu-nome
```

O parâmetro `-u` configura o acompanhamento da branch remota. Nos próximos envios dessa branch, será possível utilizar apenas:

```bash
git push
```

Acesse o GitHub e confira se sua branch foi publicada corretamente.

## 8. Criar um Pull Request (PR)

O Pull Request é uma solicitação de integração das alterações de uma branch em outra, geralmente na `main`.

Para criar um PR:

1. Acesse o repositório no GitHub.
2. Entre na seção **Pull requests**.
3. Clique em **New pull request**.
4. Selecione a `main` como branch de destino (*base*).
5. Selecione sua branch como origem (*compare*).
6. Preencha o título e a descrição do PR.
7. Clique em **Create pull request**.

Exemplo de título:

```text
docs: adiciona contribuição do participante
```

Exemplo de descrição:

```markdown
## Descrição

Adiciona minha contribuição à oficina de Git e GitHub.

## Alterações realizadas

- Criação do arquivo do participante.
```

Após criar o PR, as alterações estarão disponíveis para revisão.

## 9. Realizar um code review

O code review é o processo de revisão das alterações realizadas por outro desenvolvedor antes da integração.

Durante a oficina, cada participante deverá revisar o PR de um colega.

Na revisão, observe:

* Se as alterações correspondem à descrição do PR.
* Se os arquivos modificados são os esperados.
* Se existe algum problema de clareza ou organização.
* Se a documentação está adequada.
* Ache a palavra errada adicionada pelo seu colega.

O GitHub permite adicionar comentários diretamente nas linhas modificadas, aprovar o PR ou solicitar alterações (*Request changes*).

Caso sejam solicitados ajustes, retorne à sua branch local, faça as alterações e envie um novo commit:

```bash
git add .
git commit -m "docs: ajusta contribuição do participante"
git push
```

O PR existente será atualizado automaticamente com o novo commit.

## 10. Fazer o merge

Após a revisão e a aprovação, o PR poderá ser integrado à branch de destino.

Para a oficina, utilizaremos o **Create a merge commit**, que integra todos os commits da branch na branch de destino.

O merge pode ser realizado pela interface do GitHub, utilizando o botão correspondente no Pull Request.

Após a integração, a alteração passará a fazer parte da `main`.

> Durante a oficina, somente os PRs revisados e aprovados deverão ser integrados à branch principal.

## 11. Atualizar a branch local

Após o merge, retorne à branch principal e sincronize o repositório local:

```bash
git checkout main
git pull origin main
```

Agora, as alterações integradas pelos demais participantes também estarão disponíveis localmente.

Para excluir sua branch local, depois de confirmar que o merge foi concluído:

```bash
git branch -d feat/participante-seu-nome
```

A branch remota também poderá ser excluída pelo GitHub, após a integração do PR.

---

# Referência rápida de comandos

| Comando                       | Descrição                                               |
| ----------------------------- | ------------------------------------------------------- |
| `git clone <url>`             | Clona um repositório remoto.                            |
| `git status`                  | Exibe o estado atual do repositório.                    |
| `git checkout main`             | Alterna para a branch principal.                        |
| `git pull origin main`        | Atualiza a branch local com o remoto.                   |
| `git checkout -b <branch>`      | Cria e acessa uma nova branch.                          |
| `git branch`                  | Lista as branches locais.                               |
| `git add <arquivo>`           | Adiciona alterações ao staging.                         |
| `git commit -m "mensagem"`    | Cria um commit.                                         |
| `git log --oneline`           | Exibe o histórico resumido de commits.                  |
| `git push -u origin <branch>` | Publica a branch e configura seu acompanhamento remoto. |
| `git push`                    | Envia novos commits à branch remota acompanhada.        |
| `git branch -d <branch>`      | Exclui uma branch local já integrada.                   |

---

# Conceitos importantes

| Conceito         | Descrição                                                                            |
| ---------------- | ------------------------------------------------------------------------------------ |
| **Git**          | Sistema distribuído de controle de versão.                                           |
| **GitHub**       | Plataforma para hospedagem de repositórios e colaboração.                            |
| **Repository**   | Diretório do projeto acompanhado pelo Git e seu histórico.                           |
| **Branch**       | Linha independente de desenvolvimento.                                               |
| **Commit**       | Registro de alterações no histórico.                                                 |
| **Staging**      | Área que reúne as alterações selecionadas para o próximo commit.                     |
| **Push**         | Envio dos commits locais ao repositório remoto.                                      |
| **Pull**         | Busca e integração das alterações remotas na branch atual.                           |
| **Pull Request** | Solicitação de revisão e integração de alterações.                                   |
| **Code review**  | Processo de revisão das alterações de código ou documentação.                        |
| **Merge**        | Integração de alterações de uma branch em outra.                                     |
| **Conflito**     | Situação em que o Git não consegue combinar automaticamente determinadas alterações. |
