---
title: Usar provedores de dados para integrar dados de terceiros ao Adobe Target
seo-title: Usar provedores de dados para integrar dados de terceiros ao Adobe Target
description: Os provedores de dados são uma função que permite passar dados de terceiros facilmente para o Target.  Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# Usar provedores de dados para integrar dados de terceiros ao Adobe Target

[!UICONTROL Os provedores de dados são uma função que permite passar dados de terceiros facilmente para o Target.]  Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Como usar provedores de dados

1. O especialista de implementação adiciona código antes do at.js (ou na seção Cabeçalho da biblioteca do at.js) que faz a chamada da API para terceiros, analisa a resposta e especifica com pares de nome/valor da resposta para enviar [!DNL Target].
1. O at.js gerencia a oscilação e inclui os pares de nome/valor como parâmetros personalizados na solicitação de Público alvo global.
1. O Marketer cria audiências na [!DNL Target] interface com base nesses parâmetros personalizados.
1. O profissional de marketing usa essas audiências para público alvo de experiências, atividades e métricas, bem como para audiências de relatórios.

>[!NOTE]
>
>[!UICONTROL Os provedores] de dados exigem o at.js 1.3 ou superior

## Materiais de suporte

* [Implementação de provedores de dados em at.js e Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentação dos provedores de dados](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)