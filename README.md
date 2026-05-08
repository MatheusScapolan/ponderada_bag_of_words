# Atividade Ponderada — Bag of Words

**Inteli — Instituto de Tecnologia e Liderança**
Curso: Sistemas de Informação
Módulo 6 — Processamento de Linguagem Natural
Disciplina: Computação
Professor: Bryan Kano
Aluno: Matheus Henrique Scapolan Silva

---

## Sobre a Atividade

Esta atividade ponderada integra o Módulo 6 do curso de Sistemas de Informação do Inteli, módulo dedicado ao desenvolvimento de aplicações que processam e analisam textos por meio de inteligência artificial. O parceiro de projeto do módulo é a **Zamp**, empresa que opera marcas de alimentação rápida no Brasil e que demanda soluções de análise de linguagem natural para compreender o comportamento de clientes em canais digitais.

O objetivo central da atividade é consolidar a compreensão do modelo **Bag of Words (BoW)**, que representa a base histórica e conceitual de todo o Processamento de Linguagem Natural moderno. Conforme apresentado por Jurafsky e Martin em *Speech and Language Processing* (Stanford University, 2024), antes de qualquer algoritmo de aprendizado de máquina operar sobre linguagem, o texto precisa ser convertido em uma representação numérica de dimensão fixa. O BoW cumpre exatamente essa função ao mapear documentos para vetores de contagem de palavras, descartando a ordem mas preservando a frequência de ocorrência de cada termo.

A atividade foi desenvolvida a partir da leitura do tutorial *Bag-of-Words Model for Beginners*, de Vipul Gandhi, disponível no Kaggle, e expandida com implementações originais, análises comparativas entre vetorizadores e testes sobre dois corpora distintos — um em inglês e outro em português — totalizando 50 frases ao todo.

---

## Por que o Bag of Words importa no contexto do Módulo 6

O Módulo 6 propõe a construção de sistemas de análise de sentimentos, classificação semântica e extração de conhecimento a partir de dados textuais. Todas essas tarefas dependem de uma etapa anterior fundamental que é a transformação do texto bruto em vetores numéricos que os algoritmos de machine learning possam processar.

O BoW é o ponto de partida dessa cadeia. Sobre ele foram construídas representações mais sofisticadas como TF-IDF, Word2Vec, GloVe, FastText e, mais recentemente, os embeddings contextuais de modelos como BERT e GPT. Compreender o BoW em profundidade, incluindo seus fundamentos matemáticos, suas variantes de implementação e suas limitações, é uma condição necessária para compreender por que métodos mais avançados foram desenvolvidos e quando cada um deles é mais adequado.

No projeto Zamp, avaliações de clientes em aplicativos e redes sociais precisam ser vetorizadas antes de alimentar classificadores de sentimento. O BoW e o TF-IDF são abordagens diretamente aplicáveis a esse problema, especialmente em cenários onde o volume de dados é grande e a interpretabilidade dos resultados é valorizada.

---

## Estrutura do Notebook

O notebook está organizado em 19 seções progressivas, cada uma com sua respectiva célula de texto explicativa e célula de código funcional.

**Seção 1 — Contexto e Motivação**
Apresenta o enquadramento da atividade no Módulo 6 e no projeto Zamp, com embasamento bibliográfico em Jurafsky e Martin (2024) e Manning, Raghavan e Schütze (2008).

**Seção 2 — Instalação e Configuração do Ambiente**
Instala todas as dependências necessárias e configura os recursos linguísticos do NLTK e o modelo neural do spaCy para português.

**Seção 3 — Importações**
Centraliza todos os imports do projeto, organizados por biblioteca e propósito.

**Seção 4 — O que é o Bag of Words e por que ele importa**
Apresenta a formulação matemática formal do modelo, incluindo a definição da Matriz Documento-Termo (MDT) e uma discussão sobre esparsidade com a fórmula de cálculo e exemplo numérico.

**Seção 5 — Corpus de Testes em Inglês**
Define as 25 frases em inglês distribuídas em cinco domínios semânticos distintos, incluindo casos de interesse analítico como negação, vocabulário raro e sobreposição intencional de termos.

**Seção 6 — CountVectorizer**
Aplica o vetorizador de contagem do scikit-learn, constrói o vocabulário, gera a MDT e calcula a esparsidade da matriz resultante. Inclui também um teste com palavras fora do vocabulário (OOV).

**Seção 7 — TfidfVectorizer**
Implementa a vetorização TF-IDF com análise dos valores de IDF por token, ranking das palavras mais e menos discriminativas e análise detalhada dos pesos de uma frase específica.

**Seção 8 — Similaridade por Cosseno**
Calcula a matriz de similaridade completa entre os 25 documentos em inglês, identifica o par mais similar e o par mais dissimilar com suas respectivas frases e pontuações.

**Seção 9 — HashingVectorizer**
Demonstra a vetorização via função hash, discutindo o tradeoff entre escalabilidade e interpretabilidade, e compara a similaridade calculada nesse espaço com a calculada via TF-IDF.

**Seção 10 — Keras Tokenizer e Hashing Trick**
Utiliza a API de pré-processamento do Keras para construir um índice de palavras ordenado por frequência, demonstra os quatro modos de codificação (binary, count, tfidf, freq) e aplica o hashing trick do Keras.

**Seção 11 — N-gramas**
Implementa bigramas combinados com unigramas via CountVectorizer e demonstra o efeito da negação na similaridade entre documentos, comparando o comportamento de unigramas e bigramas em um par de frases semanticamente opostas.

**Seção 12 — Corpus de Testes em Português**
Define as 25 frases em português cobrindo tecnologia, alimentação, cotidiano com negação, ciência e esporte, com escolhas lexicais que exploram desafios específicos do idioma como acentuação, contrações e morfologia verbal complexa.

**Seção 13 — Pré-processamento Textual em Português**
Implementa o pipeline completo de pré-processamento com as etapas de tokenização via NLTK, normalização para minúsculas, remoção de stopwords e aplicação em paralelo de stemming com RSLP e lematização neural com spaCy. Exibe uma comparação qualitativa entre as duas técnicas em três frases representativas.

**Seção 14 — Bag of Words em Português**
Integra o pipeline de pré-processamento baseado em spaCy ao CountVectorizer e ao TfidfVectorizer do scikit-learn por meio de um tokenizador personalizado, gerando a MDT em português com vocabulário lematizado.

**Seção 15 — Similaridade por Cosseno em Português**
Repete a análise de similaridade para o corpus em português, identificando os pares mais similares e mais dissimilares após a lematização.

**Seção 16 — Análise Comparativa de Esparsidade**
Calcula e tabela a esparsidade de todas as matrizes geradas ao longo do notebook (CountVectorizer EN, TfidfVectorizer EN, HashingVectorizer EN, CountVectorizer PT e TfidfVectorizer PT), evidenciando o impacto do pré-processamento na densidade das representações.

**Seção 17 — Análise de Frequência e Lei de Zipf**
Calcula a frequência total de cada token nos dois corpora e apresenta os 20 tokens mais frequentes em cada idioma, conectando os resultados à Lei de Zipf e discutindo como esse fenômeno justifica o uso de stopwords e TF-IDF.

**Seção 18 — Quadro Comparativo dos Vetorizadores**
Tabela comparativa com todos os vetorizadores utilizados no notebook, organizada pelas dimensões de escala, tipo de vocabulário, interpretabilidade e casos de uso recomendados.

**Seção 19 — Conclusão e Referências Bibliográficas**
Síntese dos aprendizados consolidados em cada seção, conexão com o projeto Zamp e lista completa de referências bibliográficas.

---

## Tecnologias Utilizadas

**scikit-learn**
Biblioteca principal para vetorização de texto em inglês. São utilizados o `CountVectorizer` para contagem bruta de tokens, o `TfidfVectorizer` para ponderação por frequência inversa de documentos e o `HashingVectorizer` para mapeamento de tokens via função hash sem vocabulário explícito. A função `cosine_similarity` do módulo `sklearn.metrics.pairwise` é utilizada para calcular matrizes de similaridade.

**TensorFlow e Keras**
A API `keras.preprocessing.text` fornece o `Tokenizer`, que constrói um índice de palavras ordenado por frequência e codifica documentos em quatro modos distintos (binary, count, tfidf, freq). Também são utilizados `text_to_word_sequence` e `hashing_trick` para demonstrar a codificação baseada em hash no estilo Keras.

**NLTK (Natural Language Toolkit)**
Utilizado exclusivamente para o pré-processamento em português. Os recursos empregados são a lista de stopwords em português (`nltk.corpus.stopwords`), o tokenizador baseado no algoritmo Punkt (`nltk.tokenize.word_tokenize`) e o stemmer RSLP (`nltk.stem.RSLPStemmer`), desenvolvido especificamente para o português brasileiro.

**spaCy com modelo pt_core_news_sm**
Responsável pela lematização neural contextualizada em português. O modelo `pt_core_news_sm` realiza POS tagging (identificação de classe gramatical) e lematização baseada em modelo morfológico treinado, produzindo formas canônicas válidas no léxico e com maior precisão do que o stemming por regras heurísticas.

**NumPy e Pandas**
Utilizados para manipulação e exibição de matrizes e séries de dados ao longo das análises exploratórias, incluindo o cálculo de esparsidade e o ranqueamento de tokens por frequência e por IDF.

---

## Corpora de Teste

### 25 frases em inglês

As frases em inglês foram organizadas em cinco grupos temáticos.

O primeiro grupo cobre tecnologia e inteligência artificial, com frases sobre redes neurais, transformers, gradiente descendente, overfitting e transfer learning.

O segundo grupo abrange gastronomia, com frases sobre culinária lenta, pão de fermentação natural, o sabor umami, cold brew e temperagem de chocolate.

O terceiro grupo contempla esporte e movimento, com frases sobre maratona, futebol, escalada, natação e atletismo.

O quarto grupo trata de ciência e natureza, com frases sobre fotossíntese, buracos negros, microbioma humano, tectônica de placas e emaranhamento quântico.

O quinto grupo é composto por frases do cotidiano com variações linguísticas relevantes, incluindo negações, opiniões, rotinas e decisões administrativas, projetadas para evidenciar o comportamento do BoW diante de construções gramaticalmente complexas.

### 25 frases em português

As frases em português foram organizadas com atenção aos desafios específicos do idioma e à aderência temática ao projeto Zamp.

O primeiro grupo trata de tecnologia e dados, com frases sobre redes neurais, gradiente descendente, modelos de linguagem de grande escala, análise de sentimentos e embeddings.

O segundo grupo cobre alimentação e consumo, com frases que simulam avaliações de clientes sobre hambúrguer, entrega, cardápio digital, programa de fidelidade e sobremesa, domínio diretamente relevante para o projeto Zamp.

O terceiro grupo contém frases do cotidiano com negação, incluindo falhas em pagamento por aproximação, horários incorretos em sites, qualidade de atendimento e comunicação de promoções.

O quarto grupo aborda ciência e natureza, com frases sobre fotossíntese, buracos negros, microbioma intestinal, placas tectônicas e emaranhamento quântico.

O quinto grupo contempla esporte e saúde, com frases sobre maratona, natação, monitoramento cardíaco, yoga e análise de desempenho por GPS.

---

## Como Executar

O notebook foi desenvolvido para execução no **Google Colab**, plataforma que não requer nenhuma configuração local prévia. Os passos abaixo descrevem o processo completo de execução.

**Passo 1 — Abrir o notebook no Google Colab**
Acesse o endereço colab.research.google.com, selecione a opção de abrir notebook a partir de arquivo local e carregue o arquivo `ponderada_bag_of_words.ipynb`.

**Passo 2 — Executar a Seção 2 (Instalação)**
A primeira célula de código instala todas as dependências necessárias (`scikit-learn`, `tensorflow`, `nltk`, `spacy`) e faz o download dos recursos linguísticos do NLTK e do modelo `pt_core_news_sm` do spaCy. Aguarde a conclusão antes de prosseguir.

**Passo 3 — Executar as células em ordem**
Após a instalação, execute as células sequencialmente. Cada seção constrói sobre os objetos criados nas seções anteriores, portanto a ordem de execução deve ser respeitada.

**Passo 4 — Utilizar a opção "Run All"**
Após a execução bem-sucedida da Seção 2, é possível utilizar o atalho `Runtime > Run all` para executar todas as células restantes de uma vez. O tempo total estimado de execução é de aproximadamente 3 a 5 minutos.

**Requisitos mínimos**
O Google Colab gratuito é suficiente para executar todo o notebook. Nenhuma GPU é necessária. O ambiente de execução deve ser Python 3.8 ou superior.

---

## Resultados Obtidos

**Corpus em inglês**

O vocabulário construído pelo `CountVectorizer` sobre as 25 frases em inglês contém 239 tokens únicos, com esparsidade de 95,16 por cento na Matriz Documento-Termo. O par de frases mais similar identificado pelo `TfidfVectorizer` com similaridade por cosseno foi o formado pelas frases sobre redes neurais e overfitting, ambas pertencentes ao domínio de tecnologia e compartilhando os tokens `data` e `training`. O `HashingVectorizer` com espaço de 1024 posições produziu uma representação funcional sem vocabulário explícito, evidenciando o tradeoff entre escalabilidade e interpretabilidade. A análise de n-gramas demonstrou que bigramas capturam a negação de forma mais precisa que unigramas ao comparar frases semanticamente opostas que compartilham o mesmo vocabulário de base.

**Corpus em português**

O vocabulário lematizado pelo spaCy e vetorizado pelo `CountVectorizer` em português produziu uma matriz com menor esparsidade do que a versão sem lematização, confirmando que o pré-processamento adequado reduz redundâncias morfológicas. A comparação qualitativa entre stemming com RSLP e lematização com spaCy demonstrou que o stemmer produz radicais como `pesquis` e `corr`, que não são palavras válidas no léxico, enquanto o lematizador neural produz formas canônicas como `pesquisador` e `correr`. O par mais similar no corpus em português foi identificado entre duas frases do domínio de tecnologia que compartilhavam os tokens `modelo` e `gradiente` após lematização.

**Análise comparativa de esparsidade**

A tabela gerada na Seção 16 evidenciou que o `HashingVectorizer` produz a matriz mais densa pelo fato de o espaço de hash ser fixo e independente do vocabulário real. O `TfidfVectorizer` em inglês apresentou esparsidade idêntica ao `CountVectorizer` em termos de posições não-zero, já que a transformação TF-IDF apenas repondera os valores sem alterar o suporte. O pré-processamento com lematização em português resultou em um vocabulário menor e, consequentemente, em matrizes com menor número total de dimensões.

---

## Limitações Conhecidas do Modelo Bag of Words

A atividade aborda explicitamente as quatro principais limitações do BoW, discutidas na Seção 4 e retomadas na Seção 19.

A primeira limitação é a **perda de ordem**. O BoW descarta completamente a sequência das palavras, tornando frases como "o médico não recomenda o produto" e "o médico recomenda o produto não" matematicamente idênticas. N-gramas mitigam parcialmente esse problema, mas RNNs, LSTMs e Transformers são as arquiteturas que resolvem essa limitação de forma abrangente.

A segunda limitação é a **ausência de semântica**. No espaço BoW, palavras como "carro" e "automóvel" são ortogonais, ou seja, têm similaridade zero apesar de serem sinônimas. Embeddings densos como Word2Vec e GloVe resolvem esse problema ao posicionar palavras semanticamente próximas em regiões vizinhas do espaço vetorial.

A terceira limitação é a **alta dimensionalidade**. Vocabulários reais facilmente ultrapassam dezenas de milhares de tokens, produzindo vetores de altíssima dimensão com enorme esparsidade. Técnicas como SVD/PCA (utilizadas em Latent Semantic Analysis) e o HashingVectorizer são estratégias para contornar esse problema.

A quarta limitação é a **polissemia**. Uma palavra com múltiplos significados, como "banco" (assento ou instituição financeira), recebe um único vetor no BoW independentemente do contexto em que aparece. Modelos contextuais como BERT e GPT resolvem esse problema ao produzir representações dinâmicas que variam conforme o contexto local.

---

## Referências Bibliográficas

Bird, S., Klein, E. e Loper, E. (2009). *Natural Language Processing with Python*. O'Reilly Media. Disponível em nltk.org/book/

Gandhi, V. (2020). Bag-of-Words Model for Beginners. *Kaggle*. Disponível em kaggle.com/code/vipulgandhi/bag-of-words-model-for-beginners

Jurafsky, D. e Martin, J. H. (2024). *Speech and Language Processing*, 3ª edição. Stanford University. Disponível em web.stanford.edu/~jurafsky/slp3/

Manning, C., Raghavan, P. e Schütze, H. (2008). *Introduction to Information Retrieval*. Cambridge University Press.

spaCy. (2024). Documentação Oficial. Disponível em spacy.io/usage