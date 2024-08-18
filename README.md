# Entendimento do Negócio

## Abordagem CRISP-DM

Este projeto seguirá a metodologia CRISP-DM (Cross-Industry Standard Process for Data Mining) para otimização do planejamento de manutenção de uma empresa de transporte terceirizada. A empresa mantém uma frota de caminhões para entregas em todo o país, e apesar de um tamanho de frota constante, houve um aumento significativo nos custos de manutenção relacionados aos sistemas de ar desses veículos nos últimos 3 anos.

### Objetivo

O objetivo é desenvolver estratégias orientadas por dados para reduzir os custos de manutenção especificamente associados aos sistemas de ar nos caminhões. Isso inclui analisar dados históricos de manutenção, identificar padrões ou preditores de falhas nos sistemas de ar, e propor agendas otimizadas de manutenção ou intervenções para mitigar custos.

---
## Valores de Manutenção

- Se um caminhão é enviado para manutenção e não são encontrados defeitos no sistema de ar, uma taxa de $10 é cobrada pelo tempo de inspeção pela equipe especializada.
- Se um caminhão é enviado para manutenção e defeitos são identificados no sistema de ar, é realizado um serviço de reparo preventivo custando $25.
- Se um caminhão com defeitos no sistema de ar não é enviado imediatamente para manutenção, os custos de manutenção corretiva para a empresa são de $500. Isso inclui mão de obra, substituição de peças e outros inconvenientes associados (como quebras durante o trânsito).

## Tendências de Custos de Manutenção

![Tendências de Custos de Manutenção](Imagens/Custo%20por%20ano.jpg)

Legenda: Gráfico mostrando os custos de manutenção relacionados aos sistemas de ar ao longo dos últimos anos.

---

As próximas seções detalharão cada fase do processo CRISP-DM conforme aplicado a este projeto.

# Entendimento dos Dados

## Fonte e Preparação dos Dados

Durante a reunião de alinhamento com os stakeholders do projeto e a equipe de TI da empresa, foram fornecidas as seguintes informações:

- A equipe técnica informou que todos os dados relacionados ao sistema de ar dos caminhões serão fornecidos, mas devido a razões contratuais, todas as colunas tiveram que ser codificadas.
- Além disso, devido aos esforços recentes de digitalização, pode haver informações ausentes no banco de dados fornecido.
- A fonte dos dados é o setor de manutenção da empresa, que inclui uma coluna denominada "class": caminhões com defeitos no sistema de ar são rotulados como "pos", enquanto caminhões com defeitos em outros sistemas são rotulados como "neg".

Esses detalhes estabelecem a base para entender o conjunto de dados, incluindo suas origens, limitações potenciais e o esquema de codificação usado para colunas sensíveis.

---

# Preparação dos Dados

## Limpeza e Imputação de Dados

A preparação inicial dos dados envolveu várias etapas para garantir a qualidade e a completude do conjunto de dados:

- Valores ausentes (NA) foram identificados e substituídos por valores nulos (`NaN`).
- Colunas com alto percentual de valores ausentes foram cortadas do conjunto de dados.
- Valores nulos foram imputados usando a média das variáveis respectivas.

## Seleção de Variáveis

A seleção de variáveis foi realizada usando um modelo de Random Forest:

- As variáveis foram classificadas com base em suas pontuações de importância derivadas de um classificador Random Forest.
- Apenas as variáveis mais relevantes foram selecionadas para análise adicional, focando naquelas que contribuem mais significativamente para prever os custos de manutenção relacionados aos sistemas de ar dos caminhões.

---

## Tratamento de Dados Desbalanceados

O conjunto de dados apresenta um problema de desbalanceamento de classe, onde o evento de interesse (defeitos no sistema de ar) é raro:

- Em cerca de 60.000 registros, apenas 1.000 instâncias representam ocorrências de defeitos no sistema de ar.
- Esse desbalanceamento pode representar desafios durante o desenvolvimento e a avaliação do modelo.

## Desafios na Exploração de Dados

A exploração dos dados foi dificultada pelos seguintes motivos:

- Codificação de colunas: Muitas colunas foram codificadas, limitando a interpretação direta das variáveis.
- Informações ausentes: Grandes quantidades de dados estavam ausentes, impactando a completude e a abrangência do conjunto de dados.

---

# Modelagem

## Modelos Baseline

Inicialmente, foram criados modelos baseline sem nenhum tratamento especial no conjunto de dados:

- Os resultados desses modelos não foram satisfatórios, como documentado no notebook [baseline](Códigos/1_BIX_Technical_Challenge_Modelo_Baseline.ipynb) anexado ao projeto.

## Modelo Desafiante

Após a avaliação dos modelos baseline, procedemos ao desenvolvimento de um modelo mais robusto com o conjunto de dados tratado:

- Este modelo desafiante incorpora técnicas avançadas de pré-processamento e abordagens de modelagem para melhorar as previsões de defeitos nos sistemas de ar dos caminhões.
- Detalhes sobre o desenvolvimento e a avaliação deste modelo serão fornecidos no notebook [desafiante](Códigos/3_BIX_Technical_Challenge_Modelo_Desafiante.ipynb).

# Resultado do Modelo

Com nosso modelo inicial desenvolvido, teríamos economizado cerca de 33,72% no ano atual.

| Cenário    | Gasto Projetado    	| Redução (%) 	|
|------------|---------------------	|-------------	|
| Atual      | R$ 343.750,00      	| 0%          	|
| Modelo     | R$ 227.675,00      	| 33,85%      	|

Podemos conferir mais detalhadamente na imagem a seguir:

![Resultado - Modelo](Imagens/Resultado%20-%20Modelo.jpg)

Legenda: Comparação dos gastos projetados entre o cenário atual e o modelo proposto.


# Próximas Etapas

Após os resultados obtidos, as próximas etapas incluem:

1. **Avaliação pelos Stakeholders**: Apresentar os resultados aos stakeholders para avaliação e aprovação do modelo proposto. A economia projetada de 33,85% deve ser destacada como um indicador do potencial impacto positivo na operação da empresa.

2. **Preparação para Deploy**: Caso aprovado, será necessário coordenar com o time de TI para planejar e implementar o deploy do modelo em ambiente produtivo. Isso inclui a verificação das necessidades de infraestrutura e integração com os sistemas existentes.

3. **Tunagem do Modelo**: Como etapa contínua, recomenda-se realizar a tunagem do modelo. Isso pode envolver ajustes adicionais nos hiperparâmetros do modelo, inclusão de novas variáveis relevantes identificadas durante o processo, ou aplicação de técnicas avançadas para melhorar ainda mais a precisão e a economia de custos prevista.

Essas etapas garantem que os benefícios identificados sejam maximizados e que o modelo proposto possa ser implementado de forma eficaz e sustentável na operação da empresa.

# Atividades do desafio

- A respostas das atividades propostas podem ser encontradas [aqui](Dados/Challenge%20Activities.docx).

