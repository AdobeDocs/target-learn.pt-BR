---
title: Como buscar o Recommendations com a API de entrega
description: Essa parte do tutorial orienta os desenvolvedores pelas etapas necessárias para buscar conteúdo de recomendações usando a API de entrega do Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 1%

---

# Buscando [!DNL Recommendations] com a API de entrega

A Adobe Target e a Adobe Target [!DNL Recommendations] As APIs podem ser usadas para fornecer respostas às páginas da Web, mas também podem ser usadas em experiências não baseadas em HTML, incluindo aplicativos, telas, consoles, emails, quiosques e outros dispositivos de exibição. Em outras palavras, quando [!DNL Target] Não é possível usar bibliotecas e JavaScript, a variável **[!DNL Target]API de entrega** ainda nos permite acessar a gama completa de [!DNL Target] para fornecer experiências personalizadas.

>[!NOTE]
>
> Ao solicitar conteúdo contendo recomendações reais (produtos ou itens recomendados), use a variável [!DNL Target] API de entrega.

Para recuperar as recomendações, envie uma chamada de POST da API de entrega do Adobe Target com as informações contextuais apropriadas, que podem incluir uma ID de usuário (para uso com recomendações específicas de perfil, como os itens visualizados recentemente pelo usuário), nome da mbox relevante, parâmetros da mbox, parâmetros do perfil ou outros atributos. A resposta incluirá entity.ids recomendadas (e pode incluir outros dados de entidade) no formato JSON ou HTML, que pode ser exibido no dispositivo.

O [API de entrega](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} para Adobe Target expõe todos os recursos existentes que um padrão [!DNL Target] A solicitação fornece.

>[!NOTE]
>A API de entrega:
>* Permite recuperar experiências ou ofertas para um local e um público-alvo de maneira RESTful.
>* Não requer autenticação.
>* Somente POSTs.
>* Não processa cookies ou redireciona chamadas.
>* Não requer ou reconhece &quot;funções de usuário&quot;. Basta buscar conteúdo ou relata eventos em [!DNL Target] servidores de borda.


Para usar a API de entrega para entrega [!DNL Target] experiências — incluindo recomendações — siga estas etapas:

1. Crie um [!DNL Target] atividade (A/B, XT, AP ou [!DNL Recommendations]) usando o Composer baseado em formulário (não o Visual Experience Composer).
2. Use a API de entrega para obter uma resposta para as solicitações geradas pela variável [!DNL Target] atividade que você acabou de criar.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Criar uma recomendação usando o Experience Composer baseado em formulário

Para criar recomendações que podem ser usadas com a API de entrega, use o [Compositor baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

1. Primeiro, crie e salve um design baseado em JSON para usar em sua recomendação. Para obter exemplos de JSON, além de informações sobre como as respostas JSON podem ser retornadas ao configurar uma atividade baseada em formulário, consulte a documentação em [Criando Designs De Recomendação](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en). Neste exemplo, o design é nomeado como *JSON simples.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Em [!DNL Target], navegue até **[!UICONTROL Atividades] > [!UICONTROL Criar atividade] > [!UICONTROL Recommendations]**, em seguida selecione **[!UICONTROL Formulário]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Selecione uma propriedade e clique em **[!UICONTROL Próximo]**.
4. Defina o local onde deseja que os usuários recebam a resposta da recomendação. O exemplo abaixo usa um local chamado *api_charter*. Selecione o design baseado em JSON, criado anteriormente, com o nome *JSON simples.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salve e ative a recomendação. Ele vai gerar resultados. [Quando os resultados estiverem prontos](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en), é possível usar a API de entrega para recuperá-las.

## Usar a API de entrega

A sintaxe da variável [API de entrega](https://developer.adobe.com/target/implement/delivery-api/#tag/Delivery-API){target=_blank} é:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Observe que o código de cliente é obrigatório. Como lembrete, seu código de cliente pode ser encontrado no Adobe Target navegando até **[!UICONTROL Recommendations] > [!UICONTROL Configurações]**. Observe que **[!UICONTROL Código do cliente]** na variável **[!UICONTROL Token de API do Recommendation]** seção.
   ![client-code.png](assets/client-code.png)
1. Depois de ter seu código de cliente, crie sua chamada de API de entrega. O exemplo abaixo começa com a variável **[!UICONTROL Chamada da API de entrega de mboxes em lote na Web]** no [Coleção Postman da API de entrega](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), introduzindo as alterações pertinentes. Por exemplo:
   * o **navegador** e **endereço** objetos foram removidos do **Corpo**, uma vez que não são exigidas para casos de uso não HTML
   * *api_charter* está listado como o nome da localização neste exemplo
   * a entity.id é especificada, já que esta recomendação se baseia na Similaridade de conteúdo, que requer que uma chave de item atual seja passada para [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Lembre-se de configurar os parâmetros de consulta corretamente. Por exemplo, certifique-se de especificar 
`{{CLIENT_CODE}}` conforme necessário. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envie a solicitação. Isso é executado em relação à variável *api_charter* local, que tem uma recomendação ativa sendo executada, definido com seu design JSON que resultará em uma lista de entidades recomendadas.
1. Receba uma resposta com base no design JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
A resposta inclui a ID da chave, bem como as IDs de entidade das entidades recomendadas.

Usar a API de entrega com [!DNL Recommendations] dessa forma, o permite executar etapas adicionais antes de exibir recomendações para o visitante em dispositivos que não sejam HTML. Por exemplo, você pode obter a resposta da API de entrega para executar uma pesquisa adicional em tempo real de detalhes do atributo da entidade (inventário, preço, classificação etc.) de outro sistema (como uma plataforma CMS, PIM ou comércio eletrônico), antes de exibir os resultados finais.

Usando a abordagem descrita neste tutorial, você pode obter qualquer aplicativo do para aproveitar a resposta do [!DNL Target] para fornecer recomendações personalizadas!

## Exemplo de implementações

Os recursos a seguir fornecem exemplos de várias implementações não focadas em HTML. Lembre-se de que cada implementação será única, devido ao sistema e aos dispositivos envolvidos.

| Recurso | Detalhes |
| --- | --- |
| [Adobe Target em qualquer lugar - Implementar o lado do servidor ou no IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab, que fornece experiência prática para um aplicativo React que utiliza APIs do lado do servidor do Adobe Target. |
| [Adobe Target em um aplicativo móvel sem o SDK do Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Este guia mostra como configurar o Adobe Target no aplicativo móvel sem instalar o SDK do Adobe. Essa solução usa a visualização Web do SDK do Tealium e o módulo Comandos remotos para enviar e receber solicitações à API do visitante do Adobe (Experience Cloud) e à API do Adobe Target. |
| [Como a Adobe Target funciona em aplicativos móveis](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | How [!DNL Target] funciona com o SDK móvel |
| [Configurar a [!DNL Target] extensão no Experience Platform Launch e implementação [!DNL Target] APIs](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Etapas para configurar o [!DNL Target] no Experience Platform Launch, adicionar a [!DNL Target] Extensão para o aplicativo e implementação [!DNL Target] APIs para solicitar atividades, ofertas de busca prévia e Entrar no modo de visualização visual. |
| [Cliente de nó do Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Fornecido por software livre [!DNL Target] Node.js SDK v1.0 |
| [Visão geral do lado do servidor](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Informações sobre APIs de entrega do lado do servidor do Adobe Target, APIs de entrega em lote do lado do servidor, SDK do Node.js e Adobe Target [!DNL Recommendations] APIs. |
| [Adobe Campaign Content Recommendations em Email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que descreve como aproveitar as recomendações de conteúdo em email pelo Adobe Target e Adobe I/O Runtime no Adobe Campaign. |

## Gerenciamento [!DNL Recommendations] Configuração com APIs

Na maioria das vezes, as recomendações são configuradas na interface do usuário do Adobe Target e, em seguida, usadas ou acessadas por meio do [!DNL Target] APIs, por motivos como os mencionados nas seções acima. Essa coordenação da API da interface do usuário é comum. No entanto, às vezes os usuários podem querer executar todas as ações por meio de APIs, tanto a configuração quanto o uso dos resultados. Embora seja muito menos comum, os usuários podem configurar, executar, *e* aproveite os resultados das recomendações totalmente usando as APIs.

Aprendemos em um [seção anterior](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank} como gerenciar entidades do Adobe Target Recommendations e fornecê-las do lado do servidor. Da mesma forma, o Adobe I/O permite gerenciar critérios, promoções, coleções e modelos de design sem precisar fazer logon no Adobe Target. Uma lista completa de todos [!DNL Recommendations] É possível encontrar APIs [here](https://developers.adobetarget.com/api/recommendations/), mas aqui está um resumo para referência.

| Recurso | Detalhes |
| --- | --- |
| [Coleções](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | Listar, criar, obter, editar e excluir coleções. |
| [Critérios](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lista e obtenha critérios. |
| [Designs](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | Listar, criar, obter, editar, excluir e validar designs. |
| [Entidades](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvar, excluir e obter entidades. |
| [Promoções](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Listar, criar, obter, editar e excluir promoções. |
| [Critérios de categoria](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Listar, criar, obter, editar e excluir critérios de categoria. |
| [Critérios personalizados](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Listar, criar, obter, editar e excluir critérios personalizados. |
| [Critérios do item](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Listar, criar, obter, editar e excluir critérios de item. |
| [Critérios de popularidade](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Listar, criar, obter, editar e excluir critérios de popularidade. |
| [Critérios dos atributos do perfil](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Liste, crie, obtenha, edite e exclua os critérios do atributo de perfil. |
| [Critérios recentes](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Listar, criar, obter, editar e excluir critérios recentes. |
| [Critérios de sequência](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Listar, criar, obter, editar e excluir critérios de sequência. |

## Documentação de referência

* [Documentação da API de administrador do Adobe Target](https://developer.adobe.com/target/administer/admin-api/){target=_blank}
* [API de entrega do Adobe Target](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}
* [Integrar o  [!DNL Recommendations]  ao email](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumo e revisão

Parabéns! Ao concluir este tutorial, você aprendeu a:
* [Gerenciar o catálogo usando a API do Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank}
* [Gerenciar critérios personalizados usando a API do Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=_blank}
* [Usar a API de entrega com o Recommendations](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
