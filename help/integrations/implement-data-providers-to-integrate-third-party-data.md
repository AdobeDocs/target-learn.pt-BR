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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Implementar [!UICONTROL Provedores de dados] para integrar dados de terceiros ao Adobe Target

Detalhes de implementação e exemplos de como usar o Adobe Target [!UICONTROL Provedores de dados] recurso para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Target.

>[!NOTE]
>
>[!UICONTROL Provedores de dados] exige `at.js` 1.3 ou superior

## Implementar os componentes básicos dos provedores de dados

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Uma visão geral rápida dos componentes básicos de um `dataProvider` e como colocar seu código na ordem correta.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrar a uma API de terceiros

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Um exemplo mais realista, integrar uma API meteorológica.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrar a vários provedores

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Como incorporar dados de vários provedores no seu modelo global [!DNL Target] solicitação.\
Um exemplo prático com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar impacto do carregamento de página

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimize o impacto no tempo de carregamento da página armazenando dados em um objeto de armazenamento de sessão. Como alternativa, você pode transmitir os valores como parâmetros de perfil usando o `profile.` prefixo e apenas transmita-os no primeiro [!DNL Target] solicitação da sessão. No entanto, você estaria limitado a transmitir cinquenta parâmetros de perfil por solicitação.

Um exemplo prático com o código usado no vídeo pode ser encontrado aqui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiais de suporte

* [Usar provedores de dados com o Adobe Target](use-data-providers-to-integrate-third-party-data.md)
