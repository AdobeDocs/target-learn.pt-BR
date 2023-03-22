---
title: Como configurar relatórios do A4T em [!DNL Analysis Workspace] para [!DNL Auto-Target] Atividades
description: Como configurar relatórios do A4T em [!DNL Analysis Workspace] para obter os resultados esperados durante a execução [!UICONTROL Direcionamento automático] atividades?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 538dfe6a26b4f62c52b24d54a189738677e63bf3
workflow-type: tm+mt
source-wordcount: '2641'
ht-degree: 1%

---

# Configuração de relatórios do A4T em [!DNL Analysis Workspace] para [!DNL Auto-Target] atividades

>[!IMPORTANT]
>
>Para [!UICONTROL Direcionamento automático] você deve verificar os relatórios em [!DNL Analytics Workspace] e criar manualmente um painel A4T.

O [!UICONTROL Analytics para Target] Integração do (A4T) para [!DNL Auto-Target] As atividades usam a variável [!DNL Adobe Target] agrupe algoritmos de aprendizado de máquina (ML) para escolher a melhor experiência para cada visitante com base em seu perfil, comportamento e contexto, ao usar um [!DNL Adobe Analytics] métrica de meta.

Embora os recursos de análise avançada estejam disponíveis em [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão **[!UICONTROL Analytics para Target]** são necessários para interpretar corretamente o painel [!DNL Auto-Target] atividades, devido a diferenças entre as atividades de experimentação (manual [!UICONTROL Teste A/B] e [!UICONTROL Alocação automática]) e atividades de personalização ([!UICONTROL [!UICONTROL Direcionamento automático]]).

Este tutorial aborda as modificações recomendadas para analisar [!UICONTROL Direcionamento automático] atividades em [!DNL Analysis Workspace], que se baseiam nos seguintes conceitos principais:

* O **[!UICONTROL Controle vs. Direcionado]** pode ser usada para distinguir entre [!UICONTROL Controle] experiências versus as servidas pela [!UICONTROL Direcionamento automático] algoritmo do conjunto ML.
* As Visitas devem ser usadas como a métrica de normalização ao visualizar detalhamentos de desempenho no nível da experiência. Além disso, [A metodologia de contagem padrão da Adobe Analytics pode incluir visitas em que o usuário não vê realmente o conteúdo da atividade](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}, mas esse comportamento padrão pode ser modificado usando um segmento com escopo apropriado (detalhes abaixo).
* A atribuição de escopo de retrospectiva de visita, também conhecida como &quot;janela de retrospectiva de visita&quot; no modelo de atribuição prescrito, é usada pelo [!DNL Adobe Target] Modelos ML durante as fases de treinamento e o mesmo modelo de atribuição (não padrão) devem ser usados ao detalhar a métrica de meta.

## Criar o A4T para [!UICONTROL Direcionamento automático] no painel [!DNL Analysis Workspace]

Para criar um A4T para [!UICONTROL Direcionamento automático] , comece com **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace], como mostrado abaixo, ou comece com uma tabela de forma livre. Em seguida, faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: Você pode escolher qualquer experiência; no entanto, você substituirá essa opção posteriormente. Observe que para [!UICONTROL Direcionamento automático] , a experiência de controle é realmente uma estratégia de controle, que é a) Servir aleatoriamente entre todas as experiências ou b) Servir uma única experiência (essa escolha é feita no momento da criação da atividade em [!DNL Adobe Target]). Mesmo que tenha optado pela escolha (b), a [!UICONTROL Direcionamento automático] atividade designada como controle uma experiência específica. Você ainda deve seguir a abordagem descrita neste tutorial para analisar o A4T para [!UICONTROL Direcionamento automático] atividades.
2. **[!UICONTROL Métrica de normalização]**: Selecionar [!UICONTROL Visitas].
3. **[!UICONTROL Métricas de sucesso]**: Embora seja possível selecionar qualquer métrica para gerar relatórios, geralmente é necessário visualizar os relatórios sobre a mesma métrica que foi escolhida para otimização durante a criação da atividade em [!DNL Target].

   ![[!UICONTROL Analytics para Target] configuração do painel para [!UICONTROL Direcionamento automático] atividades.](assets/Figure1.png)

   *Figura 1: [!UICONTROL Analytics para Target] configuração do painel para [!UICONTROL Direcionamento automático] atividades.*

>[!TIP]
>
>Para configurar o [!UICONTROL Analytics para Target] painel para [!UICONTROL Direcionamento automático] , escolha qualquer experiência de controle, escolha [!UICONTROL Visitas] como a métrica de normalização e escolha a mesma métrica de meta que foi escolhida para otimização durante [!DNL Target] criação da atividade.

## Use o [!UICONTROL Controle vs. segmentado] para comparar a dimensão [!DNL Target] agrupe o modelo ML no seu controle

O painel A4T padrão foi projetado para o clássico (manual) [!UICONTROL Teste A/B] ou [!UICONTROL Alocação automática] atividades nas quais o objetivo é comparar o desempenho de experiências individuais com a experiência de controle. Em [!UICONTROL Direcionamento automático] , no entanto, a primeira comparação de pedidos deve ser entre o controle *estratégia* e o *estratégia*. Em outras palavras, determinar o aumento do desempenho geral do [!UICONTROL Direcionamento automático] Conter o modelo ML sobre a estratégia de controlo.

Para executar essa comparação, use o **[!UICONTROL Controle versus Direcionado (Analytics for Target)]** dimensão. Arraste e solte para substituir o **[!UICONTROL Experiências do Target]** no relatório A4T padrão.

Observe que essa substituição invalida o padrão [!UICONTROL Lift e Confidence] cálculos no painel A4T. Para evitar confusão, você pode remover essas métricas do painel padrão, deixando o seguinte relatório:

![[!UICONTROL Experiências por conversões de atividade] no painel [!DNL Analysis Workspace]](assets/Figure2.png)

*Figura 2: O relatório de linha de base recomendado para [!DNL Auto-Target] atividades. Este relatório foi configurado para comparar o tráfego direcionado (servido pelo modelo ML do conjunto) com seu tráfego de controle.*

>[!NOTE]
>
>Atualmente, [!UICONTROL Lift e Confidence] não estão disponíveis para [!UICONTROL Controle vs. Direcionado] dimensões para relatórios A4T para [!UICONTROL Direcionamento automático]. Até que o suporte seja adicionado, [!UICONTROL Lift e Confidence] pode ser calculado manualmente baixando a variável [calculadora de confiança](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## Adicionar detalhamentos de métricas em nível de experiência

Para obter mais informações sobre o desempenho do modelo ML do conjunto, você pode examinar detalhamentos no nível da experiência do **[!UICONTROL Controle vs. Direcionado]** dimensão. Em [!DNL Analysis Workspace], arraste a **[!UICONTROL Experiências do Target]** em seu relatório, em seguida, detalhe cada uma das dimensões de controle e direcionadas separadamente.

![[!UICONTROL Experiências por conversões de atividade] no painel [!DNL Analysis Workspace]](assets/Figure3.png)

*Figura 3: Detalhamento da dimensão Direcionada por experiências do Target*

Um exemplo do relatório resultante é mostrado aqui.

![[!UICONTROL Experiências por conversões de atividade] no painel [!DNL Analysis Workspace]](assets/Figure4.png)

*Figura 4: Padrão [!UICONTROL Direcionamento automático] com detalhamentos de experiência. Observe que sua métrica de meta pode ser diferente, e sua estratégia de controle pode ter uma única experiência.*

>[!TIP]
>
>Em [!DNL Analysis Workspace], clique no ícone de engrenagem para ocultar as porcentagens no [!UICONTROL Índice de conversão] para ajudar a manter o foco nas taxas de conversão da experiência. As taxas de conversão serão formatadas como decimais, mas as interpretarão como porcentagens de acordo.

## Por que &quot;[!UICONTROL Visitas]&quot; é a métrica de normalização correta para [!UICONTROL Direcionamento automático] atividades

Ao analisar uma [!UICONTROL Direcionamento automático] atividade , sempre escolha [!UICONTROL Visitas] como a métrica de normalização padrão. [!UICONTROL Direcionamento automático] a personalização seleciona uma experiência para um visitante uma vez por visita (formalmente, uma vez por [!DNL Target] sessão), o que significa que a experiência exibida para um visitante pode mudar em cada visita única. Assim, se você usar [!UICONTROL Visitantes únicos] como a métrica de normalização, o fato de que um único usuário pode acabar visualizando várias experiências (em diferentes visitas) levaria a taxas de conversão confusas.

Um exemplo simples demonstra esse ponto: considere um cenário em que dois visitantes acessam uma campanha com apenas duas experiências. O primeiro visitante visita duas vezes. Eles são atribuídos à Experiência A na primeira visita, mas à Experiência B na segunda visita (devido ao estado do perfil ter mudado na segunda visita). Após a segunda visita, o visitante é convertido ao fazer um pedido. A conversão é atribuída à experiência exibida mais recentemente (Experiência B). O segundo visitante também visita duas vezes e a Experiência B é exibida duas vezes, mas nunca converte.

Vamos comparar os relatórios a nível de visitante e a nível de visita:

| Experiência | Visitantes únicos | Visitas | Conversões | Taxa de conversão normalizada pelo visitante | Taxa de conversão normalizada da visita |
| --- | --- | --- | --- | --- | --- |
| Um | 1 | 1 | - | 0% | 0% |
| B  | 2 | 3 | 1 | 50% | 33.3% |
| Totais | 2 | 4 | 1 | 50% | 25% |

*Quadro 1: Exemplo que compara relatórios normalizados de visitantes e relatórios normalizados de visitas para um cenário em que as decisões são aderentes a uma visita (e não a um visitante, como com testes A/B regulares). Métricas normalizadas do visitante são confusas nesse cenário.*

Conforme mostrado na tabela, há uma clara incongruência de números no nível do visitante. Apesar do fato de haver dois visitantes únicos totais, essa não é uma soma de visitantes únicos individuais para cada experiência. Embora a taxa de conversão no nível do visitante não esteja necessariamente errada, quando você compara experiências individuais, as taxas de conversão no nível da visita provavelmente fazem muito mais sentido. Formalmente, a unidade de análise (&quot;visitas&quot;) é a mesma que a unidade de decisão, o que significa que os detalhamentos das métricas no nível da experiência podem ser adicionados e comparados.

## Filtrar as visitas reais à atividade

O [!DNL Adobe Analytics] metodologia de contagem padrão para visitas a um [!DNL Target] atividade pode incluir visitas nas quais o usuário não interagiu com a [!DNL Target] atividade . Isso se deve à maneira como [!DNL Target] as atribuições de atividade são mantidas no [!DNL Analytics] contexto do visitante. Como resultado, o número de visitas ao [!DNL Target] às vezes, a atividade pode ser inflacionada, resultando em uma depressão das taxas de conversão.

Se você preferir relatar sobre visitas nas quais o usuário interagiu com a [!UICONTROL Direcionamento automático] atividade (por meio da entrada na atividade , de um evento de exibição ou de visita ou de uma conversão), é possível:

1. Crie um segmento específico que inclua ocorrências do [!DNL Target] em questão e, em seguida,
1. Filtre o [!UICONTROL Visitas] usando este segmento.

**Para criar o segmento:**

1. Selecione o **[!UICONTROL Componentes > Criar segmento]** na [!DNL Analysis Workspace] barra de ferramentas.
2. Especifique um **[!UICONTROL Título]** para o seu segmento. No exemplo mostrado abaixo, o segmento é nomeado como [!DNL "Hit with specific Auto-Target activity"].
3. Arraste o **[!UICONTROL Atividades do Target]** dimensão ao segmento **[!UICONTROL Definição]** seção.
4. Use o **[!UICONTROL igual]** operador.
5. Procure por seu [!DNL Target] atividade .
6. Clique no ícone de engrenagem e selecione **[!UICONTROL Modelo de atribuição > Instância]** conforme mostrado na figura abaixo.
7. Clique em **[!UICONTROL Salvar]**.

![Segmentar em [!DNL Analysis Workspace]](assets/Figure5.png)

*Figura 5: Use um segmento como o mostrado aqui para filtrar a variável [!UICONTROL Visitas] em seu A4T para [!UICONTROL Direcionamento automático] relatório*

Depois que o segmento for criado, use-o para filtrar a variável [!UICONTROL Visitas] para [!UICONTROL Visitas] inclui apenas visitas em que o usuário interagiu com a [!DNL Target] atividade .

**Para filtrar [!UICONTROL Visitas] usando este segmento:**

1. Arraste o segmento recém-criado da barra de ferramentas dos componentes e passe o mouse sobre a base do **[!UICONTROL Visitas]** rótulo da métrica até um azul **[!UICONTROL Filtrar por]** for exibido.
2. Solte o segmento. O filtro é aplicado a essa métrica.

O painel final aparece da seguinte maneira:

![[!UICONTROL Experiências por conversões de atividade] no painel [!DNL Analysis Workspace]](assets/Figure6.png)

*Figura 6: Painel de relatórios com o segmento &quot;Ocorrência com atividade de direcionamento automático específica&quot; aplicado ao [!UICONTROL Visitas] métrica. Esse segmento garante que somente visitas nas quais um usuário interagiu com a [!DNL Target] atividade em questão são incluídas no relatório.*

## Garanta que a métrica de meta e a atribuição estejam alinhadas ao seu critério de otimização

A integração A4T permite a [!UICONTROL Direcionamento automático] Modelo ML a utilizar *treinado* usando os mesmos dados de evento de conversão que [!DNL Adobe Analytics] usa para *gerar relatórios de desempenho*. Todavia, na formação dos modelos de ML, há determinados pressupostos que devem ser utilizados na interpretação destes dados, que diferem dos pressupostos predefinidos durante a fase de comunicação em [!DNL Adobe Analytics].

Especificamente, a variável [!DNL Adobe Target] Modelos ML usam um modelo de atribuição com escopo de visitas. Ou seja, os modelos de ML pressupõem que uma conversão deve ocorrer na mesma visita que uma exibição do conteúdo da atividade para que a conversão seja &quot;atribuída&quot; à decisão tomada pelo modelo de ML. Isso é necessário para [!DNL Target] Garantir a formação atempada dos seus modelos; [!DNL Target] não é possível aguardar até 30 dias para uma conversão (a janela de atribuição padrão para relatórios em [!DNL Adobe Analytics]) antes de incluí-lo nos dados de treinamento de seus modelos.

Assim, a diferença entre a atribuição usada pela variável [!DNL Target] modelos (durante o treinamento) versus a atribuição padrão usada na consulta de dados (durante a geração do relatório) podem levar a discrepâncias. Pode até parecer que os modelos de ML têm um desempenho ruim, quando, de fato, o problema está na atribuição.

>[!TIP]
>
>Se os modelos de ML estiverem otimizando uma métrica atribuída de forma diferente da métrica que você está visualizando em um relatório, os modelos podem não funcionar conforme esperado. Para evitar isso, assegure-se de que as métricas de meta em seu relatório usem a mesma definição de métrica e atribuição usadas pela variável [!DNL Target] Modelos ML.

A definição exata de métrica e as configurações de atribuição dependem do [critério de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} você especificou durante a criação da atividade.

### Conversões definidas pelo Target ou [!DNL Analytics] métricas com *Maximizar valor de métrica por visita*

Quando a métrica é uma [!DNL Target] conversão ou uma [!DNL Analytics] métricas com **Maximizar valor de métrica por visita**, a definição da métrica de meta permite que vários eventos de conversão ocorram na mesma visita.

Para visualizar métricas de meta que tenham a mesma metodologia de atribuição usada pela [!DNL Target] Modelos ML, siga estas etapas:

1. Passe o mouse sobre o ícone de engrenagem da métrica de meta:

   ![gearicon.png](assets/gearicon.png)

1. No menu resultante, role até **[!UICONTROL Configurações de dados]**.
1. Selecionar **[!UICONTROL Usar modelo de atribuição não padrão]** (se ainda não estiver selecionado).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Clique em **[!UICONTROL Editar]**.
1. Selecionar **[!UICONTROL Modelo]**: **[!UICONTROL Participação]** e **[!UICONTROL Janela de pesquisa]**: **[!UICONTROL Visita]**.

   ![Participação porVisit.png](assets/ParticipationbyVisit.png)

1. Clique em **[!UICONTROL Aplicar]**.

Essas etapas garantem que seu relatório atribua a métrica de meta à exibição da experiência, se o evento de métrica de meta tiver ocorrido *qualquer hora* (&quot;participação&quot;) na mesma visita que uma experiência foi exibida.

### [!DNL Analytics] métricas com *Taxas de conversão de visita única*

**Definir a visita com o segmento de métrica positiva**

No cenário selecionado *Maximize a taxa de conversão de visitas exclusivas* como os critérios de otimização, a definição correta da taxa de conversão é a fração de visitas em que o valor da métrica é positivo. Isso pode ser feito criando uma filtragem de segmentos para visitas com um valor positivo da métrica e, em seguida, filtrando a métrica de visitas.

1. Como antes, selecione o **[!UICONTROL Componentes > Criar segmento]** na [!DNL Analysis Workspace] barra de ferramentas.
2. Especifique um **[!UICONTROL Título]** para o seu segmento.

   No exemplo mostrado abaixo, o segmento é nomeado como [!DNL "Visits with an order"].

3. Arraste a métrica base usada na meta de otimização para o segmento.

   No exemplo mostrado abaixo, usamos a variável **ordens** para que a taxa de conversão meça a fração de visitas em que um pedido é registrado.

4. Na parte superior esquerda do contêiner de definição de segmento, selecione **[!UICONTROL Incluir]** **Visita**.
5. Use o **[!UICONTROL é maior que]** e defina o valor como 0.

   Definir o valor como 0 significa que esse segmento inclui visitas nas quais a métrica de pedidos é positiva.

6. Clique em **[!UICONTROL Salvar]**.

![Figura 7.png](assets/Figure7.png)

*Figura 7: A filtragem da definição de segmento para visitas com uma ordem positiva. Dependendo da métrica de otimização da sua atividade, você deve substituir os pedidos por uma métrica apropriada*

**Aplique isso às visitas na métrica filtrada de atividades**

Esse segmento agora pode ser usado para filtrar visitas com um número positivo de pedidos e onde houve uma ocorrência para a variável [!DNL Auto-Target] atividade . O procedimento de filtragem de uma métrica é semelhante a antes e depois de aplicar o novo segmento à métrica de visita já filtrada, o painel Relatório deve se parecer com a Figura 8

![Figura 8.png](assets/Figure8.png)

*Figura 8: O painel de relatórios com a métrica de conversão de visita única correta: o número de visitas em que uma ocorrência da atividade foi registrada e em que a métrica de conversão (pedidos neste exemplo) foi diferente de zero.*

## Etapa final: Crie uma taxa de conversão que capture a mágica acima

Com as modificações na [!UICONTROL Visita] e métricas de meta nas seções anteriores, a modificação final que você deve fazer no padrão A4T para [!DNL Auto-Target] o painel de relatórios é criar taxas de conversão que são a proporção correta, a da métrica de meta corrigida, para uma métrica de &quot;Visitas&quot; filtrada apropriadamente.

Faça isso criando uma [!UICONTROL Métrica calculada] usando as seguintes etapas:

1. Selecione o **[!UICONTROL Componentes > Criar métrica]** na [!DNL Analysis Workspace] barra de ferramentas.
1. Especifique um **[!UICONTROL Título]** para sua métrica. Por exemplo, &quot;Taxa de conversão corrigida de visitas para a atividade XXX&quot;.
1. Selecionar **[!UICONTROL Formato]** = Porcentagem e **[!UICONTROL Casas decimais]** = 2.
1. Arraste a métrica de meta relevante para a atividade (por exemplo, [!UICONTROL Conversões de atividade]) na definição e use o ícone de engrenagem nessa métrica de meta para ajustar o modelo de atribuição para (Participação|Visita), conforme descrito anteriormente.
1. Selecionar **[!UICONTROL Adicionar > Contêiner]** na parte superior direita do **[!UICONTROL Definição]** seção.
1. Selecione o operador de divisão ( pai) entre os dois contêineres.
1. Arraste o segmento criado anteriormente, chamado de &quot;Ocorrência com um segmento específico [!UICONTROL Direcionamento automático] atividade&quot; neste tutorial para este [!DNL Auto-Target] atividade .
1. Arraste o **[!UICONTROL Visitas]** no contêiner de segmento.
1. Clique em **[!UICONTROL Salvar]**.

>[!TIP]
>
> Também é possível criar essa métrica usando a [funcionalidade de métrica calculada rápida](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

A definição completa da métrica calculada é mostrada aqui.

![Figura9.png](assets/Figure9.png)

*Figura 7: A definição de métrica de taxa de conversão do modelo corrigida de visitas e de atribuição. (Observe que essa métrica depende da métrica de meta e da atividade. Em outras palavras, essa definição de métrica não é reutilizável em atividades do .)*

>[!IMPORTANT]
>
>O [!UICONTROL Conversão] a métrica de taxa do painel A4T não está vinculada ao evento de conversão ou à métrica de normalização na tabela. Quando você faz as modificações sugeridas neste tutorial, a função [!UICONTROL Conversão] não se adapta automaticamente às alterações. Portanto, se você fizer a modificação na atribuição do evento de conversão ou na métrica de normalização (ou ambos), lembre-se de uma etapa final para também modificar a variável [!UICONTROL Conversão] , como mostrado acima.

## Resumo: Amostra final [!DNL Analysis Workspace] painel para [!UICONTROL Direcionamento automático] relatórios

Combinando todas as etapas acima em um único painel, a figura abaixo mostra uma visualização completa do relatório recomendado para [!UICONTROL Direcionamento automático] Atividades do A4T. Este relatório é igual ao utilizado pela variável [!DNL Target] Modelos ML para otimizar sua métrica de meta. O relatório incorpora todas as nuances e recomendações discutidas neste tutorial. Esse relatório também é o mais próximo das metodologias de contagem usadas nos métodos tradicionais [!DNL Target]com base em relatórios [!UICONTROL Direcionamento automático] atividades.

Clique em para expandir a imagem.

![Relatório final A4T em [!DNL Analysis Workspace]](assets/Figure10.png "Relatório A4T no Analysis Workspace"){width="600" zoomable="yes"}

*Figura 10: O A4T final [!UICONTROL Direcionamento automático] relatório em [!DNL Adobe Analytics] [!DNL Workspace], que combina todos os ajustes nas definições de métrica descritas nas seções anteriores deste tutorial.*
