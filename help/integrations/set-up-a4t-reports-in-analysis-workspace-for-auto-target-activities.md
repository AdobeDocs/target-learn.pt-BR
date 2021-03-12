---
title: Como configurar relatórios do A4T no Analysis Workspace para atividades de direcionamento automático
description: Como configurar relatórios do A4T no Analysis Workspace para obter os resultados esperados ao executar atividades de Direcionamento automático
kt: null
audience: business user
doc-type: tutorial
activity: use, setup
feature: Analytics for Target (A4T), Direcionamento automático
topic: Analytics for Target (A4T), Direcionamento automático
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 814ce9b49eff6cbc41a84bb65718f4e5f4f0142d
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Como configurar relatórios do A4T no Analysis Workspace para atividades [!DNL Auto-Target]

A integração do Analytics for Target (A4T) para as atividades [!DNL Auto-Target] usa os algoritmos de aprendizado de máquina (ML) do conjunto do Adobe Target para escolher a melhor experiência para cada visitante com base em seu perfil, comportamento e contexto, tudo isso usando uma métrica de meta do Adobe Analytics.

Embora os recursos de análise avançada estejam disponíveis no Adobe Analytics Analysis Workspace, algumas modificações no painel **[!UICONTROL Analytics for Target]** padrão são necessárias para interpretar corretamente as atividades [!DNL Auto-Target], devido às diferenças entre as atividades de experimentação (A/B manual e Alocação automática) e as atividades de personalização ([!DNL Auto-Target]).

Este tutorial aborda as modificações recomendadas para analisar [!DNL Auto-Target] atividades no Workspace, que são baseadas nos seguintes conceitos principais:

* A dimensão **[!UICONTROL Controle vs Targeted]** pode ser usada para distinguir entre as experiências de Controle versus aquelas servidas pelo algoritmo ML do conjunto [!DNL Auto-Target].
* As Visitas devem ser usadas como a métrica de normalização ao visualizar detalhamentos de desempenho no nível da experiência. Além disso, a metodologia de contagem padrão do [Adobe Analytics pode incluir visitas nas quais o usuário não vê realmente o conteúdo da atividade](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), mas esse comportamento padrão pode ser modificado usando um segmento com escopo apropriado (detalhes abaixo).
* A atribuição com escopo de retrospectiva de visita - também conhecida como &quot;janela de retrospectiva de visita&quot; no modelo de atribuição prescrito - é usada por modelos ML da Adobe Target durante suas fases de treinamento, e o mesmo modelo de atribuição (não padrão) deve ser usado ao detalhar a métrica de meta.

## Criar o A4T para o painel [!DNL Auto-Target] no Workspace

Para criar um relatório A4T para [!DNL Auto-Target], comece com o painel **[!UICONTROL Analytics for Target]** no Workspace, conforme mostrado abaixo, ou comece com uma tabela de forma livre. Em seguida, faça as seguintes seleções:

1. **[!UICONTROL Experiência]** de controle: Você pode escolher qualquer experiência; no entanto, substituiremos essa opção posteriormente. Observe que para atividades [!DNL Auto-Target], a experiência de controle é realmente uma estratégia de controle, que é: a) Servir aleatoriamente entre todas as experiências ou b) Servir uma única experiência (essa escolha é feita no momento da criação da atividade no Adobe Target). Mesmo que você tenha optado pela escolha (b) - sua atividade [!DNL Auto-Target] designada uma experiência específica como Controle - você ainda deve seguir a abordagem descrita neste tutorial para analisar o A4T para atividades [!DNL Auto-Target] .
2. **[!UICONTROL Métrica]** de normalização: Selecione Visitas.
3. **[!UICONTROL Métricas]** de sucesso: Embora seja possível selecionar qualquer métrica para gerar relatórios, geralmente é necessário exibir relatórios sobre a mesma métrica escolhida para otimização durante a criação da atividade no Adobe Target.

![Figura 1.](assets/Figure1.png)
*pngFigura 1: Configuração do painel do Analytics for Target para  [!DNL Auto-Target] atividades.*

>[!NOTE]
>
>Para configurar o painel Analytics for Target para atividades de Direcionamento automático, escolha qualquer experiência de controle, escolha Visitas como a métrica de normalização e escolha a mesma métrica de meta que foi escolhida para otimização durante a criação da atividade do Target.

## Use a dimensão Controle versus Direcionado para comparar o modelo ML do conjunto da Adobe Target ao seu controle

O painel A4T padrão foi projetado para testes A/B clássicos (manuais) ou atividades de Alocação automática, onde o objetivo é comparar o desempenho de experiências individuais com a experiência de Controle. No entanto, em [!DNL Auto-Target] atividades, a primeira comparação de pedidos deve ser entre o Control *strategy* e o Targeted *strategy* (em outras palavras, determinar o aumento do desempenho geral do [!DNL Auto-Target] modelo ML do conjunto sobre a estratégia de Controle).

Para executar essa comparação, use a dimensão **[!UICONTROL Controle vs Destino (Analytics for Target)]** . Arraste e solte para substituir a dimensão **[!UICONTROL Experiências do Target]** no relatório A4T padrão.

Observe que essa substituição invalida os cálculos padrão de Aumento e Confiança no painel A4T. Para evitar confusão, você pode remover essas métricas do painel padrão, deixando o seguinte relatório:

![Figura 2.](assets/Figure2.png)
*pngFigura 2: O relatório de linha de base recomendado para  [!DNL Auto-Target] atividades. Este relatório foi configurado para comparar o tráfego Direcionado (servido pelo modelo ML do conjunto) com seu tráfego de Controle.*

>[!NOTE]
>
>Atualmente, os números de Lift e Confidence não estão disponíveis para as dimensões Control vs Targeted para os relatórios A4T para Direcionamento automático. Até que o suporte seja adicionado, o Aumento e a Confiança podem ser calculados manualmente baixando a [calculadora de confiança](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Adicionar detalhamentos de métricas no nível da experiência

Para obter mais informações sobre o desempenho do modelo ML do conjunto, você pode examinar os detalhamentos no nível da experiência da dimensão **[!UICONTROL Controle vs Target]**. No Workspace, arraste a dimensão **[!UICONTROL Experiências do Target]** para o relatório e depois detalhe cada uma das dimensões de Controle e Direcionado separadamente.

![Figura 3.](assets/Figure3.png)
*pngFigura 3: Detalhamento da dimensão Direcionada por experiências do Target*

Um exemplo do relatório resultante é mostrado aqui.

![Figura 4.](assets/Figure4.png)
*pngFigura 4: Um  [!DNL Auto-Target] relatório padrão com detalhamentos de nível de experiência. Observe que sua métrica de meta pode ser diferente, e sua estratégia de Controle pode ter uma única experiência.*

>[!TIP]
>
>No Workspace, clique no ícone de engrenagem para ocultar as Porcentagens na coluna Índice de conversão para ajudar a manter o foco nas taxas de conversão da experiência. Observe que as taxas de conversão serão formatadas como decimais, mas interprete-as como porcentagens de acordo.

## Por que &quot;Visitas&quot; é a métrica de normalização correta para atividades [!DNL Auto-Target]

Ao analisar uma atividade [!DNL Auto-Target], sempre escolha Visitas como a métrica de normalização padrão. [!DNL Auto-Target] a personalização seleciona uma experiência para um visitante uma vez por visita (formalmente, uma vez por sessão do Adobe Target), o que significa que a experiência exibida para um usuário pode mudar em cada visita única. Assim, se você usar Visitantes únicos como a métrica de normalização, o fato de que um único usuário pode acabar visualizando várias experiências (em diferentes visitas) levaria a taxas de conversão confusas.

Um exemplo simples demonstra esse ponto: considere um cenário em que dois visitantes entram em uma campanha que tem apenas duas experiências. O primeiro visitante visita duas vezes. Eles são atribuídos à Experiência A na primeira visita, mas à Experiência B na segunda visita (devido ao estado do perfil ter mudado na segunda visita). Após a segunda visita, o visitante é convertido ao fazer um pedido. A conversão é atribuída à experiência exibida mais recentemente (Experiência B). O segundo visitante também visita duas vezes e a Experiência B é exibida duas vezes, mas nunca converte.

Vamos comparar os relatórios a nível de visitante e a nível de visita:

| Experiência | Visitantes únicos | Visitas | Conversões | Norma do visitante. Conv. Taxa | Norma de visita. Conv. Taxa |
| --- | --- | --- | --- | --- | --- |
| Um | 1 | 3 | - | 0% | 0% |
| B  | 2 | 3 | 1 | 50% | 33,3% |
| Totais | 2 | 4 | 3 | 50% | 25% |
*Quadro 1: Exemplo comparando relatórios normalizados de visitantes e relatórios normalizados de visitas para um cenário em que as decisões são aderentes a uma visita (e não a um visitante, como com testes A/B regulares). Métricas normalizadas do visitante são confusas neste cenário.*

Conforme mostrado na tabela, há uma clara incongruência de números no nível do visitante. Apesar do fato de haver dois visitantes únicos totais, essa não é uma soma de visitantes únicos individuais para cada experiência. Embora a taxa de conversão no nível do visitante não esteja necessariamente errada, quando você compara experiências individuais, as taxas de conversão no nível da visita provavelmente fazem muito mais sentido. Formalmente, a unidade de análise (&quot;visitas&quot;) é a mesma que a unidade de decisão, o que significa que os detalhamentos das métricas no nível da experiência podem ser adicionados e comparados.

## Filtrar as visitas reais à atividade

A metodologia de contagem padrão do Adobe Analytics para visitas a uma atividade do Target pode incluir visitas em que o usuário não interagiu com a atividade do Target. Isso se deve à forma como as atribuições de atividade do Target são mantidas no contexto de visitante do Analytics. Como resultado, o número de visitas à atividade do Target pode, às vezes, ser inflado, resultando em uma depressão das taxas de conversão.

Se preferir relatar sobre visitas em que o usuário interagiu com a atividade de Direcionamento automático (por meio de uma entrada na atividade, um evento de exibição/visita ou uma conversão), é possível:

1. Crie um segmento específico que inclua ocorrências da atividade do Target em questão e
1. Filtre a métrica Visitas usando esse segmento.

**Para criar o segmento:**

1. Selecione a opção **[!UICONTROL Componentes > Criar segmento]** na barra de ferramentas do Workspace.
2. Insira um **[!UICONTROL Título]** para seu segmento. No exemplo mostrado abaixo, o segmento é nomeado [!DNL "Hit with specific Auto-Target activity"].
3. Arraste a dimensão **[!UICONTROL Atividades do Target]** para a seção **[!UICONTROL Definição]** do segmento.
4. Use o operador **[!UICONTROL equals]**.
5. Procure sua atividade específica do Target.
6. Selecione o ícone de engrenagem e selecione **[!UICONTROL Attribution model > Instance]** conforme mostrado na figura abaixo.
7. Clique em **[!UICONTROL Salvar]**.

![Figura 5.](assets/Figure5.png)
*pngFigura 5: Use um segmento como o mostrado aqui para filtrar a métrica Visitas no seu A4T para  [!DNL Auto-Target] relatório*

Depois que o segmento tiver sido criado, use-o para filtrar a métrica Visitas, de modo que a métrica Visitas inclua apenas visitas onde o usuário interagiu com a atividade do Target.

**Para filtrar Visitas usando este segmento:**

1. Arraste o segmento recém-criado da barra de ferramentas dos componentes e passe o mouse sobre a base do rótulo da métrica **[!UICONTROL Visitas]** até que um prompt azul **[!UICONTROL Filtrar por]** seja exibido.
2. Solte o segmento. O filtro será aplicado a essa métrica.

O painel final será exibido da seguinte maneira.

![Figura 6.](assets/Figure6.png)
*pngFigura 6: Painel de relatórios com o segmento &quot;Ocorrência com atividade de Direcionamento automático específica&quot; aplicado à métrica   Visitas. Isso garante que somente as visitas em que um usuário interagiu com a atividade do Target em questão sejam incluídas no relatório.*

## Alinhe a atribuição entre o treinamento do modelo ML e a geração de métrica de meta

A integração A4T permite que o modelo ML de [!DNL Auto-Target] seja *treinado* usando os mesmos dados de evento de conversão que o Adobe Analytics usa para *gerar relatórios de desempenho*. No entanto, há certos pressupostos que devem ser utilizados na interpretação destes dados na formação dos modelos ML, que diferem dos pressupostos predefinidos durante a fase de comunicação na Adobe Analytics.

Especificamente, os modelos ML da Adobe Target usam um modelo de atribuição com escopo de visitas. Ou seja, eles presumem que uma conversão deve ocorrer na mesma visita que uma exibição de conteúdo para a atividade, para que a conversão seja &quot;atribuída&quot; à decisão tomada pelo modelo ML. Tal é necessário para que o Target garanta a formação atempada dos seus modelos; O Target não pode esperar até 30 dias por uma conversão (a janela de atribuição padrão para relatórios no Adobe Analytics), antes de incluí-la nos dados de treinamento de seus modelos.

Assim, a diferença entre a atribuição usada pelos modelos do Target (durante o treinamento) e a atribuição padrão usada na consulta de dados (durante a geração do relatório) pode levar a discrepâncias. Pode até parecer que os modelos de ML têm um desempenho ruim, quando, de fato, o problema está na atribuição.

>[!TIP]
>
>Se os modelos de ML estão otimizando para uma métrica que é atribuída de forma diferente da métrica que você está visualizando em um relatório, os modelos podem não funcionar como esperado! Para evitar isso, assegure-se de que as métricas de meta em seu relatório usem a mesma atribuição usada pelos modelos ML do Target.

Para visualizar métricas de meta que tenham a mesma metodologia de atribuição usada por modelos ML Adobe Target, siga estas etapas:

1. Passe o mouse sobre o ícone de engrenagem da métrica de meta:
   ![gearicon.png](assets/gearicon.png)
1. No menu resultante, role até **[!UICONTROL Data settings]**.
1. Selecione **[!UICONTROL Usar modelo de atribuição não padrão]** (se ainda não estiver selecionado):
   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. Clique em **[!UICONTROL Editar]**.
1. Selecione **[!UICONTROL Modelo]**: **[!UICONTROL Participação]** e **[!UICONTROL Janela de pesquisa]**: **[!UICONTROL Visita]**.
   ![Participação porVisit.png](assets/ParticipationbyVisit.png)
1. Clique em **[!UICONTROL Aplicar]**.

Essas etapas garantem que seu relatório atribua a métrica de meta à exibição da experiência, se o evento da métrica de meta tiver ocorrido *a qualquer momento* (&quot;participação&quot;) na mesma visita que uma experiência foi exibida.

## Etapa final: Crie uma taxa de conversão que capture a mágica acima

Com as modificações nas métricas de Visita e meta nas seções anteriores, a modificação final que você deve fazer no seu painel de relatórios padrão A4T para [!DNL Auto-Target] é criar taxas de conversão que sejam a proporção correta - a de uma métrica de meta com a atribuição correta, a uma métrica de &quot;Visitas&quot; filtrada apropriadamente.

Faça isso criando uma Métrica calculada usando as seguintes etapas:

1. Selecione a opção **[!UICONTROL Componentes > Criar métrica]** na barra de ferramentas do Workspace.
1. Insira um **[!UICONTROL Título]** para sua métrica. Por exemplo, &quot;Taxa de conversão corrigida de visitas para a atividade XXX&quot;.
1. Selecione **[!UICONTROL Format]** = Percent e **[!UICONTROL Decimal Places]** = 2.
1. Arraste a métrica de meta relevante para sua atividade (por exemplo, Conversões de atividade) para a definição e use o ícone de engrenagem nessa métrica de meta para ajustar o modelo de atribuição para (Participação|Visita), conforme descrito anteriormente.
1. Selecione **[!UICONTROL Add > Container]** no canto superior direito da seção **[!UICONTROL Definition]**.
1. Selecione o operador de divisão ( pai) entre os dois contêineres.
1. Arraste o segmento criado anteriormente, chamado &quot;Ocorrência com atividade [!DNL Auto-Target] específica&quot; neste tutorial, para esta atividade [!DNL Auto-Target] específica.
1. Arraste a métrica **[!UICONTROL Visitas]** para o contêiner do segmento.
1. Clique em **[!UICONTROL Salvar]**.

A definição completa da métrica calculada é mostrada aqui.

![Figura 7.](assets/Figure7.png)
*pngFigura 7: A definição de métrica de taxa de conversão do modelo corrigido de visitas e atribuições. (Observe que essa métrica depende da métrica de meta e da atividade. Em outras palavras, essa definição de métrica não é reutilizável em atividades.)*

>[!IMPORTANT]
>
>A métrica Índice de conversão do painel A4T não está vinculada ao evento de conversão ou à métrica de normalização na tabela. Quando você faz as modificações sugeridas neste tutorial, a taxa de conversão não se adapta automaticamente às alterações. Portanto, se você fizer a modificação para uma (ou ambas) a atribuição do evento de conversão e a métrica de normalização, deverá lembrar como uma etapa final para também modificar a Taxa de conversão, conforme mostrado acima.

## Resumo: Painel Espaço de trabalho de amostra final para relatórios [!DNL Auto-Target]

Combinando todas as etapas acima em um único painel, a figura abaixo mostra uma visualização completa do relatório recomendado para [!DNL Auto-Target] atividades do A4T. Este relatório é o mesmo usado pelos modelos de aprendizado de máquina do Target para otimizar sua métrica de meta, e incorpora todas as nuances e recomendações discutidas neste tutorial. Este relatório também é o mais próximo das metodologias de contagem usadas nas atividades tradicionais [!DNL Auto-Target] orientadas por relatórios do Target.

![Figura 8.](assets/Figure8.png)
*pngFigura 8: O  [!DNL Auto-Target] relatório final do A4T no Adobe Analytics Workspace, que combina todos os ajustes às definições de métricas descritas nas seções anteriores deste documento.*
