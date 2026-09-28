---
title: O que é a API do Adobe Recommendations?
description: Este tutorial orienta os desenvolvedores na prática usando as APIs do Adobe Target Recommendations para configurar e gerenciar catálogos e critérios personalizados do Recommendations, além de usar a API de entrega para recuperar o conteúdo das recomendações.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
TQID: 'https://experienceleague.adobe.com/NQpsNnhLA0MRP-pJQLS35ymJ2lnulZebvI-Yv4-xSxw'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 6%
---
# Visão geral da API do Adobe Recommendations

As APIs relevantes para [!DNL Recommendations] incluem [APIs de administrador](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=pt-BR) que permitem:

* Gerencie seu catálogo de produtos ou conteúdo recomendáveis
* Gerencie seus algoritmos e atividades do [!DNL Recommendations]

Usando a [!DNL Target] [API de entrega](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=pt-BR) com o Recommendations, você também pode:

* Recupere recomendações em objetos JSON, HTML ou XML para que elas possam ser exibidas na Web, em dispositivos móveis, em emails, na Internet das Coisas (IOT) e em outros canais.

## Descrição do tutorial

Este tutorial orienta os desenvolvedores pela prática do uso das APIs do [!DNL Recommendations] para configurar e gerenciar catálogos e critérios personalizados do [!DNL Recommendations], além de usar a API de entrega para recuperar o conteúdo das recomendações. Ao final deste tutorial, você será capaz de:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Entenda como usar o Recommendations com a API de entrega para usar os resultados das recomendações em dispositivos que não sejam HTML

## Público-alvo

Este tutorial destina-se a desenvolvedores novos nas APIs do Target ou nas APIs do Recommendations.

## Pré-requisitos

O uso das APIs de administrador do Target requer a [configuração de autenticação do Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=pt-BR){target="_blank"}. Verifique se você configurou este tutorial antes de iniciá-lo.

## Recursos

Observe os seguintes recursos, que são necessários para entender este tutorial e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação da conta. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API, e a Adobe Target fornece várias coleções do Postman para ajudar a executar suas APIs e saber como elas operam. O restante deste tutorial pressupõe conhecimento prático do Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | A familiaridade com os seguintes recursos é assumida durante o restante deste tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação do Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentação da API do Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Próximo &quot;Gerenciar o catálogo de recomendações&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html?lang=pt-BR){target="_blank"}
