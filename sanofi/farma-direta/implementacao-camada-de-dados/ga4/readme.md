![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados GA4 - Farma Direta
Última atualização: 27/04/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

---

<br />

## Sumário

- [Objetivo](#objetivo)
- [Instalação](#instala%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Enhanced E-commerce](#enhanced-e-commerce)


---
<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics 4 referentes ao ambiente de [https://www.farmadireta.com.br/](https://www.farmadireta.com.br/).

---
<br />

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics 4 devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

<br />

## Instalação

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.


**Inserir a camada de dados antes do snippet de instalação do Google Tag Manager.
Exemplo:**


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

<br />

### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.

---

<br />

### Implementação dos Eventos
<br />


### Enhanced E-commerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    event: 'view_promotion',
    ecommerce: {
        items: [{
        promotion_id: '[[promotion-id]]',
        promotion_name: '[[nome-promocao]]',
        creative_slot: '[[posicao-promocao]]'
        }]
    }
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[id-promocao]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'remedios-desconto' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1', '2' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'select_promotion',
  ecommerce: {
    items: [{
        promotion_id: '[[promotion-id]]',
        promotion_name: '[[nome-promocao]]',
        creative_slot: '[[posicao-promocao]]'
    }]
  }
});
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[id-promocao]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'remedios-desconto' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1', '2' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'view_item_list',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_list_name: '[[lista-produto]]',
      index: '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[lista-produto]] | 'xxxxxx' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'select_item',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_list_name: '[[lista-produto]]',
      index: '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[lista-produto]] | 'xxxxxx' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />

**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'view_item',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_list_name: '[[lista-produto]]',
      item_variant: '[[variacao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[lista-produto]] | 'xxxxxx' | Nome da lista que o produto aparece |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'add_to_cart',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_list_name: '[[lista-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[lista-produto]] | 'xxxxxx' | Nome da lista que o produto aparece |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da Sacola;
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'remove_from_cart',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_list_name: '[[lista-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[lista-produto]] | 'xxxxxx' | Nome da lista que o produto aparece |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />

**No carregamento da etapa do checkout 'Carrinho'**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'view_cart',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />


**Ao clicar no botão 'Comprar'**<br />

- **Onde:** Na página do carrinho
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'begin_checkout',
  ecommerce: {
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />


**No carregamento da etapa do checkout 'Endereço'**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'add_shipping_info',
  ecommerce: {
    shipping_tier: '[[tipo-entrega]]',
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[tipo-entrega]] | 'sedex', 'transportadora' e etc | Tipo de entrega escolhida |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />


**No carregamento da etapa do checkout 'Pagamento'**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'add_payment_info',
  ecommerce: {
    payment_type: '[[tipo-pagamento]]',
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[tipo-pagamento]] | 'boleto', 'cartao-credito' e etc | Tipo de pagamento escolhido |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />


**Na finalização da compra**<br />

- **Onde:** Na página de confirmação de compra
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'purchase',
  ecommerce: {
    currency: 'BRL',
    value: '[[total-transacao]]',
    tax: '[[total-taxas]]',
    shipping: '[[total-entrega]]',
    transaction_id: '[[id-transacao]]',
    coupon: '[[cupom]]',
    items: [{
      item_name: '[[nome-produto]]',
      item_id: '[[id-produto]]',
      price: '[[preco-produto]]',
      item_brand: '[[marca-produto]]',
      item_category: '[[categoria-produto]]',
      item_variant: '[[variacao-produto]]',
      quantity: '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[total-transacao]] | '250.50' | Valor total da transação incluindo frete e taxas |
| [[total-taxas]] | '2.39' | Valor de taxas da transação |
| [[total-entrega]] | '15.98' | Valor do frete da transação |
| [[id-transacao]] | 'xxxxxxx' | ID único da transação |
| [[cupom]] | 'cupom-2021' | Cupom de desconto utilizado na transação |
| [[nome-produto]] | 'allegra', 'dorflex' e etc | Nome do produto |
| [[id-produto]] | 'xxxxxxxx' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'medley', 'sanofi' e etc | Marca do produto |
| [[categoria-produto]] | 'medicamentos', 'bebe-crianca', 'vitaminas-alimentos' e etc | Categoria do produto |
| [[variacao-produto]] | 'xxxxx' | Variação do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />

---


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
