---
title: O que é a API do Adobe Recommendations?
description: Este tutorial orienta os desenvolvedores por práticas práticas práticas práticas usando as APIs do Adobe Target Recommendations para configurar e gerenciar catálogos Recommendations e critérios personalizados, bem como usar a API de entrega para recuperar conteúdo de recomendações.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---

# Visão geral da API do Adobe Recommendations

As APIs relevantes para [!DNL Recommendations] incluem [APIs de administrador](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) que permitem:

* Gerenciar o catálogo de produtos ou conteúdo recomendáveis
* Gerencie seus algoritmos e atividades do [!DNL Recommendations]

Usando a [!DNL Target] [API de entrega](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) com o Recommendations, também é possível:

* Recupere as recomendações em objetos JSON, HTML ou XML para que possam ser exibidas na Web, em dispositivos móveis, em email, na Internet das coisas (IOT) e em outros canais.

## Descrição do tutorial

Este tutorial orienta os desenvolvedores pela prática prática prática prática prática prática usando as [!DNL Recommendations] APIs para configurar e gerenciar [!DNL Recommendations] catálogos e critérios personalizados, bem como usando a API de entrega para recuperar conteúdo de recomendações. Ao final deste tutorial, você poderá:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Entenda como usar o Recommendations com a API de entrega para usar resultados de recomendações em dispositivos não HTML

## Público-alvo

Este tutorial é destinado a desenvolvedores novos em APIs do Target ou APIs do Recommendations.

## Pré-requisitos

O uso das APIs de administrador do Target requer [configuração de autenticação do Adobe](../apis/configure-io-target-integration.md). Certifique-se de ter isso configurado antes de iniciar este tutorial.

## Recursos

Observe os seguintes recursos, que são necessários para entender este tutorial e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação de contas. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API e o Adobe Target fornece várias coleções de Postman para ajudar a executar suas APIs e aprender como elas operam. O resto deste tutorial assume conhecimento prático de Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | A familiarização com os seguintes recursos é assumida no restante deste tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação do Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentação da API do Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Próximo: &quot;Gerenciar seu catálogo do Recommendations&quot; >](manage-catalog.md)
