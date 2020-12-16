---
title: Adicionar solicitações do Adobe Target
description: 'O SDK do Adobe Mobile Services (v4) fornece métodos e funcionalidades da Adobe Target que permitem que você personalize seu aplicativo com diferentes experiências para usuários diferentes.   '
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# Adicionar solicitações do Adobe Target

O SDK do Adobe Mobile Services (v4) fornece métodos e funcionalidades da Adobe Target que permitem que você personalize seu aplicativo com diferentes experiências para usuários diferentes. Normalmente, uma ou mais solicitações são feitas do aplicativo para a Adobe Target para recuperar o conteúdo personalizado e medir o impacto desse conteúdo.

Nesta lição, você preparará o aplicativo We.Travel para personalização implementando [!DNL Target] solicitações.

## Pré-requisitos

Certifique-se de [baixar e atualizar o aplicativo de amostra](download-and-update-the-sample-app.md).

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Armazenar várias ofertas [!DNL Target] em cache (ou seja, conteúdo personalizado) usando uma solicitação de busca prévia em lote
* Carregar locais [!DNL Target] pré-buscados
* Carregar um local [!DNL Target] em tempo real (sem busca prévia)
* Limpar locais pré-buscados do cache
* Validar solicitações pré-buscadas e em tempo real

## Terminologia

Abaixo está uma parte da terminologia principal do Público alvo que será usada no restante deste tutorial.

* **Solicitação:**  uma solicitação de rede para os servidores Adobe Target
* **Oferta:**  um trecho de código ou outro conteúdo com base em texto, definido na interface do  [!DNL Target] usuário (ou com API), que é fornecido na resposta. Geralmente, JSON quando [!DNL Target] é usado em aplicativos móveis nativos.
* **Localização:**  um nome definido pelo usuário fornecido a uma solicitação, usado na  [!DNL Target] interface para associar ofertas a solicitações específicas
* **Solicitação em lote:**  uma única solicitação que inclui vários locais
* **Solicitação de pré-busca:**  uma única solicitação que recupera ofertas e as armazena em cache na memória para uso futuro no aplicativo
* **Solicitação de pré-busca em lote:**  uma única solicitação que pré-busca ofertas para vários locais
* **Audiência:**  um grupo de visitantes definido na  [!DNL Target] interface ou compartilhado com  [!DNL Target] de outros aplicativos Adobe (por exemplo, &quot;visitantes para iPhone X&quot;, &quot;visitantes na Califórnia&quot;, &quot;Abertura do primeiro aplicativo&quot;)
* **Atividade:**  uma  [!DNL Target] construção, definida na interface do  [!DNL Target] usuário (ou com a API) que vincula locais, ofertas e Audiências para criar uma experiência personalizada

## Adicionar uma solicitação de busca prévia em lote

A primeira solicitação que implementaremos em We.Travel é uma solicitação de busca prévia em lote com dois [!DNL Target] locais na tela inicial. Em uma lição posterior, configuraremos ofertas para esses locais que exibem mensagens para ajudar a orientar novos usuários no processo de reserva.

Uma solicitação de busca prévia busca o conteúdo [!DNL Target] o mínimo possível ao armazenar a resposta do servidor Adobe Target em cache (oferta). Uma solicitação de pré-busca em lote recupera e armazena em cache várias ofertas, cada uma associada a um local diferente. Todos os locais pré-buscados são armazenados em cache no dispositivo para uso futuro na sessão do usuário. Ao pré-buscar vários locais na tela inicial, podemos recuperar ofertas para usá-las posteriormente à medida que o visitante navega pelo aplicativo. Consulte a [documentação de busca prévia](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) para obter mais detalhes sobre métodos de busca prévia.

### Adicionar a solicitação de busca prévia em lote

Vamos atualizar o controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.weTravel > Controller. Adicionaremos os dois blocos de código mostrados em vermelho:

Nós teremos o start do controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.weTravel > Controller.

Adicionaremos os dois blocos de código mostrados em vermelho:

![Código de pré-busca HomeActivity](assets/homeactivity.jpg)

Role para baixo até o final do código do HomeActivity e adicione o código fornecido abaixo após a função `setHeader()` e *substituindo* a função `onResume()` atual:

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

Seu IDE provavelmente avisará que você não tem as classes [!DNL Target] importadas no arquivo. Certifique-se de importar as classes [!DNL Target] na parte superior do controlador HomeActivity, como mostrado em vermelho abaixo:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar as classes de Públicos alvos](assets/import.jpg)

Você provavelmente também verá erros para &quot;não é possível localizar a variável de símbolo weTravel_engagement_home&quot; e &quot;não é possível encontrar a variável de símbolo weTravel_contact_search&quot;. Adicione-os ao arquivo `Constant.java` (em app > src > main > java > com > weTravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Adicione os nomes do local ao arquivo Constant.java](assets/constants.jpg)

### Explicação do código de solicitação de pré-busca em lote

| Código | Descrição |
|--- |--- |
| `targetPrefetchContent()` | Uma função definida pelo usuário (não parte do SDK) que usa métodos [!DNL Target] para recuperar e armazenar em cache dois locais [!DNL Target]. |
| `prefetchContent()` | O método SDK [!DNL Target] que envia a solicitação de busca prévia |
| `Constant.wetravel_engage_home` | Nome do local [!DNL Target] pré-obtido que exibirá o conteúdo da oferta na tela inicial |
| `Constant.wetravel_engage_search` | Nome do local [!DNL Target] pré-obtido que exibirá seu conteúdo de oferta na tela Resultados da pesquisa. Como esse é um segundo local na busca prévia, essa solicitação de busca prévia é chamada de &quot;solicitação em lote de busca prévia&quot;. |
| setUp() | Uma função definida pelo usuário que renderiza a tela inicial do aplicativo após a busca prévia das [!DNL Target] ofertas |

### Sobre assíncrono vs. síncrono

Com o código que acabamos de implementar, a solicitação de busca prévia é feita como uma chamada síncrona de bloqueio, antes da tela inicial ser renderizada. Quando colamos o novo código no controlador HomeActivity, movemos a execução da função `setUp()` da função `onResume()` para depois da solicitação do Público alvo. Isso pode ser benéfico em cenários nos quais você deseja personalizar o conteúdo quando o aplicativo é aberto pela primeira vez, pois garante que o conteúdo personalizado dos servidores de Público alvo retorne (ou tenha expirado) antes da primeira renderização de tela. Para permitir que as solicitações sejam carregadas de forma assíncrona (em segundo plano), basta chamar `setUp()` na função `onCreate()` em vez disso.

### Validar a solicitação de pré-busca em lote

Recrie o aplicativo e abra o Android Emulator. (As capturas de tela a seguir usam o Pixel 2 no Android Q versão 9+, nível 29 da API). A resposta de pré-busca deve ler-se &quot;resposta de pré-busca recebida&quot;:

Quando a tela Início for renderizada, a solicitação de busca prévia deverá ser carregada. Com o Logcat, filtre por [!DNL "Target"] para ver a solicitação e a resposta:

![Validar as solicitações na tela inicial](assets/prefetch_validation.jpg)

Se você não estiver vendo uma resposta bem-sucedida, verifique as configurações no arquivo `ADBMobileConfig.json` e na sintaxe do código no arquivo HomeActivity.

Dois locais agora são armazenados em cache no dispositivo. Os nomes de localização serão carregados lentamente em breve na interface [!DNL Target], onde podem ser selecionados em vários menus suspensos quando você os usa em uma atividade.

### Adicionar solicitações de carregamento para cada localização em cache

Agora que os locais são pré-buscados e suas respostas são armazenadas em cache no dispositivo, vamos adicionar o método `Target.loadRequest()` que recupera o conteúdo da oferta do cache para que você possa usá-lo para atualizar seu aplicativo. Adicionaremos um novo método personalizado chamado `engageMessage()` que será executado com a solicitação de busca prévia. `engageMessage()` ligará  `Target.loadRequest()`. `engageMessage()` é executado antes  `setUp()` para garantir que a solicitação de carregamento seja chamada antes da tela ser configurada.

Primeiro, adicione a chamada e o método `engageMessage()` para o local weTravel_engagement_home no HomeActivity:

![Adicionar primeira solicitação de carregamento](assets/wetravel_engage_home_loadRequest.jpg)

Este é o código atualizado:

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Agora, adicione a chamada e o método `engageMessage()` para o local de pesquisa_weTravel_involved_search no SearchBusActivity. Observe que a chamada `engageMessage()` está definida no método `onResume()` antes da chamada para `setUpSearch()` para que ela seja executada antes da tela ser configurada:

![Adicionar segunda solicitação de carregamento](assets/wetravel_engage_search_loadRequest.jpg)

Este é o código atualizado:

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Como você acabou de adicionar métodos de Público alvo ao SearchBusActivity, certifique-se de importar as classes [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Adicionar uma solicitação em tempo real

A próxima solicitação que adicionaremos ao aplicativo será uma solicitação em tempo real na tela Obrigado. Por &quot;tempo real&quot;, significa que a solicitação será feita e a resposta será aplicada imediatamente (não será armazenada em cache para mais tarde). Em uma lição posterior, criaremos uma experiência usando essa solicitação, que é personalizada para o destino de viagem do usuário.

Então vamos adicionar uma solicitação em tempo real na tela Obrigado. No arquivo ObrigadoAtividade, fazemos as alterações mostradas em vermelho:
![Adicione um local em tempo real na tela de agradecimento](assets/thankyou.jpg)

Role até o final do arquivo ObrigadoAtividade. Comente as três linhas na função `getRecommandations()` e adicione a invocação da função `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Adicione essa linha de código à função `getRecommandations()`:

```java
targetLoadRequest(recommandation.recommandations);
```

Agora, precisamos definir a função `targetLoadRequest()`:
![Adicione um local em tempo real na tela de agradecimento](assets/thankyou2.jpg)

Adicione este bloco de código após a função `filterRecommendationBasedOnOffer()`:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

Como você acabou de adicionar métodos de Público alvo à atividade de agradecimento, certifique-se de importar as classes de Público alvo:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest() Code Explication

| Código | Descrição |
|--- |--- |
| `targetLoadRequest()` | Uma função definida pelo usuário (não parte do SDK) que aciona `Target.loadRequest()` que carrega e exibe o local weTravel_context_dest |
| `Target.loadRequest()` | O método SDK que faz a solicitação para o servidor do Público alvo |
| Constant.wetravel_context_dest | O nome do local atribuído à solicitação que usaremos posteriormente quando construirmos a atividade na interface [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Uma função definida pelo usuário no aplicativo que tira a oferta do local da resposta do Público alvo e decide como o aplicativo deve ser alterado com base no conteúdo da oferta |
| `recommandations.addAll()` | Uma função definida pelo usuário no aplicativo que era executada por padrão quando a tela Obrigado era carregada, mas agora é executada após a resposta do Público alvo ser recebida e analisada por `filterRecommendationBasedOnOffer()` |

Esta foi uma atualização mais sofisticada que fizemos ao aplicativo na época com a solicitação que adicionamos à tela inicial, então vamos levar um momento para rever o que fizemos:

1. Interrompemos o comportamento anterior do aplicativo de mostrar três promoções padrão, comentando as linhas de código
1. Em vez disso, pedimos ao aplicativo para executar uma nova função, que nomeamos arbitrariamente como targetLoadRequest
1. Definimos a função `targetLoadRequest` para fazer uma solicitação ao Público alvo usando o método Público alvo.loadRequest e executar imediatamente a função `filterRecommendationBasedOnOffer()` quando a resposta de oferta [!DNL Target] for recebida
1. A função `filterRecommendationBasedOnOffer()` interpreta a resposta e decide quais promoções devem ser aplicadas à tela

Este é um padrão de uso muito comum ao usar [!DNL Target] em aplicativos móveis.  Ele é muito poderoso, pois você pode personalizar quase todos os aspectos do seu aplicativo móvel. Também requer coordenação entre o código do aplicativo e as ofertas que definiremos posteriormente na interface [!DNL Target]. Devido a essa coordenação, alguns casos de uso de personalização podem exigir que você atualize seu aplicativo na app store para iniciar a atividade.

### Validar a solicitação em tempo real

Abra o Android Emulator e siga todas as etapas para reservar uma viagem: Home > Resultados da pesquisa de barramento > Seleção de assento, Opções de pagamento (qualquer opção de pagamento com dados em branco funcionará).

Na tela final de Agradecimentos, assista Logcat pela resposta. A resposta deve ler &quot;O conteúdo padrão foi retornado para &quot;weTravel_context_dest&quot;:

![Adicionar um local em tempo real na tela de agradecimento](assets/thankyou_validation.jpg)

## Limpando locais pré-selecionados do cache

Pode haver situações em que locais pré-buscados precisam ser apagados durante uma sessão. Por exemplo, quando uma reserva ocorre, faz sentido limpar os locais em cache, já que o usuário agora está &quot;engajado&quot; e entende o processo de reserva. Se eles fizerem outra viagem durante a sessão, não precisarão dos locais originais na tela inicial e na tela de resultados da pesquisa para orientar sua reserva. Seria mais lógico limpar os locais do cache e buscar novas ofertas para talvez um segundo agendamento ou outro cenário relevante. A lógica pode ser adicionada à tela inicial e à tela de resultados da pesquisa para realizar uma busca prévia em novos locais se uma reserva tiver ocorrido durante a sessão.

Neste exemplo, nós apenas limparemos os locais pré-buscados para a sessão quando uma reserva ocorrer. Isso é feito chamando a função `Target.clearPrefetchCache()`. Defina a função dentro da função `targetLoadRequest()` como mostrado abaixo:

```java
Target.clearPrefetchCache()
```

![Limpar locais pré-selecionados do cache](assets/clearPrefetch.jpg)

Parabéns! Seu aplicativo agora tem a estrutura para personalização. Na próxima lição, aprimoraremos nossos recursos de personalização adicionando parâmetros a esses locais.

**[PRÓXIMO : &quot;Adicionar parâmetros&quot; >](add-parameters.md)**
