![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization <br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BP - CENTRAL DE MARCAÇÃO ONLINE
Última atualização: 20/07/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br)   /   [rodolfo.nogueira@reamp.com.br](rodolfo.nogueira@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Geral](#geral)
- [Home](#home)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueceu-sua-senha](#esqueceu-sua-senha)
- [Escolha o procedimento-Consultas](#escolha-o-procedimento-consultas)
- [Escolha o procedimento-Exames de diagnostico](#escolha-o-procedimento-exames-de-diagnostico)
- [Setor de exames](#setor-de-exames)
- [Meus convenios](#meus-convenios)
- [Data e horario](#data-e-horario)
- [Verifique os dados](#verifique-os-dados)
- [marcacao confirmada](#marcacao-confirmada)
- [Painel](#painel)
- [Meus dados](#meus-dados)
- [Duvidas frequentes](#duvidas-frequentes)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://hospitalbp.centraldemarcacao.com.br/](https://hospitalbp.centraldemarcacao.com.br/)

<br />

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

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

### Geral

**Quando: No clique de algum elemento do header.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'menu' e 'logo'.|  Deve retornar com o nome do elemento clicado no header.  |


<br />

**Quando: No clique do sub-menu superior lateral.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:link',
    'eventLabel': '[[sub-menu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-formulario]] | 'nova-marcacao', 'minhas-marcacao', 'meus-convenios', 'meus-dados' e etc. |  Deve retornar com o nome do elemento clicado no sub-menu.  |


<br />

**Quando: Ao clicar em abrir formulario de chat.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao',
    'eventLabel': '[[acao-chat]]:formulario-chat'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[acao-chat]]|  'abriu' e 'fechou'. |  Deve retornar com a ação realizada.  |


<br />

**Quando: Na interação com os campos do chat de contato.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'interacao:formulario-chat:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]] |  email', 'nome', 'telefone', 'motivo-de-contato' e etc.|  Deve retornar o nome do campo preenchido.  |


<br />


**Quando: Ao clicar nos botões do formulario de contato.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:botao-formulario-chat',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-botao]] |  'iniciar' e 'enviar'.|  Deve retornar com o nome do botão clicado.  |


<br />

**Quando: Ao clicar nos botões inferior.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:geral',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]] |  'link' ou 'botao'.|Deve Retornar com o nome do elemento clicado.|
|[[nome-elemento]] |   'proximo-passo' e 'cancelar'.|   Deve retornar o nome do botão clicado.|


<br />

**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'bp-cm:geral-formulario-chat',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]] |  'sucesso', 'erro-inesperado'.| Deve retornar a mensagem de sucesso ou o tipo de erro. |



<br />

### Home

**Quando:No clique do botão de cadastro .**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:home',
    'eventAction': 'clique:botao',
    'eventLabel': 'realizar-cadastro'
  });
</script>

```

<br />

### Cadastro

**Quando: Na interação com os campos.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]|'nome', 'email', 'bairro', 'cpf', 'telefone' e etc.|Deve retornar o nome do campo preenchido. |


<br />

**Quando:Na interação com o checkbox.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'interacao:checkbox',
    'eventLabel': '[[acao]]:autorizo-o-uso-dos-meus-dados'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[acao]]|'marcou, 'desmarcou'.|Deve retornar a ação do usuário. |


<br />

**Quando:No clique dos botões.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-botao]]|'confirmar-cadastro' e 'cancelar'.|Deve retornar o nome do botão clicado. |


<br />


**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Na página de cadastro.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'bp-cm:cadastro',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]] |'sucesso', 'erro-inesperado'.| Deve retornar a mensagem de sucesso ou o tipo de erro.|

<br />

### Login

**Quando: Na interação com os campos.**<br />

- **Onde:**  Na página de login.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:login',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]| 'cpf' e 'senha'.| Deve retornar o nome do campo preenchido. |


<br />

**Quando:No clique dos botões ou links.**<br />

- **Onde:**  Na página de login.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:login',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|  'link' ou 'botao'.|  Deve Retornar com o nome do elemento clicado. |
|[[nome-botao]]|  'acessar-perfil' e 'esqueci-minha-senha'.|  Deve retornar o nome do botão clicado.  |


<br />

**Quando: Na tentativa de callback para envio de formulario de contato.**<br />

- **Onde:**  Na página de Login.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'bp-cm:login,
    'eventAction': 'callback:formulario-login',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]] |'sucesso', 'erro-inesperado'.| Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />

### Esqueceu sua senha

**Quando:Na interação com os campos.**<br />

- **Onde:**  Na página de "esqueceu sua senha".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:esqueceu-sua-senha',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]|  'cpf'.|Deve retornar o nome do campo preenchido. |



<br />

**Quando:Ao clicar me botões ou link.**<br />

- **Onde:**  Na página de "esqueceu sua senha".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:esqueceu-sua-senha',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]| 'botao' e 'link'.| Deve retornar com o tipo do elemento.|
|[[botao-ou-link]]| 'recuperar-senha, 'voltar-e-fazer-login'.| Deve retornar com o nome do botao ou link clicado.|




<br />

### Escolha o procedimento-Consultas

**Quando:Na interação com qualquer checkbox.**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Consultas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'interacao:checkbox:[[secao]]',
    'eventLabel': '[[acao]]:[[nome-check]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[secao]]|selecione-tipo-agendamento', 'voce-nao-cadastrou-seu-convenio', 'digite-o-nome-da-especialidade' , 'deseja-escolher-algum-medico'.|Deve retornar com o nome da seção.|
|[[acao]]|'marcou', 'desmarcou'.|  Deve retornar com o tipo de ação realizada.|
|[[nome-check]]|'agendamento-convencional' , 'agendamento-para-teleconsulta', 'particular', 'sim', 'nao' e etc.| Deve retornar com o nome do checkbox interagido.|

<br />

**Quando:Na interação com qualquer filtro.**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Consultas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'interacao:filtro:[[secao]]',
    'eventLabel': '[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[secao]]|'digite-o-nome-da-especialidade-que-deseja-realizar' , 'deseja-escolher-algum-medico?'.|Deve retornar com o nome da seção.|
|[[nome-filtro]]|'cirurgia-geral', 'dermatologia', 'rodrigo-oliveira', 'antonio-moriz' e etc.|Deve retornar com o nome da opção selecionada do filtro.|


<br />

**Quando: Ao interagir com o checkbox de termos de serviços.**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Consultas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'interacao:checkbox:termo-de-servico',
    'eventLabel': '[[acao]]:autorizo-o-uso-dos-meus-dados'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[acao]]| 'check', 'uncheck'.|Deve retornar a ação do usuário.|



<br />

**Quando:  No clique de qualquer elemento (botão ou link).**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Consultas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[botao-ou-link]]|  'botao' e 'link'.| Deve retornar com o tipo do elemento.|
|[[nome-elemento]]| 'selecionar', 'proximo-passo' e 'voltar'.|Deve retornar com o nome do botao ou link clicado.|


<br />

### Escolha o procedimento-Exames de diagnostico


**Quando:Na interação com qualquer checkbox.**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Exames de diagnostico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'interacao:checkbox:[[secao]]',
    'eventLabel': '[[acao]]:[[nome-check]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[secao]]|'qual-forma-de-realizacao-de-procedimento' e etc.|Deve retornar com o nome da seção.|
|[[acao]]|'marcou', 'desmarcou'.|  Deve retornar com o tipo de ação realizada.|
|[[nome-check]]|'convênio-bronze' , 'convênio-ouro' e etc.| Deve retornar com o nome do checkbox interagido.|

<br />

**Quando:Na interação com qualquer filtro.**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Exames de diagnostico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'interacao:filtro:[[secao]]',
    'eventLabel': '[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[secao]]|'escolha-o-procedimento-que-deseja-realizar-o-agendamento'.|Deve retornar com o nome da seção.|
|[[nome-filtro]]|'unidade-paulista','mirante' e etc.|Deve retornar com o nome da opção selecionada do filtro.|


<br />


**Quando:  No clique de qualquer elemento (botão ou link) .**<br />

- **Onde:**  Na página de "escolha o procedimentos" na aba de Exames de diagnostico.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:procedimento-[[nome-aba]]',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[botao-ou-link]]|  'botao' e 'link'.| Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'ultrassonografia-doppler-bp-paulista', 'ressonancia-magnetica-bp-paulista', 'selecionar', 'gerenciar-meus-convenios-e-plano' e etc.|Deve retornar com o nome do botao, box ou link clicado.|


<br />

### Setor de exames

**Quando: Na interação com qualquer filtro interno de cada box.**<br />

- **Onde:** Na aba de "exames de diagnostico" nos filtros interno dos boxes.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:setor-exames-[[nome-aba]]',
    'eventAction': 'interacao:filtro:[[secao]]',
    'eventLabel': '[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-aba]]|'consultas' ou 'exames-de-diagnostico'.| Deve retornar com o nome da aba que o usuario está interagindo.|
|[[secao]]|'escolha-o-procedimento-que-deseja-realizar-o-agendamento'.| Deve retornar com o nome da seção.|
|[[nome-filtro]]|'unidade-paulista', 'mirante' e etc.| Deve retornar com o nome da opção selecionada do filtro.|



<br />

### Meus convenios

**Quando: Na interação com algum campo de filtro do formulário.**<br />

- **Onde:** Na página/aba de "meus convênios".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-convenios',
    'eventAction': 'interacao:filtro:[[titulo-filtro]]',
    'eventLabel': 'preencheu:[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[titulo-filtro]]| 'qual-seu-convenio' e 'qual-seu-plano'.| Deve retornar com o titulo do filtro.|
|[[nome-elemento]]|'porto-seguro', 'gama-saude', 'fusex', 'bronze1', 'ouro' e etc .|Deve retornar com o nome do filtro selecionado.|


<br />

**Quando:  Na interação com campo do formulário .**<br />

- **Onde:** Na página/aba de "meus convênios".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-convenios',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]|'numero-carteirinha' e etc.| Deve retornar o nome do campo interagido.|

<br />

**Quando:No clique de qualquer botão ou link do formulário.**<br />

- **Onde:** Na página/aba de "meus convênios".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-convenios',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|  'botao' e 'link'.| Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'adicionar-convenio, 'cancelar' e 'fechar'.|Deve retornar com o nome do botao ou link clicado.|


<br />

**Quando:Na tentativa de callback para envio de formulario de convênio.**<br />

- **Onde:** Na página/aba de "meus convênios".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-convenios',
    'eventAction': 'callback:formulario-convenio',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]]| 'sucesso', 'erro:inesperado', 'erro:pagina-fora-do-ar' e etc.|Deve retornar a mensagem de sucesso ou o tipo de erro. |

<br />

### Data e horario

**Quando: Na interação com o campo de filtro do formulário.**<br />

- **Onde:** Na página de "Data e Horário".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:data-e-horario',
    'eventAction': 'interacao:filtro:[[titulo-filtro]]',
    'eventLabel': 'preencheu:[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[titulo-filtro]]| 'medico' e 'unidade'.| Deve retornar com o titulo do filtro.|
|[[nome-filtro]]| 'rodrigo-olivia', 'vincenzo-pugliese', 'unidade-bp-mirante','paulista'  e etc .| Deve retornar com o nome do filtro selecionado.|


<br />

**Quando: No clique de qualquer link de horário para consulta.**<br />

- **Onde:** Na página de "Data e Horário".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:data-e-horario',
    'eventAction': 'clique:link',
    'eventLabel': 'data:[[data]]--horario:[[nome-link]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[data]]| '22/07/21', '23/07/21' e etc.|Deve retornar com o nome da data selecionada.|
|[[nome-link]]|'8:00', '10:00', '11:00'  e etc.| Deve retornar com o nome do link clicado.|


<br />

**Quando:No clique de qualquer botão ou link do formulário.**<br />

- **Onde:** Na página de "Data e Horário".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:data-e-horario',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|'botao' ou 'link'.|Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'proximo-passo'e 'voltar'.| Deve retornar com o nome do botao ou link clicado.|


<br />

### Verifique os dados

**Quando:No clique de qualquer botão ou link.**<br />

- **Onde:** Na página de "verifique os dados".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:verifique-os-dados',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|'botao' ou 'link'.|Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'confirmacao-marcacao'e 'voltar'.| Deve retornar com o nome do botao ou link clicado.|


<br />

### marcacao confirmada

**Quando:No clique de qualquer botão ou link.**<br />

- **Onde:** Na página de "marcação confirmada".
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:marcacao-confirmada',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-elemento]]|'marcar-novo-procedimento', 'ir-para-area' e 'imprimir'.| Deve retornar com o nome do botao clicado.|


<br />

### minhas marcacoes

**Quando:No clique de qualquer botão ou link .**<br />

- **Onde:** Na página de "minhas marcações".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:minhas-marcacoes',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|'botao' ou 'link'.| Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'imprimir', 'excluir' e 'anterior' e etc.| Deve retornar com o nome do botao ou link clicado.|



<br />

### Painel

**Quando:No clique de qualquer botão.**<br />

- **Onde:** Na página do painel.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:painel',
    'eventAction': 'clique:botao-[[secao]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[secao]]| 'servicos', 'minha-area', 'outros'.|  Deve retornar com o nome da seção interagida.|
|[[nome-botao]]|'nova-marcacao', 'meus-convenios', 'duvidas-frequentes' e etc.|  Deve retornar com o nome do botao ou link clicado.|

<br />

### Meus dados

**Quando:Na interação com os campos.**<br />

- **Onde:** Na página de "meus dados".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-dados',
    'eventAction': 'interacao:formulario:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-campo]]| 'nome', 'email', 'altura', 'peso', 'telefone', 'senha', 'confirmar-senha' e etc.| Deve retornar o nome do campo preenchido. |


<br />

**Quando:No clique de qualquer botão ou link .**<br />

- **Onde:** Na página de "meus dados".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:meus-dados',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-elemento]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[botao-ou-link]]|'botao' ou 'link'.| Deve retornar com o tipo do elemento.|
|[[nome-elemento]]|'salvar' e 'cancelar' .| Deve retornar com o nome do botao ou link clicado.|



<br />

### Duvidas frequentes


**Quando:Na interação com as dúvidas.**<br />

- **Onde:** Na página de "dúvidas frequentes".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'bp-cm:duvidas-frequentes',
    'eventAction': 'interacao:duvidas',
    'eventLabel':'[[nome-pergunta]]:[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[nome-pergunta]]| 'ao-agendar-online-tenho-algum-custo?, 'tem-como-o-paciente-pagar-online?', 'eu-posso-agendar-do-meu-smart-phone?' e etc|Deve retornar o nome da pergunta.|
|[[acao]]| 'abriu' ou 'fechou' |Deve retornar a ação do usuário.|



<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
