---
title: Como gerenciar critérios personalizados
description: Esta parte do tutorial orienta os desenvolvedores pelas etapas necessárias para usar as APIs do Adobe Target para gerenciar, criar, listar, editar, obter e excluir os critérios do Adobe Target Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 1%

---

# Gerenciar critérios personalizados

Às vezes, os algoritmos fornecidos por [!DNL Recommendations] não são capazes de exibir itens específicos que você gostaria de promover. Em tal situação, os critérios personalizados fornecem uma maneira de fornecer um conjunto específico de itens recomendados para um determinado item-chave ou categoria. Você define o mapeamento entre o item ou a categoria principal e os itens recomendados e importa esse mapeamento como um critério personalizado. Esse processo é descrito na [documentação de critérios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en). Conforme observado nessa documentação, você pode criar, editar e excluir critérios personalizados por meio da [!DNL Target] interface do usuário (UI). No entanto, [!DNL Target] também fornece um conjunto de APIs de Critérios personalizados que permitem um gerenciamento mais detalhado de seus critérios personalizados.

>[!IMPORTANT]
>
>Siga esta diretriz de uso para critérios personalizados:
>
> Faça tudo (crie, edite, exclua) para um determinado critério personalizado usando as APIs ou faça tudo (crie, edite, exclua) usando a interface do usuário. O gerenciamento de seus critérios personalizados por meio de uma combinação da interface do usuário e da API pode gerar informações conflitantes ou resultados inesperados. Por exemplo, criar um critério personalizado na interface do usuário, mas editá-lo por meio da API, não refletirá suas atualizações na interface do usuário, embora ele seja atualizado no back-end, como visível pela API.

## Criar critérios personalizados

Para criar critérios personalizados usando a [Criar API de critérios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), a sintaxe é:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Os critérios personalizados criados usando a API Criar critérios personalizados, conforme descrito neste exercício, serão exibidos na interface do usuário, onde persistirão. Não será possível editá-los ou excluí-los da interface do usuário. Você pode editá-los ou excluí-los **por meio da API**, mas de qualquer maneira, eles continuarão a aparecer na interface do usuário [!DNL Target]. Para manter a opção de editar ou excluir da interface do usuário, crie os critérios personalizados usando a interface do usuário de [a documentação](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en), em vez de usar a API Criar critérios personalizados .

Continue com este tutorial somente depois de ler o aviso acima e esteja confortável em criar novos critérios personalizados que não podem ser excluídos subsequentemente da interface do usuário.

1. Verifique `TENANT_ID` e `API_KEY` para **Criar critérios personalizados** fazem referência às variáveis de ambiente Postman estabelecidas anteriormente. Use a imagem abaixo para comparação.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Adicione seu **Body** como **raw** JSON que define o local do seu arquivo CSV de critérios personalizados. Use o exemplo fornecido na documentação [Criar API de critérios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) como um modelo, fornecendo seu `environmentId` e outros valores, conforme necessário. Neste exemplo, usamos LAST_PURCHASED como a chave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envie a solicitação e observe a resposta, que contém os detalhes dos critérios personalizados que você acabou de criar.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Para verificar se seus critérios personalizados foram criados, navegue dentro do Adobe Target para **[!UICONTROL Recommendations] > [!UICONTROL Critérios]** e pesquise seus critérios por nome, ou use a **API de critérios personalizados de lista** na próxima etapa.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

Nesse caso, temos um erro. Vamos investigar o erro examinando os critérios personalizados mais detalhadamente, usando a **List Custom Criteria API**.

## Listar critérios personalizados

Para recuperar uma lista de todos os critérios personalizados, juntamente com os detalhes de cada um, use a [List Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). A sintaxe é:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verifique `TENANT_ID` e `API_KEY` como antes e envie a solicitação. Na resposta, observe a ID de critério personalizado, bem como os detalhes relacionados à mensagem de erro anotada anteriormente.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

Nesse caso, o erro ocorreu porque as informações do servidor estão incorretas, o que significa que [!DNL Target] não pode acessar o arquivo CSV que contém a definição de critérios personalizados. Vamos editar os critérios personalizados para corrigir isso.

## Editar critérios personalizados

Para alterar os detalhes de uma definição de critério personalizado, use a [Editar API de critérios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). A sintaxe é:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verifique `TENANT_ID` e `API_KEY`, como antes.
   ![EditarCritériosPersonalizados1](assets/EditCustomCriteria1.png)

1. Especifique a ID de critério dos critérios personalizados (únicos) que deseja editar.
   ![EditarCritériosPersonalizados2](assets/EditCustomCriteria2.png)

1. No Corpo, forneça o JSON atualizado com as informações corretas do servidor. (Para esta etapa, especifique o acesso FTP a um servidor que você pode acessar.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Envie a solicitação e anote a resposta.
   ![EditarCritériosPersonalizados4](assets/EditCustomCriteria4.png)

Vamos verificar o sucesso dos critérios personalizados atualizados, usando a **Obter API de critérios personalizados**.

## Obter critérios personalizados

Para exibir detalhes de critérios personalizados para um critério personalizado específico, use a [Obter API de critérios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). A sintaxe é:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique a ID do critério do critério personalizado cujos detalhes você deseja obter. Envie a solicitação e revise a resposta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verificar sucesso. (No nosso caso, verifique se não há mais erros de FTP.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Verifique se a atualização reflete com precisão na interface do usuário.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Excluir critérios personalizados

Usando a ID de critérios anotada anteriormente, exclua seus critérios personalizados usando a [Excluir API de critérios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). A sintaxe é:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique a ID de critério dos critérios personalizados (únicos) que deseja excluir. Clique em **Enviar**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Verifique se os critérios foram excluídos usando Obter critérios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
Nesse caso, o erro 404 esperado indica que os critérios excluídos não podem ser encontrados.

>[!NOTE]
>Como lembrete, os critérios não serão removidos da interface do usuário [!DNL Target] mesmo que tenha sido excluída, pois foi criada usando a API Criar critérios personalizados .

Parabéns! Agora é possível criar, listar, editar, excluir e obter detalhes sobre critérios personalizados usando a API [!DNL Recommendations]. Na próxima seção, você usará a [!DNL Target] API de entrega para recuperar recomendações.

[Próximo &quot;Buscar o Recommendations com a API de entrega do lado do servidor&quot; >](fetch-recs-server-side-delivery-api.md)
