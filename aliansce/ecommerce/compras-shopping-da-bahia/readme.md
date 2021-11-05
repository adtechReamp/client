![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Compras Shopping da Bahia
Última atualização: 02/11/2021 <br />
Em caso de dúvidas, entrar em contato com: [leandro.mori@jellyfish.com](leandro.mori@jellyfish.com)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueci minha senha](#esqueci-minha-senha)
- [Home](#home)
- [Lista de Produtos](#lista-de-produtos)
- [PDP](#pdp)
- [Meu carrinho modal](#meu-carrinho-modal)
- [Checkout](#checkout)
- [Enhanced E-commerce](#enhanced-e-commerce)




## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://compras.shoppingdabahia.com.br/](https://compras.shoppingdabahia.com.br/).

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

### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.



### Dimensões Globais:

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
        'dimension5': '[[Localização]]',
   		'dimension6': '[[[Device ID]]',
    	'dimension7': '[[CPF]]',
    	'dimension8': '[[Email]]'
	
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID definido após o cadastro e login										|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-NM5JRBW'		| ID do container do GTM instalado no ambiente										|
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja  |
| [[Localização]] | 'capao-redondo', 'morumbi', 'santa-cruz' e etc. | Deve retornar a localização  |
| [[Device ID]]   | 'XXXXXXX' | Deve retornar o ID do dispositivo utilizado   |
| [[CPF]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o CPF do usuário hasheado em SHA256   |
| [[Email]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o email do usuário hasheado em SHA256   |

---

### Geral


**Quando: Ao realizar uma busca na barra de pesquisa.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:geral',
    'eventAction': 'interacao:campo:busca',
    'eventLabel': '[[termo-buscado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-buscado]] | 'toalha-de-banho', 'camiseta-polo', 'cama-mesa-e-banho' e etc. | Deve retornar o termo buscado na barra de pesquisa.    |


<br />

### Cadastro


**Quando: Na interação com os campos.**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:cadastro',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'nome', 'email', 'bairro' e etc | Deve retornar o nome do campo preenchido.  |


<br />


**Quando: Na tentativa de callback para efetuar o cadastro**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'compras-shopping-da-bahia:cadastro',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |


<br />


### Login

**Quando: Na interação com os campos**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:login',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'email', 'senha' | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: Na tentativa de callback para efetuar o login**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'login',
    'eventCategory': 'compras-shopping-da-bahia:login',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |

<br />

### Esqueci minha senha

**Quando: Na interação com os campos**<br />

- **Onde:** Na página "Esqueci minha senha"
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:esqueci-minha-senha',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'email' e etc | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: Na tentativa de callback para cadastrar a nova senha**<br />

- **Onde:** Na página "Esqueci minha senha".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:esqueci-minha-senha',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:nao-encontramos-sua-conta' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />


### Home

**Quando: Ao preencher os campos de formulário de newsletter**<br />

- **Onde:** Na página Home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:home',
    'eventAction': 'interacao:campo:formulario',
    'eventLabel': 'newsletter:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | nome', 'email' e etc | Deve retornar o nome do campo preenchido.|


<br />

**Quando: No callback do formulário de newsletters**<br />

- **Onde:** Na página Home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:home',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:campo-email-nao-preenchido' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro.|


<br />

### PDP

**Quando: No clique para selecionar a cor do produto.**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:pdp',
    'eventAction': 'clique:cor',
    'eventLabel': '[[nome-cor]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-cor]] | 'branco', 'preto', 'azul' e etc | Deve retornar a cor selecionada. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |


<br />

### Checkout

**Quando: Na interação com os campos de cada etapa do checkout**<br />

- **Onde:** Em todas as etapas do checkout em que estiver disponivel.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:checkout',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]:[[step]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'cupom-de-desconto', 'cep', 'cartao-de-credito' e etc | Deve retornar o nome do campo preenchido. |
| [[step]] | 'carrinho', 'entrega', 'pagamento' e etc | Deve retornar o nome da etapa do checkout. |


<br />

**Quando: No callback de finalização de compras**<br />

- **Onde:** Em todas as etapas do checkout que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-shopping-da-bahia:checkout',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] |  'sucesso', 'erro:campo-cartao-nao-preenchido', 'erro:campo-cep-nao-preenchido' | Deve retornar com sucesso ou o tipo de erro. |

<br />


### Enhanced E-commerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
  'eventAction': 'promotionClick',
    'ecommerce': {
    'promoClick': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[nome-promocao]]',
        'position': '[[posicao-promocao]]',
        'creative': '[[arte-banner]]'
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory':'compras-shopping-da-bahia:enhanced-ecommerce',
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
               'coupon': '[[cupom-produto]]',
               'dimension4': '[[nome-loja]]'
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
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />

**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
  'eventCategory':'compras-shopping-da-bahia:enhanced-ecommerce',
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
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
        'coupon': '[[cupom-produto]]',
        'dimension4': '[[nome-loja]]'
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
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |


<br />


**Ao selecionar uma opção de entrega**<br />

- **Onde:** Na página de checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce,
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
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'purchase',
  'eventCategory': 'compras-shopping-da-bahia:enhanced-ecommerce',
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


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
