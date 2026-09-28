---
title: Como implementar provedores de dados para integrar dados de terceiros
description: Este tutorial fornece detalhes de implementação e exemplos de como usar o recurso Provedores de dados da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt:
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: 'https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%
---
# Implementar [!UICONTROL Provedores de dados] para integrar dados de terceiros ao Adobe Target

Detalhes de implementação e exemplos de como usar o recurso [!UICONTROL Provedores de dados] da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Target.

>[!NOTE]
>
>[!UICONTROL Provedores de Dados] requer `at.js` 1.3 ou superior

## Implementar os componentes básicos dos provedores de dados

>[!VIDEO](https://video.tv.adobe.com/v/33341/?captions=por_br&quality=12)

Uma visão geral rápida dos componentes básicos de um `dataProvider` e como colocar seu código na ordem correta.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrar a uma API de terceiros

>[!VIDEO](https://video.tv.adobe.com/v/33344?captions=por_br)

Um exemplo mais realista, integrar uma API meteorológica.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrar a vários provedores

>[!VIDEO](https://video.tv.adobe.com/v/36853?captions=por_br)

Como incorporar dados de vários provedores à sua solicitação global [!DNL Target].\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar impacto do carregamento de página

>[!VIDEO](https://video.tv.adobe.com/v/36855?captions=por_br)

Minimize o impacto no tempo de carregamento da página armazenando dados em um objeto de armazenamento de sessão. Como alternativa, você pode passar os valores como parâmetros de perfil usando o prefixo `profile.` e apenas passá-los na primeira solicitação [!DNL Target] da sessão. No entanto, você estaria limitado a transmitir cinquenta parâmetros de perfil por solicitação.

Um exemplo prático com o código usado no vídeo pode ser encontrado aqui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiais de suporte

* [Usar Provedores de Dados com o Adobe Target](use-data-providers-to-integrate-third-party-data.md)
