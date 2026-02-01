# Gerenciar repositórios remote

Aprenda a trabalhar com seus repositórios locais no seu computador e repositórios remotos hospedados no GitHub.

## Adicionar um repositório remoto

Para adicionar um novo controle remoto, use o comando `git remote add` no terminal, no diretório em que o repositório está armazenado.

O comando `git remote add` usa dois argumentos:

* Um nome de repositório remoto, por exemplo, `origin`
* Uma URL remota, por exemplo, `https://github.com/OWNER/REPOSITORY.git`

Por exemplo:

```shell
$ git remote add origin https://github.com/OWNER/REPOSITORY.git
# Set a new remote

$ git remote -v
# Verify new remote
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
```

Para obter mais informações sobre a URL que deve ser usada, confira [Sobre repositórios remote](/pt/get-started/git-basics/about-remote-repositories).

### Solução de problemas: A origem remota já existe

Esse erro significa que você tentou adicionar um remoto com um nome que já existe no repositório local.

```shell
$ git remote add origin https://github.com/octocat/Spoon-Knife.git
> fatal: remote origin already exists.
```

Para corrigir isso, você pode:

* Usar um nome diferente para o novo remoto
* Renomeie o repositório remoto existente antes de adicionar o novo repositório remoto. Para obter mais informações, confira [Renomear um repositório remoto](#renaming-a-remote-repository) abaixo.
* Exclua o repositório remoto existente antes de adicionar o novo repositório remoto. Para obter mais informações, confira [Remover um repositório remoto](#removing-a-remote-repository) abaixo.

## Alterar a URL de um repositório remoto

O comando `git remote set-url` altera uma URL do repositório remoto existente.

> \[!TIP]
> Para obter informações sobre a diferença entre URLs HTTPS e SSH, confira [Sobre repositórios remote](/pt/get-started/git-basics/about-remote-repositories).

O comando `git remote set-url` usa dois argumentos:

* Um nome remote existente. Por exemplo, `origin` ou `upstream` são duas opções comuns.
* Uma nova URL para o remote. Por exemplo:

  * Se estiver atualizando para usar HTTPS, a URL poderá ser parecida com esta:

  ```shell
  https://github.com/OWNER/REPOSITORY.git
  ```

  * Se estiver atualizando para usar SSH, a URL poderá ser parecida com esta:

  ```shell
  git@github.com:OWNER/REPOSITORY.git
  ```

### Alternar URLs remotes de SSH para HTTPS

1. Abra <span class="platform-mac">Terminal</span><span class="platform-linux">Terminal</span><span class="platform-windows">Git Bash</span>.

2. Altere o diretório de trabalho atual para seu projeto local.

3. Liste seus remotes existentes para obter o nome do remote que deseja alterar.

   ```shell
   $ git remote -v
   > origin  git@github.com:OWNER/REPOSITORY.git (fetch)
   > origin  git@github.com:OWNER/REPOSITORY.git (push)
   ```

4. Altere a URL do repositório remoto do SSH para HTTPS com o comando `git remote set-url`.

   ```shell
   git remote set-url origin https://github.com/OWNER/REPOSITORY.git
   ```

5. Verifique se o URL remote foi alterado.

   ```shell
   $ git remote -v
   # Verify new remote URL
   > origin  https://github.com/OWNER/REPOSITORY.git (fetch)
   > origin  https://github.com/OWNER/REPOSITORY.git (push)
   ```

Na próxima vez que você usar `git fetch`, `git pull` ou `git push` para o repositório remoto, deverá fornecer seu nome de usuário e senha do GitHub. Quando o Git solicitar sua senha, insira seu personal access token. Como alternativa, você pode usar um auxiliar de credenciais como o [Gerenciador de Credenciais do Git](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md). A autenticação baseada em senha para o Git foi removida em favor de métodos de autenticação mais seguros. Para saber mais, confira [Gerenciar seus tokens de acesso pessoal](/pt/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

É possível [usar um auxiliar de credencial](/pt/get-started/git-basics/caching-your-github-credentials-in-git) para que o Git se lembre do nome de usuário do GitHub e do personal access token toda vez que se comunicar com o GitHub.

### Mudar as URLs remotas de HTTPS para SSH

1. Abra <span class="platform-mac">Terminal</span><span class="platform-linux">Terminal</span><span class="platform-windows">Git Bash</span>.

2. Altere o diretório de trabalho atual para seu projeto local.

3. Liste seus remotes existentes para obter o nome do remote que deseja alterar.

   ```shell
   $ git remote -v
   > origin  https://github.com/OWNER/REPOSITORY.git (fetch)
   > origin  https://github.com/OWNER/REPOSITORY.git (push)
   ```

4. Altere a URL do seu remoto de HTTPS para SSH com o comando `git remote set-url`.

   ```shell
   git remote set-url origin git@github.com:OWNER/REPOSITORY.git
   ```

5. Verifique se o URL remote foi alterado.

   ```shell
   $ git remote -v
   # Verify new remote URL
   > origin  git@github.com:OWNER/REPOSITORY.git (fetch)
   > origin  git@github.com:OWNER/REPOSITORY.git (push)
   ```

### Solução de problemas: Não há tal '\[name]' remoto '

Este erro informa que o remote que você tentou alterar não existe:

```shell
$ git remote set-url sofake https://github.com/octocat/Spoon-Knife
> fatal: No such remote 'sofake'
```

Verifique se você inseriu corretamente o nome do remote.

## Renomear um repositório remoto

Use o comando `git remote rename` para renomear um remoto existente.

O comando `git remote rename` usa dois argumentos:

* Um nome remoto existente, por exemplo, `origin`
* Um novo nome para o remoto, por exemplo, `destination`

### Exemplo de como renomear um repositório remoto

Esses exemplos pressupõem que você esteja [clonando usando HTTPS](/pt/get-started/git-basics/about-remote-repositories#cloning-with-https-urls), o que é recomendado.

```shell
$ git remote -v
# View existing remotes
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)

$ git remote rename origin destination
# Change remote name from 'origin' to 'destination'

$ git remote -v
# Verify remote's new name
> destination  https://github.com/OWNER/REPOSITORY.git (fetch)
> destination  https://github.com/OWNER/REPOSITORY.git (push)
```

### Solução de problemas: Não foi possível renomear a seção de configuração 'remote.\[old name]' para 'remote.\[new name]'

Este erro significa que o nome remoto antigo digitado não existe.

Você pode verificar quais remotos existem atualmente com o comando `git remote -v`:

```shell
$ git remote -v
# View existing remotes
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
```

### Solução de problemas: Já existe um \[new name] remoto

Esse erro informa que o nome de remote que você deseja usar já existe. Para resolver isso, use um nome remoto diferente ou renomeie o remoto original.

## Remover um repositório remoto

Use o comando `git remote rm` para remover uma URL remota do repositório.

O comando `git remote rm` usa um argumento:

* Um nome de repositório remoto, por exemplo, `destination`

A remoção do URL remoto do repositório apenas desvincula os repositórios locais e remotos. Isso não exclui o repositório remoto.

### Exemplo de como remover um repositório remoto

Esses exemplos pressupõem que você esteja [clonando usando HTTPS](/pt/get-started/git-basics/about-remote-repositories#cloning-with-https-urls), o que é recomendado.

```shell
$ git remote -v
# View current remotes
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
> destination  https://github.com/FORKER/REPOSITORY.git (fetch)
> destination  https://github.com/FORKER/REPOSITORY.git (push)

$ git remote rm destination
# Remove remote
$ git remote -v
# Verify it's gone
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
```

> \[!NOTE]
> `git remote rm` não exclui o repositório remoto do servidor. Ele simplesmente remove o remoto e suas referências do repositório local.

### Solução de problemas: Não foi possível remover a seção 'remote.\[name]'

Esse erro informa que o remote que você tentou excluir não existe:

```shell
$ git remote rm sofake
> error: Could not remove config section 'remote.sofake'
```

Verifique se você inseriu corretamente o nome do remote.

## Leitura adicional

* ["Como trabalhar com repositórios remotos" do livro *Pro Git*](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

Anotação
Destacar
Explicar