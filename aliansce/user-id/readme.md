![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## User Id - Aliansce 
Última atualização: 09/03/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Processo User Id](#processo-user-id)

## Objetivo
Este documento tem como objetivo instruir a implementação do User Id no Projeto da Aliansce Sonae para todos os sites. Definimos o user ID como Cpf e Email hasheados.

## Processo User Id

Definimos como processo do User Id os seguintes passos abaixo;


1 - Coleta dos protodados via dataLayer (cpf/email) através das dimensões globais solicitadas no tagbook e documentação técnica de cada site. Essas dimensões são globais, 
ou seja, após o usuário se cadastrar ou logar deverá ser enviada via datalayer em todos os hits.<br />
2 - Envio desses dados ao Google Analytics como dimensões personalizadas.<br />
3 - Extração dos dados do Google Analytics pelo Datahub.<br />
4 - Armazenamento dos dados no Big Query.<br />
5 - Solicitação de lista de audiência.<br />
6 - Segmentação de base para identificar os IDs.<br />
7 - Cruzamento com a base já preparada no data lake com cpf/email hasheados.<br />
8 - Com a lista do data lake já montada, importamos para Facebook e Google Ads para geração de mídia.<br />



> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
