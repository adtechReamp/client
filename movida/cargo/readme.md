![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Área - Digital Analytics <br />
> Documento de Especificação Técnica


## Implementação da Camada de dados - Movida - Cargo
Última atualização: 04/10/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Movida - Cargo](https://www.movida.com.br/cargo).


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

### Parâmetros indispensáveis do datalayer:

**Onde:** - Em todos as etapas de reserva do veículo. <br />

```html
<script>
dataLayer.push({
        'user_id': [[user_id]],
        'client_id': [[client_id]],
        'valor_total_geral': [[valor_total_diarias]],
        'grupo_de_carros': [[grupo_de_carros]],
        'data_devolucao': [[data_devolucao]],
        'data_retirada': [[data_retirada]],
        'hora_devolucao': [[hora_devolucao]],
        'hora_retirada': [[hora_retirada]],
        'local_devolucao': [[local_devolucao]],
        'local_retirada': [[local_retirada]]
});
</script>
```


| Variável 				| Exemplo 				| Descrição 					|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id do usuário.			|
| [[client_id]] 			| '123456'				| Deve retornar o id que é gerado pelo GA.	|
| [[valor_total_geral]]			| '200,00'				| Deve retornar o valor da reserva.		|
| [[grupo_de_carros]]		| 'Grupo H - C4, 2008, Duster ou similar'	| Deve retornar o grupo do carro.	|
| [[data_devolucao]]			| '20/10/2021'				| Deve retornar a data de devolução.	|
| [[data_retirada]]			| '19/10/2021'				| Deve retornar a data de retirada.	|
| [[hora_devolucao]]			| '14:00'				| Deve retornar a hora de devolução.	|
| [[hora_retirada]]			| '14:00'				| Deve retornar a hora de retirada.	|
| [[local_devolucao]]		| 'SAO PAULO - GUARULHOS AEROPORTO'			| Deve retornar o local de devolução. |
| [[local_retirada]]		| 'SAO PAULO - GUARULHOS AEROPORTO'			| Deve retornar o local de retirada. |


---

### Especificação de Micro-conversões:

**Onde:** - Na página Home ou Modelos Veículos. <br />
**Quando:** - Ao clicar no botão "Quero Esse".

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'cargo:home',
		'eventAction': 'clique:botao',
		'eventLabel': 'quero-esse',
		'user_id': [[user_id]],
                'client_id': [[client_id]],
		'grupo_de_carros': [[grupo_de_carros]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id do usuário.										|
| [[client_id]] 			| '123456'				| Deve retornar o id que é gerado pelo GA.									|
| [[grupo_de_carros]]			| 'Grupo H - C4, 2008, Duster ou similar'				| Deve retornar o grupo do carro.										|

---

**Onde:** - Na página Home ou Modelos Veículos. <br />
**Quando:** - Ao clicar no botão "Quero Contratar".

```html
<script>
	dataLayer.push({
		'event': 'genericEvent',
		'eventCategory': 'cargo:home',
		'eventAction': 'clique:botao',
		'eventLabel': 'quero-contratar',
		'user_id': [[user_id]],
                'client_id': [[client_id]]
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 						|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[user_id]] 			| '1234'				| Deve retornar o id do usuário.		  		|
| [[client_id]] 			| '123456'				| Deve retornar o id que é gerado pelo GA.		|

---

**Onde:** - Na página de Detalhes do Veículo. <br />
**Quando:** - Ao clicar no botão "continuar".

```html
<script>
dataLayer.push({
        'event': 'genericEvent',
        'eventCategory': 'cargo:detalhes',
        'eventAction': 'clique:botao',
        'eventLabel': 'continuar',
        'franquia': [[franquia]]
});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[franquia]]			| '1 mês - 1000 km'				| Deve retornar a franquia selecionada.	|

---

**Onde:** - Na página de Proteções e Itens. <br />
**Quando:** - Ao clicar no botão "continuar".

```html
<script>
dataLayer.push({
        'event': 'genericEvent',
        'eventCategory': 'cargo:protecoes',
        'eventAction': 'clique:botao',
        'eventLabel': 'continuar',
	'protecoes': [[protecoes]]
});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[protecoes]]			| 'Super Mensal'				|  Deve retornar as proteções da reserva.	|

---

### Enhanced Ecommerce:
Em caso de dúvidas sobre a configuração do Enhanced Ecommerce, acesse o este link: [https://developers.google.com/tag-manager/enhanced-ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce)

**Onde:** - Na página de Finalizar Reserva. <br />
**Quando:** - Ao clicar no botão "Finalizar Reserva".

```html
<script>
dataLayer.push({
        'event': 'purchase',
        'eventCategory': 'cargo:purchase',
        'eventAction': 'clique:botao',
        'eventLabel': 'continuar',
	'id_confirmacao': [[id_confirmacao]],
        'transaction_id': [[transaction_id]],
        'ecommerce': [
                'purchase': [
                        'actionField': [
                                'action': 'purchase',
                                'fluxo': 'purchase', 
                                'id': [[id_ecommerce]],
                                'revenue': [[revenue]],
                                'tax': [[tax]]
                        ]
                        'product': [
                                'category': [[category]],
                                'name': [[name]],
                                'price': [[price]],
                                'quantity': [[quantity]]
                        ]
                ]
        ]
});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[id_confirmacao]]			| 'MIX864H4'				|  Deve retornar o código da reserva.	|
| [[transaction_id]]			| '123456'				|  Deve retornar o Id da transação da reserva.	|
| [[id_ecommerce]]			| '654321'				|  Deve retornar o Id do purchase.	|
| [[revenue]]			| '1.500,00'				|  Deve retornar oo valor total da reserva.	|
| [[tax]]			| '45,00'				|  Deve retornar o valor da taxa da reserva.	|
| [[category]]			| 'Protecao, Grupo, Acessorio e etc'	|  Deve retornar a categoria do produto.	|
| [[name]]			| 'PROTEAAOBASICA, AX, CarbonFree e etc'|  Deve retornar o nome do produto.	|
| [[price]]			| '200,00'				|  Deve retornar o preço diário do produto.	|
| [[quantity]]			| '1, 15, 30'				|  Deve retornar a quantidade de diárias.	|


---


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<script>
  document.addEventListener("DOMContentLoaded", function(event) {
    document.querySelectorAll("h1 a")[0].style.display = 'none';
  });
</script>