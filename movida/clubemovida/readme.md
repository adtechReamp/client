![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Área - Digital Analytics <br />
> Documento de Especificação Técnica


## Implementação da Camada de dados - Clube Movida
Última atualização: 05/07/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Clube Movida](https://www.movida.com.br/clubemovida).


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

**Home Clube Movida:**<br />

- **Quando:** Ao clicar no botão "Compare e escolha o melhor plano".
- **Onde:** Na página home de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:home',
		'eventAction': 'clique:botao',
		'eventLabel': 'compare'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| 	    				| 						|	                                    		|

- **Quando:** Ao clicar nos botões "Quero assinar".
- **Onde:** Na página home de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:home',
		'eventAction': 'clique:botao',
		'eventLabel': [[plano]]:[[valor]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[plano]]			    | 'Plano 10000'			| Deve retornar o nome do plano selecionado. 	|
| [[valor]]		    	| '299,00'				| Deve retornar o valor do plano selecionado.   |

- **Quando:** Ao clicar no link "Ver todos".
- **Onde:** Na página home de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:home',
		'eventAction': 'clique:link',
		'eventLabel': 'ver-todos'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| 	                	| 			        	| 								         		|

- **Quando:**  Ao clicar no link "Termos e condições do Clube".
- **Onde:** Na página home de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:home',
		'eventAction': 'clique:botao',
		'eventLabel': 'termos-condicoes'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| 	                	| 			        	| 								         		|

---

**Assinar Clube:**<br />

- **Quando:** Ao clicar no botão "Assinar clube".
- **Onde:** Na página de Assinar clube de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:assinar',
		'eventAction': 'clique:link',
		'eventLabel': [[plano]]:[[valor]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[plano]]		    	| 'Plano 10000'			| Deve retornar o nome do plano selecionado. 	|
| [[valor]]		    	| '299,00'				| Deve retornar o valor do plano selecionado.   |

---

**Parceiros:**<br />

- **Quando:** Ao clicar nos botões "Eu quero".
- **Onde:** Na página de parceiros de Clube Movida.

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'clube-movida:parceiros',
		'eventAction': 'clique:botao',
		'eventLabel': '[[parceiro]]'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[parceiro]]		    | 'Disney'		    	| Deve retornar o nome do parceiro selecionado. |

---

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<script>
  document.addEventListener("DOMContentLoaded", function(event) {
    document.querySelectorAll("h1 a")[0].style.display = 'none';
  });
</script>