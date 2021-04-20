---
title: Como buscar o Recommendations com a API de entrega
description: Essa parte do tutorial orienta os desenvolvedores pelas etapas necessárias para buscar conteúdo de recomendações usando a API de entrega do Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---


# Buscar [!DNL Recommendations] com a API de entrega

As APIs [!DNL Recommendations] do Adobe Target e do Adobe Target podem ser usadas para fornecer respostas a páginas da Web, mas também podem ser usadas em experiências não baseadas em HTML, incluindo aplicativos, telas, consoles, emails, quiosques e outros dispositivos de exibição. Em outras palavras, quando as bibliotecas [!DNL Target] e o JavaScript não podem ser usados, a **[!DNL Target]API de entrega** ainda nos permite acessar a gama completa da funcionalidade [!DNL Target] para fornecer experiências personalizadas.

>[!NOTE]
>
> Ao solicitar conteúdo contendo recomendações reais (produtos ou itens recomendados), use a [!DNL Target] API de entrega.

Para recuperar as recomendações, envie uma chamada de POST da API de entrega do Adobe Target com as informações contextuais apropriadas, que podem incluir uma ID de usuário (para uso com recomendações específicas de perfil, como os itens visualizados recentemente pelo usuário), nome da mbox relevante, parâmetros da mbox, parâmetros do perfil ou outros atributos. A resposta incluirá entity.ids recomendadas (e pode incluir outros dados de entidade) no formato JSON ou HTML, que pode ser exibido no dispositivo.

A [API de entrega](https://developers.adobetarget.com/api/delivery-api/) para Adobe Target expõe todos os recursos existentes que uma solicitação padrão [!DNL Target] fornece.

>[!NOTE]
>A API de entrega:
>* Permite recuperar experiências ou ofertas para um local e um público-alvo de maneira RESTful.
>* Não requer autenticação.
>* Somente POSTs.
>* Não processa cookies ou redireciona chamadas.
>* Não requer ou reconhece &quot;funções de usuário&quot;. Basta buscar conteúdo ou relatar eventos em servidores de borda [!DNL Target].


Para usar a API de entrega para entregar [!DNL Target] experiências, incluindo recomendações, siga estas etapas:

1. Crie uma atividade [!DNL Target] (A/B, XT, AP ou [!DNL Recommendations]) usando o Composer baseado em formulário (não o Visual Experience Composer).
2. Use a API de entrega para obter uma resposta para as solicitações geradas pela atividade [!DNL Target] que você acabou de criar.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Criar uma recomendação usando o Experience Composer baseado em formulário

Para criar recomendações que podem ser usadas com a API de entrega, use o [Composer baseado em formulário](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. Primeiro, crie e salve um design baseado em JSON para usar em sua recomendação. Para obter exemplos de JSON, além de informações sobre como as respostas JSON podem ser retornadas ao configurar uma atividade baseada em formulário, consulte a documentação em [Criar designs de recomendação](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). Neste exemplo, o design é chamado de *Simple JSON.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Em [!DNL Target], navegue até **[!UICONTROL Atividades] > [!UICONTROL Criar Atividade] > [!UICONTROL Recommendations]** e selecione **[!UICONTROL Formulário]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Selecione uma propriedade e clique em **[!UICONTROL Next]**.
4. Defina o local onde deseja que os usuários recebam a resposta da recomendação. O exemplo abaixo usa um local chamado *api_charter*. Selecione o design baseado em JSON, criado anteriormente, chamado *Simple JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salve e ative a recomendação. Ele vai gerar resultados. [Quando os resultados estiverem prontos](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), você poderá usar a API de entrega para recuperá-los.

## Usar a API de entrega

A sintaxe para a [API de entrega](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) é:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Observe que o código de cliente é obrigatório. Como lembrete, seu código de cliente pode ser encontrado no Adobe Target navegando até **[!UICONTROL Recommendations] > [!UICONTROL Settings]**. Observe o valor **[!UICONTROL Código do cliente]** na seção **[!UICONTROL Token de API do Recommendation]**.
   ![client-code.png](assets/client-code.png)
1. Depois de ter seu código de cliente, crie sua chamada de API de entrega. O exemplo abaixo começa com a **[!UICONTROL Chamada da API de entrega de mboxes em lote da Web]** fornecida na [Coleção do postman da API de entrega](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), fazendo modificações relevantes. Por exemplo:
   * os objetos **browser** e **address** foram removidos do **Body**, uma vez que não são necessários para casos de uso não-HTML
   * *api_* charteris listado como o nome do local neste exemplo
   * a entity.id é especificada, já que esta recomendação se baseia na Similaridade de conteúdo, que requer que uma chave de item atual seja passada para [!DNL Target].
      ![server-side-Delivery-API-call.](assets/server-side-delivery-api-call2.png)
pngLembre-se de configurar seus parâmetros de consulta corretamente. Por exemplo, certifique-se de especificar 
`{{CLIENT_CODE}}` conforme necessário. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envie a solicitação. Isso é executado no local *api_charter*, que tem uma recomendação ativa em execução, definida com o design JSON que gerará uma lista de entidades recomendadas.
1. Receba uma resposta com base no design JSON.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
pngA resposta inclui a ID da chave, bem como as IDs de entidade das entidades recomendadas.

Usar a API de entrega com [!DNL Recommendations] dessa forma permite executar etapas adicionais antes de exibir recomendações para o visitante no dispositivo não HTML. Por exemplo, você pode obter a resposta da API de entrega para executar uma pesquisa adicional em tempo real de detalhes do atributo da entidade (inventário, preço, classificação etc.) de outro sistema (como uma plataforma CMS, PIM ou comércio eletrônico), antes de exibir os resultados finais.

Usando a abordagem descrita neste tutorial, você pode obter qualquer aplicativo para aproveitar a resposta de [!DNL Target] para fornecer recomendações personalizadas!

## Exemplo de implementações

Os recursos a seguir fornecem exemplos de várias implementações não focadas em HTML. Lembre-se de que cada implementação será única, devido ao sistema e aos dispositivos envolvidos.

| Recurso | Detalhes |
| --- | --- |
| [Consumo de RESTful APIs no AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Como criar e implantar um pacote OSGi do Adobe Experience Manager que consome dados de um serviço Web RESTful de terceiros. |
| [Adobe Target em qualquer lugar - Implementar o lado do servidor ou no IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab, que fornece experiência prática para um aplicativo React que aproveita as APIs do lado do servidor do Adobe Target. |
| [Adobe Target em um aplicativo móvel sem o SDK do Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Este guia mostra como configurar o Adobe Target no aplicativo móvel sem instalar o SDK do Adobe. Essa solução usa a visualização Web do SDK do Tealium e o módulo Comandos remotos para enviar e receber solicitações à API do visitante do Adobe (Experience Cloud) e à API do Adobe Target. |
| [Como a Adobe Target funciona em aplicativos móveis](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Como o [!DNL Target] funciona com o SDK móvel |
| [Configuração  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] das APIs](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Etapas para configurar a extensão [!DNL Target] no Experience Platform Launch, adicionar a extensão [!DNL Target] ao aplicativo e implementar [!DNL Target] APIs para solicitar atividades, ofertas de pré-busca e Inserir modo de visualização. |
| [Cliente de nó do Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | [!DNL Target] SDK Node.js de fonte aberta v1.0 |
| [Visão geral do lado do servidor](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informações sobre APIs de entrega do lado do servidor do Adobe Target, APIs de entrega em lote do servidor, SDK do Node.js e APIs do Adobe Target [!DNL Recommendations]. |
| [Adobe Campaign Content Recommendations em Email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que descreve como aproveitar as recomendações de conteúdo em email pelo Adobe Target e Adobe I/O Runtime no Adobe Campaign. |

## Gerenciando [!DNL Recommendations] a configuração com APIs

Na maioria das vezes, as recomendações são configuradas na interface do usuário do Adobe Target e usadas ou acessadas por meio das APIs [!DNL Target], por motivos como os mencionados nas seções acima. Essa coordenação da API da interface do usuário é comum. No entanto, às vezes os usuários podem querer executar todas as ações por meio de APIs, tanto a configuração quanto o uso dos resultados. Embora seja muito menos comum, os usuários podem absolutamente configurar, executar, *e* aproveitar os resultados das recomendações totalmente usando as APIs.

Aprendemos em uma [seção anterior](manage-catalog.md) como gerenciar entidades do Adobe Target Recommendations e fornecê-las do lado do servidor. Da mesma forma, o Adobe I/O permite gerenciar critérios, promoções, coleções e modelos de design sem precisar fazer logon no Adobe Target. Uma lista completa de todas as [!DNL Recommendations] APIs pode ser encontrada [aqui](http://developers.adobetarget.com/api/recommendations/), mas aqui está um resumo para referência.

| Recurso | Detalhes |
| --- | --- |
| [Coleções](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Listar, criar, obter, editar e excluir coleções. |
| [Critérios](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lista e obtenha critérios. |
| [Designs](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Listar, criar, obter, editar, excluir e validar designs. |
| [Entidades](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvar, excluir e obter entidades. |
| [Promoções](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Listar, criar, obter, editar e excluir promoções. |
| [Critérios de categoria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Listar, criar, obter, editar e excluir critérios de categoria. |
| [Critérios personalizados](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Listar, criar, obter, editar e excluir critérios personalizados. |
| [Critérios do item](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Listar, criar, obter, editar e excluir critérios de item. |
| [Critérios de popularidade](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Listar, criar, obter, editar e excluir critérios de popularidade. |
| [Critérios dos atributos do perfil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Liste, crie, obtenha, edite e exclua os critérios do atributo de perfil. |
| [Critérios recentes](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Listar, criar, obter, editar e excluir critérios recentes. |
| [Critérios de sequência](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Listar, criar, obter, editar e excluir critérios de sequência. |

## Documentação de referência

* [Documentação da API do Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [API de entrega do Adobe Target](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Integração com email](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumo e revisão

Parabéns! Ao concluir este tutorial, você aprendeu a:
* [Gerenciar o catálogo usando a API do Recommendations](manage-catalog.md)
* [Gerenciar critérios personalizados usando a API do Recommendations](manage-custom-criteria.md)
* [Usar a API de entrega com o Recommendations](fetch-recs-server-side-delivery-api.md)
