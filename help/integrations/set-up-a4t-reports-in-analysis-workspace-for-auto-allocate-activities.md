---
title: Como configurar relatórios do A4T no Analysis Workspace para atividades de alocação automática
description: Depois que a integração do Analytics for Target (A4T) estiver em vigor e você estiver executando atividades de Alocação automática, como você pode garantir que está interpretando os resultados corretamente? Siga estas etapas para configurar relatórios do A4T no Analysis Workspace para obter os resultados esperados ao executar atividades de Alocação automática.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: null
source-git-commit: eb7232f1c6ed52860aa5ef86b50427fb96ab7894
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Configuração de relatórios do A4T no Analysis Workspace para [!DNL Auto-Allocate] atividades

Um [!DNL Auto-Allocate] identifica um vencedor entre duas ou mais experiências e realoca automaticamente mais tráfego para o vencedor enquanto o teste continua a ser executado e aprendido. A integração do Analytics for Target (A4T) para o [!DNL Auto-Allocate] O permite visualizar seus dados de relatórios no Adobe Analytics e também pode otimizar para eventos personalizados ou métricas definidas no Adobe Analytics.

Embora os recursos de análise avançada estejam disponíveis no Adobe Analytics Analysis Workspace, algumas modificações no padrão **[!UICONTROL Analytics para Target]** são necessários para interpretar corretamente o painel [!DNL Auto-Allocate] , devido às nuances em [critérios de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Este tutorial aborda as modificações recomendadas para analisar [!DNL Auto-Allocate] no Workspace. Os principais conceitos são:

* Os visitantes devem ser sempre usados como a métrica de normalização em [!DNL Auto-Allocate] atividades.
* Quando a métrica é uma Métrica do Adobe Analytics, o numerador apropriado para a taxa de conversão depende do tipo de critério de otimização escolhido durante a configuração da atividade.
   * O critério de otimização &quot;maximizar a taxa de conversão de visitante único&quot; tem uma taxa de conversão cujo numerador é uma contagem de visitantes únicos com um valor positivo da métrica.
   * O &quot;valor máximo da métrica por visitante*&quot; tem uma taxa de conversão cujo numerador é o valor da métrica regular no Adobe Analytics. Isso é fornecido por padrão no **[!UICONTROL Analytics para Target]** no Workspace.
* Quando sua métrica de otimização é uma métrica de conversão definida pelo Target, o valor padrão **[!UICONTROL Analytics para Target]** no Workspace manipula a configuração do painel.
* Os números de confiança vistos no Workspace não refletem o [estatísticas mais conservadoras usadas pela alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629)e assim deve ser removido.


## Criar o A4T para [!DNL Auto-Allocate] painel no Workspace

Para criar um A4T para [!DNL Auto-Allocate] início do relatório com **[!UICONTROL Analytics para Target]** no Workspace, como mostrado abaixo. Em seguida, faça as seguintes seleções:

1. **[!UICONTROL Experiência de controle]**: Você pode escolher qualquer experiência
2. **[!UICONTROL Métrica de normalização]**: Selecionar visitantes - A alocação automática sempre normaliza as taxas de conversão por visitantes únicos.
3. **[!UICONTROL Métricas de sucesso]**: Selecione a mesma métrica que você usou durante a criação da atividade. Se essa for uma métrica de Conversão definida pelo Target, selecione **Conversão de atividade**. Caso contrário, selecione a métrica do Adobe Analytics que você usou.

![AAFigure1.png](assets/AAFigure1.png)
*Figura 1: Configuração do painel do Analytics for Target para [!DNL Auto-Allocate] atividades.*

>[!NOTE]
>
> Você também pode chegar a um **[!UICONTROL Analytics para Target]** painel se você clicar no link da tela de relatório no Adobe Target.

## Métricas de conversão do Target ou métricas do Analytics com os critérios de otimização &quot;Maximizar valor da métrica por visitante&quot;

Os identificadores padrão do painel A4T [!DNL Auto-Allocate] atividades nas quais a métrica de meta é uma Conversão do Target ou uma métrica do Analytics com critério de otimização &quot;Maximizar valor da métrica por visitante&quot;.

Um exemplo desse painel é mostrado para a métrica Receita, onde &quot;Maximizar valor de métrica por visitante&quot; foi selecionado como o critério de otimização no momento da criação da atividade. Como mencionado anteriormente, [!DNL Auto-Allocate] O usa cálculos de confiança mais conservadores em comparação aos usados pela **[!UICONTROL Analytics para Target]** painel. Portanto, é recomendável remover a métrica de confiança, bem como as métricas de aumento superior e inferior relacionadas.

![Figura 2.png](assets/AAFigure2.png)
*Figura 2: O relatório recomendado para [!DNL Auto-Allocate] atividades com uma métrica do Analytics Maximizar valor da métrica por critério de otimização do visitante. Para esses tipos de métricas, assim como as métricas de conversão definidas pelo Target, o padrão **[!UICONTROL Analytics para Target]**no espaço de trabalho pode ser usado.*


## Métricas do Analytics com critérios de otimização de &quot;Maximizar taxa de conversão de visitantes únicos&quot;

Quando uma métrica do Adobe Analytics é usada com um critério de otimização de *Maximizar a taxa de conversão de visitantes únicos*, o padrão **[!UICONTROL Analytics para Target]** no espaço de trabalho deve ser modificado.

A métrica de sucesso agora é uma contagem de visitantes únicos para os quais a métrica de conversão foi positiva. Isso pode ser feito criando um segmento que filtra as ocorrências com um valor positivo da métrica. Crie este segmento da seguinte maneira:

1. Selecione o **Componentes** > **Criar segmento** na barra de ferramentas do Workspace.
1. Arraste a métrica usada no momento da criação da atividade do painel esquerdo para o **Definição** caixa do segmento.
1. Selecione os valores da métrica que são **maior que** um valor numérico de 0.
1. No **Incluir** lista suspensa, selecione **Visitantes**
1. Dê um nome adequado ao seu segmento

Um exemplo da criação de segmento é mostrado na figura abaixo, onde selecionamos visitantes para os quais a Receita é positiva.

![Figura 3.png](assets/AAFigure3.png)
*Figura 3: Criação de segmentos para métricas do Adobe Analytics com critérios de otimização iguais a Maximizar taxa de conversão de visitante único. Neste exemplo, a métrica é Receita, e o objetivo da otimização é maximizar o número de visitantes com receita positiva.*

Depois que o segmento apropriado for criado, o padrão  **[!UICONTROL Analytics para Target]** no espaço de trabalho pode ser modificado.

1. Adicionar um segundo **Visitantes únicos** ao lado da coluna de métrica visitantes existente
2. Arraste o segmento recém-criado abaixo da primeira coluna para produzir um painel semelhante à Figura 4. Observe a diferença - o número de visitantes únicos com receita positiva é uma fração do número total de visitantes únicos atribuídos a cada experiência.
   ![Figura 4.png](assets/AAFigure4.png)
   *Figura 4: Filtragem de visitantes únicos pelo segmento recém-criado*
3. Uma taxa de conversão pode ser [rapidamente calculado](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) destacando a primeira e a segunda colunas, clicando com o botão direito do mouse, selecionando **Criar métrica a partir da seleção** > **Dividir**. A taxa de conversão padrão deve ser removida e substituída por essa nova métrica calculada, como mostrado na imagem abaixo. Talvez seja necessário editar a métrica calculada recém-criada para ser exibida como uma **Formato** > **Porcentagem** até duas casas decimais, como mostrado.
   ![Figura 4.png](assets/AAFigure5.png)

   *Figura 4: O painel Alocação automática final que mostra as taxas de conversão de uma métrica binarizada de conversão de receita*


## Conclusão 

As etapas acima demonstraram como configurar corretamente [!DNL Workspace] para exibir os dados de relatório de Alocação automática . Para resumir:

* Quando a métrica for uma métrica de conversão definida pelo Target ou uma Métrica do Adobe Analytics com critério de otimização *Maximizar valor de métrica por visitante*, o painel espaço de trabalho padrão configurado com visitantes como métrica de normalização deve ser usado.
* Quando a métrica for uma métrica do Adobe Analytics com critério de otimização &quot;Maximizar taxa de conversão de visitante único&quot;, você deverá usar uma taxa de conversão definida como a fração de visitantes para os quais a métrica é positiva. Isso é feito criando um segmento correspondente, que filtra a métrica de visitante único.
