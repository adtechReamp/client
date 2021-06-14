![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - LP BTG+
Última atualização: 14/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)
- [LP simulador invest+](#lp-simulador-invest)
- [LP Calculadora de carbono](#lp-calculadora-de-carbono)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [http://btg.site.tkoa.me/](http://btg.site.tkoa.me/).

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

**Observações Gerais:**<br />
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
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | 	ID definido após o envio com sucesso do formulário					|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-xxxxxx'		| ID do container do GTM instalado no ambiente										|

---

### Geral


**Quando: No clique do logo do header**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:header',
    'eventLabel': 'logo'
  });
</script>
```

<br />

**Quando: No clique do link no footer**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:footer',
    'eventLabel': 'termos-de-uso'
  });
</script>
```

<br />

**Quando: No clique do botões ou links de cada seção**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-secao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao ou link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] | 'seja-btg+' e etc | Deve retornar o nome do item clicado.   |
| [[nome-secao]] | 'inove-seu-jeito-de-usar-o-banco', 'baixe-o-app-e-abra-sua-conta', 'cartao-btg+-black' e etc | Deve retornar o nome o titulo do item clicado.  |

<br />

**Quando: Na interação com os campos do formulário**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:formulario',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome-completo', 'email' e etc |  Retornar o nome do campo preenchido. |

<br />

**Quando: Na interação com os checkbox do formulário**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:checkbox:formulario',
    'eventLabel': '[[nome-checkbox]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-checkbox]] | 'li-e-concordo-com-a-politica', 'estou-de-acordo' e etc | Retornar o nome do checkbox que teve interação. |

<br />

**Quando: No clique dos botões do formulário**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao:formulario',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'cadastre-se-e-baixe-o-app', 'fechar', 'baixar-na-app-store'  e etc | Retornar o nome do botão clicado.  |

<br />

**Quando: Na tentativa de callback de envio do formulário**<br />

- **Onde:** Na lp de BTG+
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'callback:formulario',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc |  Retornar a mensagem de sucesso ou tipo de erro.  |
| [[User ID]]			| '1234656'			    | 	ID definido após o envio com sucesso do formulário					|


<br />

**Quando: Na interação com os botões**<br />

- **Onde:** Na página de sucesso de envio de formulário
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'disponivel-no-google-play:cadastro-feito-com-sucesso', 'baixar-na-apple-store:cadastro-feito-com-sucesso' |  Deve retornar o nome do botão clicado.|



<br />


---

### LP simulador invest+

**Quando: Ao clicar em algum dos cards**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:card',
    'eventLabel': 'selecionado-cartao:[[titulo-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-card]] |  'basico', 'avancado' ou 'black' |  Deve retornar o nome do card clicado.|



<br />

**Quando: Ao clicar em botoes de rendimento**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao',
    'eventLabel': '[[pergunta]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[pergunta]] | 'por-quanto-tempo-voce-deixa-seu-dinheiro-rendendo-em-btg?' |  Deve retornar a pergunta.|
| [[nome-botao]] | '1-ano's, '2-anos', '3-anos' e etc. |  Deve retornar o nome do botao clicado.|

<br />

**Quando: Ao clicar no botão crescente ou descrecente de gasto mensal com cartão de crédito**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao:[[nome-botao]]',
    'eventLabel': 'gasto-mensal-no-credito:[[gasto-credito]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'crescente' ou 'descrecente'. |  Deve retornar o nome do botao clicado.|
| [[gasto-credito]] | '1.500', '5.000', '10.000' e etc | Deve retornar com o valor do crédito gastado mensalmente.|

<br />

**Quando: Ao clicar no botao de solicitação de cartão**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'quero-meu-cartao-btg-mais'. |  Deve retornar o nome do botao clicado.|


<br />

### LP Calculadora de carbono

**Quando:Ao clicar em alguma aba do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:aba:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': '[[acao]]:aba:[[nome-aba]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] |  'abriu' ou 'fechou'.|  Deve retornar com a ação realizada na aba.|
| [[nome-aba]] |  'casa', 'transporte-do-dia-a-dia', 'tipo-de-viagem' , 'seu-relatorio-esta-quase-pronto' e etc.|Deve retornar o nome da aba clicada no formulário.|

<br />


**Quando:Ao interagir com qualquer campo do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:campo:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': 'preecheu: [[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'quantas-pessoas-vivem-na-sua-casa', 'consumo-eletrico', 'nome-completo', 'e-mail', 'telefone' , 'consumo-de-gas'e etc.|  Deve retornar o nome do campo preenchido.|


<br />

**Quando:Ao clicar em qualquer sub-aba do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:sub-aba:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': 'aba:[[nome-sub-aba]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-sub-aba]]|  'transporte-publico', 'individual', 'aerea', 'terrestre-carro-ou-moto' e etc.|  Deve retornar o nome da sub-aba clicada no formulário.|


<br />


**Quando:Ao interagir com qualquer checkbox do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:checkbox:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': 'pp:[[pergunta]]--ac: [[acao]]:[[nome-check]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[pergunta]] | 'voce-sabe-seu-consumo-de-agua-no-mes' e etc;|Deve retornar com o nome da pergunta relacionada ao checkbox.|
| [[acao]] | 'marcou' ou 'desmarcou'.|Deve retornar o nome da acao realizada.|
| [[nome-check]] |'sim' ou 'nao'.|Deve retonar com o nome do checkbox interagido.|

<br />


**Quando:Ao interagir com qualquer filtro do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:filtro:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': '[[tipo-filtro]]:selecionou:[[nome-filtro]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[tipo-filtro]] |  'cidade-de-origem', 'cidade-destino', 'quantidade','tipo-de-viagem', 'periocidade', 'meio-de-transporte'  e etc.|Deve retornar com o nome do tipo de filtro interagido.|
| [[nome-filtro]]|  'abadia-de-goias-go-brasil' , ' abate-mg-brasil', 'carro', 'ida-e-volta' e etc.|Deve retonar com o nome do filtro interagido.|

<br />

**Quando:Ao clicar em qualquer botão de adicionar ou excluir opção de viagem no formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': '[[acao]]:[[nome-aba]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]]| 'adicionou' ou 'exclui-o'.|Deve retornar com o nome da ação realizada.|
| [[nome-aba]]|  'tipo-de-viajem' ou 'transporte-do-dia-a-dia'.| Deve retornar o nome da aba onde está havendo interação.|

<br />

**Quando: Ao clicar em qualquer botão 'anterior' ou 'proximo' do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'clique:botao:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': 'aba:[[nome-aba]]:botao:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-aba]]|  'tipo-de-viajem' ou 'transporte-do-dia-a-dia'.|Deve retornar o nome da aba onde está havendo interação.|
| [[nome-botao]] | 'anterior' ou 'proximo'.| Deve retornar com o nome do botão clicado.|

<br />

**Quando: Ao interagir com o checkbox de 'concordo de politica de privacidade' no formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'interacao:checkbox:formulario:calcule-a-sua-pegada-de-carbono',
    'eventLabel': 'politica-de-privacidade:marcou:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]]|  'aceito' ou 'nao-aceito'.|Deve retornar o nome da acao realizada.|

<br />

**Quando: Na tentativa de callback de envio do formulário de calculo de carbono.**<br />

- **Onde:** Na lp de BTG+.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'lp-btgmais',
    'eventAction': 'callback:formulario',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]]|  'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.|Retornar a mensagem de sucesso ou tipo de erro. |

<br />

---

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
