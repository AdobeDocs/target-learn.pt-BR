---
title: Gerenciar critérios personalizados
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
source-wordcount: '959'
ht-degree: 1%

---


# Gerenciar critérios personalizados

Às vezes, os algoritmos fornecidos por não [!DNL Recommendations] são capazes de exibir itens específicos que você gostaria de promover. Nessa situação, os critérios personalizados fornecem uma maneira de fornecer um conjunto específico de itens recomendados para um determinado item-chave ou categoria. Você define o mapeamento entre o item-chave ou a categoria e os itens recomendados e importa esse mapeamento como um critério personalizado. Esse processo é descrito na documentação [de critérios](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)personalizados. Conforme observado nessa documentação, você pode criar, editar e excluir critérios personalizados por meio da interface do [!DNL Target] usuário. Entretanto, [!DNL Target] também fornece um conjunto de APIs de critérios personalizados que permitem o gerenciamento mais detalhado de seus critérios personalizados.

>[!IMPORTANT]
>
>Siga estas diretrizes de uso para obter os critérios personalizados:
>
> Faça tudo (crie, edite, exclua) para um determinado critério personalizado usando as APIs ou faça tudo (crie, edite, exclua) usando a interface do usuário. O gerenciamento de seus critérios personalizados por meio de uma combinação da interface do usuário e da API pode resultar em informações conflitantes ou resultados inesperados. Por exemplo, criar um critério personalizado na interface do usuário, mas editá-lo por meio da API, não refletirá suas atualizações na interface do usuário, mesmo que elas sejam atualizadas no backend, como visível pela API.

## Criar critérios personalizados

Para criar critérios personalizados usando a API [](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)Criar critérios personalizados, a sintaxe é:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Os critérios personalizados criados usando a API Criar critérios personalizados, conforme descrito neste exercício, aparecerão na interface do usuário, onde eles persistirão. Você não poderá editá-los ou excluí-los da interface do usuário. Você pode editá-los ou excluí-los **por meio da API**, mas, de qualquer forma, eles continuarão a aparecer na [!DNL Target] interface do usuário. Para manter a opção de edição ou exclusão da interface do usuário, crie os critérios personalizados usando a interface do usuário de acordo com [a documentação](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), em vez de usar a API Criar critérios personalizados.

Continue com este tutorial somente depois de ler o aviso acima e esteja confortável em criar novos critérios personalizados que não possam ser excluídos posteriormente da interface do usuário.

1. Verifique `TENANT_ID` e `API_KEY` para **Criar critérios** personalizados, consulte as variáveis de ambiente Postman estabelecidas anteriormente. Use a imagem abaixo para comparação.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Adicione seu **Corpo** como JSON **bruto** que define a localização do arquivo CSV de critérios personalizados. Use o exemplo fornecido na documentação da API [](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) Criar critérios personalizados como um modelo, fornecendo seus `environmentId` e outros valores, conforme necessário. Neste exemplo, usamos LAST_PURCHASED como a chave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envie a solicitação e observe a resposta, que contém os detalhes dos critérios personalizados que você acabou de criar.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Para verificar se seus critérios personalizados foram criados, navegue dentro do Adobe Target para **[!UICONTROL Recommendations]>[!UICONTROL Critérios]** e pesquise seus critérios por nome, ou use a API **** Lista Custom Criteria na próxima etapa.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

Neste caso, temos um erro. Vamos investigar o erro examinando os critérios personalizados mais detalhadamente, usando a API **de critérios personalizados de** Lista.

## Critérios personalizados de Lista

Para recuperar uma lista de todos os critérios personalizados, juntamente com detalhes de cada um, use a API [de critérios personalizados de](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)Lista. A sintaxe é:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verifique `TENANT_ID` e `API_KEY` como antes e envie a solicitação. Na resposta, observe a ID de critérios personalizados, bem como detalhes sobre a mensagem de erro anotada anteriormente.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

Nesse caso, o erro ocorreu porque as informações do servidor estão incorretas, o que significa que [!DNL Target] não é possível acessar o arquivo CSV que contém a definição de critérios personalizados. Vamos editar os critérios personalizados para corrigir isso.

## Editar critérios personalizados

Para alterar os detalhes de uma definição de critérios personalizados, use a API [](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)Editar critérios personalizados. A sintaxe é:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verifique `TENANT_ID` e `API_KEY`, como antes.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Especifique a ID de critérios dos critérios personalizados (únicos) que você deseja editar.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. No Corpo, forneça JSON atualizado com as informações corretas do servidor. (Para esta etapa, especifique o acesso FTP a um servidor que você possa acessar.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Envie a solicitação e anote a resposta.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Vamos verificar o sucesso dos critérios personalizados atualizados, usando a API **** Obter critérios personalizados.

## Obter critérios personalizados

Para visualização de detalhes de critérios personalizados para um critério personalizado específico, use a API [](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)Obter critérios personalizados. A sintaxe é:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique a ID de critérios dos critérios personalizados cujos detalhes você deseja obter. Envie a solicitação e reveja a resposta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verificar sucesso. (No nosso caso, verifique se não há mais erros de FTP.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Verifique se a atualização reflete com precisão na interface do usuário.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Excluir critérios personalizados

Usando a ID de critérios anotada anteriormente, exclua seus critérios personalizados usando a API [](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)Excluir critérios personalizados. A sintaxe é:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique a ID de critérios dos critérios personalizados (únicos) que você deseja excluir. Clique em **Enviar**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Verifique se os critérios foram excluídos usando Obter critérios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)Nesse caso, o erro 404 esperado indica que os critérios excluídos não foram encontrados.

>[!NOTE]
>Como lembrete, os critérios não serão removidos da [!DNL Target] interface do usuário mesmo que tenham sido excluídos, pois foram criados usando a API Criar critérios personalizados.

Parabéns! Agora você pode criar, lista, editar, excluir e obter detalhes sobre critérios personalizados usando a [!DNL Recommendations] API. Na próxima seção, você usará a API de [!DNL Target] Delivery para recuperar as recomendações.

[Próximo &quot;Busque a Recommendations com a API do Delivery do lado do servidor&quot; >](fetch-recs-server-side-delivery-api.md)
