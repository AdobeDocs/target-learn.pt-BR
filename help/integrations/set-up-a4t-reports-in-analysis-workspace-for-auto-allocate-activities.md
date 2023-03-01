---
title: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para [!UICONTROL Alocação automática] Atividades
description: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para obter os resultados esperados durante a execução [!UICONTROL Alocação automática] atividades.
badgeBeta: label="Beta" type="Informative"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: ba33152906afda02ebf65365d9783ba8a4ea3c83
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# Configuração de relatórios do A4T no [!DNL Analysis Workspace] para [!DNL Auto-Allocate] atividades

>[!NOTE]
>
>No momento, essa funcionalidade está na versão beta e estará disponível para todos [!UICONTROL Target] clientes em uma versão futura.

Um [!DNL Auto-Allocate] a atividade identifica um vencedor entre duas ou mais experiências e realoca automaticamente mais tráfego para o vencedor enquanto o teste continua a ser executado e aprendido. A variável [!UICONTROL Analytics for Target] Integração do (A4T) para [!UICONTROL Alocação automática] permite visualizar os dados de relatórios no [!DNL Adobe Analytics]e você pode até otimizar para eventos ou métricas personalizados definidos em [!DNL Analytics].

Embora os recursos avançados de análise estejam disponíveis no [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão **[!UICONTROL Analytics for Target]** para interpretar corretamente as [!DNL Auto-Allocate] atividades, devido às nuances nas [critérios de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Este tutorial aborda as modificações recomendadas para análise [!DNL Auto-Allocate] atividades no [!DNL Analysis Workspace]. Os principais conceitos são:

* [!UICONTROL Visitantes] deve ser sempre usada como a métrica de normalização em [!DNL Auto-Allocate] atividades.
* Quando a métrica é uma [!DNL Adobe Analytics] , o numerador apropriado para a taxa de conversão depende do tipo de critérios de otimização escolhidos durante a configuração da atividade.
   * O critério de otimização &quot;maximizar a taxa de conversão de visitante único&quot; tem uma taxa de conversão cujo numerador é uma contagem dos visitantes únicos com um valor positivo da métrica.
   * O &quot;valor máximo de métrica por visitante* tem uma taxa de conversão cujo numerador é o valor de métrica regular em [!DNL Adobe Analytics]. Isso é fornecido por padrão no **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace].
* Quando sua métrica de otimização é uma [!DNL Target] métrica de conversão definida, o padrão **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace] O lida com a configuração do seu painel.
* A variável [!UICONTROL Confiança] números vistos em [!DNL Analysis Workspace] não refletem a [estatísticas mais conservadoras usadas pelo [!UICONTROL Alocação automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), e assim devem ser removidos.

## Criar o A4T para [!DNL Auto-Allocate] painel no [!DNL Analysis Workspace]

Para criar um A4T para [!DNL Auto-Allocate] relatório começa com o **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace], conforme mostrado abaixo. Faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: você pode escolher qualquer experiência.
2. **[!UICONTROL Métrica de normalização]**: selecione Visitors. [!DNL Auto-Allocate] O sempre normaliza as taxas de conversão de acordo com visitantes únicos.
3. **[!UICONTROL Métricas de sucesso]**: selecione a mesma métrica usada durante a criação da atividade. Se isso foi um [!DNL Target] métrica de conversão definida, selecione **Conversão de atividade**. Caso contrário, selecione o [!DNL Adobe Analytics] que você usou.

![[!UICONTROL Analytics for Target] configuração do painel para [!DNL Auto-Allocate] atividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configuração do painel para [!DNL Auto-Allocate] atividades.*

>[!NOTE]
>
> Você também pode chegar a um pré-construído **[!UICONTROL Analytics for Target]** se você clicar no link da tela de relatório no [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversão] métricas [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar valor de métrica por visitante&quot;

As alças padrão do painel A4T [!DNL Auto-Allocate] atividades nas quais a métrica de meta é uma [!DNL Target] conversão ou um [!DNL Analytics] com critério de otimização &quot;Maximizar valor de métrica por visitante&quot;.

Um exemplo desse painel é mostrado para a variável [!UICONTROL Receita] , em que &quot;Maximizar valor de métrica por visitante&quot; foi selecionado como critério de otimização no momento da criação da atividade. Como já foi referido, [!DNL Auto-Allocate] utilizou cálculos de confiança mais conservadores em comparação com os utilizados **[!UICONTROL Analytics for Target]** painel. A Adobe recomenda remover a métrica de confiança, bem como as métricas de aumento inferiores e superiores relacionadas.

![[!UICONTROL Relatório do Analytics for Target - Alocação automática] painel](assets/AAFigure2.png)

*Figura 2: O relatório recomendado para [!DNL Auto-Allocate] atividades com um [!DNL Analytics] métrica &quot;Maximizar valor de métrica por otimização de visitante&quot; critério. Para esses tipos de métricas, bem como [!DNL Target] métricas de conversão definidas, o padrão **[!UICONTROL Analytics for Target]**painel no [!DNL Analysis Workspace] pode ser usado.*

## [!DNL Analytics] métricas com os critérios de otimização &quot;Maximizar a taxa de conversão de visitante único&quot;

Quando um [!DNL Adobe Analytics] é usada com um critério de otimização de *Maximizar a taxa de conversão do visitante único*, o padrão **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace] deve ser modificado.

A métrica de sucesso agora é uma contagem de visitantes únicos para os quais a métrica de conversão foi positiva. Isso pode ser feito criando um segmento que filtre as ocorrências com um valor positivo da métrica. Crie esse segmento da seguinte maneira:

1. Selecione o **[!UICONTROL Componentes]** > **[!UICONTROL Criar segmento]** opção no [!DNL Analysis Workspace] barra de ferramentas.
1. Arraste a métrica usada no momento da criação da atividade do painel esquerdo para a **[!UICONTROL Definição]** do segmento.
1. Selecionar valores da métrica que são **maior que** um valor numérico de 0.
1. No **[!UICONTROL Incluir]** selecione **[!UICONTROL Visitantes]**.
1. Dê um nome apropriado ao segmento.

Um exemplo da criação de segmento é mostrado na figura abaixo, onde você seleciona [!UICONTROL Visitantes com receita positiva].

![[!UICONTROL Visitantes com receita positiva] segmento em [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Criação de segmentos para [!DNL Adobe Analytics] métricas com critérios de otimização iguais a &quot;[!UICONTROL Maximizar a taxa de conversão do visitante único].&quot; Neste exemplo, a métrica é [!UICONTROL Receita], e a meta de otimização é maximizar o número de visitantes com receita positiva.*

Após a criação do segmento apropriado, o padrão  **[!UICONTROL Analytics for Target]** painel no [!DNL Analysis Workspace] pode ser modificado.

1. Adicionar um segundo **Visitantes únicos** juntamente com a métrica existente [!UICONTROL Visitantes] coluna de métrica.
2. Arraste o segmento recém-criado para baixo da primeira coluna para produzir um painel que se assemelha à Figura 4. Observe a diferença: o número de visitantes únicos com receita positiva é uma fração do número total de visitantes únicos atribuídos a cada experiência.

   ![Figura4.png](assets/AAFigure4.png)

   *Figura 4: Filtragem [!UICONTROL Visitantes únicos] pelo segmento recém-criado*

3. Uma taxa de conversão pode ser [calculado rapidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) realçando a primeira e a segunda colunas, clicando com o botão direito do mouse, selecionando **[!UICONTROL Criar métrica a partir da seleção]** > **[!UICONTROL Divisão]**.

   A taxa de conversão padrão deve ser removida e substituída por essa nova métrica calculada, como mostrado na imagem abaixo. Talvez seja necessário editar a métrica calculada recém-criada para exibir como uma **[!UICONTROL Formato]** > **[!UICONTROL Percentual]** até duas casas decimais, como mostrado.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: A versão final [!UICONTROL Alocação automática] painel que mostra as taxas de conversão para uma métrica de conversão de receita binarizada*

## Resumo

As etapas deste tutorial demonstraram como configurar corretamente [!DNL Analysis Workspace] para exibir [!UICONTROL Alocação automática] dados de relatórios.

Para resumir:

* Quando a métrica é uma [!DNL Target] métrica de conversão definida ou um [!DNL Adobe Analytics] métrica com critério de otimização &quot;Maximizar valor de métrica por visitante&quot;, o painel do espaço de trabalho padrão configurado com visitantes como uma métrica de normalização deve ser usado.
* Quando a métrica é uma [!DNL Adobe Analytics] com critério de otimização &quot;Maximizar a taxa de conversão de visitantes únicos&quot;, você deve usar uma taxa de conversão definida como a fração de visitantes para os quais a métrica é positiva. Isso é feito criando um segmento correspondente que filtra as [!UICONTROL Visitante único] métrica.
