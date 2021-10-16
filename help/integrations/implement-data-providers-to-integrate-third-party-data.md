---
title: Como implementar provedores de dados para integrar dados de terceiros
description: Este tutorial fornece detalhes de implementação e exemplos de como usar o recurso Provedores de dados da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Implemente [!UICONTROL Data Providers] para integrar dados de terceiros ao Adobe Target

Detalhes de implementação e exemplos de como usar o recurso [!UICONTROL Provedores de dados] da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Target.

>[!NOTE]
>
>[!UICONTROL Os ] provedores de dados exigem o  `at.js` 1.3 ou superior

## Implementar os componentes básicos dos provedores de dados

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Uma visão geral rápida dos componentes básicos de um `dataProvider` e como colocar o código na ordem correta.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integração com uma API de terceiros

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Um exemplo mais realista, integrando uma API meteorológica.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integração com vários provedores

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Como incorporar dados de vários provedores em sua solicitação global [!DNL Target].\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar o impacto no carregamento da página

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimize o impacto no tempo de carregamento da página armazenando dados em um objeto de armazenamento de sessão. Como alternativa, você pode passar os valores como parâmetros de perfil usando o prefixo `profile.` e passá-los na primeira solicitação [!DNL Target] da sessão. No entanto, você estaria limitado a transmitir cinquenta parâmetros de perfil por solicitação.

Um exemplo prático com o código usado no vídeo pode ser encontrado aqui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiais de suporte

* [Usar provedores de dados com o Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentação dos provedores de dados](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
