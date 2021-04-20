---
title: Como usar provedores de dados para integrar dados de terceiros
description: Este tutorial apresenta usuários a provedores de dados. Saiba como usar o recurso Provedores de dados para transmitir dados facilmente de terceiros para a Adobe Target.
role: Business Practitioner, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 22%

---


# Usar provedores de dados para integrar dados de terceiros ao Adobe Target

[!UICONTROL Os provedores de dados são uma função que permite passar dados de terceiros facilmente para o Target.]  Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Como usar provedores de dados

1. O especialista em implementação adiciona código antes da at.js (ou na seção Cabeçalho da biblioteca da at.js) que faz a chamada da API para terceiros, analisa a resposta e especifica com pares de nome/valor da resposta para enviar para [!DNL Target].
1. A at.js gerencia a cintilação e inclui os pares de nome/valor como parâmetros personalizados na solicitação global do Target.
1. O profissional de marketing cria públicos na interface [!DNL Target] com base nesses parâmetros personalizados.
1. O profissional de marketing usa esses públicos para direcionar experiências, atividades e métricas, bem como para relatórios de públicos.

>[!NOTE]
>
>[!UICONTROL Os ] provedores de dados exigem a at.js 1.3 ou superior

## Materiais de suporte

* [Implementar provedores de dados na at.js e no Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentação dos provedores de dados](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)