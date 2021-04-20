---
title: Criar públicos e ofertas no Adobe Target
description: 'Nesta lição, criamos públicos e ofertas no Adobe Target para os três locais que implementamos nas lições anteriores. Eles serão usados para exibir experiências personalizadas na próxima lição.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---


# Criar públicos e ofertas no Adobe Target

Nesta lição, entraremos na interface [!DNL Target] e criaremos públicos e ofertas para os três locais que implementamos nas lições anteriores.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Criar públicos-alvo no Adobe Target
* Criar ofertas no Adobe Target

Mais especificamente, nesta lição, criaremos públicos e ofertas necessários para realizar os casos de uso de personalização definidos no início do tutorial. Queremos usar as telas Início e Pesquisa para ajudar os usuários do aplicativo a reservar suas viagens e queremos usar a tela Agradecimentos para exibir algumas promoções relevantes com base no destino do usuário. Esta é uma tabela que representa o que criaremos nesta lição para cada local:

| Localização | Público-alvo | Oferta |
| --- | --- | --- |
| weTravel_engagement_home | Novos usuários de aplicativos móveis | &quot;Selecione a Origem e o Destino para procurar as rotas de barramento disponíveis&quot; |
| web_training_search | Novos usuários de aplicativos móveis | &quot;Use filtros para restringir seus resultados de pesquisa&quot; |
| weTravel_engagement_home | Retornar usuários de aplicativos móveis | &quot;Bem-vindo de volta! Use o código promocional BACK30 durante o check-out para obter um desconto de 10%.&quot; |
| web_training_search | Retornar usuários de aplicativos móveis | conteúdo padrão |
| weTravel_context_dest | Destino: San Diego | &quot;DJ&quot; |
| weTravel_context_dest | Destino: Los Angeles | &quot;Universal&quot; |

## Selecione seu espaço de trabalho

Se sua empresa usa Propriedades e espaços de trabalho para estabelecer limites para personalizar aplicativos e sites, e você implementou o parâmetro at_property na última lição, primeiro verifique se você está no espaço de trabalho correto antes de prosseguir com esta lição. Se você não usar Propriedades e espaços de trabalho, ignore esta etapa. Selecione o Espaço de trabalho usado na lição anterior para copiar o valor at_property:

![Exemplo de espaço de trabalho](assets/workspace.jpg)

## Criar públicos-alvo

Agora vamos criar os públicos-alvo que usaremos para personalizar o aplicativo.

### Criar um público-alvo para novos usuários

Públicos-alvo da Adobe Target são usados para identificar grupos específicos de visitantes. As ofertas podem então ser direcionadas para esses grupos específicos. Nos dois primeiros locais, usaremos um público-alvo de &quot;Novos usuários&quot;:

1. Clique em **[!UICONTROL Públicos-alvo]** na navegação superior.
1. Clique no botão **[!UICONTROL Criar público-alvo]**.
   ![Criar um novo público-alvo de usuário](assets/audience_new_mobile_app_users_1.jpg)

1. Insira **[!UICONTROL New Mobile App Users]** como o nome do público.
1. Selecione **[!UICONTROL Adicionar Regra]**.
1. Selecione uma regra **[!UICONTROL Personalizada]**.
   ![Criar um novo público-alvo de usuário](assets/audience_new_mobile_app_users_2.jpg)

1. Selecione **[!UICONTROL a.Launches]**.
1. Selecione **[!UICONTROL é menor que]**.
1. Insira **5**.
1. Salve o novo público.
   ![Criar um novo público-alvo de usuário](assets/audience_new_mobile_app_users_3.jpg)

### Criar um público-alvo para usuários recorrentes

Siga as mesmas etapas listadas acima para criar um público-alvo para usuários recorrentes.

1. Nomeie o público-alvo como _Usuários do aplicativo móvel que retornam_.
1. Usar **[!UICONTROL a.Launches é maior ou igual a 5]** como regra personalizada.
1. Salve o novo público.

   ![Criar um público-alvo de usuário recorrente](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>Todas as Medições de ciclo de vida e dimensões coletadas no SDK móvel [!DNL Target] são anexadas a &quot;a&quot; (por exemplo, a.Launches) e estão disponíveis na opção &quot;Personalizado&quot; do menu suspenso e podem ser usadas para criar públicos-alvo.

### Crie um público-alvo para usuários que estão reservando uma viagem para San Diego

Em seguida, criaremos alguns públicos-alvo para alguns dos destinos oferecidos pelo aplicativo We.Travel. Na última lição, passamos o destino como um parâmetro de localização na solicitação de local weTravel_context_dest. Esse parâmetro está disponível na opção &quot;Personalizado&quot; do menu suspenso.

>[!NOTE]
>
>Se um parâmetro que você espera ver na lista suspensa Personalizado não aparecer na interface [!DNL Target] , verifique novamente se ele está realmente sendo transmitido na solicitação. Se tiver verificado que está na solicitação, mas não foi carregado lentamente na interface [!DNL Target], você pode digitar o nome do parâmetro e pressionar Enter para continuar definindo seu público-alvo

1. Nomeie o público _Destino: San Diego_.
1. Use uma regra personalizada com esta definição: _locationDest contém San Diego_.
1. Salve o novo público.

   ![Criar público-alvo do &quot;San Diego&quot;](assets/audience_locationDest_san_diego.jpg)

### Crie um público-alvo para usuários que estão reservando uma viagem para Los Angeles

1. Nomeie o público _Destino: Los Angeles_
1. Use uma regra personalizada com esta definição: _locationDest contém Los Angeles_
1. Salve o novo público.

![Criar público-alvo de &quot;Los Angeles&quot;](assets/audience_locationDest_los_angeles.jpg)

## Crie ofertas

Agora, vamos criar ofertas para exibir essas mensagens. Como lembrete, as ofertas são trechos de código/conteúdo, que são fornecidos na resposta [!DNL Target]. Eles são criados com mais frequência na interface do usuário [!DNL Target], mas também podem ser criados por meio da API ou usando a integração dos Fragmentos de experiência com o Adobe Experience Manager. Em aplicativos móveis, as ofertas JSON são comuns. Neste tutorial, estaremos usando ofertas HTML, que podem ser usadas para fornecer qualquer conteúdo de texto simples (incluindo JSON) ao aplicativo.

### Criar a oferta para novos usuários

Primeiro, vamos criar ofertas para as mensagens para novos usuários:

1. Clique em **[!UICONTROL Offers]** na navegação superior.
1. Clique em **[!UICONTROL Criar]**.
1. Selecione **[!UICONTROL Oferta HTML]**.

   ![Criar Oferta Inicial](assets/offer_home_1.jpg)

1. Dê um nome para a oferta _Início: Envolva novos usuários_.
1. Insira _Select Source and Destination para procurar os barramentos disponíveis_ como o código.
1. Salve a nova oferta.

   ![Criar oferta HTML inicial](assets/offer_home_2.jpg)

### Criar a oferta para usuários recorrentes

Agora vamos criar a oferta única para usuários recorrentes (a segunda oferta será conteúdo padrão, que será exibido como nada):

1. Dê um nome para a oferta _Início: Retornando usuários_.
1. Digite _Bem-vindo de volta! Use o código promocional BACK30 durante o check-out para obter um desconto de 10%._ como o código HTML.
1. Salve a nova oferta.

   ![Criar oferta HTML inicial](assets/offer_home_returning_users.jpg)

### Crie a oferta de San Diego

Quando &quot;DJ&quot; for retornado para a atividade ThankYou , a lógica na função filterRecommendationOnOffer() exibirá um banner para &quot;Rock Night with DJ SAM&quot;:

1. Dê um nome para a oferta _Promoção para San Diego_.
1. Insira _DJ_ como o código HTML.
1. Salve a nova oferta.

![Criar oferta de &quot;San Diego&quot;](assets/offer_san_diego.jpg)

### Criar oferta para usuários indo para Los Angeles

Quando &quot;Universal&quot; for retornado à atividade de Obrigado, a lógica na função filterRecommendationOnOffer() exibirá um banner para &quot;Universal Studios&quot; será exibida:

1. Nomeie a oferta como _Promoção para Los Angeles_.
1. Insira _Universal_ como o código HTML.
1. Salve a nova oferta.

![Criar oferta de &quot;Los Angeles&quot;](assets/offer_los_angeles.jpg)

## Conclusão 

Agora temos nossos Públicos-alvo e Ofertas. Na próxima lição, criaremos atividades que unem os locais, públicos e ofertas para criar as experiências personalizadas!

**[PRÓXIMO : &quot;Personalizar layouts&quot; >](personalize-layouts.md)**
