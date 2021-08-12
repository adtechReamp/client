![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization <br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BTG - BTG+ Business
Última atualização: 09/08/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Camada de dados](#camada-de-dados)
- [Geral](#geral)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://d22halzc75qm2m.cloudfront.net/](https://d22halzc75qm2m.cloudfront.net/)

<br />



## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---
	
	
## Camada de dados

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

**Quando: No clique dos itens do header.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'nossos-produtos', 'logo', 'entrar', 'seja-btg-business' e etc | Retornar o nome do item clicado. |



<br />

**Quando: No clique do menu superior**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[nome-menu]]:[[submenu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-menu]]  |  'solucoes', 'parceiros', 'pme-insights' e etc |  Retornar o nome do menu clicado. |
| [[submenu]]| 'abra-sua-conta', 'energia-solar', 'seguro'e etc |Retornar o nome do submenu clicado. |


<br />

**Quando: No clique do botão no sub-menu do header na aba de 'soluções'.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'clique:menu-botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'antecipe-agora'. |Deve retonar o nome do botão clicado. |


<br />

**Quando: Na interação do botao de expansão "ver mais informações" e "ver menos informações"  no footer.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'interacao:footer-botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]]|'ver-mais-informacoes' e 'ver-menos-informacoes'. |Deve retonar o nome do botão clicado.  |


<br />

**Quando: No clique do itens do footer**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]] |  'explore', 'veja-tambem', 'baixe-nosso-app', 'fale-conosco' e etc| Retornar o nome da seção.  |
|[[nome-item]]  | 'parceiros', 'google-play', '1138-3336', 'desenvolvedores' , 'facebook' e etc.| Retornar o nome do item clicado dentro da seção.|



<br />


**Quando: Na interação com as dúvidas**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:[[nome-pagina]]',
    'eventAction': 'interacao:duvidas',
    'eventLabel': '[[nome-pergunta]]:[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
| [[nome-pergunta]] |  'o-que-e-o-btg-business', 'para-que-e' , 'como-faco-para-contratar-solucoes-btg+-business'e etc| Deve retornar o nome da pergunta.  |
| [[acao]] | 'abriu' ou 'fechou' | Deve retornar a ação do usuário.|



<br />



**Quando:No clique dos botões dos banners.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:geral',
    'eventAction': 'clique:botao:banner',
    'eventLabel': '[[nome-botao]]:[[nome-banner]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-botao]]|  'antecipe-agora', 'abra-sua-conta' e etc| Retornar o nome do botão clicado.|
|[[nome-banner]]|   'para-fazer-seu-negocio, 'Conta digital PJ', 'Antecipação de cartões', 'Mercado livre de energia '  e etc| Retornar o nome do banner clicado. |




<br />

**Quando:   Ao clicar na seção de abas.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'clique:aba',
    'eventLabel': '[[nome-aba]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-aba]]|   'pix', 'solucoes-de-pagamento', 'gestao-financeira' e etc| Retornar o nome do aba clicado.  |




<br />

**Quando:  Ao clicar nos botões dentro das abas.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'clique:botao:[[nome-aba]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-aba]]|  'pix', 'solucoes-de-pagamento', 'gestao-financeira' e etc| Retornar o nome do aba clicado.  |
|[[nome-botao]]|  'abra-sua-conta' e etc.|  Retornar com o nome do botão clicado |






<br />

**Quando:  No clique dos botões ou links de cada seção.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-item]]:[[nome-secao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[botao-ou-link]]| 'botao' ou 'link'| Deve retornar o tipo de elemento clicado.   |
|[[nome-item]] | 'faca-sua-reserva', 'tabela-de-tarifas', 'ver-todas', 'conta-digital', 'setas' e etc| Retornar o nome do item clicado.|
|[[nome-secao]] | 'vantagens-de-abrir-a-conta digital-pj- do-btgmais-business', ' duvidas' 'nossas-solucoes'  e etc| Retornar o nome seção. |

<br />

---

<br />

**Quando: No clique dos links de cada card.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'clique:[[botao ou link]]-card',
    'eventLabel': '[[nome-item]]:[[nome-secao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[botao-ou-link]]| 'botao' ou 'link'| Deve retornar o tipo de elemento clicado.   |
|[[nome-item]] |  'o-que-e-fluxo-de-caixa-e-como-ele-ajuda-sua empresa?', 'como-lidar-com-a-pressao-de-empreender?', 'saiba-mais' e etc| Retornar o nome do item clicado.|
|[[nome-secao]] |'parceiros-em-destaque', ' nossos-parceiros' 'pmes-insights'  e etc| Retornar o nome seção. |

<br />

**Quando: Na interação com os campos do formulário**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'interacao:formulario:[[nome-formulario]]',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-formulario]]| 'o-btg-business-tambem-e-para-desenvolvedores', 'mercado-livre-de-energia ', 'faca-a-sua-reserva' e etc| Deve retornar o nome do formulário.  |
|[[nome-campo]]| 'nome-completo', 'email', 'telefone', 'empresa', 'valor-de-gasto-energia-da-empresa', 'cnpj' e etc| Retornar o nome do campo preenchido. |

<br />

**Quando: Na interação com os checkbox do formulário**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'interacao:checkbox:formulario:[[nome-formulario]]',
    'eventLabel': 'selecionou:[[nome-checkbox]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-formulario]]| 'o-btg-business-tambem-e-para-desenvolvedores', 'mercado-livre-de-energia ', 'faca-a-sua-reserva' e etc| Deve retornar o nome do formulário.|
|[[nome-checkbox]]|'por-e-mail', 'por-telefone' e etc | Retornar o nome do checkbox que teve interação.|

<br />

---

<br />

**Quando: No clique dos botões do formulário**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'clique:botao:formulario:[[nome-formulario]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-formulario]]| 'o-btg-business-tambem-e-para-desenvolvedores', 'mercado-livre-de-energia ', 'faca-a-sua-reserva' e etc| Deve retornar o nome do formulário. |
|[[nome-botao]]|'continuar', 'quero-saber-mais' e etc| Retornar o nome do botão clicado. |

<br />

**Quando: Na tentativa de callback de envio do formulário**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'btgmais-business:[[nome-pagina]] ',
    'eventAction': 'callback:formulario:[[nome-formulario]]',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] |   'abra-sua-conta', 'pix', 'antecipacao-de-cartoes' e etc.| Deve retornar o nome da página. |
|[[nome-formulario]]| 'o-btg-business-tambem-e-para-desenvolvedores', 'mercado-livre-de-energia ', 'faca-a-sua-reserva' e etc| Deve retornar o nome do formulário. |
|[[status]]|'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc|Retornar a mensagem de sucesso ou tipo de erro.|

<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
