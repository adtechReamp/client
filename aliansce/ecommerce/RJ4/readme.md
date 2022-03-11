![Jellyfish](https://github.com/adtechReamp/client/blob/main/Jellyfish-Logo-Blue-01.jpg?raw=true)

> Analytics & Optimization<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados VTex - RJ4
Última atualização: 11/03/2022 <br />
Em caso de dúvidas, entrar em contato com: [ao.br@jellyfish.com](ao.br@jellyfish.com)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementacao)
- [Especificações Globais](#especificacoes-globais)
- [Dimensões Globais](#dimensoes-globais)
- [Geral](#geral)
- [Login e cadastro](#login-e-cadastro)
- [Home](#home)
- [Contato](#contato)
- [Editar Perfil](#editar-perfil)
- [Enhanced E-commerce](#enhanced-e-commerce)




## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://shoppingalso2021qa.myvtex.com/](https://shoppingalso2021qa.myvtex.com/).

<br />

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

## Implementacao

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

### Especificacoes Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.



### Dimensoes Globais:

**Dimensões Customizadas para todas as páginas:**<br />
Deve ser disparado um push de dataLayer no momento de carregamento de todas as páginas do site (Considerar também todas as trocas de Path, quando o conteúdo da página é alterado mas a página não recarrega).<br />


```html
<script>
	window.dataLayer = window.dataLayer || [];
	dataLayer.push({
		'dimension1': '[[User ID]]',
		'dimension2': '[[GA ClientID]]',
		'dimension3': '[[GTM-ID]]',
        'dimension4': '[[Nome Loja]]',
        'dimension5': '[[Nome Ambiente]]',
   		'dimension6': '[[Localização]]',
    	'dimension7': '[[Device ID]]',
    	'dimension8': '[[CPF]]',
        'dimension9': '[[SKU Produto]]',
        'dimension10': '[[Email]]'
	
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID definido após o cadastro e login										|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-NM5JRBW'		| ID do container do GTM instalado no ambiente										|
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja  |
| [[Nome Ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do shopping  |
| [[Localização]] | 'capao-redondo', 'morumbi', 'santa-cruz' e etc. | Deve retornar a localização  |
| [[Device ID]]   | 'XXXXXXX' | Deve retornar o ID do dispositivo utilizado   |
| [[CPF]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o CPF do usuário hasheado em SHA256   |
| [[SKU Produto]] | '45632187', '45612302' etc. | Deve retornar o sku do produto  |
| [[Email]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o email do usuário hasheado em SHA256   |

---

### Lista de Produtos

**Quando: Ao selecionar um dos checkboxes de filtro.**<br />

- **Onde:** Na página de lista de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:lista-de-produtos',
    'eventAction': 'interacao:checkbox:filtro',
    'eventLabel': '[[secao]]:[[nome-filtro]]:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'categoria', 'marca', 'cor' e etc. | Deve retornar o nome da seção do filtro.  |
| [[nome-filtro]] | 'branco', 'lacoste', 'infantil' e etc. | Deve retornar o nome do checkbox de filtro clicado.  |
| [[acao]] | 'check' ou 'uncheck' | Deve retornar se o usuário marcou ou desmarcou o checkbox.  |


<br />

**Quando: Ao clicar em uma das sugestões de consulta.**<br />

- **Onde:** Na página de lista de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:lista-de-produtos',
    'eventAction': 'clique:sugestao',
    'eventLabel': '[[consulta-sugerida]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[consulta-sugerida]] | 'camisa-feminina', 'toalha-de-banho' e etc. | Deve retornar o nome do termo de consulta clicado.  |


<br />

### PDP

**Quando: No clique para selecionar a cor do produto.**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:pdp',
    'eventAction': 'clique:cor',
    'eventLabel': '[[nome-cor]]:[[nome-produto]]',
    'dimension4': '[[nome-loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-cor]] | 'branco', 'preto', 'azul' e etc | Deve retornar a cor selecionada. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |



<br />

**Quando: No clique para selecionar o tamanho do produto**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:pdp',
    'eventAction': 'clique:tamanho',
    'eventLabel': '[[tamanho-selecionado]]:[[nome-produto]]',
    'dimension4': '[[nome-loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[tamanho-selecionado]] | '35', '40', '41'  e etc | Deve retornar o tamanho selecionado. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:pdp',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]',
    'dimension4': '[[nome-loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[quantidade-escolhida]] | '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:pdp',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-produto]]',
    'dimension4': '[[nome-loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[botao-ou-link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] | 'adicionar-a-sacola', 'favorita' e etc | Deve retornar o nome do botao ou link clicado. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />

### Sacola Modal

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página do modal da sacola
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:sacola-modal',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[botao-ou-link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] |  'continuar-comprando', 'finalizar-compra', 'fechar' e etc | Deve retornar o nome do botao ou link clicado. | |


<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na página do modal da sacola
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:sacola-modal',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[quantidade-escolhida]] |  '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

### Checkout

**Quando: No clique dos botões das etapas do checkout**<br />

- **Onde:** Em todas as etapas do checkout que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:checkout',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[step]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-botao]] |  'fechar-pedido', 'escolher-mais-produtos' e etc | Deve retornar o nome do botão clicado. |
| [[step]] |  'carrinho', 'entrega', 'pagamento' | Deve retornar o nome da etapa do checkout. |


<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na etapa do carrinho
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:checkout',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]:carrinho'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[quantidade-escolhida]] |   '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |


<br />

**Quando: Na interação com o campos de cada etapa do checkout**<br />

- **Onde:** Em todas as etapas do checkout que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:compras:checkout',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]:[[step]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-campo]] |  'cupom-de-desconto', 'cep, 'cartao-de-credito' | Deve retornar o nome do campo preenchido. |
| [[step]] | 'carrinho', 'entrega', 'pagamento' | Deve retornar o nome da etapa do checkout. |


<br />

**Quando: No callback de erro, caso haja erro para concluir a compra**<br />

- **Onde:** Na ultima etapa do checkout
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': '[[nome-ambiente]]:compras:checkout',
    'eventAction': 'callback',
    'eventLabel': 'erro:[[tipo-erro]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[tipo-erro]] |  'o-pedido-nao-pode-ser-criado', 'pagina-fora-do-ar' e etc | Deve retornar o tipo do erro, pelo qual o usuário não conseguiu finalizar a compra.  |


<br />


### Enhanced E-commerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory':'[[nome-ambiente]]:compras:enhanced-ecommerce',
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
        'position': '[[posicao-produto]]',
        'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
               'position': '[[posicao-produto]]',
               'coupon': '[[cupom-produto]]',
               'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />

**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
        'coupon': '[[cupom-produto]]',
        'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'addToCart',
  'eventCategory':'[[nome-ambiente]]:compras:enhanced-ecommerce',
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
        'coupon': '[[cupom-produto]]',
        'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da Sacola;
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'removeFromCart',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
        'quantity': '[[quantidade-produto]]',
        'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />

**No carregamento das etapas do checkout**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkout',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[opcao escolhida]] | 'receber', 'retirar' | Deve retornar os nomes dos tipos de entrega. |
| [[previsao-entrega]] |  'em-ate-4-dias-uteis', 'pompeia-em-ate-2-dias' | Usar essa variável apenas para etapa de entrega. Retorna as informações de forma de entrega. |


<br />


**Ao selecionar uma opção de pagamento**<br />

- **Onde:** Na página de carrinho e de checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
| [[opcao escolhida]] | 'cartao-de-credito', 'boleto' etc | Deve retornar os nomes dos tipos de entrega. |


<br />

**Na finalização da compra**<br />

- **Onde:** Na página de confirmação de compra
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'purchase',
  'eventCategory': '[[nome-ambiente]]:compras:enhanced-ecommerce',
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
        'coupon': '[[cupom-produto]]',
        'dimension4': '[[nome-loja]]'

      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'carioca-shopping', 'caxias-shopping', 'bangu-shopping' e etc. | Deve retornar o nome do ambiente.  |
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
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />

---

