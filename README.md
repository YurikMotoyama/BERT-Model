# BERT: Bidirectional Encoder Representations from Transformers

O **BERT** é um modelo pré-treinado de processamento de linguagem natural (**NLP**) desenvolvido pela equipe de pesquisa do Google AI. Ele utiliza aprendizado profundo e é baseado na arquitetura Transformer, permitindo compreender o contexto em textos de maneira mais avançada do que modelos anteriores.

---

## O que o BERT faz?

O BERT é projetado para realizar diversas tarefas de NLP, incluindo:

- **Classificação de texto**: Classificação de sentimentos, categorização de tópicos, etc.
- **Reconhecimento de entidades nomeadas**: Identificar nomes, datas, locais, e mais em textos.
- **Resolução de correferência**: Identificar quais palavras ou expressões se referem à mesma entidade.
- **Resposta a perguntas**: Compreender perguntas e localizar respostas em textos.
- **Tradução de linguagem**: Em aplicações específicas de ajuste fino.
- **Previsão de palavras e compreensão de contexto bidirecional**.

---

## Como o BERT funciona?

### Contexto Bidirecional

O BERT processa palavras considerando o contexto de ambas as direções (antes e depois delas), diferentemente de modelos unidirecionais como o GPT-1, que analisam apenas o contexto à esquerda ou à direita.

### Etapas principais:

1. **Pré-treinamento**:
   - **Masked Language Modeling (MLM)**: O modelo é treinado para prever palavras mascaradas com base no contexto.
   - **Next Sentence Prediction (NSP)**: Treina o modelo para entender a relação entre duas frases (se uma segue a outra ou não).

2. **Ajuste fino**:
   - Após o pré-treinamento, o BERT é ajustado para tarefas específicas, como classificação de texto ou resposta a perguntas, usando datasets menores.

3. **Transformers**:
   - O BERT utiliza a arquitetura Transformer, com mecanismos de atenção para capturar relações entre palavras em uma sequência, independentemente da distância entre elas.
  

# Transformers

Transformers são uma arquitetura de rede neural revolucionária introduzida no artigo *"Attention Is All You Need"* (Vaswani et al., 2017). Eles transformaram o campo do Processamento de Linguagem Natural (NLP) e do aprendizado profundo, substituindo estruturas recorrentes (RNNs, LSTMs) por mecanismos de atenção.

## Principais Componentes

- **Mecanismo de Self-Attention**: 
  - Avalia as relações entre palavras em uma sequência, independentemente da distância.
  - Resolve problemas como o desvanecimento de gradiente em sequências longas.

- **Encoder e Decoder**: 
  - **Encoder**: Aprende representações ricas da entrada (usado em modelos como BERT).
  - **Decoder**: Gera saídas baseadas nas representações do encoder (usado em modelos como GPT).

- **Positional Embeddings**: 
  - Adicionam informações de posição para compensar a ausência de recorrência ou convoluções.

- **Multi-Head Attention**: 
  - Captura múltiplos aspectos do contexto ao dividir a atenção em várias "cabeças".

- **Feed-Forward Layers**: 
  - Camadas totalmente conectadas para aprendizado adicional após a atenção.

## Por Que Transformers São Importantes?

1. **Eficiência Paralela**: Processam tokens simultaneamente, aproveitando melhor hardware moderno.
2. **Resultados Superiores**: Dominam benchmarks em tradução, resumo, resposta a perguntas e mais.
3. **Extensibilidade**: Base para modelos como BERT, GPT, T5, entre outros.

Os Transformers continuam sendo uma tecnologia central em NLP e aprendizado profundo, com aplicações em diversas áreas além de texto, como visão computacional.


---

## Para que o BERT é útil?

O BERT é amplamente utilizado em aplicações que envolvem texto, como:

- **Assistentes virtuais**: Interpretar perguntas e fornecer respostas precisas (e.g., Google Assistant).
- **Motores de busca**: Melhorar a compreensão de consultas dos usuários (e.g., Google Search).
- **Análise de sentimentos**: Avaliar sentimentos em análises de produtos ou redes sociais.
- **Suporte ao cliente**: Automatizar respostas em chatbots.
- **Resumo de textos**: Criar resumos de documentos longos.
- **Sistemas de recomendação**: Entender preferências de usuários baseadas em textos.



---

## Impacto

O BERT revolucionou o campo de NLP, definindo novos padrões de desempenho para várias tarefas. Ele permite que máquinas entendam o significado profundo de palavras e frases no contexto completo, algo essencial para lidar com a complexidade da linguagem humana.

# Testando o Modelo BERT com Hugging Face

Este guia ensina como testar o modelo **BERT Base Uncased** da Hugging Face no Google Colab. O modelo é útil para diversas tarefas de NLP, como classificação, extração de informações e análise de similaridade.

---

## Requisitos

1. Conta no [Google Colab](https://colab.research.google.com/).
2. Noções básicas de Python.
3. Conhecimento básico sobre modelos de linguagem (opcional).

---

## Passo a Passo

### 1. Instale as dependências

No Google Colab, instale as bibliotecas necessárias executando o comando abaixo:

```bash
!pip install transformers torch
```
### 2. Carregue o modelo e o tokenizador

Use o código abaixo para carregar o modelo BERT Base Uncased e seu tokenizador:

```bash
from transformers import BertTokenizer, BertModel

# Carregar o tokenizador e o modelo
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
model = BertModel.from_pretrained('bert-base-uncased')

print("Modelo carregado com sucesso!")
```
### 3. Tokenize um texto
Escolha um texto e transforme-o em tensores para processamento:
```bash
# Texto de exemplo
text = "Hugging Face is creating a tool that democratizes AI."

# Tokenizar o texto
inputs = tokenizer(text, return_tensors='pt', padding=True, truncation=True)

print("Tokens gerados:", inputs)
```
### 4. Processe o texto com o modelo

Passe os dados tokenizados pelo modelo e inspecione as saídas:

```bash
# Obter as saídas do modelo
outputs = model(**inputs)

# Representações retornadas
last_hidden_state = outputs.last_hidden_state  # Representações por token
pooler_output = outputs.pooler_output  # Representação da frase inteira

print("Last hidden state shape:", last_hidden_state.shape)
print("Pooler output shape:", pooler_output.shape)
```

### 5. Entendendo as saídas
last_hidden_state: Representações contextuais de cada token no texto. Útil para tarefas como NER (Reconhecimento de Entidades Nomeadas) ou análise de tokens.
pooler_output: Vetor que representa a frase inteira, baseado no token especial [CLS]. Ideal para tarefas como classificação ou análise de similaridade.

