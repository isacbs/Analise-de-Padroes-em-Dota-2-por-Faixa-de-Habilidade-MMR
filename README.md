# Análise de Padrões de Escolha e Desempenho de Heróis em Dota 2 por Faixa de Habilidade (MMR)

## Objetivo do projeto
 
Projeto de prática da disciplina Inteligência Artificial 7ºJ feito para desenvolver um sistema de análise de dados baseado em aprendizado de máquina para identificar padrões de escolha e desempenho de heróis do Dota 2 nas diferentes faixas de habilidade (MMR) dos jogadores. Os objetivos específicos são:
 
* Coletar os dados de picks, vitórias e taxa de vitória por herói e por faixa de MMR diretamente da OpenDota API;
* Realizar a análise exploratória dos dados coletados;
* Aplicar técnicas de clusterização (K-means e clusterização hierárquica) para identificar arquétipos de heróis;
* Aplicar um modelo supervisionado (Random Forest) para prever o desempenho de um herói a partir de seus atributos e papéis;
* Avaliar os resultados obtidos por meio de métricas de clusterização e de classificação.
 
## Dataset
 
**Fonte:** OpenDota API — Endpoint público `GET /api/heroStats` (https://docs.opendota.com/#tag/hero-stats/paths/~1heroStats/get).

**Descrição:** Conjunto de dados coletado diretamente pelo grupo por meio de uma requisição HTTP ao endpoint, contendo estatísticas agregadas de 92 heróis do jogo Dota 2, o endpoint não retornou os 124 heróis atualmente jogáveis no momento da extração, uma limitação da própria fonte. Para cada herói são informados o nome, o atributo primário (Força, Agilidade, Inteligência ou Universal) e os papéis estratégicos (roles), além do número de picks e de vitórias em cada uma das oito faixas de MMR (Herald, Guardian, Crusader, Archon, Legend, Ancient, Divine e Immortal), a partir dos quais a taxa de vitória de cada faixa foi calculada pelo grupo, totalizando 28 colunas. A faixa Immortal foi retornada com 0 picks e 0 vitórias para todos os heróis, também uma limitação de disponibilidade de dados da fonte. Não há nenhuma informação pessoal ou individualizada de jogadores, apenas estatísticas agregadas por herói e por faixa de habilidade, o que dispensa qualquer tratamento sob a ótica da LGPD.
 
## Integrantes do grupo
 
* David Haim Raiber — 10395618@mackenzista.com.br
* Isadora Caetano Brandão de Sousa — 10420646@mackenzista.com.br
* Jennifer Aparecida de Sousa Tondade — 10420574@mackenzista.com.br
* Lucas Lacerda Gomes — 10322644@mackenzista.com.br
  
## Arquivos da entrega - N1
 
* `Análise_de_Padrões_de_Escolha_e_Desempenho_de_Heróis_em_Dota_2_por_Faixa_de_Habilidade__MMR__.pdf` — Relatório do Projeto.
* `dota2_herostats_opendota_live.csv` — Dataset original, coletado via requisição HTTP ao endpoint heroStats da OpenDota API.
* `dota2_hero_preference_tratado.csv` — Dataset após tratamento.
* `visualizacao_dos_dados_dota2.ipynb` — Notebook com a análise exploratória.
* `tratamento_dos_dados_dota2.ipynb` — Notebook com o tratamento e preparação dos dados.
