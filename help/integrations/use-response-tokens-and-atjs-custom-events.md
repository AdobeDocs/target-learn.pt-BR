---
title: Usar tokens de resposta e Eventos personalizados at.js com Adobe Target
seo-title: Usar tokens de resposta e Eventos personalizados at.js com Adobe Target
description: Tokens de resposta e Eventos personalizados at.js permitem que você compartilhe informações de perfil de Públicos alvos para sistemas de terceiros. Qualquer objeto no perfil do visitante do Público alvo, incluindo atributos personalizados do perfil, informações geográficas, detalhes da atividade e perfis incorporados, pode ser adicionado à resposta do Público alvo, onde você pode usar o JavaScript personalizado para integração com terceiros.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Usar tokens de resposta e Eventos personalizados at.js com Adobe Target

Tokens de resposta e Eventos `at.js` personalizados permitem que você compartilhe informações do perfil de [!DNL Target] para sistemas de terceiros. Qualquer objeto no perfil do [!DNL Target] visitante, incluindo atributos personalizados do perfil, informações geográficas, detalhes da atividade e perfis incorporados, pode ser adicionado à [!DNL Target] resposta onde você pode usar o JavaScript personalizado para integração com terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Como usar os Tokens de resposta e os Eventos personalizados do at.js

1. Determine de quais dados você precisa [!DNL Target]
1. Ative os Tokens de Resposta para os dados de que necessita ao virar a alternância na tela Configurar->Tokens de Resposta
1. Determine que ouvinte de evento você precisa usar
1. Escreva o JavaScript necessário para acompanhar o evento Adobe Target, ler os tokens de resposta e fazer o que você precisa para sua integração
1. Implante o JavaScript do ouvinte de eventos usando uma ação de código personalizada em Iniciar após a ação &quot;Carregar Público alvo&quot; ou adicione-o à seção Rodapé da biblioteca do at.js na tela Configuração->Implementação e salve um novo arquivo do at.js
1. Faça o controle de qualidade e publique sua integração

## Recursos adicionais

* [Use o Experience Cloud Debugger com o Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentação do token de resposta](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentação personalizada do Evento At.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Uso de provedores de dados do Adobe Target](use-data-providers-to-integrate-third-party-data.md)