---
title: Adicionar parâmetros às solicitações
description: Nesta lição, adicionaremos medições de ciclo de vida do Adobe e parâmetros personalizados às solicitações do Target adicionadas na lição anterior. Essas métricas e parâmetros serão usados para criar públicos personalizados posteriormente no tutorial.
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
source-wordcount: '835'
ht-degree: 0%

---


# Adicionar parâmetros às solicitações

Nesta lição, adicionaremos medições de ciclo de vida do Adobe e parâmetros personalizados às solicitações [!DNL Target] adicionadas na lição anterior. Essas métricas e parâmetros serão usados para criar públicos personalizados posteriormente no tutorial.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Adicionar as medições de ciclo de vida do Adobe Mobile
* Adicionar parâmetros a uma solicitação de pré-busca
* Adicionar parâmetros a um local ativo
* Validar os parâmetros de ambas as solicitações

## Adicionar os parâmetros de ciclo de vida

Vamos ativar as [medições de ciclo de vida móvel do Adobe](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). Isso adicionará parâmetros às solicitações de localização contendo informações avançadas sobre o dispositivo do usuário e o envolvimento com o aplicativo. Criaremos públicos na próxima lição usando dados que a solicitação do ciclo de vida fornecer.

Para ativar as medições de ciclo de vida, abra o controlador HomeActivity novamente e adicione `Config.collectLifecycleData(this);` à função onResume() :

![Solicitação de ciclo de vida](assets/lifecycle_code.jpg)

### Validar os parâmetros do ciclo de vida para a solicitação de busca prévia

Execute o Emulador e use o Logcat para validar os parâmetros do ciclo de vida. Filtre por &quot;pré-busca&quot; para encontrar a resposta da pré-busca e procurar os novos parâmetros:
![Validação do Ciclo de Vida](assets/lifecycle_validation.jpg)

Mesmo que tenhamos adicionado apenas `Config.collectLifecycleData()` ao controlador HomeActivity, você deve ver as medições de ciclo de vida enviadas com a solicitação do Target em sua tela de agradecimento também.

## Adicionar o parâmetro at_property à solicitação de busca prévia

As propriedades do Adobe Target são definidas na interface [!DNL Target] e são usadas para estabelecer limites para personalizar aplicativos e sites. O parâmetro at_property identifica a propriedade específica na qual suas ofertas e atividades são acessadas e mantidas. Adicionaremos uma propriedade à busca prévia e às solicitações de localização ativa.

>[!NOTE]
>
>Você pode ou não ver as opções de Propriedades na interface [!DNL Target], dependendo da sua licença. Se você não tiver essas opções, ou se não usar as Propriedades na empresa, pule para a próxima seção desta lição.

Você pode recuperar o valor de at_property na interface [!DNL Target] em [!UICONTROL Setup] > [!UICONTROL Properties].  Passe o mouse sobre a propriedade, selecione o ícone do trecho de código e copie o valor `at_property`:

![Copiar at_property](assets/at_property_interface.jpg)

Adicione-o como um parâmetro para cada local na solicitação de pré-busca como esta:
![Adicionar parâmetro at_property](assets/params_at_property.jpg)
Este é o código atualizado para a função `targetPrefetchContent()` (certifique-se de atualizar o _[!UICONTROL seu valor at_property vai aqui]_ texto de espaço reservado!):

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Observação sobre parâmetros

Para projetos futuros, você pode implementar parâmetros adicionais. O método `createTargetPrefetchObject()` permite três tipos de parâmetros: `locationParams`, `orderParams` e `productParams`. Consulte a documentação para [mais detalhes sobre como adicionar esses parâmetros à solicitação de pré-busca](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html).

Observe também que diferentes parâmetros de localização podem ser adicionados a cada local na solicitação de pré-busca. Por exemplo, você pode criar outro Mapa chamado param2, colocar um novo parâmetro nele e, em seguida, definir param2 em um local e param1 com o outro local. Veja um exemplo:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validar o parâmetro at_property na solicitação de busca prévia

Agora execute o emulador e use o Logcat para verificar se a at_property está sendo exibida na solicitação de pré-busca e na resposta para ambos os locais:
![Validar o parâmetro at_property](assets/parameters_at_property_validation.jpg)

## Adicionar parâmetros personalizados à solicitação de local em tempo real

A solicitação de local ativo (weTravel_context_dest) foi adicionada na lição anterior para podermos exibir uma promoção relevante na tela de confirmação final do processo de reserva. Gostaríamos de personalizar a promoção com base no destino do usuário e, para isso, adicionaremos isso como parâmetro à solicitação. Também adicionaremos um parâmetro para a origem do trop e o valor de at_property.

Adicione os seguintes parâmetros à função targetLoadRequest() no controlador ThankYouActivity:
![Adicionar Parâmetros à Solicitação de Local ao Vivo](assets/parameters_live_location.jpg)
Este é o código atualizado da função targetLoadRequest() (certifique-se de atualizar o texto do espaço reservado &quot;adicionar seu valor at_property aqui&quot;!):

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Validar os parâmetros personalizados na solicitação de local em tempo real

Execute o emulador e abra o Logcat. Filtre um dos parâmetros para verificar se a solicitação contém os parâmetros necessários:
![Validar os Parâmetros Personalizados no Pedido de Localização em Tempo Real](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Solicitações e parâmetros de confirmação de pedido: Embora não seja usado neste projeto de demonstração, os detalhes do pedido geralmente são capturados em uma implementação real, de modo que [!DNL Target] pode usar os detalhes do pedido como métricas/dimensões. Consulte a documentação para obter instruções sobre como [implementar a solicitação de confirmação de pedido e os parâmetros](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html).

>[!NOTE]
>
>Analytics for Target (A4T): O Adobe Analytics pode ser configurado como a fonte de relatórios para [!DNL Target]. Isso permite que todas as métricas/dimensões coletadas pelo SDK do Target sejam visualizadas no Adobe Analytics. Consulte a [Visão geral do A4T](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) para obter mais detalhes.

Bom trabalho! Agora que os parâmetros estão em vigor, estamos prontos para usar esses parâmetros para criar públicos e ofertas no Adobe Target.

**[PRÓXIMO : &quot;Criar públicos e ofertas&quot; >](create-audiences-and-offers.md)**
