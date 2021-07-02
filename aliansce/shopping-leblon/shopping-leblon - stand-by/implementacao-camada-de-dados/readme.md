![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Shopping Leblon
Última atualização: 14/05/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Home](#home)
- [Cinema](#cinema)
- [Gastronomia](#gastronomia)
- [Eventos](#eventos)
- [Casa do Saber](#casa-do-saber)
- [Fale Conosco](#fale-conosco)
- [Solar](#solar)
- [Login](#login)
- [Esqueci minha senha](#esqueci-minha-senha)
- [Editar Perfil](#editar-perfil)
- [Meus Cartões](#meus-cartoes)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://shoppingleblon.com.br/](https://shoppingleblon.com.br/).

<br />

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

## Implementação

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:


```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```
---

<h3 align="center"> Ajustes e implementações que devem ser realizadas </h3>

### Home

**Quando: No clique do botões dos banners**<br />

- **Onde:** Ao clicar nos cards.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 12) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:home',
    'eventAction': 'clique:card:link',
    'eventLabel': 'lebron-fotos-instagram'
  });
</script>

```
<br />

---


### Cinema

**Quando: No clique dos botões do modal "horarios e detalhes"**<br />

- **Onde:** Na página Cinema.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 28) </b>


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:botao:modal-horario-e-detalhes',
    'eventLabel': '[[nome-botao]]:[[nome-filme]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['eventAction'] | 'clique:botao:modal-horario-e-detalhes' | Deve retornar 'clique:botao:modal-horario-e-detalhes' |


<br />

---

### Gastronomia


**Quando:  Ao clicar no link "Carregar Mais"**<br />

- **Onde:** Na página de Gastronomia.

<b> Deve ser adicionado o botão na pagina e implementado o DataLayer (Tagbook aba de validação site em homologação - linha 35) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:gastronomia',
    'eventAction': 'clique:link',
    'eventLabel': 'carregar-mais'
  });
</script>
```

<br />

---

### Eventos


**Quando:  No clique dos cards**<br />

- **Onde:** Na página de Evento.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 35) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:eventos',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'vogue-noivas', 'circuito-time-brasil' e etc| Deve retornar o nome do card clicado. |



<br />

---
### Casa do Saber


**Quando:  No clique dos botões**<br />

- **Onde:** Na página de "Casa do Saber".

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 35) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
     'eventCategory': 'shopping-leblon:casa-do-saber',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-card]]:comprar-ingresso'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'comprar-ingresso'  | Deve retornar o nome do card clicado. |



<br />

---

### Fale Conosco

**Quando: Nos cliques dos botões/links "ver-mapa" e "email"**<br />

- **Onde:** Na página fale conosco.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 55) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:fale-conosco',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'ver-mapa', 'email' e etc | Deve retornar o nome do botão clicado.  |


<br />

---

### Solar

**Quando: Na interação com os campos do formulário**<br />

- **Onde:** Na página Solar.

<b> Deve ser ajustado a taxonomia dos campos (Tagbook aba de validação site em homologação - linha 60) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'interacao:campo:formulario',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome', 'cpf' e etc | Deve retornar o nome do campo preenchido.  |


<br />

---

### Login

**Quando: Na tentativa de callback para efetuar o login**<br />

- **Onde:** Na página de login.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 55) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'login',
    'eventCategory': 'shopping-leblon:login',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1: '[[User ID]]
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |

<br />

---

### Esqueci minha senha

**Quando: Na tentativa de callback para cadastrar a nova senha**<br />

- **Onde:** Na página "Esqueci minha senha".

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 57) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:esqueci-minha-senha',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:nao-encontramos-sua-conta' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />

---
### Editar Perfil

**Quando: No clique dos botões no formulário dados de cadastro**<br />

- **Onde:** Na página "Editar Perfil" na área logada do site

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 73) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:area-logada:editar-perfil',
    'eventAction': 'clique:botao:formulario-dados-de-cadastro',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'salvar', 'cancelar' e etc | Deve conter o nome do botão. |


<br />
---

### Meus cartões

**Quando: No clique dos botões no menu meus cartões**<br />

- **Onde:** Na página "meus cartoes" na área logada do site.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 75) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:area-logada:editar-perfil',
    'eventAction': 'clique:botao:meus-cartoes',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'salvar', 'cancelar' e etc | Deve conter o nome do botão. |


<br />
---

**Quando: Ao preencher um dos campos no formulário meus cartões**<br />

- **Onde:** Na página "meus cartoes" na área logada do site.

<b> Campo "numero do cartao" deve ser ajustado pois esta disparando o evento a cada numero inserido (Tagbook aba de validação site em homologação - linha 76) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:area-logada:editar-perfil',
    'eventAction': 'interacao:formulario-meus-cartoes:campo',
    'eventLabel': '[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'numero-do-cartao' | Deve conter o numero do botão. |


<br />

---

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)


<script> document.querySelector('h1').style.display = 'none' </script>
