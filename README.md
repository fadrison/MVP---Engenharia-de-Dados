# MVP-Engenharia-de-Dados
Aluno: Fadrison Andre Cavalcante Barros
Contato: fadrisonacb@gmail.com
## Dados de viagens do Portal da Tranparência 2025
## Contextualização e objetivos gerais

Os registros de deslocamentos de agentes públicos representam uma das áreas de maior utilidade para auditoria contínua das finanças publicas o
controle do Uso do Dinheiro Público, detecção de Anomalias e Sobreposições possibilitam a observação de como se dá o caminho do dinheiro publico dessas atividades que necessitam de investimento em viagens.</br>
Sendo assim esse trabalho veio com o objetivo de:
 * Preparar as bases de dados conforme o nível de tratamento;
 * Mesclar (join) as bases para obter uma base composta por todos os campos financeiros do conjunto de base;
 * Identificar os estados com maior investimento em viagens;
 * Identificar os órgãos com maior investimento em viagens;

## Detalhamento o projeto
### 📋 Descrição das Tabelas

1. **`Viagens` (Tabela Principal / Cabeçalho):**
   - **Função:** Armazena os dados consolidados do processo de viagem, identificação do servidor, órgão solicitante, período total e motivo do deslocamento.
   - **Campos-chave:** `ID_VIAGEM`, `CPF_SERVIDOR`, `NOME_SERVIDOR`, `ORGAO_SOLICITANTE`, `PERIODO_INICIO`, `PERIODO_FIM`, `MOTIVO_VIAGEM`, `VALOR_TOTAL`.

2. **`Trechos` (Logística Geográfica):**
   - **Função:** Detalha cada etapa/percurso realizado dentro de uma mesma viagem.
   - **Campos-chave:** `ID_TRECHO`, `ID_VIAGEM`, `CIDADE_ORIGEM`, `CIDADE_DESTINO`, `DATA_SAIDA`, `MEIO_TRANSPORTE`.

3. **`Passagens` (Aquisição de Bilhetes):**
   - **Função:** Registra os bilhetes aéreos, terrestres ou fluviais emitidos por companhias e agências contratadas.
   - **Campos-chave:** `ID_PASSAGEM`, `ID_VIAGEM`, `COMPANHIA_AEREA`, `NUMERO_BILHETE`, `VALOR_PASSAGEM`, `TAXA_SERVICO`.

4. **`Pagamentos` (Fluxo Financeiro e Diárias):**
   - **Função:** Detalha as parcelas financeiras pagas ao servidor (diárias de hospedagem/alimentação, adicionais) ou devoluções/restituições ao erário via GRU.
   - **Campos-chave:** `ID_PAGAMENTO`, `ID_VIAGEM`, `TIPO_PAGAMENTO`, `QUANTIDADE_DIARIAS`, `VALOR_PAGO`, `DATA_PAGAMENTO`.

---

## Preparação das bases
No primeiro momento obtivemos a base em .csv, ela foi salva na camada **Bronze**.</br>
Logo em seguida, lemos a tabela csv em Pyspark, foram identificadas alguns pontos de melhoria, como retirar os espaços dos nomes das variáveis, os valores monetários e as datas estavam em formato de string, então foram ajustas para o formato double e date. Verificamos também se havia valores inconsistentes com data de ida maior que data de volta, valores duplicados e salvamos na camada **Silver**.</br>
Para a camada **Gold**, optou-se criar uma tabela composta de todos os valores financeiros das 4 tabelas existentes - custos_viagens, como podemos ver na imagem abaixo: </br>



<img width="303" height="396" alt="image" src="https://github.com/user-attachments/assets/cdf6f560-1195-4fdd-84ef-d7631dbb4e32" /></br>

## Análise de dados
Entres os pontos de avaliação de dados buscou-se o números de orgãos distintos na base de viagens, onde tivemos 35 órgãos públicos compondo a base de dados:</br>
<img width="682" height="263" alt="image" src="https://github.com/user-attachments/assets/1d44ef04-89e5-40da-a7cf-a02879caec63" /></br>
Dentre os 35 órgãos, os 10 que mais apresentam registros na base são:</br>
<img width="528" height="493" alt="image" src="https://github.com/user-attachments/assets/7ea7a0ea-a236-4256-a176-8c6dc652f623" /></br>
Sendo os estados (UF) com maiores destinos:</br>
<img width="482" height="449" alt="image" src="https://github.com/user-attachments/assets/741b2301-4f85-4264-83cd-402dfcc0d344" /></br>

E os orgãos que mais investem:</br>
<img width="514" height="441" alt="image" src="https://github.com/user-attachments/assets/f7de0704-966c-43bd-8eb8-6251742ce987" /></br>

## Considerações finais
A relevância da rastreabilidade do dinheiro público é muito importante para a auditoria e também para o conhecimento da população em geral, organiza as  bases em camadas de manuzeios temos a possibilidade de identificar e ajustar possíveis erros ao logo do processo, ferramentas como o Databicks ,entre outras, nos dão a autonomia de trabalhar e tratar esses dados de forma que possamos ter resultados de armazenamento e processamento com robustez.  
## Autoavaliação
De modo geral o trabalho entregou as camadas de acordo com os manuseios necessários e as análises em pyspark e sql, entretanto houve muita dificuldade em puxar as bases com a url e salvar as bases em parquet, no google colab onde dei inicio ao trabalho conseguimos puxar a base com a url e salvar em parquet sem nenhum problema. Sendo assim, foi necessário fazer upload das bases direto da máquina e também salvar em formato csv. No mas, tudo foi de acordo com o solicitado.



