---
title: Gerar uma nova chave GPG
intro: 'Caso você não tenha uma chave GPG atual, é possível gerar uma nova para usar na assinatura de commits e tags.'
redirect_from:
  - /articles/generating-a-new-gpg-key
  - /github/authenticating-to-github/generating-a-new-gpg-key
  - /github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Identity
  - Access management
---

{% data reusables.gpg.supported-gpg-key-algorithms %}

## Gerar uma chave GPG

{% note %}

**Observação:** antes de gerar uma nova chave GPG, confirme se verificou seu endereço de e-mail. Caso seu endereço de e-mail não tenha sido verificado, você não conseguirá assinar commits e tags com GPG.{% ifversion fpt or ghec %} Para obter mais informações, consulte "[Verificar seu endereço de e-mail](/articles/verifying-your-email-address)".{% endif %}

{% endnote %}

1. Baixe e instale [as ferramentas da linha de comando GPG](https://www.gnupg.org/download/) para seu sistema operacional. A instalação da última versão de seu sistema operacional é recomendada.
{% data reusables.command_line.open_the_multi_os_terminal %}
3. Gere um par de chaves GPG. Já que existem várias versões do GPG, é possível que você tenha de consultar a [_página man_](https://en.wikipedia.org/wiki/Man_page) relevante para encontrar o comando de geração de chaves apropriado. A sua chave deve usar RSA.
    - Se a sua versão for 2.1.17 ou posterior, cole o texto abaixo para gerar um par de chaves GPG.
      ```shell
      $ gpg --full-generate-key
      ```
    - Se a sua versão não for 2.1.17 ou posterior, o comando `gpg --full-generate-key` não funcionará. Cole o texto abaixo e passe para a etapa 6.
      ```shell
      $ gpg --default-new-key-algo rsa4096 --gen-key
      ```
4. Mediante instrução, especifique o tipo de tecla que você deseja ou pressione `Enter` para aceitar o padrão.
5. Mediante instrução, especifique o tamanho da chave que você deseja ou pressione `Enter` para aceitar o padrão. Sua chave deve ter, no mínimo, `4096` bits.
6. Digite o prazo de validade da chave. Pressione `Enter` para estipular a seleção padrão, indicando que chave não expira. A menos que você exija uma data de validade, recomendamos aceitar este padrão.
7. Verifique se suas seleções estão corretas.
8. Insira seu ID de usuário.

  {% note %}

  **Obervação:** quando solicitado a digitar seu endereço de e-mail, confirme que inseriu o endereço de e-mail verificado da sua conta GitHub. {% data reusables.gpg.private-email %} {% ifversion fpt or ghec %}  Para obter mais informações, consulte "[Verificar seu endereço de e-mail](/articles/verifying-your-email-address)" e "[Configurar o commit de seu endereço de e-mail](/articles/setting-your-commit-email-address)".{% endif %}

  {% endnote %}

9. Digite uma frase secreta segura.
{% data reusables.gpg.list-keys-with-note %}
{% data reusables.gpg.copy-gpg-key-id %}
10. Cole o texto abaixo, substituindo o ID da chave GPG que você quer usar. Neste exemplo, o ID da chave GPG é `3AA5C34371567BD2`:
  ```shell
  $ gpg --armor --export <em>3AA5C34371567BD2</em>
  # Prints the GPG key ID, in ASCII armor format
  ```
11. Copie sua chave GPG, que inicia com `-----BEGIN PGP PUBLIC KEY BLOCK-----` e termina com `-----END PGP PUBLIC KEY BLOCK-----`.
12. [Adicione a chave GPG à sua conta GitHub](/articles/adding-a-gpg-key-to-your-github-account).

## Leia mais

* "[Verificar se há chaves GPG existentes](/articles/checking-for-existing-gpg-keys)"
* "[Adicionar uma chave GPG à sua conta do GitHub](/articles/adding-a-gpg-key-to-your-github-account)"
* "[Avisar o Git sobre sua chave de assinatura](/articles/telling-git-about-your-signing-key)"
* "[Associar um e-mail à sua chave GPG](/articles/associating-an-email-with-your-gpg-key)"
* "[Assinar commits](/articles/signing-commits)"
* "[Assinar tags](/articles/signing-tags)"
