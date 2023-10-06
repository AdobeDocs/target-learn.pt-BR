---
title: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para [!UICONTROL Alocação automática] Atividades
description: Como configurar [!UICONTROL Analytics for Target] Relatórios do (A4T) no [!DNL Adobe] [!DNL Analysis Workspace] ao executar [!UICONTROL Alocação automática] atividades.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 194579db80fdac60e204e36ab769975be2795eee
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 0%

---

# Configuração de relatórios do A4T no [!DNL Analysis Workspace] para [!DNL Auto-Allocate] atividades

Um [!UICONTROL Alocação automática] atividade no [!DNL Adobe Target] O identifica um vencedor entre duas ou mais experiências e realoca automaticamente o tráfego de visitantes para o vencedor enquanto o teste continua a ser executado e aprendido. A variável [!UICONTROL Analytics for Target] Integração do (A4T) para [!UICONTROL Alocação automática] permite exibir dados de relatórios em [!DNL Adobe Analytics]e você poderá otimizar para eventos ou métricas personalizados definidos em [!DNL Analytics].

Embora os recursos avançados de análise estejam disponíveis no [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no padrão [!UICONTROL Analytics for Target] pode ser necessário para interpretar corretamente [!UICONTROL Alocação automática] atividades. Essas modificações são necessárias devido às nuances nas [critérios de métrica de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Cada tipo de métrica de otimização requer uma configuração de relatório diferente no A4T, da seguinte maneira:

* Uso de um [!DNL Analytics] métrica

   * [!UICONTROL Maximizar valor de métrica por visitante]
   * [!UICONTROL Maximizar o índice de conversão de visitantes únicos]

* Uso de um [!DNL Target]métrica de conversão definida pelo

Este tutorial aborda a orientação geral do A4T e as etapas de configuração de relatório específicas dos critérios.

## Orientações gerais para [!UICONTROL Analytics for Target] (A4T) {#guidance}

É possível navegar para um modelo pré-criado [!UICONTROL Analytics for Target] clicando no link da tela de relatório no [!UICONTROL Adobe Target] (isso é mencionado posteriormente neste guia como o &quot;[!DNL Target]relatório acionado pelo (&quot;). Como alternativa, você pode criar o painel A4T no [!DNL Analytics] (detalhes mais adiante nesta seção).

As seções a seguir especificam quais configurações são necessárias, dependendo de quais desses métodos você escolher:

* As métricas de confiança devem ser removidas do painel A4T, independentemente do método de criação do painel (ambos são detalhados abaixo). Em vez disso, faça referência a esses valores em [!DNL Target] relatórios. Além disso, os vencedores da atividade podem ser identificados em [!DNL Target] relatórios. Detalhes sobre a identificação do vencedor da atividade podem ser encontrados na [Identificar o vencedor da atividade](#winner) abaixo.
>>
* Para evitar confusão, desmarque a opção &quot;[!UICONTROL Percentual]&quot;Apresentação da [!UICONTROL Índice de conversão] métrica. Para obter mais informações, consulte [Ocultar a porcentagem da variável [!UICONTROL Índice de conversão] coluna](#hide-percentage) abaixo.
>>
* Se estiver criando um painel A4T, verifique se os intervalos de data e hora correspondem aos do [!DNL Target] relatório. Para obter mais informações, consulte [Alinhar a data e a hora no painel A4T](#aligning-date-and-time) abaixo.

### Ocultar a porcentagem da variável [!UICONTROL Índice de conversão] coluna {#hide-percentage}

1. Clique em **engrenagem** ícone ao lado do título da variável [!UICONTROL Índice de conversão] coluna.

   ![Ícone de engrenagem na coluna Taxa de conversão](/help/integrations/assets/coversion-rate-gear-icon.png)

   A variável [!UICONTROL Coluna] caixa de diálogo de configurações é exibida:

   ![Caixa de diálogo Configurações de coluna](/help/integrations/assets/column-settings-dialog-box.png)

1. Desmarque a opção **[!UICONTROL Percentual]** caixa de seleção

Seu painel A4T agora não inclui porcentagens como Taxa de conversão e corresponde a [!DNL Target], conforme mostrado abaixo:

![A coluna Taxa de conversão não exibe porcentagens](/help/integrations/assets/no-percentages.png)

### Alinhar a data e a hora no painel A4T {#aligning-date-and-time}

1. Acima de cada painel, verifique o intervalo de datas referenciado pelo painel para garantir que o intervalo de datas corresponda ao do [!DNL Target] relatório.

   ![Intervalo de datas no painel A4T](/help/integrations/assets/date-range.png)

1. Entrada [!DNL Analytics], defina o intervalo de tempo como 12h - 11h59min.

### Identificar o vencedor da atividade {#winner}

[!DNL Auto-Allocate] os vencedores da atividade são selecionados quando há uma taxa de conversão vencedora com valores de confiança maiores ou iguais a 95%. Esses valores devem ser referenciados na variável [!DNL Target] relatórios, já que os cálculos de confiança refletem os métodos mais [!DNL Target] recomenda para [!UICONTROL Alocação automática] atividades. Para obter mais informações, consulte [Garantias estatísticas da alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} no *[!UICONTROL Guia do profissional de negócios do Adobe Target]*.

>[!NOTE]
>
Os emblemas &quot;Ainda não há vencedor&quot; e &quot;Vencedor&quot; não estão disponíveis no painel A4T no [!DNL Analysis Workspace] e também não disponível no [!DNL Target] relatório. Para obter mais informações, consulte [Alocação automática](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *Suporte do A4T para atividades de Alocação automática e Direcionamento automático* no *[!UICONTROL Guia do profissional de negócios do Adobe Target]*.

## Criar o A4T para [!UICONTROL Alocação automática] painel no [!DNL Analysis Workspace]

1. Para criar um painel A4T para um [!UICONTROL Alocação automática] relatório de atividades, comece com o [!UICONTROL Analytics for Target] painel no [!DNL Analysis Workspace], conforme mostrado abaixo.

   ![Analytics for Target - Relatório de alocação automática](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Faça as seguintes seleções:

   * **[!UICONTROL Experiência de controle]**: escolha qualquer experiência.
   * **[!UICONTROL Métrica de normalização]**: Selecionar **[!UICONTROL Visitantes]** (incluído no painel A4T por padrão). [!UICONTROL Alocação automática] O sempre normaliza as taxas de conversão de acordo com visitantes únicos.
   * **Métricas de sucesso**: selecione a mesma métrica (otimização) usada durante a criação da atividade. Se isso foi um [!DNL Target]métrica de conversão definida por, selecione **[!UICONTROL Conversão de atividade]**. Caso contrário, selecione o [!DNL Adobe Analytics] que você usou.

## Métricas do Analytics com &quot;[!UICONTROL Maximizar valor de métrica por visitante]&quot; critérios de otimização

**Definição**: (Valor de métrica geral) / (# de visitantes)

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

![Maximizar o valor de métrica para a receita](/help/integrations/assets/maximize-metric-value-revenue.png)

| Alterações necessárias | [!DNL Target]relatório acionado por | Relatório do painel A4T |
| --- | --- | --- |
| Maximizar valor de métrica para um [!DNL Analytics] métrica | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>[!UICONTROL Aumento (Baixo)] e [!UICONTROL Lift (alto)] deve ser removido.</li><li>A métrica da taxa de conversão deve ser renomeada para &quot;Métrica/Visitante&quot;.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>[!UICONTROL Aumento (Baixo)] e [!UICONTROL Lift (alto)] deve ser removido.</li><li>A métrica da taxa de conversão deve ser renomeada para &quot;Métrica/Visitante&quot;.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê na variável [!DNL Target] relatório. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> |

## [!DNL Analytics] métricas com &quot;[!UICONTROL Índice de conversão de visitante único]&quot; critérios de otimização

**Definição**: (# de Visitantes únicos com um valor positivo da métrica) / (Número total de Visitantes únicos)

Exemplo: suponha que sua métrica de otimização seja [!UICONTROL Receita]. Há cinco visitantes únicos na atividade e três desses visitantes únicos fazem uma compra. Neste exemplo, este valor = (3 visitantes para os quais [!UICONTROL Receita] é positivo) / (5 total de visitantes únicos) = 0,6 = 60%.

>[!NOTE]
>
O índice de conversão referenciado aqui pode se referir a ações fora de pedidos, como cliques, impressões e assim por diante. Nesses casos, o critério ainda seria maximizar a contagem de visitantes que clicam ou visualizam a página, respectivamente.

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

| Alterações necessárias | Relatório acionado pelo Target | Relatório do painel A4T |
| --- | --- | --- |
| Maximizar conversões para um [!DNL Analytics] métrica | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>Todos [!UICONTROL Elevação] métricas devem ser removidas.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. (Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>Todos [!UICONTROL Elevação] métricas devem ser removidas.</li><li>Crie um segmento para filtrar visitantes com um valor de métrica positivo que visualizaram a atividade analisada. Para obter mais informações, consulte [Criar um segmento](#segment) abaixo.</li><li>Substitua o preenchido automaticamente [!UICONTROL Índice de conversão] para que seja a divisão entre [!UICONTROL Visitantes únicos] com um valor de métrica positivo e visitantes únicos. Para obter mais informações, consulte [Atualizar a métrica Taxa de conversão](#update-conversion-metric) abaixo.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê na variável [!DNL Target] relatório. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> |

### Relatório do painel A4T padrão - orientação adicional

As seções a seguir contêm mais informações sobre orientações adicionais à medida que você configura o relatório padrão do painel A4T.

#### Criar um segmento {#segment}

1. Clique em **Sinal &quot;+&quot;** ao lado de **[!UICONTROL Segmentos]** no painel esquerdo.

   ![Sinal de mais ao lado de segmentos no painel esquerdo.](/help/integrations/assets/plus-sign.png)

1. Atribua um título ao segmento &quot;Visitantes com valor de métrica positivo&quot;.
1. Em **[!UICONTROL Definição]**, ao lado de **[!UICONTROL Incluir]**, selecione **[!UICONTROL Visitante]**.
1. Em **[!UICONTROL Definição]**, selecione a métrica de otimização na atividade.

   Neste exemplo, considere [!UICONTROL Receita] como a métrica de otimização.

1. Selecione o &quot;[!UICONTROL é maior que]&quot; e especifique &quot;0&quot;.

   Essas configurações filtram para todos os visitantes com um valor de métrica positivo.

1. Clique em **[!UICONTROL Salvar]**.

   ![Valor de métrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Adicione o segmento recém-criado chamado &quot;Visitantes com valor de métrica positivo&quot; ao painel A4T.
1. Arraste e solte a [!UICONTROL Visitantes únicos] na mesma coluna que &quot;Visitantes com valor de métrica positivo&quot;.

   Essa configuração cria um segmento de todos os visitantes únicos para os quais o valor da métrica é positivo. Neste exemplo, todos os visitantes únicos cuja receita foi maior que zero.

#### Atualize o [!UICONTROL Índice de conversão] métrica {#update-conversion-metric}

1. Se ainda não tiver feito isso, remova a existente [!UICONTROL Índice de conversão] do painel, conforme explicado acima.
1. Adicione uma métrica clicando no sinal &quot;+&quot; ao lado da variável **[!UICONTROL Métricas]** no painel esquerdo.
1. Nomeie a métrica &quot;Taxa de conversão&quot; e defina-a como &quot;([!UICONTROL Visitantes únicos] com valor de métrica positivo)&quot; dividido por &quot;Visitantes únicos&quot;, como mostrado abaixo.

   Adicione o segmento recém-criado (etapas definidas acima) de &quot;Visitantes com valor de métrica positivo&quot;, o operador de divisão, a métrica &quot;Visitantes únicos&quot; no numerador e &quot;Visitantes únicos&quot; como denominador.

   ![Taxa de conversão no painel A4T.](/help/integrations/assets/conversion-rate.png)

1. Clique em **[!UICONTROL Salvar]**.

1. Arraste e solte a métrica &quot;Taxa de conversão&quot; recém-criada no painel existente.
1. Clique no ícone de engrenagem e desmarque a **[!UICONTROL Percentual]** , pois esse valor pode causar confusão.

A configuração correta do relatório deve produzir um resultado que se assemelha à seguinte ilustração:

![Índice de conversão de visita exclusiva no relatório de painel do A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]taxa de conversão definida pelo

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

| Alterações necessárias | Relatório acionado pelo Target | Relatório do painel A4T |
| --- | --- | --- |
| [!DNL Analytics] relatórios com [!DNL Target] métrica de conversão | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>[!UICONTROL Aumento (Baixo)] e [!UICONTROL Lift (alto)] deve ser removido.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> | <ul><li>[!UICONTROL Confiança] métricas devem ser removidas.</li><li>[!UICONTROL Aumento (Baixo)] e [!UICONTROL Lift (alto)] deve ser removido.</li><li>Desmarque a apresentação de porcentagem do [!UICONTROL Índice de conversão] para evitar confusão. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê na variável [!DNL Target] relatório. Para obter mais informações, consulte [Orientação geral](#guidance) acima.</li></ul> |

A configuração correta do relatório deve produzir um resultado que se assemelha à seguinte ilustração:

![Conversões de atividade](/help/integrations/assets/optimized-table.png)









