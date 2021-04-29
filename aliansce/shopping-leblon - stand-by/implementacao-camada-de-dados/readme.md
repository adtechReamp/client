![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Shopping Leblon
Última atualização: 13/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Home](#home)
- [Shopping](#shopping)
- [Vitrine de produtos](#vitrine-de-produtos)
- [Eventos](#eventos)
- [Fale Conosco](#fale-conosco)
- [Solar](#solar)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueci minha senha](#esqueci-minha-senha)
- [Área Logada](#&aacute;rea-logada)



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

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 13) </b>
    
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
### Shopping

**Quando: Na interação dos card**<br />

- **Onde:** Na página shopping.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 15) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:shopping',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] | 'torres-de-escritorio-chopping-leblon', 'responsabilidade-social' e etc | Deve retornar o nome do card clicado. |


<br />

### Vitrine de produtos

**Quando: Na interação com os filtros.**<br />

- **Onde:** Na página de vitrine de produtos.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 17) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] |  'categoria', 'lojas', 'todos-os-canais' e etc | Deve retornar o nome do filtro. |
| [[item-filtrado]] | 'infantil', 'adcos' e etc | Deve retornar o nome filtrado.  |


<br />

**Quando: No clique nos cards dos produtos.**<br />

- **Onde:** Na página de vitrine de produtos.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 18) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'biquini-infantil-babados', 'coelho-orelhao' e etc | Deve retornar o nome do card clicado.  |


<br />

**Quando: Ao clicar nos botões dentro dos cards**<br />

- **Onde:** Na página de vitrine de produtos.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 19) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'whatsapp', 'site-da-loja' e etc. | Deve retornar o  nome do botão clicado.  |
| [[nome-card]] |  'biquini-infantil-babados', 'coelho-orelhao' e etc | Deve retornar o nome do card clicado.  |


<br />

**Quando: Ao clicar no Link "ver mais produtos"**<br />

- **Onde:** Na página de vitrine de produtos.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 20) </b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:link',
    'eventLabel': 'ver-mais-produtos'
  });
</script>
```
<br />


### Eventos


**Quando:  No clique dos cards**<br />

- **Onde:** Na página de Evento.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 37) </b>

    
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

### Planeje sua visita

**Quando: No clique dos cards**<br />

- **Onde:** Na página de visita.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 41) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:planeje-sua-visita',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] | 'destinos-cariocas' e etc |  Deve retornar o nome do card. |


<br />

---

### Fale Conosco

**Quando: Nos cliques dos botões/links "ver-mapa" e "email"**<br />

- **Onde:** Na página fale conosco.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 45) </b>
    
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


**Quando: Na tentativa de callback do envio do formulario**<br />

- **Onde:** Na página fale conosco.

<b> Deve ser implementado o DataLayer, não está mais disparando esse evento (Tagbook aba de validação site em homologação - linha 47) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'shopping-leblon:fale-conosco',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:cpd-invalido' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />

### Solar

**Quando: No clique dos botões**<br />

- **Onde:** Na página Solar.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 49) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'regulamento', 'enviar' e etc | Deve retornar o nome do botão clicado. |


<br />

**Quando: Na interação com os campos do formulário**<br />

- **Onde:** Na página Solar.

<b> Deve ser ajustado a taxonomia dos campos (Tagbook aba de validação site em homologação - linha 50) </b>

    
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

**Quando: Na tentativa de callback do envio do formulario**<br />

- **Onde:** Na página Solar.

<b> Deve ser ajustado o nome do event para "conversion" (Tagbook aba de validação site em homologação - linha 51) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:cpd-invalido' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro.   |


<br />

### Cadastro

**Quando: Na tentativa de callback para efetuar o cadastro**<br />

- **Onde:** Na página de cadastro.

<b> Deve ser implementado o DataLayer (Tagbook aba de validação site em homologação - linha 53) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'shopping-leblon:cadastro',
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

### Área Logada

<b> Não conseguimos validar os elementos da área logada, não está carregando a página <b>




> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
