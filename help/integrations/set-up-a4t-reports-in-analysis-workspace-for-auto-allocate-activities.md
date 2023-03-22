---
title: Como configurar relatórios do A4T em [!DNL Analysis Workspace] para [!UICONTROL Alocação automática] Atividades
description: Como configurar relatórios do A4T em [!DNL Analysis Workspace] para obter os resultados esperados durante a execução [!UICONTROL Alocação automática] atividades.
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 1dc33affb1e9782f1b9c1d01402124dd40dac436
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Configuração de relatórios do A4T em [!DNL Analysis Workspace] para [!DNL Auto-Allocate] atividades

Um [!DNL Auto-Allocate] identifica um vencedor entre duas ou mais experiências e realoca automaticamente mais tráfego para o vencedor enquanto o teste continua a ser executado e aprendido. O [!UICONTROL Analytics para Target] Integração do (A4T) para [!UICONTROL Alocação automática] permite que você veja seus dados de relatório em [!DNL Adobe Analytics]e você também pode otimizar para eventos personalizados ou métricas definidas no [!DNL Analytics].

Embora os recursos de análise avançada estejam disponíveis em [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão **[!UICONTROL Analytics para Target]** são necessários para interpretar corretamente o painel [!DNL Auto-Allocate] , devido às nuances em [critérios de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Este tutorial aborda as modificações recomendadas para analisar [!DNL Auto-Allocate] atividades em [!DNL Analysis Workspace]. Os principais conceitos são:

* [!UICONTROL Visitantes] deve ser sempre usada como a métrica de normalização em [!DNL Auto-Allocate] atividades.
* Quando a métrica é uma [!DNL Adobe Analytics] , o numerador apropriado para a taxa de conversão depende do tipo de critério de otimização escolhido durante a configuração da atividade.
   * O critério de otimização &quot;maximizar a taxa de conversão de visitante único&quot; tem uma taxa de conversão cujo numerador é uma contagem de visitantes únicos com um valor positivo da métrica.
   * O &quot;valor de métrica maximizada por visitante&quot; tem uma taxa de conversão cujo numerador é o valor de métrica regular em [!DNL Adobe Analytics]. Isso é fornecido por padrão no **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace].
* Quando sua métrica de otimização é uma [!DNL Target] métrica de conversão definida, o padrão **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace] O controla a configuração do painel.
* Para todos [!UICONTROL Alocação automática] atividades criadas antes da [!DNL Target Standard/Premium] Versão 23.3.1 (28 de março de 2023) [!DNL Analytics Workspace] e [!DNL Target] exibir o mesmo valor para [!UICONTROL Confiança].

   Para todos [!UICONTROL Alocação automática] atividades criadas após 28 de março de 2023, os valores do intervalo de confiança são vistos em [!DNL Analysis Workspace] não reflita o [estatísticas mais conservadoras usadas por [!UICONTROL Alocação automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} se essas atividades tiverem *both* das seguintes condições:

   * [!DNL Analytics] como fonte de geração de relatórios (A4T)
   * [!DNL Analytics] métricas de otimização

   If *both* Dessas condições, as métricas de confiança devem ser removidas do painel A4T. Em vez disso, faça referência a esses valores em [!DNL Target] relatórios.

## Criar o A4T para [!DNL Auto-Allocate] no painel [!DNL Analysis Workspace]

Para criar um A4T para [!DNL Auto-Allocate] início do relatório com **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace], conforme mostrado abaixo. Em seguida, faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: Você pode escolher qualquer experiência.
2. **[!UICONTROL Métrica de normalização]**: Selecione Visitantes. [!DNL Auto-Allocate] O sempre normaliza as taxas de conversão por visitantes únicos.
3. **[!UICONTROL Métricas de sucesso]**: Selecione a mesma métrica que você usou durante a criação da atividade. Se isso fosse um [!DNL Target] métrica de conversão definida, selecione **Conversão de atividade**. Caso contrário, selecione a [!DNL Adobe Analytics] métrica utilizada.

![[!UICONTROL Analytics para Target] configuração do painel para [!DNL Auto-Allocate] atividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics para Target] configuração do painel para [!DNL Auto-Allocate] atividades.*

>[!NOTE]
>
> Você também pode chegar a um **[!UICONTROL Analytics para Target]** se você clicar no link da tela de relatório em [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversão] métricas ou [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar valor de métrica por visitante&quot;

Os identificadores padrão do painel A4T [!DNL Auto-Allocate] atividades nas quais a métrica de meta é uma [!DNL Target] conversão ou [!DNL Analytics] métrica com critério de otimização &quot;Maximizar valor da métrica por visitante&quot;.

Um exemplo desse painel é mostrado para a variável [!UICONTROL Receita] , onde &quot;Maximizar valor de métrica por visitante&quot; foi selecionado como o critério de otimização no momento da criação da atividade. Como mencionado anteriormente, [!DNL Auto-Allocate] O usa cálculos de confiança mais conservadores em comparação com os usados no **[!UICONTROL Analytics para Target]** painel. O Adobe recomenda remover a métrica de confiança do painel A4T, bem como as métricas de aumento superior e inferior relacionadas. Em vez disso, faça referência a esses valores em [!DNL Target] relatórios.

![[!UICONTROL Analytics for Target - Relatório de alocação automática] painel](assets/AAFigure2.png)

*Figura 2: O relatório recomendado para [!DNL Auto-Allocate] com uma [!DNL Analytics] métrica &quot;Maximizar valor de métrica por otimização do visitante&quot;. Para esses tipos de métricas, assim como [!DNL Target] métricas de conversão definidas, o padrão **[!UICONTROL Analytics para Target]**no painel [!DNL Analysis Workspace] pode ser usada.*

## [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar taxa de conversão de visitantes únicos&quot;

Quando uma [!DNL Adobe Analytics] é usada com um critério de otimização de *Maximizar a taxa de conversão de visitantes únicos*, o padrão **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace] deve ser modificado.

A métrica de sucesso agora é uma contagem de visitantes únicos para os quais a métrica de conversão foi positiva. Isso pode ser feito criando um segmento que filtra as ocorrências com um valor positivo da métrica. Crie este segmento da seguinte maneira:

1. Selecione o **[!UICONTROL Componentes]** > **[!UICONTROL Criar segmento]** na [!DNL Analysis Workspace] barra de ferramentas.
1. Arraste a métrica usada no momento da criação da atividade do painel esquerdo para a **[!UICONTROL Definição]** caixa do segmento.
1. Selecione os valores da métrica que são **maior que** um valor numérico de 0.
1. No **[!UICONTROL Incluir]** , selecione **[!UICONTROL Visitantes]**.
1. Dê um nome apropriado ao seu segmento.

Um exemplo da criação de segmentos é mostrado na figura abaixo, onde você seleciona [!UICONTROL Visitantes Com Receita Positiva].

![[!UICONTROL Visitantes com receita positiva] segmento no [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Criação de segmentos para [!DNL Adobe Analytics] métricas com critérios de otimização iguais a &quot;[!UICONTROL Maximizar a taxa de conversão de visitantes únicos].&quot; Neste exemplo, a métrica é [!UICONTROL Receita]e a meta da otimização é maximizar o número de visitantes com receita positiva.*

Depois que o segmento apropriado for criado, o padrão  **[!UICONTROL Analytics para Target]** no painel [!DNL Analysis Workspace] pode ser modificado.

1. Adicionar um segundo **Visitantes únicos** ao lado da métrica existente [!UICONTROL Visitantes] coluna de métrica.
2. Arraste o segmento recém-criado abaixo da primeira coluna para produzir um painel que se assemelhe à Figura 4. Observe a diferença: o número de visitantes únicos com receita positiva é uma fração do número total de visitantes únicos atribuídos a cada experiência.

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtragem [!UICONTROL Visitantes únicos] pelo segmento recém-criado*

3. Uma taxa de conversão pode ser [rapidamente calculado](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) destacando a primeira e a segunda colunas, clicando com o botão direito do mouse, selecionando **[!UICONTROL Criar métrica a partir da seleção]** > **[!UICONTROL Dividir]**.

   A taxa de conversão padrão deve ser removida e substituída por essa nova métrica calculada, como mostrado na imagem abaixo. Talvez seja necessário editar a métrica calculada recém-criada para ser exibida como uma **[!UICONTROL Formato]** > **[!UICONTROL Porcentagem]** até duas casas decimais, como mostrado.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: A final [!UICONTROL Alocação automática] painel mostrando as taxas de conversão de uma métrica de conversão de receita binarizada*

## Resumo

As etapas neste tutorial demonstraram como configurar corretamente [!DNL Analysis Workspace] para exibir [!UICONTROL Alocação automática] dados de relatório.

Para resumir:

* Quando a métrica é uma [!DNL Target] métrica de conversão definida ou uma [!DNL Adobe Analytics] métrica com critério de otimização &quot;Maximizar valor de métrica por visitante&quot;, o painel do espaço de trabalho padrão configurado com visitantes como métrica de normalização deve ser usado.
* Quando a métrica é uma [!DNL Adobe Analytics] métrica com critério de otimização &quot;Maximizar taxa de conversão de visitante único&quot;, você deve usar uma taxa de conversão definida como a fração de visitantes para os quais a métrica é positiva. Isso é feito criando um segmento correspondente que filtra a variável [!UICONTROL Visitante único] métrica.
