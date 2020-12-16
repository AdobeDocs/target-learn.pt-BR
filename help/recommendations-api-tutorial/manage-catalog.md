---
title: Gerenciar seu catálogo Recommendations usando APIs
keywords: recommendations;adobe recommendations;premium;api;apis
description: A Adobe Target Recommendations inclui um conjunto dedicado de APIs que permitem gerenciar seu catálogo de produtos e/ou conteúdo recomendáveis; gerenciar seus algoritmos e campanhas de recomendações; e fornecer recomendações em objetos JSON, HTML ou XML a serem exibidos em Web, dispositivos móveis, email, IOT e outros canais.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---


# Gerenciar seu catálogo [!DNL Recommendations] usando APIs

Nesse ponto, você aprendeu a gerar um token de acesso, usando o fluxo de autenticação JWT, para usar as Adobe Target Admin APIs com a Adobe I/O.

Você pode usar as [APIs do Recommendations](https://developers.adobetarget.com/api/recommendations/) para adicionar, atualizar ou excluir itens no catálogo de recomendações. Assim como no restante das APIs de administração da Adobe Target, as [!DNL Recommendations] APIs exigem autenticação.

>[!TIP]
>
>Envie o **[!UICONTROL IMS: JWT Gerar + autenticação por meio do Token do usuário]** solicita sempre que for necessário atualizar seu token de acesso para autenticação, pois ele expira após 24 horas. Consulte [Configurar autenticação da API do Adobe](../apis/configure-io-target-integration.md) para obter instruções.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>Antes de continuar, obtenha a coleção [Recommendations Postman](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Criação e atualização de itens com a API Salvar Entidades

Para preencher o banco de dados do produto [!DNL Recommendations] usando a API em vez de um feed do produto CSV ou solicitações [!DNL Target] acionadas em páginas de produtos, use a [API Salvar Entidades](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Essa solicitação adiciona ou atualiza um item em um único ambiente [!DNL Target]. A sintaxe é:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Por exemplo, Salvar Entidades pode ser usado para atualizar itens sempre que certos limites forem atingidos, como limites de inventário ou preço, a fim de sinalizar esses itens e impedir que eles sejam recomendados.

1. Navegue até **[!DNL Target]> [!UICONTROL Configuração] > [!UICONTROL Hosts] > [!UICONTROL Ambientes]** para obter a ID de Ambiente [!DNL Target] na qual deseja adicionar ou atualizar um item.

   ![SaveEntities1](assets/SaveEntities01.png)

2. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os Cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![SaveEntities3](assets/SaveEntities03.png)

3. Insira seu código JSON como **raw** no **Body**. Não se esqueça de especificar sua ID de ambiente, usando a variável `environment`. (No exemplo abaixo, a ID do ambiente é 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   Abaixo está um exemplo de JSON que adiciona entity.id kit2001 com valores de entidade associados para um produto Toaster Oven no ambiente 6781.

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. Clique em **Enviar**. Deve receber a seguinte resposta.

   ![SaveEntities6.png](assets/SaveEntities05.png)

O objeto JSON pode ser dimensionado para enviar vários produtos. Por exemplo, esse JSON especifica duas entidades.

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. Agora é a sua vez! Use a API **Salvar Entidades** para adicionar os seguintes itens ao catálogo. Use a amostra JSON acima como ponto de partida. (Você precisará estender o JSON para incluir entidades adicionais.)

   ![SaveEntities5.png](assets/SaveEntities06.png)

Parece que esses dois últimos itens não pertencem. Vamos inspecioná-los usando a API **Get Entity** e, se necessário, excluí-los usando a API **Excluir Entidades**.

## Obter detalhes do item com a API Get Entity

Para recuperar os detalhes de um item existente, use a [Get Entity API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). A sintaxe é:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Os detalhes da entidade só podem ser recuperados para uma única entidade de cada vez. Você pode usar a opção Obter entidade para confirmar se as atualizações foram feitas no catálogo conforme esperado, ou para auditar o conteúdo do catálogo de outra forma.

1. Na solicitação da API, especifique a ID da entidade, usando a variável `entityId`. O exemplo a seguir retornará detalhes para a entidade cuja entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

2. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os Cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![GetEntity2](assets/GetEntity2.png)

3. Envie a solicitação.

   ![GetEntity3](assets/GetEntity3.png)
Se você receber um erro informando que a entidade não foi encontrada, como mostrado no exemplo acima, verifique se você está enviando a solicitação para o  [!DNL Target] ambiente correto.

   >[!NOTE]
   Se nenhum ambiente for explicitamente especificado, a Get Entity tentará obter a entidade somente do ambiente padrão [a1/>. ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0) Se você quiser retirar de qualquer ambiente que não seja o seu ambiente padrão, especifique a ID do ambiente.

4. Se necessário, adicione o parâmetro `environmentId` e reenvie a solicitação.

   ![GetEntity4](assets/GetEntity4.png)

5. Envie outra solicitação **Get Entity**, desta vez para inspecionar a entidade cuja entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Suponha que você decida que essas entidades precisam ser removidas do catálogo. Vamos usar a API **Excluir Entidades**.

## Excluindo itens com a API Excluir Entidades

Para remover itens do catálogo, use a [API Excluir Entidades](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). A sintaxe é:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
Essa API exclui entidades referenciadas por IDs especificadas.
Se nenhuma ID de entidade for fornecida, todas as entidades no ambiente em questão serão excluídas. Se nenhuma ID de ambiente for fornecida, as entidades serão excluídas de todos os ambientes. Use isso com cautela!

1. Navegue até **[!DNL Target]> [!UICONTROL Configuração] > [!UICONTROL Hosts] > [!UICONTROL Ambientes]** para obter a ID de Ambiente [!DNL Target] da qual pretende eliminar itens.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. Na solicitação da API, especifique as IDs de entidade das entidades que deseja excluir, usando a sintaxe `&ids=[comma-delimited-entity-ids]` (um parâmetro de query). Ao excluir mais de uma entidade, separe as IDs usando vírgulas.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. Especifique a ID do ambiente, usando a sintaxe `&environment=[environmentId]`, caso contrário, as entidades em todos os ambientes serão excluídas.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os Cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. Envie a solicitação.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. Verifique seus resultados usando **Get Entity**, que agora deve indicar que as entidades excluídas não podem ser encontradas.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Parabéns! Agora você pode usar as [!DNL Recommendations] APIs para criar, atualizar, excluir e obter detalhes sobre as entidades em seu catálogo. Na próxima seção, você aprenderá a gerenciar critérios personalizados.

[Próximo &quot;Gerenciar critérios personalizados&quot; >](manage-custom-criteria.md)
