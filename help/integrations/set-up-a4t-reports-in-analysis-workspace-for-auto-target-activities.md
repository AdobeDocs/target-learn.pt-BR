---
title: Como configurar relatórios do A4T no Analysis Workspace para atividades de direcionamento automático
description: Depois que a integração do Analytics for Target (A4T) estiver em vigor e você estiver executando atividades de Direcionamento automático, como você pode garantir que está interpretando os resultados corretamente? Siga estas etapas para configurar relatórios do A4T no Analysis Workspace para obter os resultados esperados ao executar atividades de Direcionamento automático.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 2571964b557f696d8e0377b922d96e90611f2327
workflow-type: tm+mt
source-wordcount: '2639'
ht-degree: 1%

---

# Configuração de relatórios do A4T em [!DNL Analysis Workspace] para [!DNL Auto-Target] atividades

>[!IMPORTANT]
>
>Para [!UICONTROL Direcionamento automático] você deve verificar os relatórios em [!DNL Analytics Workspace] e criar manualmente um painel A4T.

O [!UICONTROL Analytics para Target] Integração do (A4T) para [!DNL Auto-Target] usos de atividades [!DNL Adobe Target]Os algoritmos do conjunto de aprendizado de máquina (ML) do para escolher a melhor experiência para cada visitante com base em seu perfil, comportamento e contexto, enquanto usa um [!DNL Adobe Analytics] métrica de meta.

Embora os recursos de análise avançada estejam disponíveis em [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão **[!UICONTROL Analytics para Target]** são necessários para interpretar corretamente o painel [!DNL Auto-Target] atividades, devido a diferenças entre as atividades de experimentação (A/B manual e Alocação automática) e as atividades de personalização ([!UICONTROL Direcionamento automático]).

Este tutorial aborda as modificações recomendadas para analisar [!UICONTROL Direcionamento automático] atividades em [!DNL Workspace], que se baseiam nos seguintes conceitos principais:

* O **[!UICONTROL Controle vs. Direcionado]** pode ser usada para distinguir entre as experiências de controle e as fornecidas pela variável [!UICONTROL Direcionamento automático] algoritmo do conjunto ML.
* As Visitas devem ser usadas como a métrica de normalização ao visualizar detalhamentos de desempenho no nível da experiência. Além disso, [A metodologia de contagem padrão da Adobe Analytics pode incluir visitas em que o usuário não vê realmente o conteúdo da atividade](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), mas esse comportamento padrão pode ser modificado usando um segmento com escopo apropriado (detalhes abaixo).
* A atribuição de escopo de retrospectiva de visita - também conhecida como &quot;janela de retrospectiva de visita&quot; no modelo de atribuição prescrito - é usada por [!DNL Adobe Target]Os modelos ML de s durante suas fases de treinamento e o mesmo modelo de atribuição (não padrão) devem ser usados ao detalhar a métrica de meta.

## Criar o A4T para [!UICONTROL Direcionamento automático] no painel [!DNL Workspace]

Para criar um A4T para [!UICONTROL Direcionamento automático] , comece com **[!UICONTROL Analytics para Target]** no painel [!DNL Workspace], como mostrado abaixo, ou comece com uma tabela de forma livre. Em seguida, faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: Você pode escolher qualquer experiência; no entanto, você substituirá essa opção posteriormente. Observe que para [!UICONTROL Direcionamento automático] , a experiência de controle é realmente uma estratégia de controle, que é a) Servir aleatoriamente entre todas as experiências ou b) Servir uma única experiência (essa escolha é feita no momento da criação da atividade em [!DNL Adobe Target]). Mesmo que você tenha optado pela escolha (b): [!UICONTROL Direcionamento automático] atividade designada como Controle — você ainda deve seguir a abordagem descrita neste tutorial para analisar o A4T para [!UICONTROL Direcionamento automático] atividades.
2. **[!UICONTROL Métrica de normalização]**: Selecione Visitas.
3. **[!UICONTROL Métricas de sucesso]**: Embora seja possível selecionar qualquer métrica para gerar relatórios, geralmente é necessário visualizar os relatórios sobre a mesma métrica que foi escolhida para otimização durante a criação da atividade em [!DNL Target].

![Figura1.png](assets/Figure1.png)
*Figura 1: [!UICONTROL Analytics para Target] configuração do painel para [!UICONTROL Direcionamento automático] atividades.*

>[!NOTE]
>
>Para configurar o [!UICONTROL Analytics para Target] painel para [!UICONTROL Direcionamento automático] , escolha qualquer experiência de controle, escolha [!UICONTROL Visitas] como a métrica de normalização e escolha a mesma métrica de meta que foi escolhida para otimização durante [!DNL Target] criação da atividade.

## Use o [!UICONTROL Controle vs. segmentado] para comparar a dimensão [!DNL Target] agrupe o modelo ML no seu controle

O painel A4T padrão foi projetado para testes A/B clássicos (manuais) ou [!UICONTROL Alocação automática] atividades nas quais o objetivo é comparar o desempenho de experiências individuais com a experiência de Controle. Em [!UICONTROL Direcionamento automático] , no entanto, a primeira comparação de pedidos deve ser entre o Controle *estratégia* e o Target *estratégia* (em outras palavras, determinar o aumento do desempenho geral do [!UICONTROL Direcionamento automático] modelo de conjunto ML sobre a estratégia de controle).

Para executar essa comparação, use o **[!UICONTROL Controle versus Direcionado (Analytics for Target)]** dimensão. Arraste e solte para substituir o **[!UICONTROL Experiências do Target]** no relatório A4T padrão.

Observe que essa substituição invalida os cálculos padrão de Aumento e Confiança no painel A4T. Para evitar confusão, você pode remover essas métricas do painel padrão, deixando o seguinte relatório:

![Figura 2.png](assets/Figure2.png)

*Figura 2: O relatório de linha de base recomendado para [!DNL Auto-Target] atividades. Este relatório foi configurado para comparar o tráfego Direcionado (servido pelo modelo ML do conjunto) com seu tráfego de Controle.*

>[!NOTE]
>
>Atualmente, os números de Lift e Confidence não estão disponíveis para [!UICONTROL Controle vs. Direcionado] dimensões para relatórios A4T para [!UICONTROL Direcionamento automático]. Até que o suporte seja adicionado, o Aumento e a Confiança podem ser calculados manualmente ao baixar a variável [calculadora de confiança](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Adicionar detalhamentos de métricas no nível da experiência

Para obter mais informações sobre o desempenho do modelo ML do conjunto, você pode examinar os detalhamentos no nível da experiência do **[!UICONTROL Controle vs. Direcionado]** dimensão. Em [!DNL Workspace], arraste a **[!UICONTROL Experiências do Target]** no relatório e detalhe cada uma das dimensões de Controle e Direcionado separadamente.

![Figura 3.png](assets/Figure3.png)
*Figura 3: Detalhamento da dimensão Direcionada por experiências do Target*

Um exemplo do relatório resultante é mostrado aqui.

![Figura 4.png](assets/Figure4.png)
*Figura 4: Padrão [!UICONTROL Direcionamento automático] com detalhamentos de nível de experiência. Observe que sua métrica de meta pode ser diferente, e sua estratégia de Controle pode ter uma única experiência.*

>[!TIP]
>
>Em [!DNL Workspace], clique no ícone de engrenagem para ocultar as Porcentagens no [!UICONTROL Índice de conversão] para ajudar a manter o foco nas taxas de conversão da experiência. Observe que as taxas de conversão serão formatadas como decimais, mas interprete-as como porcentagens de acordo.

## Por que &quot;Visitas&quot; é a métrica de normalização correta para [!UICONTROL Direcionamento automático] atividades

Ao analisar uma [!UICONTROL Direcionamento automático] atividade , sempre escolha [!UICONTROL Visitas] como a métrica de normalização padrão. [!UICONTROL Direcionamento automático] a personalização seleciona uma experiência para um visitante uma vez por visita (formalmente, uma vez por [!DNL Adobe Target] sessão), o que significa que a experiência mostrada a um usuário pode mudar em cada visita única. Assim, se você usar [!UICONTROL Visitantes únicos] como a métrica de normalização, o fato de que um único usuário pode acabar visualizando várias experiências (em diferentes visitas) levaria a taxas de conversão confusas.

Um exemplo simples demonstra esse ponto: considere um cenário em que dois visitantes acessam uma campanha com apenas duas experiências. O primeiro visitante visita duas vezes. Eles são atribuídos à Experiência A na primeira visita, mas à Experiência B na segunda visita (devido ao estado do perfil ter mudado na segunda visita). Após a segunda visita, o visitante é convertido ao fazer um pedido. A conversão é atribuída à experiência exibida mais recentemente (Experiência B). O segundo visitante também visita duas vezes e a Experiência B é exibida duas vezes, mas nunca converte.

Vamos comparar os relatórios a nível de visitante e a nível de visita:

| Experiência | Visitantes únicos | Visitas | Conversões | Norma do visitante. Conv. Taxa | Norma de visita. Conv. Taxa |
| --- | --- | --- | --- | --- | --- |
| Um | 1 | 1 | - | 0% | 0% |
| B  | 2 | 3 | 1 | 50% | 33,3% |
| Totais | 2 | 4 | 1 | 50% | 25% |

*Quadro 1: Exemplo que compara relatórios normalizados de visitantes e relatórios normalizados de visitas para um cenário em que as decisões são aderentes a uma visita (e não a um visitante, como com testes A/B regulares). Métricas normalizadas do visitante são confusas nesse cenário.*

Conforme mostrado na tabela, há uma clara incongruência de números no nível do visitante. Apesar do fato de haver dois visitantes únicos totais, essa não é uma soma de visitantes únicos individuais para cada experiência. Embora a taxa de conversão no nível do visitante não esteja necessariamente errada, quando você compara experiências individuais, as taxas de conversão no nível da visita provavelmente fazem muito mais sentido. Formalmente, a unidade de análise (&quot;visitas&quot;) é a mesma que a unidade de decisão, o que significa que os detalhamentos das métricas no nível da experiência podem ser adicionados e comparados.

## Filtrar as visitas reais à atividade

O [!DNL Adobe Analytics] metodologia de contagem padrão para visitas a um [!DNL Target] A atividade pode incluir visitas nas quais o usuário não interagiu com a [!DNL Target] atividade . Isso se deve à maneira como [!DNL Target] as atribuições de atividade são mantidas no [!DNL Analytics] contexto do visitante. Como resultado, o número de visitas ao [!DNL Target] às vezes, a atividade pode ser inflacionada, resultando em uma depressão das taxas de conversão.

Se você preferir relatar sobre visitas em que o usuário interagiu com o [!UICONTROL Direcionamento automático] atividade (por meio de uma entrada para a atividade, um evento de exibição/visita ou uma conversão), é possível:

1. Crie um segmento específico que inclua ocorrências do [!DNL Target] em questão e, em seguida,
1. Filtre o [!UICONTROL Visitas] usando este segmento.

**Para criar o segmento:**

1. Selecione o **[!UICONTROL Componentes > Criar segmento]** na [!DNL Workspace] barra de ferramentas.
2. Insira um **[!UICONTROL Título]** para o seu segmento. No exemplo mostrado abaixo, o segmento é nomeado como [!DNL "Hit with specific Auto-Target activity"].
3. Arraste o **[!UICONTROL Atividades do Target]** dimensão ao segmento **[!UICONTROL Definição]** seção.
4. Use o **[!UICONTROL igual]** operador.
5. Procure por seu [!DNL Target] atividade .
6. Selecione o ícone de engrenagem e selecione **[!UICONTROL Modelo de atribuição > Instância]** conforme mostrado na figura abaixo.
7. Clique em **[!UICONTROL Salvar]**.

![Figura 5.png](assets/Figure5.png)
*Figura 5: Use um segmento como o mostrado aqui para filtrar a variável [!UICONTROL Visitas] em seu A4T para [!UICONTROL Direcionamento automático] relatório*

Depois que o segmento for criado, use-o para filtrar a variável [!UICONTROL Visitas] para [!UICONTROL Visitas] inclui apenas visitas em que o usuário interagiu com a [!DNL Target] atividade .

**Para filtrar [!UICONTROL Visitas] usando este segmento:**

1. Arraste o segmento recém-criado da barra de ferramentas dos componentes e passe o mouse sobre a base do **[!UICONTROL Visitas]** rótulo da métrica até um azul **[!UICONTROL Filtrar por]** for exibido.
2. Solte o segmento. O filtro será aplicado a essa métrica.

O painel final será exibido da seguinte maneira.

![Figura 6.png](assets/Figure6.png)
*Figura 6: Painel de relatórios com o segmento &quot;Ocorrência com atividade de direcionamento automático específica&quot; aplicado ao [!UICONTROL Visitas] métrica. Isso garante somente visitas nas quais um usuário interagiu com a [!DNL Target] atividade em questão são incluídas no relatório.*

## Garanta que a métrica de meta e a atribuição estejam alinhadas ao seu critério de otimização

A integração A4T permite a [!UICONTROL Direcionamento automático] Modelo ML a utilizar *treinado* usando os mesmos dados de evento de conversão que [!DNL Adobe Analytics] usa para *gerar relatórios de desempenho*. Todavia, na formação dos modelos ML, há determinados pressupostos que devem ser utilizados na interpretação destes dados, que diferem dos pressupostos predefinidos durante a fase de comunicação em [!DNL Adobe Analytics].

Especificamente, a variável [!DNL Adobe Target] Modelos ML usam um modelo de atribuição com escopo de visitas. Ou seja, eles presumem que uma conversão deve ocorrer na mesma visita que uma exibição de conteúdo para a atividade, para que a conversão seja &quot;atribuída&quot; à decisão tomada pelo modelo ML. Isso é necessário para [!DNL Target] Garantir a formação atempada dos seus modelos; [!DNL Target] não é possível aguardar até 30 dias para uma conversão (a janela de atribuição padrão para relatórios em [!DNL Adobe Analytics]), antes de incluí-lo nos dados de treinamento de seus modelos.

Assim, a diferença entre a atribuição usada pela variável [!DNL Target] modelos (durante o treinamento) versus a atribuição padrão usada na consulta de dados (durante a geração do relatório) podem levar a discrepâncias. Pode até parecer que os modelos de ML têm um desempenho ruim, quando, de fato, o problema está na atribuição.

>[!TIP]
>
>Se os modelos de ML estão otimizando para uma métrica que é atribuída de forma diferente da métrica que você está visualizando em um relatório, os modelos podem não funcionar como esperado! Para evitar isso, assegure-se de que as métricas de meta em seu relatório usem a mesma definição de métrica e atribuição usadas pelos modelos ML do Target.

A definição exata de métrica e as configurações de atribuição dependem do [critério de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) você especificou durante a criação da atividade.

### Conversões definidas pelo Target ou métricas do Analytics com *Maximizar valor de métrica por visita*

Quando a métrica é uma conversão do Target ou uma métrica do Analytics com **Maximizar valor de métrica por visita**, a definição da métrica de meta permite que vários eventos de conversão ocorram na mesma visita.
Para visualizar métricas de meta que tenham a mesma metodologia de atribuição usada por modelos ML Adobe Target, siga estas etapas:

![gearicon.png](assets/gearicon.png)

1. No menu resultante, role até **[!UICONTROL Configurações de dados]**.
1. Selecionar **[!UICONTROL Usar modelo de atribuição não padrão]** (se ainda não estiver selecionado):

![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Clique em **[!UICONTROL Editar]**.
1. Selecionar **[!UICONTROL Modelo]**: **[!UICONTROL Participação]** e **[!UICONTROL Janela de pesquisa]**: **[!UICONTROL Visita]**.

![Participação porVisit.png](assets/ParticipationbyVisit.png)

1. Clique em **[!UICONTROL Aplicar]**.

Essas etapas garantem que seu relatório atribua a métrica de meta à exibição da experiência, se o evento de métrica de meta tiver ocorrido *qualquer hora* (&quot;participação&quot;) na mesma visita que uma experiência foi exibida.

### Métricas do Analytics com *Taxas de conversão de visita única*

**Definir a visita com o segmento de métrica positiva**

No cenário selecionado *Maximize a taxa de conversão de visitas exclusivas* como os critérios de otimização, a definição correta da taxa de conversão é a fração de visitas em que o valor da métrica é positivo. Isso pode ser feito criando uma filtragem de segmentos para visitas com um valor positivo da métrica e, em seguida, filtrando a métrica de visitas.


1. Como antes, selecione o **[!UICONTROL Componentes > Criar segmento]** na barra de ferramentas do Workspace.
2. Insira um **[!UICONTROL Título]** para o seu segmento. No exemplo mostrado abaixo, o segmento é nomeado como [!DNL "Visits with an order"].
3. Arraste a métrica base usada na meta de otimização para o segmento . No exemplo mostrado abaixo, usamos a variável **ordens** para que a taxa de conversão meça a fração de visitas em que um pedido é registrado.
4. Na parte superior esquerda do contêiner de definição de segmento, selecione **[!UICONTROL Incluir]** **Visita**.
5. Use o **[!UICONTROL é maior que]** e defina o valor como 0 (ou seja, este segmento inclui visitas em que a métrica de pedidos é positiva)
6. Clique em **[!UICONTROL Salvar]**.

![Figura 7.png](assets/Figure7.png)
*Figura 7: A filtragem da definição de segmento para visitas com uma ordem positiva. Dependendo da métrica de otimização da sua atividade, será necessário substituir os pedidos por uma métrica apropriada*

**Aplique isso às visitas na métrica filtrada de atividades**

Esse segmento agora pode ser usado para filtrar visitas com um número positivo de pedidos e onde houve uma ocorrência para a variável [!DNL Auto-Target]atividade . O procedimento de filtragem de uma métrica é semelhante a antes e depois de aplicar o novo segmento à métrica de visita já filtrada, o painel Relatório deve se parecer com a Figura 8

![Figura 8.png](assets/Figure8.png)
*Figura 8: O painel de relatórios com a métrica de conversão de visita única correta, ou seja, o número de visitas em que uma ocorrência da atividade foi registrada e em que a métrica de conversão (pedidos neste exemplo) era diferente de zero.*


## Etapa final: Crie uma taxa de conversão que capture a mágica acima

Com as modificações na [!UICONTROL Visita] e métricas de meta nas seções anteriores, a modificação final que você deve fazer no padrão A4T para [!UICONTROL Direcionamento automático] o painel de relatórios é criar taxas de conversão que sejam a proporção correta, a de uma métrica de meta com a atribuição correta, para uma métrica filtrada adequadamente [!UICONTROL Visitas] métrica.

Faça isso criando uma Métrica calculada usando as seguintes etapas:

1. Selecione o **[!UICONTROL Componentes > Criar métrica]** na [!DNL Workspace] barra de ferramentas.
1. Insira um **[!UICONTROL Título]** para sua métrica. Por exemplo, &quot;Taxa de conversão corrigida de visitas para a atividade XXX&quot;.
1. Selecionar **[!UICONTROL Formato]** = Porcentagem e **[!UICONTROL Casas decimais]** = 2.
1. Arraste a métrica de meta relevante para a atividade (por exemplo, [!UICONTROL Conversões de atividade]) na definição e use o ícone de engrenagem nessa métrica de meta para ajustar o modelo de atribuição para (Participação|Visita), conforme descrito anteriormente.
1. Selecionar **[!UICONTROL Adicionar > Contêiner]** na parte superior direita do **[!UICONTROL Definição]** seção.
1. Selecione o operador de divisão ( pai) entre os dois contêineres.
1. Arraste o segmento criado anteriormente, chamado de &quot;Ocorrência com um segmento específico [!UICONTROL Direcionamento automático] atividade&quot; neste tutorial — para este [!DNL Auto-Target] atividade .
1. Arraste o **[!UICONTROL Visitas]** no contêiner de segmento.
1. Clique em **[!UICONTROL Salvar]**.

>[!TIP]
>
> Também é possível criar essa métrica usando a [funcionalidade de métrica calculada rápida](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

A definição completa da métrica calculada é mostrada aqui.

![Figura9.png](assets/Figure9.png)
*Figura 9: A definição de métrica de taxa de conversão do modelo corrigido de visitas e atribuições. (Observe que essa métrica depende da métrica de meta e da atividade. Em outras palavras, essa definição de métrica não é reutilizável em atividades do .)*

>[!IMPORTANT]
>
>A métrica Índice de conversão do painel A4T não está vinculada ao evento de conversão ou à métrica de normalização na tabela. Quando você faz as modificações sugeridas neste tutorial, a taxa de conversão não se adapta automaticamente às alterações. Portanto, se você fizer a modificação para uma (ou ambas) a atribuição do evento de conversão e a métrica de normalização, deverá lembrar como uma etapa final para também modificar a Taxa de conversão, conforme mostrado acima.

## Resumo: Amostra final [!DNL Workspace] painel para [!UICONTROL Direcionamento automático] relatórios

Combinando todas as etapas acima em um único painel, a figura abaixo mostra uma visualização completa do relatório recomendado para [!UICONTROL Direcionamento automático] Atividades do A4T. Este relatório é igual ao utilizado pela variável [!DNL Target] Modelos ML para otimizar sua métrica de meta e incorpora todas as nuances e recomendações discutidas neste tutorial. Esse relatório também é o mais próximo das metodologias de contagem usadas nos métodos tradicionais [!DNL Target]com base em relatórios [!UICONTROL Direcionamento automático] atividades.

![Figura10.png](assets/Figure10.png)
*Figura 10: O A4T final [!UICONTROL Direcionamento automático] relatório em [!DNL Adobe Analytics] [!DNL Workspace], que combina todos os ajustes às definições de métrica descritas nas seções anteriores deste documento.*
