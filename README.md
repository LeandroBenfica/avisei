Dataset IRS – Infraestrutura Tor e Incidentes CERT.br
Este repositório disponibiliza o dataset consolidado utilizado no artigo submetido ao Simpósio Brasileiro de Cibersegurança (SBSeg), no qual é proposto o Índice de Risco Espectral (IRS) para análise de risco cibernético com base na infraestrutura da rede Tor e em estatísticas oficiais de incidentes do CERT.br.

O objetivo deste README é documentar de forma transparente a origem dos dados, o processo de consolidação e a estrutura do dataset, facilitando a reprodução dos resultados e a eventual extensão do estudo por outros pesquisadores.

1. Visão geral
Nome do arquivo principal: dataset_irs_tor_cert.csv

Período coberto: 2011–2026

Frequência temporal: mensal

Número de observações: 176 linhas

Número de variáveis: 12 colunas

Unidade de análise: cada linha representa um mês, consolidando métricas da rede Tor e categorias de incidentes do CERT.br.

O dataset foi construído especificamente para o estudo do IRS e não é uma cópia bruta de nenhuma fonte; trata-se de um dataset derivado, obtido a partir da integração de fontes públicas descritas a seguir.

2. Fontes de dados
2.1. Tor Metrics
Métricas da infraestrutura da rede Tor foram obtidas a partir do portal oficial Tor Metrics, incluindo:

Número de bridges (pontes de acesso ofuscado).

Número de relays (nós de retransmissão).

Estimativa de usuários brasileiros de relays (relay_users_br).

Estimativa de usuários brasileiros de bridges (bridge_users_br).

As séries foram extraídas em resolução mensal e harmonizadas para o mesmo período de observação utilizado nas estatísticas do CERT.br.

2.2. CERT.br
Os dados de incidentes foram obtidos a partir das estatísticas públicas disponibilizadas pelo CERT.br, agregadas em sete categorias principais:

Total: notificações agregadas mensais.

DOS: ataques de negação de serviço.

Invasao: comprometimento de sistemas.

WEB: exploração de aplicações web.

Scan: varreduras de vulnerabilidades.

Fraude: incidentes fraudulentos.

Outros: demais categorias reportadas.

3. Estrutura do dataset
O arquivo consolidado possui 176 linhas × 12 colunas, com o seguinte esquema lógico:

3.1. Colunas
data: mês de referência (formato YYYY-MM, por exemplo 2018-07).

Métricas da infraestrutura Tor

bridges: número de bridges ativos (global).

relays: número de relays ativos (global).

relay_users_br: estimativa de usuários brasileiros de relays.

bridge_users_br: estimativa de usuários brasileiros de bridges.

Incidentes CERT.br

total_incidentes: total de notificações mensais.

dos: incidentes da categoria DOS.

invasao: incidentes da categoria Invasão.

web: incidentes da categoria WEB.

scan: incidentes da categoria Scan.

fraude: incidentes da categoria Fraude.

outros: demais incidentes agregados.

Esse conjunto atende diretamente às análises descritas no artigo: construção do IRS via PCA, testes de causalidade de Granger e modelagem por Random Forest.

4. Pré-processamento e consolidação
O pipeline de preparação dos dados seguiu as etapas abaixo:

Download das séries brutas

Extração de métricas Tor Metrics e estatísticas mensais do CERT.br em arquivos separados.

Harmonização temporal

Alinhamento das séries em escala mensal, preservando apenas os meses em que havia dados concomitantes de Tor e CERT.br.

Auditoria de consistência

Verificação de valores ausentes pontuais e inconsistências evidentes.

Não houve exclusão sistemática de registros; o horizonte temporal (176 meses) foi preservado integralmente.

Integração em um único dataset

Junção por chave temporal (data), resultando em uma matriz onde cada linha corresponde a um mês e cada coluna a uma métrica específica.

Transformações adicionais (para análise, não para o arquivo bruto)

Para a construção do IRS e para a modelagem, as variáveis contínuas foram reescalonadas (por exemplo, Min-Max Scaling) e centralizadas, conforme detalhado na seção de Metodologia do artigo.

Essas transformações são aplicadas nos notebooks e não alteram o arquivo original dataset_irs_tor_cert.csv, que permanece em escala de origem.

Os notebooks utilizados nesse pipeline (pré-processamento, PCA/IRS, Granger e Random Forest) também estão disponíveis neste repositório, com o objetivo de permitir reprodução e auditoria das etapas.

5. Uso esperado do dataset
O dataset foi desenhado para suportar, principalmente:

Estudos de correlação entre infraestrutura Tor e incidentes oficiais.

Análises de precedência temporal e causalidade de Granger entre séries.

Construção e avaliação de índices sintéticos de risco baseados em PCA ou técnicas afins.

Modelagem de aprendizado de máquina para previsão de tendências (direção de risco) em incidentes.

Pesquisadores podem adaptar o dataset para outros problemas, como:

Estudos comparativos entre países (caso se agreguem estatísticas de outros CERTs).

Avaliação de outras técnicas de redução de dimensionalidade (ICA, autoencoders).

Integração com indicadores de vulnerabilidade, campanhas de phishing, etc.

6. Como citar
Caso utilize este dataset ou os notebooks associados em trabalhos científicos, sugere-se citar o artigo do IRS submetido ao SBSeg (quando disponível) e o próprio repositório GitHub. Um formato genérico de citação é:

L. Benfica, et al. “Spectral Risk Index based on Tor Infrastructure and CERT.br Incidents” (submetido ao SBSeg, 2026). Dataset e código disponíveis em: <link do repositório>.

7. Considerações éticas e de uso
Todos os dados utilizados são públicos e obtidos de fontes oficiais (Tor Metrics e CERT.br); não há informações de identificação individual.

Ainda assim, recomenda-se que análises derivadas respeitem as políticas de uso de dados das fontes originais e evitem inferências indevidas sobre indivíduos ou organizações específicas.


