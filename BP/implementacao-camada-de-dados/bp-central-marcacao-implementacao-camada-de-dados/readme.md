![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization <br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Puran - Simples de tratar
Última atualização: 20/07/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Geral](#geral)
- [Home](#home)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueceu-sua-senha](#esqueceu-sua-senha)




## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://hospitalbp.centraldemarcacao.com.br/](https://hospitalbp.centraldemarcacao.com.br/)

<br />

---

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

### Geral

**Quando: No clique de algum elemento do header. .**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'menu' e 'logo'.|  Deve retornar com o nome do elemento clicado no header.  |


<br />

**Quando: No clique do sub-menu superior lateral.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:link',
    'eventLabel': '[[sub-menu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-formulario]] | 'nova-marcacao', 'minhas-marcacao', 'meus-convenios', 'meus-dados' e etc. |  Deve retornar com o nome do elemento clicado no sub-menu.  |


<br />

**Quando: Ao clicar em abrir formulario de chat.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao',
    'eventLabel': '[[acao-chat]]:formulario-chat'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[acao-chat]]|  'abriu' e 'fechou'. |  Deve retornar com a ação realizada.  |


<br />

**Quando: Na interação com os campos do chat de contato.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'interacao:formulario-chat:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]] |  email', 'nome', 'telefone', 'motivo-de-contato' e etc.|  Deve retornar o nome do campo preenchido.  |


<br />


**Quando: Ao clicar nos botões do formulario de contato. **<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao-formulario-chat',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-botao]] |  'iniciar' e 'enviar'.|  Deve retornar com o nome do botão clicado.  |


<br />

**Quando: Ao clicar nos botões inferior.  **<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]] |  'link' ou 'botao'.|Deve Retornar com o nome do elemento clicado.|
|[[nome-elemento]] |   'proximo-passo' e 'cancelar'.|   Deve retornar o nome do botão clicado.|


<br />

**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'bp-cm:geral-formulario-chat',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]] |  'sucesso', 'erro-inesperado'.| Deve retornar a mensagem de sucesso ou o tipo de erro. |



<br />

### Home

**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:home',
    'eventAction': 'clique:botao',
    'eventLabel': 'realizar-cadastro'
  });
</script>

```

<br />

### Cadastro

**Quando: Na interação com os campos.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]|'nome', 'email', 'bairro', 'cpf', 'telefone' e etc.|Deve retornar o nome do campo preenchido. |


<br />

**Quando:Na interação com o checkbox.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'interacao:checkbox',
    'eventLabel': '[[acao]]:autorizo-o-uso-dos-meus-dados'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[acao]]|'marcou, 'desmarcou'.|Deve retornar a ação do usuário. |


<br />

**Quando: No clique dos botões.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-botao]]|'confirmar-cadastro' e 'cancelar'.|Deve retornar o nome do botão clicado. |


<br />


**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro,
    'eventAction': 'clique:botao',
    'eventLabel': 'realizar-cadastro'
  });
</script>

```

<br />

### Login

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
