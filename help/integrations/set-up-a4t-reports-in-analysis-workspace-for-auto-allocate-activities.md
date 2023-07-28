---
title: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para [!UICONTROL Alocação automática] Atividades
description: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para obter os resultados esperados durante a execução [!UICONTROL Alocação automática] atividades.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 8ef61ac0abf008039561bebe7d8d20b84f447487
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Configuração de relatórios do A4T no [!DNL Analysis Workspace] para [!DNL Auto-Allocate] atividades

Um [!DNL Auto-Allocate] a atividade identifica um vencedor entre duas ou mais experiências e realoca automaticamente seu tráfego para o vencedor enquanto o teste continua a ser executado e aprendido. A variável [!UICONTROL Analytics for Target] Integração do (A4T) para [!UICONTROL Alocação automática] permite visualizar os dados de relatórios no [!DNL Adobe Analytics]e você pode até otimizar para eventos ou métricas personalizados definidos em [!DNL Analytics].

Embora os recursos avançados de análise estejam disponíveis no [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão **[!UICONTROL Analytics for Target]** pode ser necessário para interpretar corretamente [!DNL Auto-Allocate] atividades, devido às nuances nas [critérios de métrica de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Este tutorial aborda as modificações recomendadas para análise [!DNL Auto-Allocate] atividades no [!DNL Analysis Workspace]. Os principais conceitos são:

* [!UICONTROL Visitantes] deve ser sempre usada como a métrica de normalização em [!DNL Auto-Allocate] atividades.
* Quando a métrica é uma [!DNL Adobe Analytics] , o cálculo da taxa de conversão varia, dependendo do tipo de critérios de otimização definidos durante a configuração da atividade.
   * A taxa de conversão &quot;maximizar valor da métrica por visitante&quot;: o numerador é o valor da métrica regular em [!DNL Adobe Analytics] (isso é fornecido por padrão no [!UICONTROL Analytics for Target] painel no [!DNL Analysis Workspace]).
      * O que isso significa: maximiza o número de conversões por visitante (&quot;conte cada visitante&quot;).
      * Este método não requer um segmento adicional para corresponder à taxa de conversão exibida no [!DNL Target] IU.
   * A taxa de conversão &quot;maximizar a taxa de conversão de um visitante único&quot;: o numerador é uma contagem dos visitantes únicos com um valor positivo da métrica.
      * O que isso significa: maximiza o número de visitantes que convertem (&quot;conte uma vez por visitante).
      * Este método *FAZ* exigir a criação de um segmento adicional nos relatórios para corresponder à taxa de conversão exibida no [!DNL Target] IU.

* Quando sua métrica de otimização é uma [!DNL Target] métrica de conversão definida, o padrão **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace] O lida com a configuração do seu painel.
* Para todos [!UICONTROL Alocação automática] atividades criadas antes da variável [!DNL Target Standard/Premium] Versão 23.3.1 (30 de março de 2023) [!DNL Analytics Workspace] e [!DNL Target] exibir o mesmo valor para [!UICONTROL Confiança].

  Para todos [!UICONTROL Alocação automática] criado após 30 de março de 2023, os valores do intervalo de confiança vistos no [!DNL Analysis Workspace] não refletem a [estatísticas mais conservadoras usadas pelo [!UICONTROL Alocação automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} em se essas atividades tiverem *ambos* das seguintes condições:

   * [!DNL Analytics] como origem de relatório (A4T)
   * [!DNL Analytics] métricas de otimização

  As métricas de confiança devem ser removidas do painel A4T. Em vez disso, faça referência a esses valores em [!DNL Target] relatórios.

## Criar o A4T para [!DNL Auto-Allocate] painel no [!DNL Analysis Workspace]

Para criar um painel A4T para um [!DNL Auto-Allocate] relatório começa com o **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace], conforme mostrado abaixo. Faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: você pode escolher qualquer experiência.
1. **[!UICONTROL Métrica de normalização]**: seleciona Visitantes (os visitantes são incluídos no painel A4T por padrão). [!DNL Auto-Allocate] O sempre normaliza as taxas de conversão de acordo com visitantes únicos.
1. **[!UICONTROL Métricas de sucesso]**: selecione a mesma métrica usada durante a criação da atividade. Se isso foi um [!DNL Target] métrica de conversão definida, selecione **Conversão de atividade**. Caso contrário, selecione o [!DNL Adobe Analytics] que você usou.

![[!UICONTROL Analytics for Target] configuração do painel para [!DNL Auto-Allocate] atividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configuração do painel para [!DNL Auto-Allocate] atividades.*

Você também pode chegar a um pré-construído **[!UICONTROL Analytics for Target]** se você clicar no link da tela de relatório no [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversão] métricas [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar valor de métrica por visitante&quot;

Quando a métrica de meta é:

* Uma métrica de conversão do Target
* Métrica do Analytics com o critério de otimização &quot;Maximizar valor de métrica por visitante&quot;

O painel A4T padrão configura automaticamente o relatório.

Um exemplo desse painel é mostrado para a variável [!UICONTROL Receita] , em que &quot;Maximizar valor de métrica por visitante&quot; foi selecionado como critério de otimização no momento da criação da atividade. Como já foi referido, [!DNL Auto-Allocate] utilizou cálculos de confiança mais conservadores em comparação com os utilizados **[!UICONTROL Analytics for Target]** painel. A Adobe recomenda remover a métrica de confiança do painel A4T, bem como as métricas de aumento inferiores e superiores relacionadas. Em vez disso, faça referência aos valores de confiança em [!DNL Target] relatórios.

>[!NOTE]
>
>Os valores de confiança nos relatórios do A4T são menos conservadores do que [!DNL Target] relatório e pode indicar prematuramente um vencedor para uma [!UICONTROL Alocação automática] atividade.


![[!UICONTROL Relatório do Analytics for Target - Alocação automática] painel](assets/AAFigure2.png)

*Figura 2: O relatório recomendado para [!DNL Auto-Allocate] atividades com um [!DNL Analytics] métrica &quot;Maximizar valor de métrica por otimização de visitante&quot; critério. Para esses tipos de métricas, bem como [!DNL Target] métricas de conversão definidas, o padrão **[!UICONTROL Analytics for Target]**painel no [!DNL Analysis Workspace] pode ser usado.*

## [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar a taxa de conversão de visitante único&quot;

O critério de otimização &quot;Maximizar a taxa de conversão de visitante único&quot; refere-se à contagem de visitantes para os quais o valor da métrica é positivo. Por exemplo, se a taxa de conversão for definida como receita, o critério &quot;Maximizar a taxa de conversão do visitante único&quot; seria otimizado na contagem de visitantes únicos para os quais a receita foi maior que 0. Em outras palavras, esse critério maximizaria a contagem de visitantes que geram receita, em vez do valor da receita em si.

>[!NOTE]
>
>O índice de conversão referenciado aqui pode se referir a ações fora de pedidos, como cliques, impressões e assim por diante. Nesses casos, o critério ainda seria maximizar a contagem de visitantes que clicam ou visualizam a página, respectivamente.

A variável [!DNL Analytics for Target] painel no [!DNL Analysis Workspace] deve ser modificado se este critério de otimização for usado com um [!DNL Adobe Analytics] métrica.

Quando esse critério de otimização é usado, a métrica de sucesso é uma contagem de visitantes únicos para os quais a métrica de conversão foi positiva. Portanto, para visualizar esse valor, um novo segmento deve ser criado para filtrar as ocorrências com um valor positivo para a métrica.

Crie esse segmento da seguinte maneira:

1. Selecione o **[!UICONTROL Componentes]** > **[!UICONTROL Criar segmento]** opção no [!DNL Analysis Workspace] barra de ferramentas.
1. Arraste a métrica usada no momento da criação da atividade do painel esquerdo para a **[!UICONTROL Definição]** do segmento.
1. Selecionar valores da métrica que são **maior que** um valor numérico de 0.
1. No **[!UICONTROL Incluir]** selecione **[!UICONTROL Visitantes]**.
1. Dê um nome apropriado ao segmento.

Um exemplo da criação de segmento é mostrado na figura abaixo, onde a métrica de sucesso é [!UICONTROL Visitantes com receita positiva].

![[!UICONTROL Visitantes com receita positiva] segmento em [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Criação de segmentos para [!DNL Adobe Analytics] métricas com critérios de otimização iguais a &quot;[!UICONTROL Maximizar a taxa de conversão do visitante único].&quot; Neste exemplo, a métrica é [!UICONTROL Receita], e a meta de otimização é maximizar o número de visitantes com receita positiva.*

Após criar o segmento apropriado, você pode modificar o padrão  **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace] para exibir os valores dos critérios de otimização. Isso é feito fazendo o seguinte:

1. Adicionar um segundo **Visitantes únicos** juntamente com a métrica existente [!UICONTROL Visitantes] coluna de métrica.
2. Arraste o segmento recém-criado para baixo da primeira coluna para produzir um painel que se assemelha à Figura 4. Observe a diferença nos valores das colunas: o número de visitantes únicos com receita positiva deve ser uma fração do número total de visitantes únicos atribuídos a cada experiência (como mostrado abaixo).

   ![Figura4.png](assets/AAFigure4.png)

   *Figura 4: Filtragem [!UICONTROL Visitantes únicos] pelo segmento recém-criado*

3. Uma taxa de conversão pode ser [calculado rapidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) realçando a primeira e a segunda colunas, clicando com o botão direito do mouse, selecionando **[!UICONTROL Criar métrica a partir da seleção]** > **[!UICONTROL Divisão]**.

   A taxa de conversão padrão deve ser removida e substituída por essa nova métrica calculada, como mostrado na imagem abaixo. Talvez seja necessário editar a métrica calculada recém-criada para exibir como uma **[!UICONTROL Formato]** > **[!UICONTROL Percentual]** até duas casas decimais, como mostrado.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: A versão final [!UICONTROL Alocação automática] painel que mostra as taxas de conversão para uma métrica de conversão de receita binarizada*

## Resumo

As etapas deste tutorial demonstraram como configurar corretamente [!DNL Analysis Workspace] para exibir [!UICONTROL Alocação automática] dados de relatórios.

Para resumir:

* Quando a métrica é uma [!DNL Target] métrica de conversão definida ou um [!DNL Adobe Analytics] métrica com critério de otimização &quot;Maximizar valor de métrica por visitante&quot;, o painel do espaço de trabalho padrão configurado com visitantes como uma métrica de normalização deve ser usado.
* Quando a métrica é uma [!DNL Adobe Analytics] com critério de otimização &quot;Maximizar a taxa de conversão de visitante único&quot;, você deve determinar a fração de visitantes com valor de métrica positivo em relação ao total de visitantes. Isso é feito criando um segmento correspondente que filtra as [!UICONTROL Visitante único] nessa métrica.
