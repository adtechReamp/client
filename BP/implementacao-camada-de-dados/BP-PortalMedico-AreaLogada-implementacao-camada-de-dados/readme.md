![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BP - Portal Médico - Area Logada
Última atualização: 02/09/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Geral](#geral)
- [Login](#login)
- [Cadastro](#cadastro)
- [Home](#home)
- [Perfil](#perfil)
- [ServiceDesk](#servicedesk)
- [Contato](#contato)
- [Cadastro Médico](#cadastro-médico)
- [Resultado de Exames](#resultado-de-exames)
- [Plataformas para o médico](#plataformas-para-o-médico)
- [Conveniências](#conveniências)
- [Agendamento de cirurgias](#agendamento-de-cirurgias)
- [Como agendar uma cirurgia](#como-agendar-uma-cirurgia)
- [Agendamento cirúrgico online](#agendamento-cirúrgico-online)
- [Status autorizações](#status-autorizações)
- [Admissões de pacientes](#admissões-de-pacientes)
- [Transferência de pacientes](#transferência-de-pacientes)
- [Programa de relacionamento médico](#programa-de-relacionamento-médico)
- [Educação](#educação)
- [Cursos de residência fellowship e especialização](#cursos-de-residência-fellowship-e-especialização)
- [Cursos de pós-graduação](#cursos-de-pós-graduação)
- [Escola de enfermagem São Joaquim](#escola-de-enfermagem-são-joaquim)
- [Cursos de BLS e ACLS](#cursos-de-bls-e-acls)
- [Envio de certificados](#envio-de-certificados)
- [Eventos científicos presenciais e virtuais](#eventos-científicos-presenciais-e-virtuais)
- [Teleducação EAD Programa de desenvolvimento médico](#teleducacao-ead-programa-de-desenvolvimento-médico)
- [Pesquisa](#pesquisa)
- [Ferramentas de pesquisa](#ferramentas-de-pesquisa)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://bp.homolog.enken.cloud/estatico/paginas/home/home.html](https)

<br />

<h3> INSTALAÇÃO DO GOOGLE TAG MANAGER</H3>

### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie e cole o seguinte código abaixo o mais alto possível na tag '<head>' da página:.

```html

<html>
  <head>
  <!-- Google Tag Manager -->
      <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
      new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
      j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
      'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
      })(window,document,'script','dataLayer','GTM-5K7SXZR');</script>
  <!-- End Google Tag Manager -->

  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação '<body>' de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
    <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-5K7SXZR"
    height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Caso o site já possua o Google Analytics instalado, será necessário a remoção do código de **todas as páginas do site**: <br />

```html

<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXXXXX-X', 'auto');
ga('send', 'pageview');
</script>

```

---

```html

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-XXXXXXX-X"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-XXXXXXX-X');
</script>
```

---

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

### Geral

**Quando: No clique dos itens do header.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:geral",
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'busca'e 'notificacoes' |  Deve retornar o nome do item clicado.   |


<br />

**Quando: Ao interagir com o campo de busca.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:geral",
    'eventAction': 'campo:busca,
    'eventLabel': '[[termo-buscado]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-buscado]] | 'guia', 'protocolo' e etc | Deve retornar o termo buscado no campo de busca.   |

<br />

**Quando: No clique dos itens do menu lateral**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[nome-menu]]:[[submenu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-menu]] | 'cadastro', 'ferramentas', 'desenvolvimento-profissional' e etc | Deve retornar o nome do menu clicado.   |
| [[sub-menu]] | 'cadastro-medico', 'resultado-de-exames', 'conveniencias:bp-mirante', 'educacao:envio-de-certificados' e etc | Deve retornar o nome do sub-menu clicado.   |

<br />

**Quando: Na interação com os vídeos.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:geral",
    'eventAction': 'campo:busca,
    'eventLabel': '[[termo-buscado]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-buscado]] | 'guia', 'protocolo' e etc | Deve retornar o termo buscado no campo de busca.   |

<br />

---
### Login

**Quando: Na interação com os campos.**<br />

- **Onde:**  Na página de login
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:login',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'crm' e 'senha' | Deve retornar o nome do campo preenchido.   |

<br />

**Quando: Ao clicar em "esqueceu sua senha?"**<br />

- **Onde:**  Na página de login
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:login',
    'eventAction': 'clique:link',
    'eventLabel': 'esqueceu-sua-senha'
  });
</script>

```
**Quando: Ao clicar em "crie uma conta"**<br />

- **Onde:**  Na página de login
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:login',
    'eventAction': 'clique:link',
    'eventLabel': 'crie-uma-conta'
  });
</script>
```

**Quando: Na tentativa de callback para efetuar o login.**<br />

- **Onde:**  Na página de login
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:login',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[user-id]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso' e 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc. | Deve retornar a mensagem de sucesso ou o tipo de erro.   |
| [[user-id]] | 'xxxxxxxx' e 'zzzzzzzzzzz' | Deve retornar o userID.   |

<br />
---

### Cadastro
**Quando: Na interação com os campos.**<br />

- **Onde:**  Na página de cadastro
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:cadastro,
    'eventAction': 'interacao:step:[[nome-step]]:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-step]] | 'insira-seus-dados', 'defina-sua-senha' e etc. | Deve retornar o nome do step.   |
| [[nome-campo]] | 'crm', 'cpf', 'email', 'telefone' e etc. | Deve retornar o nome do campo preenchido.   |

<br />

**Quando: Na interação com checkbox de politica de privacidade.**<br />

- **Onde:**  Na página de cadastro
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-medico:cadastro,
    'eventAction': 'interacao:step:politica-de-privacidade-checkbox',
    'eventLabel': 'marcou:[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] | 'aceito' e 'nao-aceito' | Deve retornar o tipo de ação realizada.   |


<br />

**Quando: Na tentativa de callback para efetuar o cadastro.**<br />

- **Onde:**  Na página de cadastro
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'portal-medico:cadastro,
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc. | Deve retornar a mensagem de sucesso ou o tipo de erro.   |

<br />

### Home
**Quando: Ao clicar em algum banner.**<br />

- **Onde:**  Na home
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:home',
    'eventAction': 'clique:banner',
    'eventLabel': '[[nome-banner]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-banner]] | 'centro-oncologico:nucleo-de-excelencia-em-cancer-de-mama-e-ginecologico' e etc | Deve retornar o nome do banner clicado.   |

<br />

**Quando: Ao clicar nos botões na seção "resultados de exames.**<br />

- **Onde:**  Na home
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:home',
    'eventAction': 'clique:botao',
    'eventLabel': 'resultados-de-exames:[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'resultado-laboratorios' e 'outros-resultados' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'ver-exames' | Deve retornar o nome do botão clicado.   |

**Quando: Ao clicar nos botões na seção "plataformas para o medico.**<br />

- **Onde:**  Na home
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:home',
    'eventAction': 'clique:botao',
    'eventLabel': 'plataforma-para-medicos:[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'tasy' e 'indicador-de-performance' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-tasy' e 'abrir-2im' | Deve retornar o nome do botão clicado.   |

<br />

### Perfil

<br />

### ServiceDesk
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página ServiceDesk
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:service-desk',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'problemas-relacionados-a-manutencao' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-tesy', 'codigo:827' e 'codigo:10881' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao clicar nos telefones.**<br />

- **Onde:**  Na Página ServiceDesk
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:service-desk',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-guia]]:[[telefone]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'falha-de-conexao-e-problemas-de-acesso-as-ferramentas' | Deve retornar o nome da guia clicada.   |
| [[telefone]] | '1135051085' | Deve retornar o telefone.   |

<br />

### SAC

### Contato
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Contato
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:contato',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'gerentes-medicos-das-unidades-bp', 'guia-de-contatos' e 'encontre-um-medico' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-planilha', 'abrir-pdf' e 'saiba-mais' | Deve retornar o nome do botão clicado.   |

<br />

### Cadastro Médico
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Cadastro Médico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cadastro-medico',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'guia-de-acessos', 'guia-de-contatos', 'guia-bp-para-medicos' e 'codigo-de-conduta' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-pdf' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao clicar nos links da página.**<br />

- **Onde:**  Na Página Cadastro Médico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cadastro-medico',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-link]] | 'formulario-de-recredenciamento', 'email' e 'telefone' | Deve retornar o nome do link clicado.   |

<br />

**Quando: Ao preencher um dos campos do formulário de recredenciamento.**<br />

- **Onde:**  Na Página Cadastro Médico > Ficha de recredenciamento
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cadastro-medico:recredenciamento',
    'eventAction': 'preencheu-campo',
    'eventLabel': '[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome', 'unidade-bp-paulista', 'unidade-bp-mirante' e etc. | Deve retornar o nome do campo/checkbox preenchido.   |

<br />

### Resultado de Exames
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Resultado de Exames
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:resultado-exames',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'resultados-laboratorio' e 'outros-resultados' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'ver-exames' | Deve retornar o nome do botão clicado.   |

<br />

### Plataformas para o Médico
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Plataformas para o Médico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:plataforma-para-os-medicos',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'tasy', 'atividades-do-medico', 'honorarios-medicos', ''teleducacao-ead e etc | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-tasy', 'abrir-ferramenta', 'abrir-2im' e 'acessar-ferramenta' | Deve retornar o nome do botão clicado.   |

<br />

### Conveniências
**Quando: Ao clicar nos links.**<br />

- **Onde:**  Na Página Conveniências
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:conveniencias',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-link]] | 'hospital-bp-unidade-paulista' e  'bp-mirante' | Deve retornar o nome do link clicado.   |

<br />

**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Conveniências
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:conveniencias',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'guia-de-facilidades-e-parcerias', 'solicitacao-de-jaleco', 'solicitacao-de-segunda-via-de-cracha' e etc. | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'ver-guia' e 'abrir-formulario' | Deve retornar o nome do botão clicado.   |

<br />

### Agendamento de Cirurgias
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Agendamento de Cirurgias
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:agendamento-de-cirurgias',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'agendar-cirurgia-canal-medico', 'admissoes-de-pacientes', 'agendar-cirurgia-online', 'saber-mais' e etc. | Deve retornar o nome do botão clicado.   |

<br />

### Como agendar uma cirurgia
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Como agendar uma cirurgia
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:como-agendar-uma-cirurgia',
    'eventAction': 'clique:botao',
    'eventLabel': 'clique-para-ver-os-documentos'
  });
</script>
```
<br />

### Agendamento cirúrgico online
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Agendamento cirúrgico online
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:como-agendamento-cirurgico-online',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'entenda-como-funciona', 'plataforma-de-agendamento-cirurgico-online' e 'documentos-necessarios-para-agendamento-cirurgico' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'assistir-ao-video', 'acessar-ferramenta' e 'clique-para-ver-os-documentos' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao clicar no link da janela "Documentos necessarios para agendamento cirurgico".**<br />

- **Onde:**  Na Pagina Agendamento cirurgico online > clique para agendamento cirurgico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:como-agendamento-cirurgico-online',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-guia]]:[[nome-link]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'termo-de-consentimento-livre-e-esclarecidos-tcle' | Deve retornar o nome da guia clicada.   |
| [[nome-link]] | 'abrir-termo-de-consentimento' | Deve retornar o nome do botão clicado.   |

<br />

### Status Autorizações
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Status Autorizações
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:status-autorizacoes',
    'eventAction': 'clique:botao',
    'eventLabel': 'plataforma-de-agendamento-cirurgico-online'
  });
</script>

```

<br />

### Admissões de pacientes
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Admissões de pacientes
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:admissao-pacientes',
    'eventAction': 'clique:botao',
    'eventLabel': 'baixar-documentos-necessarios'
  });
</script>

```

<br />

### Transferência de pacientes 
**Quando: Ao clicar nos telefones da pagina.**<br />

- **Onde:**  Na Página Transferência de pacientes.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:transferencia-de-pacientes',
    'eventAction': 'clique:link',
    'eventLabel': '[[numero-telefone]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[numero-telefone]] | '1135053049', '1135053047' e '1135053048' 'plataforma-de-agendamento-cirurgico-online' e 'documentos-necessarios-para-agendamento-cirurgico' | Deve retornar o número de telefone clicado.   |

<br />

### Programa de relacionamento médico
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Programa de relacionamento médico
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:relacionamento-medico',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'indicadores-de-performance' e 'beneficios-do-programa-de-relacionamento-medico' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-2im', 'abrir-pdf' e 'resgate-seus-beneficios' | Deve retornar o nome do botão clicado.   |

<br />

### Educação
**Quando: Ao clicar nos links da pagina.**<br />

- **Onde:**  Na Página Educação
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:educacao',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-link]] | 'cursos-de-residencia-fellowship-e-especializacao', 'cursos-de-bls-e-acls', 'cursos-de-pos-graduacao' e etc | Deve retornar o nome do link clicado.   |


<br />

### Cursos de residência, fellowship e especialização
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Cursos de residência, fellowship e especialização
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cursos-de-residencia-fellowship-e-especializacao',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'acesse-todos-os-cursos-disponiveis', 'guias-informativos-da-bp' e 'coreme' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'clique-e-saiba-mais' e 'abrir-pdf' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao clicar nos telefones da pagina.**<br />

- **Onde:**  Na Página Cursos de residência, fellowship e especialização
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cursos-de-residencia-fellowship-e-especializacao',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-guia]]:[[telefone]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'acesse-todos-os-cursos-disponiveis', 'guias-informativos-da-bp' e 'coreme' | Deve retornar o nome da guia clicada.   |
| [[telefone]] | '1135055265' e '1135055266' | Deve retornar o número de telefone clicado.   |

<br />

### Cursos de pós-graduação
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Cursos de pós-graduação
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cursos-de-pos-graduacao',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'conheca-nossos-cursos-de-pos-graduacao' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'faca-sua-inscricao' | Deve retornar o nome do botão clicado.   |

<br />

### Escola de enfermagem São Joaquim
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Escola de enfermagem São Joaquim
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:escola-de-enfermagem-sao-joaquim',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'conheca-a-escola-de-enfermagem-sao-joaquim-e-acompanhe-a-abertura-de-inscricoes' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'saber-mais' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao clicar no telefone da página.**<br />

- **Onde:**  Na Página Escola de enfermagem São Joaquim
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:escola-de-enfermagem-sao-joaquim',
    'eventAction': 'clique:link`,
    'eventLabel': '[[nome-guia]]:[[telefone]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'contato' | Deve retornar o nome da guia clicada.   |
| [[telefone]] | '1135055265' | Deve retornar o telefone clicado.   |

<br />

### Cursos de BLS e ACLS
**Quando: Ao clicar no telefone da página.**<br />

- **Onde:**  Na Página Cursos de BLS e ACLS
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:cursos-de-bls-e-acls',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-guia]]:[[telefone]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'cursos-em-parceria' | Deve retornar o nome da guia clicada.   |
| [[telefone]] | '1135052015' | Deve retornar o telefone clicado.   |

<br />

### Envio de certificados
**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Envio de certificados
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:envio-de-certificados',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'formulario-de-envio-de-certificados' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'abrir-formulario' | Deve retornar o nome do botão clicado.   |

<br />

**Quando: Ao preencher um dos campos do formulário.**<br />

- **Onde:**  Na Página Envio de certificados
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:envio-de-certificados',
    'eventAction': 'preencheu-campo',
    'eventLabel': '[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome', 'uf', 'crm', 'telefone' e etc. | Deve retornar o nome do campo preenchido.   |

<br />

**Quando: Ao preencher o checkbox do formulário.**<br />

- **Onde:**  Na Página Envio de certificados
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:envio-de-certificados',
    'eventAction': 'checkbox:[[check/uncheck]]',
    'eventLabel': '[[nome-checkbox]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[check/uncheck]] | 'check' ou 'uncheck' | Deve retornar se o checkbox foi preenchido (check) ou não preenchido (uncheck).   |
| [[nome-checkbox]] | 'li-e-aceito-os-termos-de-uso-e-politicas-de-privacidade' | Deve retornar o texto do checkbox.   |

<br />

**Quando: No callback do envio do formulário.**<br />

- **Onde:**  Na Página Envio de certificados
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:envio-de-certificados',
    'eventAction': 'callback:[[status]]',
    'eventLabel': '[[descricao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'concluido' ou 'erro' | Deve retornar se o formulário foi enviado com sucesso ou se houve falhas.   |
| [[descricao]] | 'formulario-enviado-com-sucesso', 'campo-crm-nao-preenchido', 'campo-nome-nao-preenchido' e etc. | Deve retornar se foi enviado com sucesso ou qual erro houve.   |

<br />

### Eventos científicos presenciais e virtuais
**Quando: Ao clicar no botão da página.**<br />

- **Onde:**  Na Página Eventos científicos presenciais e virtuais
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:eventos-cientificos-presenciais-e-online',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-guia]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-guia]] | 'eventos-cientificos' | Deve retornar o nome da guia clicada.   |
| [[nome-botao]] | 'saber-mais' | Deve retornar o nome do botão clicado.   |

<br />

### Teleducacao EAD Programa de desenvolvimento médico

<br />

### Pesquisa
**Quando: Ao clicar nos boxes de pesquisa.**<br />

- **Onde:**  Na Página Pesquisa
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:pesquisa',
    'eventAction': 'clique:box',
    'eventLabel': '[[nome-box]]:[[nome-secao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-box]] | 'naipe', 'ferramenta-de-pesquisa', 'projetos-de-inovacao', 'biblioteca' e etc | Deve retornar o nome do box clicado.   |
| [[nome-secao]] | 'pesquisa' | Deve retornar o nome da seção interagida.   |

<br />

**Quando: Ao clicar nos botões.**<br />

- **Onde:**  Na Página Pesquisa
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:pesquisa',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[nome-secao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-secao]] | 'coordenacao-geral-de-educacao-e-pesquisa' e etc. | Deve retornar o nome da seção interagida.   |
| [[nome-botao]] | 'saiba-mais' e etc | Deve retornar o nome do botão clicado.   |

<br />

### Ferramentas de pesquisa
**Quando: Ao clicar no botão ou link dentro das abas.**<br />

- **Onde:**  Na Página Ferramentas de pesquisa
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'area-logada:ferramentas-de-pesquisa',
    'eventAction': 'clique:botao:aba-[[nome-aba]]',
    'eventLabel': '[[nome-item]]:[[nome-secao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-aba]] | 'up-to-date', 'ovid', 'lexicomp' e etc. | Deve retornar o nome da aba que o usuário está.   |
| [[nome-item]] | 'abrir-red-cap', 'abrir-ovid', 'abrir-up-to-date', 'fazer-cadastro' e etc | Deve retornar o nome do botão clicado.   |
| [[nome-secao]] | 'conheca-a-plataforma-up-to-date', 'conheca-a-plataforma-ovid', 'red-cap', 'primeiro-acesso' e etc. | Deve retornar o nome da seção interagida.   |


<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
