# Análise de Padrões de Escolha e Desempenho de Heróis em Dota 2 por Faixa de Habilidade (MMR)
 
Projeto da disciplina **Inteligência Artificial – 7ºJ SI (Noite)**, Faculdade de Computação e Informática, Universidade Presbiteriana Mackenzie. Professor: Dr. Leandro Zerbinatti.

## Integrantes do grupo
 
* David Haim Raiber — 10395618@mackenzista.com.br
* Isadora Caetano Brandão de Sousa — 10420646@mackenzista.com.br
* Jennifer Aparecida de Sousa Tondade — 10420574@mackenzista.com.br
* Lucas Lacerda Gomes — 10322644@mackenzista.com.br
 
**Vídeo de apresentação (YouTube):** [inserir link do vídeo]
 
## Objetivo do projeto
 
Desenvolver uma análise de dados baseada em aprendizado de máquina para identificar padrões de escolha e desempenho de heróis do Dota 2 nas diferentes faixas de habilidade (MMR) dos jogadores. O projeto adota a **Opção Framework** da disciplina, com a biblioteca scikit-learn.
 
Os objetivos específicos são:
 
* Coletar os dados de picks, vitórias e taxa de vitória por herói e por faixa de MMR diretamente da OpenDota API;
* Realizar a análise exploratória e a preparação dos dados coletados;
* Testar a hipótese (H1) de que o atributo primário e os papéis estratégicos permitem prever a taxa de vitória de um herói, comparando regressão linear, Ridge e Random Forest com um baseline que sempre prevê a média, por meio de validação cruzada 5×10;
* Aplicar técnicas de clusterização (K-means e clusterização hierárquica) para identificar arquétipos de heróis a partir da variação de desempenho entre faixas, da consistência e da popularidade;
* Avaliar os resultados por métricas de regressão (R² e MAE), de clusterização (silhueta, Davies-Bouldin e índice de Rand ajustado) e de classificação (acurácia na previsão do arquétipo), além de testes estatísticos (Kruskal-Wallis, Spearman e qui-quadrado).
### Mudança do objetivo principal
 
O objetivo inicial era supervisionado: prever a taxa de vitória a partir do atributo e dos papéis. Definiu-se antes da análise que um modelo só seria adotado se superasse o baseline em validação cruzada. Nenhum dos 12 modelos testados (3 modelos para cada um dos 4 alvos) o superou, e a H1 foi rejeitada. O resultado negativo é relatado integralmente no relatório, e o objetivo principal foi reformulado para descrever, por meio de arquétipos obtidos por clusterização, como o desempenho dos heróis varia entre as faixas de MMR.
 
## Principais resultados
 
* **H1 rejeitada:** para a taxa de vitória média, o baseline obteve R² médio de −0,085, contra −0,325 (regressão linear), −0,252 (Ridge) e −0,310 (Random Forest).
* **Quatro arquétipos** (K-means, k = 4, silhueta de 0,333 e Davies-Bouldin de 1,005): alto teto de habilidade (21 heróis), fortes em faixas baixas (17), consistentes e populares (20) e consistentes de nicho (34). A estrutura é fraca e pouco estável entre K-means e clusterização hierárquica (Rand ajustado de 0,335), então os arquétipos devem ser lidos como tendências.
* **Taxa de vitória e arquétipos:** a taxa de vitória média difere entre os arquétipos (Kruskal-Wallis, p = 0,010), e o pick rate médio tem correlação de Spearman de 0,40 com ela. As relações são exploratórias e não indicam causalidade.
* **Atributo e papéis não preveem o arquétipo:** acurácia de 0,359 do Random Forest, contra 0,370 do baseline da classe majoritária.
## Dataset
 
**Fonte:** OpenDota API, endpoint público `GET /api/heroStats` (https://docs.opendota.com/#tag/hero-stats/paths/~1heroStats/get).
 
**Descrição:** conjunto de dados coletado diretamente pelo grupo por meio de uma requisição HTTP ao endpoint, contendo estatísticas agregadas de 92 heróis do Dota 2. O endpoint não retornou os 124 heróis atualmente jogáveis no momento da extração, uma limitação da própria fonte. Para cada herói são informados o nome, o atributo primário (Força, Agilidade, Inteligência ou Universal) e os papéis estratégicos (roles), além do número de picks e de vitórias em cada uma das oito faixas de MMR (Herald, Guardian, Crusader, Archon, Legend, Ancient, Divine e Immortal), a partir dos quais a taxa de vitória de cada faixa foi calculada pelo grupo, totalizando 28 colunas. A faixa Immortal foi retornada com 0 picks e 0 vitórias para todos os heróis, também uma limitação de disponibilidade de dados da fonte, e por isso foi excluída dos cálculos de desempenho. Não há nenhuma informação pessoal ou individualizada de jogadores, apenas estatísticas agregadas por herói e por faixa de habilidade, o que dispensa qualquer tratamento sob a ótica da LGPD.
 
**Bases geradas no projeto:**
 
| Arquivo | Linhas × colunas | Conteúdo |
| --- | --- | --- |
| `dota2_herostats_opendota_live.csv` | 92 × 28 | Base original coletada da API |
| `dota2_hero_preference_tratado.csv` | 92 × 14 | Base tratada: papéis em variáveis binárias (multi-hot), `WinRate_Mean`, `WinRate_Std`, `WinRate_Delta` e `PickRate_Mean` |
| `dota2_hero_arquetipos.csv` | 92 × 17 | Base tratada acrescida de `Pick_Slope`, `Cluster` e `Arquétipo` |
 
## Arquivos da entrega
 
### N1
 
* `Análise_de_Padrões_de_Escolha_e_Desempenho_de_Heróis_em_Dota_2_por_Faixa_de_Habilidade__MMR__.pdf` — Relatório do Projeto (versão do primeiro bimestre).
* `dota2_herostats_opendota_live.csv` — Dataset original, coletado via requisição HTTP ao endpoint heroStats da OpenDota API.
* `dota2_hero_preference_tratado.csv` — Dataset após tratamento.
* `visualizacao_dos_dados_dota2.ipynb` — Notebook 1: análise exploratória.
* `tratamento_dos_dados_dota2.ipynb` — Notebook 2: tratamento e preparação dos dados.
### N2
 
* `Análise_de_Padrões_de_Escolha_e_Desempenho_de_Heróis_em_Dota_2_por_Faixa_de_Habilidade__MMR_.docx` — Relatório do Projeto atualizado (versão completa do segundo bimestre).
* `modelagem_dota2.ipynb` — Notebook 3: teste da hipótese supervisionada (baseline, regressão linear, Ridge e Random Forest), clusterização (K-means e hierárquica) e análise dos arquétipos.
* `dota2_hero_arquetipos.csv` — Dataset com os arquétipos atribuídos a cada herói.
* Pasta de figuras — imagens utilizadas no relatório.
## Como reproduzir
 
Os notebooks devem ser executados na ordem abaixo, na mesma pasta dos arquivos CSV. A extração via API está documentada na Seção 1 do Notebook 1, e as sementes aleatórias foram fixadas em 42.
 
1. `visualizacao_dos_dados_dota2.ipynb`
2. `tratamento_dos_dados_dota2.ipynb`
3. `modelagem_dota2.ipynb`
Bibliotecas utilizadas: `requests`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` e `scipy`.
