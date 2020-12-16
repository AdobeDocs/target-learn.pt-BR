---
title: Adicionar parâmetros às solicitações
description: Nesta lição, adicionaremos medições de ciclo de vida do Adobe e parâmetros personalizados às solicitações do Público alvo adicionadas na lição anterior. Essas métricas e parâmetros serão usados para criar audiências personalizadas posteriormente no tutorial.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Adicionar parâmetros às solicitações

Nesta lição, adicionaremos medições de ciclo de vida de Adobe e parâmetros personalizados às solicitações [!DNL Target] adicionadas na lição anterior. Essas métricas e parâmetros serão usados para criar audiências personalizadas posteriormente no tutorial.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Adicionar as medições de ciclo de vida do Adobe para dispositivos móveis
* Adicionar parâmetros a uma solicitação de busca prévia
* Adicionar parâmetros a um local ativo
* Validar os parâmetros para ambas as solicitações

## Adicionar os parâmetros de ciclo de vida

Vamos ativar as [medições de ciclo de vida móvel do Adobe](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). Isso adicionará parâmetros a solicitações de localização que contêm informações avançadas sobre o dispositivo do usuário e o envolvimento com o aplicativo. Criaremos audiências na próxima lição usando os dados fornecidos pela solicitação do ciclo de vida.

Para ativar as medições de ciclo de vida, abra novamente o controlador HomeActivity e adicione `Config.collectLifecycleData(this);` à função onResume():

![Solicitação de ciclo de vida](assets/lifecycle_code.jpg)

### Validar os parâmetros de ciclo de vida para a solicitação de pré-busca

Execute o Emulador e use o Logcat para validar os parâmetros do ciclo de vida. Filtre por &quot;busca prévia&quot; para localizar a resposta de busca prévia e procurar os novos parâmetros:
![Validação do ciclo de vida](assets/lifecycle_validation.jpg)

Mesmo que tenhamos adicionado `Config.collectLifecycleData()` apenas ao controlador HomeActivity, você também deve ver as medições de ciclo de vida enviadas com a solicitação de Público alvo na tela Obrigado.

## Adicionar o parâmetro at_property à solicitação de busca prévia

As Propriedades do Adobe Target são definidas na interface [!DNL Target] e são usadas para estabelecer limites para personalizar aplicativos e sites. O parâmetro at_property identifica a propriedade específica na qual suas ofertas e atividades são acessadas e mantidas. Adicionaremos uma propriedade às solicitações de busca prévia e de localização ativa.

>[!NOTE]
>
>Você pode ou não ver as opções de Propriedades na interface [!DNL Target], dependendo da sua licença. Se você não tiver essas opções, ou se não usar Propriedades na empresa, vá para a próxima seção desta lição.

Você pode recuperar o valor at_property na interface [!DNL Target] em [!UICONTROL Setup] > [!UICONTROL Properties].  Passe o cursor do mouse sobre a propriedade, selecione o ícone do trecho de código e copie o valor `at_property`:

![Copiar na_propriedade](assets/at_property_interface.jpg)

Adicione-o como um parâmetro para cada localização na solicitação de busca prévia, como esta:
![Adicionar parâmetro at_property](assets/params_at_property.jpg)
Este é o código atualizado para a função `targetPrefetchContent()` (certifique-se de atualizar o _[!UICONTROL seu valor at_property vai para aqui]_ texto do espaço reservado!):

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

Para projetos futuros, você pode implementar parâmetros adicionais. O método `createTargetPrefetchObject()` permite três tipos de parâmetros: `locationParams`, `orderParams` e `productParams`. Consulte a documentação para obter mais detalhes sobre como adicionar esses parâmetros à solicitação de busca prévia[.](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)

Observe também que diferentes parâmetros de localização podem ser adicionados a cada local na solicitação de busca prévia. Por exemplo, você pode criar outro Mapa chamado param2, colocar um novo parâmetro nele e, em seguida, definir param2 em um local e param1 com o outro local. Veja um exemplo:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validar o parâmetro at_property na solicitação de busca prévia

Agora execute o emulador e use o Logcat para verificar se a propriedade at_está sendo exibida na solicitação de busca prévia e na resposta para ambos os locais:
![Valide o parâmetro at_property](assets/parameters_at_property_validation.jpg)

## Adicionar Parâmetros Personalizados à Solicitação de Localização em Tempo Real

A solicitação de local ativo (weTravel_context_dest) foi adicionada na lição anterior para que pudéssemos exibir uma promoção relevante na tela de confirmação final do processo de reserva. Gostaríamos de personalizar a promoção com base no destino do usuário e, para isso, adicionaremos isso como parâmetro à solicitação. Também adicionaremos um parâmetro para a origem trop e o valor at_property.

Adicione os seguintes parâmetros à função targetLoadRequest() no controlador ObrigadoActivity:
![Adicionar Parâmetros à Solicitação de Localização em Tempo Real](assets/parameters_live_location.jpg)
Este é o código atualizado para a função targetLoadRequest() (atualize o texto do espaço reservado &quot;add your at_property value here&quot;):

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

### Validar os Parâmetros Personalizados na Solicitação de Localização em Tempo Real

Execute o emulador e abra o Logcat. Filtre um dos parâmetros para verificar se a solicitação contém os parâmetros necessários:
![Valide os Parâmetros Personalizados no Live Location Request](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Solicitações e parâmetros de confirmação de pedido: Embora não seja usado neste projeto de demonstração, os detalhes do pedido são geralmente capturados em uma implementação real, de modo que [!DNL Target] pode usar os detalhes do pedido como métricas/dimensões. Consulte a documentação para obter instruções sobre como [implementar a solicitação de confirmação de pedido e os parâmetros](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html).

>[!NOTE]
>
>Analytics for Público alvo (A4T): O Adobe Analytics pode ser configurado como a origem do relatórios para [!DNL Target]. Isso permite que todas as métricas/dimensões coletadas pelo SDK do Público alvo sejam visualizadas no Adobe Analytics. Consulte [Visão geral do A4T](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) para obter mais detalhes.

Bom trabalho! Agora que os parâmetros estão em vigor, estamos prontos para usar esses parâmetros para criar audiências e ofertas no Adobe Target.

**[PRÓXIMO : &quot;Criar Audiências e Ofertas&quot; >](create-audiences-and-offers.md)**
