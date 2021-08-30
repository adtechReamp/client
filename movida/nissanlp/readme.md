![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Área - Digital Analytics <br />
> Documento de Especificação Técnica


## Implementação da Camada de dados - Movida - LP Nissan
Última atualização: 30/08/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Movida - LP Nissan](https://www.movida.com.br/).


---

## Overview e Descrições Técnicas

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

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página, permitindo a inclusão de dados adicionais.

**Instalação**
1. Elementos: ```<div>Elemento</div>``` <br />
Todos os elementos do html que serão clicados, deverão ser mapeados recebendo os atributos com sua estrutura no item.

```html
<div 	
    data-gtm-event-category="[[exemplo:valor-categoria]]"
 	data-gtm-event-action="[[exemplo:valor-acao]]"
 	data-gtm-event-label="[[exemplo:valor-rotulo]]"
 >
</div>
```

#### Importante:
> Também devem ter os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. Preenchidos conforme instruções específicas.

<br />

## Implementação


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.

---

### Especificação de Micro-conversões:

**Onde:** - Ao clicar no botão "Alugue agora" <br />
**Quando:** - Botão flutuante da LP

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'nissan:lp',
		'eventAction': 'clique:botao',
		'eventLabel': 'flutuante',
		'user_id': [[user_id]],
                'client_id': [[client_id]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id da Movida.										|
| [[client_id]]			| '123456'				| Deve retornar o id do GA.										|

---

**Onde:** - Ao clicar no botão "Alugue com cupom" <br />
**Quando:** - Botão fixo do primeiro bloco da LP

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'nissan:lp',
		'eventAction': 'clique:botao',
		'eventLabel': 'btn1',
		'user_id': [[user_id]],
                'client_id': [[client_id]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id da Movida.										|
| [[client_id]]			| '123456'				| Deve retornar o id do GA.										|

---

**Onde:** - Ao clicar no botão "Alugue com cupom" <br />
**Quando:** - Botão fixo do segundo bloco da LP

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'nissan:lp',
		'eventAction': 'clique:botao',
		'eventLabel': 'btn2',
		'user_id': [[user_id]],
                'client_id': [[client_id]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id da Movida.										|
| [[client_id]]			| '123456'				| Deve retornar o id do GA.										|

---

**Onde:** - Ao clicar no botão "Alugue com cupom" <br />
**Quando:** - Botão fixo do último bloco da LP

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'nissan:lp',
		'eventAction': 'clique:botao',
		'eventLabel': 'btn3',
		'user_id': [[user_id]],
                'client_id': [[client_id]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id da Movida.										|
| [[client_id]]			| '123456'				| Deve retornar o id do GA.										|

---

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<script>
  document.addEventListener("DOMContentLoaded", function(event) {
    document.querySelectorAll("h1 a")[0].style.display = 'none';
  });
</script>