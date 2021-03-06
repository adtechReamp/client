![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Ajustes/implementações da Camada de dados - Geral
Última atualização: 11/05/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [vitrine-de-produtos](#vitrine-de-produtos)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes aos ambientes:

[www.bangushopping.com](www.bangushopping.com),
[www.boulevardshoppingbauru.com.br](www.boulevardshoppingbauru.com.br),
[www.boulevardbelem.com.br](www.boulevardbelem.com.br),
[www.boulevardshopping.com.br](www.boulevardshopping.com.br),
[www.boulevardcampos.com.br](www.boulevardcampos.com.br),
[www.boulevardvilavelha.com.br](www.boulevardvilavelha.com.br),
[www.boulevardshoppingbrasilia.com.br](www.boulevardshoppingbrasilia.com.br),
[www.cariocashopping.com.br](www.cariocashopping.com.br),
[www.caxiasshopping.com.br](www.caxiasshopping.com.br),
[www.parqueshoppingba.com.br/](www.parqueshoppingba.com.br/),
[www.parqueshoppingbelem.com.br](www.parqueshoppingbelem.com.br),
[www.maceioparqueshopping.com.br](www.maceioparqueshopping.com.br),
[www.passeioshopping.com.br](www.passeioshopping.com.br),
[recreioshopping.com.br](recreioshopping.com.br),
[www.santanaparqueshopping.com.br](www.santanaparqueshopping.com.br),
[www.saogoncaloshopping.com.br/](www.saogoncaloshopping.com.br/),
[www.shoppingdabahia.com.br](www.shoppingdabahia.com.br),
[www.shoppinggranderio.com.br](www.shoppinggranderio.com.br),
[www.shoppingparangaba.com.br](www.shoppingparangaba.com.br),
[www.shoppingtaboao.com.br](www.shoppingtaboao.com.br),
[www.viaparqueshopping.com.br](www.viaparqueshopping.com.br),
[www.westplaza.com.br](www.westplaza.com.br),
[www.shoppingpracanovaaracatuba.com.br](www.shoppingpracanovaaracatuba.com.br),
[www.boulevardlondrinashopping.com.br/](www.boulevardlondrinashopping.com.br/),
[www.francashopping.com.br/](www.francashopping.com.br/),
[www.manauarashopping.com.br/](www.manauarashopping.com.br/),
[www.parquedpedro.com.br/](www.parquedpedro.com.br/),
[www.passeiodasaguasshopping.com.br/](www.passeiodasaguasshopping.com.br/),
[www.shoppingcampolimpo.com.br/](www.shoppingcampolimpo.com.br/),
[www.shoppingmetropole.com.br/](www.shoppingmetropole.com.br/),
[www.plazasulshopping.com.br/](www.plazasulshopping.com.br/),
[www.uberlandiashopping.com.br/](www.uberlandiashopping.com.br/),<br />
[www.pracanovashopping.com.br](www.pracanovashopping.com.br),<br />
[boulevardfeira.com.br/](boulevardfeira.com.br/)<br />
[www.montesclarosshopping.com.br/](https://www.montesclarosshopping.com.br/)<br />

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

<H3 align="center"> IFRAME </h3>



### Vitrine de produtos

**Quando: Na interação com o campo de filtro (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.


    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'interacao:filtro',
    'eventLabel': '[[tipo-filtro]]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-item]]   |  'artigos-diversos', 'conveniencia-servicos', 'alimentacao' e etc. | Deve retornar o nome do item escolhido no filtro|
| [[tipo-filtro]]   | 'categoria', 'lojar' ou 'canais'.| Deve retornar o tipo do filtro onde o usuário está interagindo.|


<br />

**Quando: No clique em alguma loja (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.

 
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:loja',
    'eventLabel': '[[nome-loja]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-loja]]  |'a-especialista', 'academia-bodytech' e etc| Deve retornar o nome da loja clicada|

<br />

**Quando: No clique dos botões de alguma loja (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.

 
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:botao:loja',
    'eventLabel': '[[nome-loja]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-loja]]  |'a-especialista', 'academia-bodytech' e etc| Deve retornar o nome da loja clicada|
| [[nome-botao]]   |'whatsapp', 'site-da-loja', 'drive-thru' e etc| Deve retornar o nome do botão clicado.|

<br />

**Quando: Ao clicar no link "ver mais" (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.

 
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:link',
    'eventLabel': 'ver-mais'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |

<br />




> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />
