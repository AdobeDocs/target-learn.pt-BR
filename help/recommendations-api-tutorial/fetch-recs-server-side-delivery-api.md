---
title: Buscando o Recommendations com a API do Delivery
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
source-git-commit: 18a9b664fe935fd5c52682b2bd798cafd75b6591
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# Busca [!DNL Recommendations] com a API do Delivery

As APIs do Adobe Target e do Adobe Target podem ser usadas para fornecer respostas a páginas da Web, mas também podem ser usadas em experiências não baseadas em HTML, incluindo aplicativos, telas, consoles, emails, quiosques e outros dispositivos de exibição. [!DNL Recommendations] Em outras palavras, quando [!DNL Target] bibliotecas e JavaScript não podem ser usadas, a API **[!DNL Target]do **Delivery ainda nos permite acessar toda a gama de[!DNL Target]funcionalidades para fornecer experiências personalizadas.

> [!NOTE]
> Ao solicitar conteúdo contendo recomendações reais (produtos ou itens recomendados), use a API [!DNL Target] de Delivery.

Para recuperar recomendações, envie uma chamada de POST da API do Delivery do Adobe Target com as informações contextuais apropriadas, que podem incluir uma ID do usuário (para uso com recomendações específicas do perfil, como os itens visualizados recentemente pelo usuário), o nome da mbox relevante, os parâmetros da mbox, os parâmetros do perfil ou outros atributos. A resposta incluirá entity.ids recomendados (e pode incluir outros dados de entidade) no formato JSON ou HTML, que pode ser exibido no dispositivo.

A API [de](https://developers.adobetarget.com/api/delivery-api/) Delivery para Adobe Target expõe todos os recursos existentes que uma [!DNL Target] solicitação padrão fornece.

>[!NOTE]
>A API do Delivery:
>* Permite recuperar experiências ou ofertas para um local e uma audiência de maneira RESTful.
>* Não requer autenticação.
>* Somente POSTs.
>* Não processa cookies ou redireciona chamadas.
>* Não requer ou reconhece &quot;funções de usuário&quot;. Basta obter conteúdo ou relatar eventos para servidores de [!DNL Target] borda.


Para usar a API do Delivery para fornecer experiências [!DNL Target] —incluindo recomendações—siga estas etapas:

1. Crie uma [!DNL Target] atividade (A/B, XT, AP ou [!DNL Recommendations]) usando o Compositor baseado em formulário (não o Visual Experience Composer).
2. Use a API do Delivery para obter uma resposta para as solicitações geradas pela [!DNL Target] atividade que você acabou de criar.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Criar uma recomendação usando o Criador de experiências baseado em forma

Para criar recomendações que podem ser usadas com a API de Delivery, use o Compositor [baseado em](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)formulário.

1. Primeiro, crie e salve um design baseado em JSON para usar em sua recomendação. Para obter exemplos de JSON, além de informações sobre como as respostas JSON podem ser retornadas ao configurar uma atividade baseada em formulário, consulte a documentação sobre [Criar designs](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)de recomendação. Neste exemplo, o design chama-se JSON *simples.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Em [!DNL Target], navegue até **[!UICONTROL Atividade]>[!UICONTROL Criar Atividade]>[!UICONTROL Recommendations]** e selecione **[!UICONTROL Formulário]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Selecione uma propriedade e clique em **[!UICONTROL Avançar]**.
4. Defina o local onde você gostaria que os usuários recebessem a resposta da recomendação. O exemplo abaixo usa um local chamado *api_charter*. Selecione seu design baseado em JSON, criado anteriormente, chamado JSON *simples.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salve e ative a recomendação. Irá gerar resultados. [Quando os resultados estiverem prontos](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), você poderá usar a API do Delivery para recuperá-los.

## Usar a API de Delivery

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Observe que o código do cliente é obrigatório. Como lembrete, seu código de cliente pode ser encontrado no Adobe Target navegando até **[!UICONTROL Recommendations]>[!UICONTROL Configurações]**. Observe o valor do Código **[!UICONTROL do]** cliente na seção Token **[!UICONTROL da API de]** recomendação.
   ![client-code.png](assets/client-code.png)
1. Depois de ter o código de cliente, crie sua chamada de API de Delivery. O exemplo abaixo começa com a Chamada **[!UICONTROL API do Delivery Mboxes em lote]** da Web fornecida na coleção [Postman da API do](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)Delivery, fazendo modificações relevantes. Por exemplo:
   * os objetos do **navegador** e **endereço** foram removidos do **Corpo**, pois não são necessários para casos de uso não HTML
   * *api_charter* é listado como o nome do local neste exemplo
   * o entity.id é especificado, já que esta recomendação se baseia na Semelhança de conteúdo, que requer que uma chave de item atual seja transmitida para [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)Lembre-se de configurar seus parâmetros de query corretamente. Por exemplo, certifique-se de especificar`{{CLIENT_CODE}}` conforme necessário. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envie a solicitação. Isso é executado em relação ao local *api_charter* , que tem uma recomendação ativa em execução, definida com seu design JSON que resultará em uma lista de entidades recomendadas.
1. Receba uma resposta com base no design JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)A resposta inclui a ID da chave, bem como as IDs de entidade das entidades recomendadas.

Usar a API de Delivery com [!DNL Recommendations] isso permite executar etapas adicionais antes de exibir recomendações ao visitante no dispositivo não HTML. Por exemplo, você pode obter a resposta da API do Delivery para executar uma pesquisa adicional em tempo real dos detalhes do atributo da entidade (inventário, preço, classificação etc.) de outro sistema (como uma plataforma CMS, PIM ou ecommerce) antes de exibir os resultados finais.

Usando a abordagem descrita neste tutorial, você pode obter qualquer aplicativo que aproveite a resposta para fornecer recomendações personalizadas [!DNL Target] !

## Exemplo de implementações

Os recursos a seguir fornecem exemplos de várias implementações não focadas em HTML. Lembre-se de que cada implementação será única, devido ao sistema e aos dispositivos envolvidos.

| Recurso | Detalhes |
| --- | --- |
| [Consumindo RESTful APIs em AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Como criar e implantar um pacote OSGi da Adobe Experience Manager que consuma dados de um serviço Web RESTful de terceiros. |
| [Adobe Target Everywhere - Implementação do lado do servidor ou na IoT](https://expleague.azureedge.net/labs/L733/index.html) | Laboratório do Adobe Summit 2019 que fornece experiência prática para um aplicativo React que aproveita as APIs do lado do servidor Adobe Target. |
| [Adobe Target em um aplicativo móvel sem o SDK Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Este guia mostra como configurar o Adobe Target em seu aplicativo móvel sem instalar o SDK do Adobe. Essa solução usa a visualização Web do SDK do Tealium e o módulo Comandos remotos para enviar e receber solicitações à API do Visitante do Adobe (Experience Cloud) e à API do Adobe Target. |
| [Como a Adobe Target funciona em aplicativos móveis](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Como [!DNL Target] funciona com o SDK móvel |
| [Configuração [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] das APIs](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Etapas para configurar a [!DNL Target] extensão no Experience Platform Launch, adicionar a [!DNL Target] extensão ao aplicativo e implementar [!DNL Target] APIs para solicitar atividade, pré-buscar oferta e entrar no modo de pré-visualização visual. |
| [Adobe Target Node Client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK v1.0 de [!DNL Target] Node.js de fonte aberta |
| [Visão geral do lado do servidor](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informações sobre APIs de delivery do lado do servidor Adobe Target, APIs de Delivery do lado do servidor, SDK do Node.js e APIs [!DNL Recommendations] do Adobe Target. |
| [Adobe Campaign Content Recommendations no email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que descreve como aproveitar as recomendações de conteúdo por email via Adobe Target e Adobe I/O Runtime no Adobe Campaign. |

## Gerenciamento da [!DNL Recommendations] configuração com APIs

Na maioria das vezes, as recomendações são configuradas na interface do usuário do Adobe Target, usadas ou acessadas por meio das [!DNL Target] APIs, por motivos como os mencionados nas seções acima. Essa coordenação de API de interface é comum. No entanto, às vezes os usuários podem querer executar todas as ações por meio de APIs, tanto pela configuração quanto pelo uso dos resultados. Embora seja muito menos comum, os usuários podem configurar, executar ** e aproveitar os resultados das recomendações totalmente usando as APIs.

Aprendemos em uma seção [](manage-catalog.md) anterior como gerenciar entidades da Adobe Target Recommendations e fornecê-las do lado do servidor. Da mesma forma, a E/S do Adobe permite gerenciar critérios, promoções, coleções e modelos de design sem precisar fazer logon no Adobe Target. Uma lista completa de todas as [!DNL Recommendations] APIs pode ser encontrada [aqui](http://developers.adobetarget.com/api/recommendations/), mas aqui está um resumo para referência.

| Recurso | Detalhes |
| --- | --- |
| [Coleções](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Lista, criar, obter, editar e excluir coleções. |
| [Critérios](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lista e obtenha critérios. |
| [Designs](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Lista, criação, obtenção, edição, exclusão e validação de designs. |
| [Entidades](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvar, excluir e obter entidades. |
| [Promoções](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Lista, criação, obtenção, edição e exclusão de promoções. |
| [Critérios de Categoria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios de categoria. |
| [Critérios personalizados](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios personalizados. |
| [Critérios do item](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios de item. |
| [Critérios de popularidade](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios de popularidade. |
| [Critérios de atributo do Perfil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Lista, criação, obtenção, edição e exclusão dos critérios de atributos do perfil. |
| [Critérios recentes](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios recentes. |
| [Critérios de sequência](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Lista, criação, obtenção, edição e exclusão de critérios de sequência. |

## Documentação de referência

* [Documentação da API do Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [API do Delivery Adobe Target](https://developers.adobetarget.com/api/delivery-api/)
* [Integrar [!DNL Recommendations] ao email](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumo e revisão

Parabéns! Ao terminar este tutorial, você aprendeu a:
* [Gerenciar seu catálogo usando a API do Recommendations](manage-catalog.md)
* [Gerenciar critérios personalizados usando a API do Recommendations](manage-custom-criteria.md)
* [Usar a API de Delivery com a Recommendations](fetch-recs-server-side-delivery-api.md)
