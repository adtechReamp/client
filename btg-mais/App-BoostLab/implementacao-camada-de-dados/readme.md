![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Puran - Simples de tratar
Última atualização: 08/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Camada-de-dados](#camada-de-dados)
- [Geral](#geral)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://app.service.boostlab.com.br/](https://app.service.boostlab.com.br/)

<br />

### **Descrição Geral**

O `snippet` do Google Tag Manager é um pequeno trecho de código javascript ou non-javascript, através do uso de um iframe quando o javascript não está disponível, que é inserido nas páginas do site, tornando possível que a configuração das tags sejam realizadas via interface.


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

<h3 align = 'center'> INSTALAÇÃO DO GOOGLE TAG MANAGER (snippet)</H3>

### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie e cole o seguinte código abaixo o mais alto possível na tag <head> da página:.

```html

<html>
  <head>
  <!-- Google Tag Manager -->
      <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
      new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
      j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
      'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
      })(window,document,'script','dataLayer','GTM-KV3NV4K');</script>
  <!-- End Google Tag Manager -->

  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação <body> de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
    <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-KV3NV4K"
    height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  </body>
</html>
```

## DataLayer

<h3 align = 'center'> DataLayer </H3>

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

<h3 align = 'center'> Implementação </H3>	
	
### Geral

**Quando: Na interação com os campo do formúlario .**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:formulario:[[titulo-formulario]]',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-formulario]] | 'informacoes-para-contato', 'faca-simulacao', 'informacoes-iniciais' e etc. |  Deve retornar o titulo da etapa.  |
| [[nome-campo]]| 'cpnj', 'razao-social', 'e-mail', 'nome', 'telefone' e etc. |  Retornar o nome do campo preenchido.|


<br />

**Quando: Ao selecionar filtros do formulario.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:formulario:[[titulo-formulario]]',
    'eventLabel': 'selecionou:filtro:[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-formulario]] | 'informacoes-para-contato', 'faca-simulacao', 'informacoes-iniciais' e etc. |  Deve retornar o titulo da etapa.  |
| [[[nome-filtro]]|  'smu-investimentos', 'kptl', 'astella', 'distrito' e etc. | Deve retornar o nome da opção selecionada no filtro do formulario.|


<br />

**Quando: Ao interagir com mat slider(feat) de quantia de crédito desejado.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:smat-slider:valor-credito-desejado',
    'eventLabel': 'R$:[[valor-credito]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[valor-credito]] | '1.500.00', '3.300.00', '5.000.00' e etc. | Deve retornar com o valor desejado de crédito.  |


<br />

**Quando: Ao interagir com o checkbox de "Termos de serviço.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:checkbox:termos-de-servico',
    'eventLabel': '[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] |  'nao-aceito' ou  'aceito'. |Deve retornar o tipo da ação realizada no checkbox.  |


<br />

**Quando: Ao interagir com qualquer checkbox no formulario.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:checkbox:[[pergunta]]',
    'eventLabel': 'selecionado:[[nome-check]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[pergunta]] | : 'como-sua-empresa-recebe-o-pagamento-desses-contratos', 'quais-credenciais-que-sua-empresa-utiliza', 'cash-runway-estimado-da-sua-empresa' e etc.| Deve retornar a pergunta para do checkbox. |
| [[nome-check]] | : 'boleto', 'credito', 'rede', 'cielo', '4-meses', '5-meses' e etc.| Deve retornar com o nome do checkbox selecionado.|



<br />


**Quando: Ao interagir com qualquer checkbox no formulario.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:checkbox:[[pergunta]]',
    'eventLabel': 'selecionado:[[nome-check]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[pergunta]] | : 'como-sua-empresa-recebe-o-pagamento-desses-contratos', 'quais-credenciais-que-sua-empresa-utiliza', 'cash-runway-estimado-da-sua-empresa' e etc.| Deve retornar a pergunta para do checkbox. |
| [[nome-check]] | : 'boleto', 'credito', 'rede', 'cielo', '4-meses', '5-meses' e etc.| Deve retornar com o nome do checkbox selecionado.|



<br />

**Quando:  Ao clicar nos botões de 'upload' ou 'baixar' documento.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'clique:botao:formulario:[[titulo-formulario]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[titulo-formulario]]| : 'informacoes-para-contato', 'faca-simulacao', 'informacoes-iniciais', 'informacoes-financeiras' e etc.| Deve retornar o titulo da etapa. |
| [[nome-botao]] | : 'enviar' ou 'baixar'.| Deve retornar o nome do botao clicado.|



<br />

**Quando:   Ao interagir com o checkbox de "autorização Btg Pactual...**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'interacao:checkbox:autorizacao-dados',
    'eventLabel': '[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[acao]]| : 'nao-autorizo' ou  'autorizo'.| Deve retornar o tipo da ação realizada no checkbox. |




<br />

**Quando:   Ao clicar nos botões do formulario de cada step.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'clique:[[botao-ou-link]]:formulario:[[titulo-formulario]]:[[etapa]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]| : 'botao' ou 'link'|  Deve retornar o tipo de elemento clicado. |
|[[titulo-formulario]]| : 'informacoes-para-contato', 'faca-simulacao', 'informacoes-iniciais' e etc.| Deve retornar o titulo da etapa. |
|[[etapa]]| : 'etapa-1', 'etapa-2',  'etapa-3' e etc.| Deve retornar o step.  |
|[[nome-botao]]| :'proximo', 'começar', 'voltar' e etc.| Deve retornar o nome do botão clicado .  |




<br />

**Quando:   Na tentativa de callback de envio do formulário.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'app:boostlab',
    'eventAction': 'callback:envio-formulario',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]]| :  'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.|  Retornar a mensagem de sucesso ou tipo de erro. |





<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
