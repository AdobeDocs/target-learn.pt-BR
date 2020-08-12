---
title: Visão geral da API do Adobe Recommendations
keywords: recommendations;adobe recommendations;premium;api;apis
description: A Adobe Target Recommendations inclui um conjunto dedicado de APIs que permitem gerenciar seu catálogo de produtos e/ou conteúdo recomendáveis; gerenciar seus algoritmos e campanhas de recomendações; e fornecer recomendações em objetos JSON, HTML ou XML a serem exibidos em Web, dispositivos móveis, email, IOT e outros canais.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---


# Visão geral da API do Adobe Recommendations

As APIs relevantes para [!DNL Recommendations] incluem APIs [de](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) administração que permitem:

* Gerenciar seu catálogo de produtos ou conteúdo recomendáveis
* Gerencie seus [!DNL Recommendations] algoritmos e atividades

Usando a API [!DNL Target] do [](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) delivery com a Recommendations, você também pode:

* Recupere as recomendações em objetos JSON, HTML ou XML para que possam ser exibidas na Web, em dispositivos móveis, no email, na Internet das coisas (IOT) e em outros canais.

## Descrição do tutorial

Este tutorial orienta os desenvolvedores pela prática prática prática prática usando as [!DNL Recommendations] APIs para configurar e gerenciar [!DNL Recommendations] catálogos e critérios personalizados, além de usar a API de delivery para recuperar o conteúdo das recomendações. No final deste tutorial, você poderá:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Saiba como usar o Recommendations com a API do Delivery para usar resultados de recomendações em dispositivos não HTML

## Público-alvo

Este tutorial é destinado a desenvolvedores novos em APIs de Público alvo ou APIs de Recommendations.

## Pré-requisitos

O uso das APIs de administração de Público alvo exige a configuração [de autenticação de](../apis/configure-io-target-integration.md)Adobe. Certifique-se de que isso esteja configurado antes de iniciar este tutorial.

## Recursos

Observe os seguintes recursos, necessários para entender este tutorial e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o aplicativo [Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação de contas. Embora não seja necessário para usar as APIs da Adobe Target em geral, o Postman facilita os workflows de API e a Adobe Target fornece várias coleções Postman para ajudar a executar suas APIs e aprender como elas operam. O resto deste tutorial assume conhecimento prático do Postman. Para obter assistência, consulte a documentação [do](https://learning.getpostman.com/)Postman. |
| Referências | A familiaridade com os seguintes recursos é assumida durante todo o restante deste tutorial:<UL><li>[Github de E/S Adobe](https://github.com/adobeio)</li><li>[Documentação de E/S do Adobe do Público alvo](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentação da API do Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Próximo &quot;Gerenciar seu catálogo Recommendations&quot; >](manage-catalog.md)