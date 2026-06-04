---
title: Como configurar relatórios do A4T no [!DNL Analysis Workspace] para atividades de [!UICONTROL Alocação automática]
description: Como configurar relatórios do [!UICONTROL Analytics for Target] (A4T) no [!DNL Adobe] [!DNL Analysis Workspace] ao executar atividades de [!UICONTROL Alocação automática].
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
TQID: https://experienceleague.adobe.com/5oQMgqqxw2VN-6cb29j4bwEP6VYmGRLXIp5AMJ3WWM4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1546
ht-degree: 0%

---

# Configurar relatórios do A4T em [!DNL Analysis Workspace] para [!DNL Auto-Allocate] atividades

Uma atividade [[!UICONTROL Alocação automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} em [!DNL Adobe Target] identifica um vencedor entre duas ou mais experiências e realoca automaticamente o tráfego de visitantes para o vencedor enquanto o teste continua a ser executado e aprendido. A integração do [!UICONTROL Analytics for Target] (A4T) para [!UICONTROL Alocação automática] permite exibir os dados de relatórios no [!DNL Adobe Analytics] e otimizar para eventos ou métricas personalizadas definidas no [!DNL Analytics].

Embora os recursos de análise avançada estejam disponíveis no [!DNL Adobe Analytics] [!DNL Analysis Workspace], algumas modificações no painel [!UICONTROL Analytics for Target] padrão podem ser necessárias para interpretar corretamente as atividades de [!UICONTROL Alocação automática]. Estas modificações são necessárias devido às nuances nos [critérios de métrica de otimização](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Cada tipo de métrica de otimização requer uma configuração de relatório diferente no A4T, da seguinte maneira:

* Usando uma métrica [!DNL Analytics]

   * [!UICONTROL Maximizar valor de métrica por visitante]
   * [!UICONTROL Maximizar a taxa de conversão de visitantes únicos]

* Usando uma métrica de conversão definida por [!DNL Target]

Este tutorial aborda a orientação geral do A4T e as etapas de configuração de relatório específicas dos critérios.

## Métricas do Analytics com os critérios de otimização &quot;[!UICONTROL Maximizar valor de métrica por visitante]&quot;

**Definição**: (Valor de Métrica Geral) / (Número de Visitantes)

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

| Alterações necessárias | Relatório acionado por [!DNL Target] | Relatório do painel A4T |
| --- | --- | --- |
| Maximizar valor de métrica para uma métrica [!DNL Analytics] | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remover [!UICONTROL Aumento (Baixo)] e [!UICONTROL Aumento (Alto)]. Manter [!UICONTROL Lift (Med)].</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li><li>Renomeie a métrica de taxa de [!UICONTROL Conversão] para &quot;Métrica/Visitante&quot;.</li></ul> | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remover [!UICONTROL Aumento (Baixo)] e [!UICONTROL Aumento (Alto)] Manter [!UICONTROL Aumento (Med)].</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li><li>Renomeie a métrica de taxa de [!UICONTROL Conversão] para &quot;Métrica/Visitante&quot;.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê no relatório [!DNL Target]. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li></ul> |

![Maximizar valor de métrica para receita](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] métricas com os critérios de otimização &quot;[!UICONTROL Taxa de conversão de visitante único]&quot;

**Definição**: (# de Visitantes únicos com um valor positivo da métrica) / (Número Total de Visitantes Únicos)

Exemplo: suponha que sua métrica de otimização seja [!UICONTROL Receita]. Há cinco visitantes únicos na atividade e três desses visitantes únicos fazem uma compra. Neste exemplo, este valor = (3 visitantes para os quais [!UICONTROL Receita] é positivo) / (5 visitantes únicos totais) = 0,6 = 60%.

>[!NOTE]
>
>O índice de conversão referenciado aqui pode se referir a ações fora de pedidos, como cliques, impressões e assim por diante. Nesses casos, o critério ainda seria maximizar a contagem de visitantes que clicam ou visualizam a página, respectivamente.

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

| Alterações necessárias | Relatório acionado pelo Target | Relatório do painel A4T |
| --- | --- | --- |
| Maximizar conversões para uma métrica [!DNL Analytics] | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remova todas as três métricas [!UICONTROL Lift].</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li></ul> | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remova todas as três métricas [!UICONTROL Lift].</li><li>Crie um segmento para filtrar visitantes com um valor de métrica positivo que visualizaram a atividade que foi analisada. Consulte [Criar um segmento](#segment) abaixo.</li><li>Substitua a métrica [!UICONTROL Taxa de conversão] preenchida automaticamente para que seja a divisão entre [!UICONTROL Visitantes únicos] com um valor de métrica positivo e visitantes únicos. Consulte [Atualizar a métrica Taxa de conversão](#update-conversion-metric) abaixo.</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê no relatório [!DNL Target]. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li></ul> |

### Relatório do painel A4T padrão - orientação adicional

As seções a seguir contêm mais informações sobre orientações adicionais à medida que você configura o relatório padrão do painel A4T.

#### Criar um segmento {#segment}

1. Clique no sinal &quot;+&quot; **&#x200B;**&#x200B;ao lado de **[!UICONTROL Segmentos]** no painel esquerdo.

   ![Sinal de adição ao lado de segmentos no painel esquerdo.](/help/integrations/assets/plus-sign.png)

1. Atribua um título ao segmento &quot;Visitantes com valor de métrica positivo&quot;.
1. Em **[!UICONTROL Definição]**, ao lado de **[!UICONTROL Incluir]**, selecione **[!UICONTROL Visitante]**.
1. Em **[!UICONTROL Definição]**, selecione a métrica de otimização na atividade.

   Neste exemplo, considere [!UICONTROL Receita] como a métrica de otimização.

1. Selecione o operador &quot;[!UICONTROL é maior que]&quot; e especifique &quot;0&quot;.

   Essas configurações filtram para todos os visitantes com um valor de métrica positivo.

1. Clique em **[!UICONTROL Salvar]**.

   ![Valor de métrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Adicione o segmento recém-criado chamado &quot;Visitantes com valor de métrica positivo&quot; ao painel A4T.
1. Arraste e solte a métrica [!UICONTROL Visitantes únicos] na mesma coluna que o &quot;Visitantes com valor de métrica positivo&quot;.

   Essa configuração cria um segmento de todos os visitantes únicos para os quais o valor da métrica é positivo. Neste exemplo, todos os visitantes únicos cuja receita foi maior que zero.

#### Atualizar a métrica [!UICONTROL Taxa de conversão] {#update-conversion-metric}

1. Se ainda não tiver feito isso, remova a coluna [!UICONTROL Taxa de conversão] existente do painel, conforme explicado abaixo.
1. Adicione uma métrica clicando no sinal &quot;+&quot; ao lado da seção **[!UICONTROL Métricas]** no painel esquerdo.
1. Nomeie a métrica &quot;Taxa de conversão&quot; e defina-a como &quot;([!UICONTROL Visitantes únicos] com valor de métrica positivo)&quot; dividido por &quot;Visitantes únicos&quot;, como mostrado abaixo.

   Adicione o segmento recém-criado (etapas definidas abaixo) de &quot;Visitantes com valor de métrica positivo&quot;, o operador de divisão, a métrica &quot;Visitantes únicos&quot; no numerador e &quot;Visitantes únicos&quot; como denominador.

   ![Taxa de conversão no painel A4T.](/help/integrations/assets/conversion-rate.png)

1. Clique em **[!UICONTROL Salvar]**.

1. Arraste e solte a métrica &quot;Taxa de conversão&quot; recém-criada no painel existente.
1. Clique no ícone de engrenagem e desmarque a caixa de seleção **[!UICONTROL Percentual]**, pois esse valor pode causar confusão.

   A configuração correta do relatório deve produzir um resultado que se assemelha à seguinte ilustração:

   ![Taxa de conversão de visitas exclusivas no relatório do painel A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Taxa de conversão definida por [!DNL Target]

Para configurar o relatório, faça as seguintes alterações no relatório do A4T:

| Alterações necessárias | Relatório acionado pelo Target | Relatório do painel A4T |
| --- | --- | --- |
| [!DNL Analytics] relatórios com [!DNL Target] métrica de conversão | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remover [!UICONTROL Aumento (Baixo)] e [!UICONTROL Aumento (Alto)]. Manter Elevação (Med).</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li></ul> | <ul><li>Remover métricas de [!UICONTROL Confiança].</li><li>Remover [!UICONTROL Aumento (Baixo)] e [!UICONTROL Aumento (Alto)]. Manter [!UICONTROL Lift (Med)].</li><li>Desmarque a apresentação de porcentagem da coluna [!UICONTROL Taxa de Conversão] para evitar confusão. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li><li>Verifique se os intervalos de data e hora estão alinhados com os valores que você vê no relatório [!DNL Target]. Consulte [Orientação geral para o A4T](#guidance) abaixo.</li></ul> |

A configuração correta do relatório deve produzir um resultado que se assemelha à seguinte ilustração:

![Conversões de atividade](/help/integrations/assets/optimized-table.png)

## Orientações gerais para o A4T {#guidance}

Você pode navegar até um painel do [!UICONTROL Analytics for Target] pré-criado clicando no link da tela de relatório no [!UICONTROL Target] (isso é mencionado posteriormente neste guia como o &quot;relatório acionado pelo [!DNL Target]&quot;). Como alternativa, você pode criar o painel do A4T em [!DNL Analytics] (detalhes mais adiante nesta seção).

As seções a seguir especificam quais configurações são necessárias, dependendo de quais desses métodos você escolher. No entanto, as seguintes etapas servem como orientação geral para o A4T:

* Remova as métricas de confiança do painel A4T, independentemente do método de criação do painel (ambos são detalhados abaixo). Em vez disso, faça referência a esses valores nos relatórios de [!DNL Target]. Além disso, os vencedores da atividade podem ser identificados nos relatórios [!DNL Target]. Detalhes sobre a identificação do vencedor da atividade podem ser encontrados na seção [Identificar o vencedor da atividade](#winner) abaixo.
&#x200B;>>
* Para evitar confusão, desmarque a apresentação &quot;[!UICONTROL Percent]&quot; da métrica [!UICONTROL Taxa de Conversão]. Consulte [Ocultar a porcentagem da [!UICONTROL Taxa de Conversão] coluna](#hide-percentage) abaixo.
&#x200B;>>
* Se você estiver criando um painel A4T, verifique se os intervalos de data e hora correspondem aos do relatório [!DNL Target]. Consulte [Alinhar a data e a hora no painel A4T](#aligning-date-and-time) abaixo.

### Ocultar a porcentagem da coluna [!UICONTROL Taxa de Conversão] {#hide-percentage}

1. Clique no ícone de **engrenagem** ao lado do título da coluna [!UICONTROL Taxa de Conversão].

   ![Ícone de engrenagem na coluna Taxa de Conversão](/help/integrations/assets/coversion-rate-gear-icon.png)

   A caixa de diálogo de configurações da [!UICONTROL Coluna] é exibida:

   ![Caixa de diálogo de configurações de coluna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Desmarque a caixa de seleção **[!UICONTROL Percentual]**.

   Seu painel do A4T agora não inclui porcentagens como a [!UICONTROL Taxa de conversão] e corresponde a [!DNL Target], como mostrado abaixo:

   ![A coluna de Taxa de Conversão não mostra porcentagens](/help/integrations/assets/no-percentages.png)

### Alinhar a data e a hora no painel A4T {#aligning-date-and-time}

1. Abaixo de cada painel, verifique o intervalo de datas referenciado pelo painel para garantir que o intervalo de datas corresponda ao do relatório [!DNL Target].

   ![Intervalo de datas no painel A4T](/help/integrations/assets/date-range.png)

1. Em [!DNL Analytics], defina o intervalo de tempo como 12:00am - 11:59pm.

### Identificar o vencedor da atividade {#winner}

Os vencedores da atividade [!DNL Auto-Allocate] são selecionados quando há uma taxa de conversão vencedora com valores de confiança maiores ou iguais a 95%. Esses valores devem ser referenciados nos relatórios [!DNL Target], já que os cálculos de confiança refletem os métodos mais conservadores que [!DNL Target] recomenda para atividades de [!UICONTROL Alocação automática]. Consulte [Garantias estatísticas de Alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} no *[!UICONTROL Guia do profissional de negócios do Adobe Target]*.

>[!NOTE]
>
>Os emblemas &quot;Ainda não há vencedor&quot; e &quot;Vencedor&quot; não estão disponíveis no painel A4T em [!DNL Analysis Workspace]. Além disso, o selo de &quot;estrela&quot; vencedor exibido nos relatórios [!DNL Target] para as atividades [!UICONTROL Alocação automática] deve ser ignorado. Consulte [Alocação automática](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} em *Suporte do A4T para atividades de Alocação automática e Direcionamento automático* no *[!UICONTROL Guia do profissional de negócios do Adobe Target]*.

### Criar o A4T para o painel [!UICONTROL Alocação automática] em [!DNL Analysis Workspace]

1. Para criar um painel do A4T para um relatório de atividades de [!UICONTROL Alocação automática], comece com o painel do [!UICONTROL Analytics for Target] no [!DNL Analysis Workspace], conforme mostrado abaixo.

   ![Analytics for Target - Relatório de Alocação automática](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Faça as seguintes seleções:

   * **[!UICONTROL Experiência de controle]**: escolha qualquer experiência.
   * **[!UICONTROL Métrica de normalização]**: selecione **[!UICONTROL Visitantes]** (incluído no painel A4T por padrão). [!UICONTROL Alocação automática] sempre normaliza as taxas de conversão de visitantes únicos.
   * **Métricas de sucesso**: selecione a mesma métrica (otimização) usada durante a criação da atividade. Se esta foi uma métrica de conversão definida por [!DNL Target], selecione **[!UICONTROL Conversão de atividade]**. Caso contrário, selecione a métrica [!DNL Adobe Analytics] que você usou.









