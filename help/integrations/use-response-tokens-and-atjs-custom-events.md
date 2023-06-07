---
title: Como usar tokens de resposta e eventos personalizados do at.js
description: Saiba como usar Tokens de resposta e Eventos personalizados do at.js para compartilhar informações de perfil do Target com sistemas de terceiros.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%

---

# Usar Tokens de resposta e Eventos personalizados do at.js com o Adobe Target

Tokens de resposta e `at.js` Os Eventos personalizados permitem compartilhar informações de perfil do [!DNL Target] a sistemas de terceiros. Qualquer objeto na variável [!DNL Target] perfil do visitante, incluindo atributos de perfil personalizados, informações geográficas, detalhes da atividade e perfis incorporados, que podem ser adicionados ao [!DNL Target] onde é possível usar o JavaScript personalizado para integrar com um provedor de terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Como usar Tokens de resposta e Eventos personalizados do at.js

1. Determine de quais dados você precisa [!DNL Target]
1. Ative os Tokens de resposta para os dados necessários, invertendo o botão de alternância na tela Configurar->Tokens de resposta
1. Determine qual ouvinte de eventos você precisa usar
1. Escreva o JavaScript necessário para ouvir o evento do Adobe Target, leia os tokens de resposta e faça o que for necessário para a integração
1. Implante o JavaScript do ouvinte de eventos usando uma ação de código personalizado no Launch após a ação &quot;Carregar o Target&quot; ou adicione-o à seção Rodapé da biblioteca da at.js na tela Configuração ->Implementação e salve um novo arquivo da at.js
1. Controle de qualidade e publique sua integração

## Recursos adicionais

* [Use o Experience Cloud Debugger com o Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentação do token de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Uso de provedores de dados do Adobe Target](use-data-providers-to-integrate-third-party-data.md)
