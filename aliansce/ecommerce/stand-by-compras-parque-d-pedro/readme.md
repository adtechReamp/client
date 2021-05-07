![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Manutenção da Camada de dados - Compras Parque D Pedro
Última atualização: 27/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Geral](#geral)
- [Bem vindo](#bem-vindo)
- [Lista de Produtos](#lista-de-produtos)
- [Enhanced E-commerce](#enhanced-e-commerce)




## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://compras.parquedpedro.com.br/](https://compras.parquedpedro.com.br/).

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

----
<H3 align="center"> AJUSTES E IMPLEMENTAÇÕES QUE DEVEM SER REALIZADOS </h3>

### Geral

**Quando: No clique dos itens do menu superior.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.

<b>Deve ser ajustado o label, pois está retornando com os valores invertidos! (Tagbook - linha 10)</b>
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[item-menu]]:[[secao]]:[[item-submenu]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[item-menu]] | 'moda-feminina', 'moda-masculina', 'joias-e-relogios' e etc. | Deve retornar o nome do item clicado no menu.   |
| [[secao]] | 'calcados', 'joias' , 'roupas' e etc. | Deve retornar, se existente, a seção do menu clicada.    |
| [[item-submenu]] | 'tenis', 'lingeries', 'aneis' e etc. | Deve retornar, se existente, o nome do item clicado no submenu.  |


<br />

---

### Enhanced E-commerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
<b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 56)</b>

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
    'eventAction': 'promotionImpression',
'noInteraction': '1',
'ecommerce': {
    'promoView': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[nome-promocao]]',
        'position': '[[posicao-promocao]]'
      }]
    }
  }
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners**<br />

- **Onde:** Em todas as páginas que estiver disponivel.

<b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 57)</b>  

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'promotionClick',
    'ecommerce': {
    'promoClick': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[nome-promocao]]',
        'position': '[[posicao-promocao]]'
	}]
    }
  }
});
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.

 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 58)</b>    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory':'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'brand': '[[marca-produto]]',
        'list': '[[lista-produto]]',
        'position': '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    
 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 59)</b>        

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[lista-produto]]'},
             'products': [{
               'name': '[[nome-produto]]',
               'id': '[[id-produto]]',
               'price':' [[preco-produto]]',
               'category': '[[categoria-produto]]',
               'brand': '[[marca-produto]]',
               'list': '[[lista-produto]]',
               'position': '[[posicao-produto]]',
               'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |

<br />

**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    
 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 60)</b>        

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'productDetail',
  'noInteraction': '1',
  'ecommerce': {
    'detail': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'brand': '[[marca-produto]]',
        'variant': '[[tamanho-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel

 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 61)</b>     

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'addToCart',
  'eventCategory':'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'addToCart',
    'ecommerce': {
    'add': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da Sacola;

 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 62)</b>     

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'removeFromCart',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'removeFromCart',
    'ecommerce': {
    'remove': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />

**No carregamento das etapas do checkout**<br />

- **Onde:** Na página do checkout
    
 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 63)</b> 

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkout',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkout',
  'noInteraction': '1',
  'ecommerce': {
    'checkout': {
      'actionField': {'step': '[[checkout-index]]'},
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkout-index]] | '1-carrinho', '2-entrega', '3-pagamento'| Retornar de acordo com a página que o usuário está. |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />


**Ao selecionar uma opção de entrega**<br />

- **Onde:** Na página de checkout
    
 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 64)</b>     

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'ecommerce': {
    'checkout_option': {
      'actionField': {'option': shipping:[[opcao escolhida]]:[[previsao-entrega]]}
{step:2},
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[opcao escolhida]] | 'receber', 'retirar' | Deve retornar os nomes dos tipos de entrega. |
| [[previsao-entrega]] |  'em-ate-4-dias-uteis', 'pompeia-em-ate-2-dias' | Usar essa variável apenas para etapa de entrega. Retorna as informações de forma de entrega. |


<br />


**Ao selecionar uma opção de pagamento**<br />

- **Onde:** Na página de carrinho e de checkout

 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 65)</b>     

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'ecommerce': {
    'checkout_option': {
      'actionField': {'option': payment:[[opcao escolhida]]}
{step:3},
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[opcao escolhida]] | 'cartao-de-credito', 'boleto' etc | Deve retornar os nomes dos tipos de entrega. |


<br />

**Na finalização da compra**<br />

- **Onde:** Na página de confirmação de compra

 <b>Deve ser implementado no código fonte do site e não via GTM, favor alterar isso! (Tagbook - linha 65)</b>      

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'purchase',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'purchase',
  'noInteraction': '1',
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': '[[id-transacao]]',
        'revenue': '[[valor-total-transacao]]',
        'shipping': '[[frete-transacao]]',
        'coupon': '[[coupon-transacao]]', 
        'tax': '[[taxa-transacao]]'
      },
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[id-transacao]] |  '000011652' | ID único da transação |
| [[valor-total-transacao]] |  '250.50' | Valor total da transação incluindo frete e taxas |
| [[frete-transacao]] |  '15.98' | Valor do frete da transação |
| [[taxa-transacao]] |  '2.39' | Valor de taxas da transação |
| [[coupon-transacao]] | 'cupom-2020' | Cupom de desconto utilizado na transação - promoção nivel pedido |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />

---


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
