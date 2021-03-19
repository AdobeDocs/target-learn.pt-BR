---
title: Como usar tokens de resposta e eventos personalizados do at.js
description: Saiba como usar Tokens de resposta e Eventos personalizados da at.js para compartilhar informações de perfil do Target com sistemas de terceiros.
role: Desenvolvedor
level: Experienciado
topic: Personalização, arquitetura, desenvolvimento
feature: Implementação
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

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
* [Documentação do token de resposta](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentação De Evento Personalizado Da At.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Uso de provedores de dados do Adobe Target](use-data-providers-to-integrate-third-party-data.md)