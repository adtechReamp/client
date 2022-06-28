![Jellyfish](https://github.com/adtechReamp/client/blob/main/Jellyfish-Logo-Blue-01.jpg?raw=true)

> Analytics & Optimization<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados Lumis - RJ4
Última atualização: 10/02/2022 <br />
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
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://alianscesonaeshoppingbangudev.lumis.com.br/](hhttps://alianscesonaeshoppingbangudev.lumis.com.br/).

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
    'dimension3': '[[GTM-ID]]',
    'dimension4': '[[Nome Loja]]',
    'dimension5': '[[Nome Ambiente]]',
    'dimension6': '[[Localização]]',
    'dimension7': '[[Device ID]]',
    'dimension8': '[[CPF]]',
    'dimension9': '[[SKU Produto]]',
    'dimension10': '[[Email]]',
    'emailAllIn': '[[emailAllIn]]'
	
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
| [[emailAllIn]]   | 'jsdkjskdj' | Deve retornar o email do usuário criptografado em 2048, em todas as páginas apos ele logar ou se cadastrar    |

---

### Geral


**Quando: Ao preencher um dos campos do formulário de newsletter.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'interacao:newsletter',
    'eventLabel': 'preencheu-campo:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[nome-campo]] | 'nome' ou 'email'. | Deve retornar o nome do campo preenchido.    |


<br />

**Quando:Na tentativa de callback para enviar o formulário de newsletter.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'callback:newsletter',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[status]] |  'sucesso', 'erro:campo-nome-nao-preechido', 'erro:campo-email-nao-fornecido' e etc. | Deve retornar se a ação foi realizada com sucesso ou então o tipo de erro.    |


<br />

### Login e Cadastro


**Quando: No callback de cadastro ou login efetuados com sucesso**<br />

- **Onde:** Em todas as páginas que estiver disponível

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:area-logada',
    'eventAction': '[[nome-acao]]',
    'dimension1': '[[User ID]]
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[nome-acao]] |  'cadastrou' ou 'logou'. | Deve retornar o nome da ação realizada pelo usuario.    |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |

<br />

### Home

**Quando: Na tentativa de callback de autorização de notificação**<br />

- **Onde:** Na página Home após fazer o login.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'callback:autorizacao-de-notificacao',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[status]] |  'sucesso', 'erro:campo-nome-nao-preechido', 'erro:campo-email-nao-fornecido' e etc. | Deve retornar se a ação foi realizada com sucesso ou então o tipo de erro.    |


<br />

### Contato

**Quando: Ao preencher um dos campos do formulario de contato**<br />

- **Onde:** Na página de Contato.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:contato',
    'eventAction': 'interacao:formulario',
    'eventLabel': 'preencheu-campo:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[nome-campo]] |  'nome', 'cpf', 'email', 'telefone' e etc. | Deve retornar o nome do campo preenchido.    |


<br />

**Quando: Na tentativa de callback após envio do formulario de contato**<br />

- **Onde:** Na página de Contato.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': '[[nome-ambiente]]:contato',
    'eventAction': 'callback:formulario',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[status]] |  'sucesso', 'erro:campo-nome-nao-preechido', 'erro:campo-email-nao-fornecido' e etc. | Deve retornar se a ação foi realizada com sucesso ou então o tipo de erro.    |


<br />

### Editar Perfil

**Quando: Ao preencher um dos campos dos formulários**<br />

- **Onde:** Na página Editar Perfil.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:area-logada:editar-perfil',
    'eventAction': 'interacao:[[nome-formulario]]',
    'eventLabel': 'preencheu-campo:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[nome-formulario]] |  'perfil', 'endereco', 'email', cartao' e etc. | Deve retornar o nome do formulario preenchido.    |
| [[nome-campo]] |  'nome', 'cpf', 'email', 'telefone' e etc. | Deve retornar o nome do campo preenchido.    |


<br />

**Quando: Na tentativa de callback após envio do formulario**<br />

- **Onde:** Na página Editar Perfil.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:area-logada:editar-perfil',
    'eventAction': 'callback:[[nome-campo]]',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do ambiente.    |
| [[nome-campo]] |  'dados-de-cadastro', 'email' ou 'meus-cartoes' | Deve  retornar o nome do campo ao qual o botão pertence.    |
| [[status]] |  'sucesso', 'erro:campo-nome-nao-preechido', 'erro:campo-email-nao-fornecido' e etc. | Deve retornar se a ação foi realizada com sucesso ou então o tipo de erro.    |


<br />

### Enhanced E-commerce

**Na visualização de algum banner ou ads**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': '[[nome-ambiente]]:institucional:enhanced-ecommerce',
    'eventAction': 'promotionImpression',
'noInteraction': '1',
'ecommerce': {
    'promoView': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[promotion-name]]',
        'position': '[[p´romotion-position]]'
      }]
    }
  }
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[promotion-name]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[promotion-position]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners ou ads**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': '[[nome-ambiente]]:institucional:enhanced-ecommerce',
  'eventAction': 'promotionClick',
    'ecommerce': {
    'promoClick': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[promotion-name]]',
        'position': '[[promotion-position]]',
      }]
    }
  }
});
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[promotion-name]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[promotion-position]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**Na visualização de uma lista de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory':'[[nome-ambiente]]:institucional:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price':' [[product-price]]',
        'category': '[[product-category]]',
        'brand': '[[product-brand]]',
        'list': '[[product-list]]',
        'position': '[[product-position]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[product-id]] | 'i17mcjf106-771-2' | SKU do produto |
| [[product-price]] | '139.99' | Preço do produto |
| [[product-category]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[product-brand]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[product-list]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[product-position]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': '[[nome-ambiente]]:institucional:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[lista-produto]]'},
             'products': [{
               'name': '[[product-name]]',
               'id': '[[product-id]]',
               'price':' [[product-price]]',
               'category': '[[product-category]]',
               'brand': '[[product-brand]]',
               'list': '[[product-list]]',
               'position': '[[product-position]]',
               'coupon': '[[product-cupom]]',
               'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[product-id]] | 'i17mcjf106-771-2' | SKU do produto |
| [[product-price]] | '139.99' | Preço do produto |
| [[product-category]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[product-brand]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[product-list]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[product-position]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[product-cupom]] | '25%' e etc' | Desconto do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />


---


> Em caso de dúvidas, entrar em contato com: [ao.br@jellyfish.com](ao.br@jellyfish.com)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
