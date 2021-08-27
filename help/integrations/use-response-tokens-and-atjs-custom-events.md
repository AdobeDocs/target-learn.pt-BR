---
title: Como usar tokens de resposta e eventos personalizados do at.js
description: Saiba como usar Tokens de resposta e Eventos personalizados da at.js para compartilhar informações de perfil do Target com sistemas de terceiros.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---

# Usar tokens de resposta e eventos personalizados do at.js com o Adobe Target

Tokens de resposta e `at.js` Eventos personalizados permitem compartilhar informações de perfil de [!DNL Target] em sistemas de terceiros. Qualquer objeto no perfil do visitante [!DNL Target], incluindo atributos de perfil personalizados, informações geográficas, detalhes da atividade e perfis incorporados, pode ser adicionado à resposta [!DNL Target], onde é possível usar JavaScript personalizado para integração com terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Como usar Tokens de resposta e Eventos personalizados do at.js

1. Determine quais dados são necessários de [!DNL Target]
1. Ative os Tokens de Resposta para os dados de que necessita, virando o botão na tela Configurar->Tokens de Resposta
1. Determine qual ouvinte de evento você precisa usar
1. Escreva o JavaScript necessário para ouvir o evento do Adobe Target, ler os tokens de resposta e fazer o que é necessário para a integração
1. Implante o JavaScript do ouvinte de eventos usando uma ação de código personalizado no Launch após a ação &quot;Carregar Target&quot; ou adicione-o à seção Rodapé da biblioteca da at.js na tela Configuração->Implementação e salve um novo arquivo da at.js
1. Faça o controle de qualidade e publique sua integração

## Recursos adicionais

* [Usar o Experience Cloud Debugger com Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentação do token de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Documentação de evento personalizado da at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/atjs-custom-events.html?lang=en)
* [Uso de provedores de dados do Adobe Target](use-data-providers-to-integrate-third-party-data.md)
