
# LangChain Text Summarization with ChatOpenAI

Este repositório demonstra um exemplo de uso da biblioteca **LangChain** com **OpenAI** para gerar resumos de informações sobre uma pessoa famosa. Utilizando **PromptTemplates** e **LLMChains**, o código solicita um resumo e dois fatos interessantes sobre a pessoa a partir de um trecho de informações.

## 1. Explicação sobre o código

Este código utiliza o LangChain para trabalhar com LLMs (Large Language Models) através de templates de prompts que podem ser enviados para o modelo de linguagem GPT-3.5 da OpenAI. O código se conecta à API da OpenAI, processa uma string de informação, e a partir dessa string, gera um resumo e dois fatos interessantes sobre a pessoa descrita.

## 2. O que é LLM?

LLM (Large Language Model) refere-se a um modelo de linguagem de grande porte, como o GPT-3.5, treinado em grandes quantidades de texto para entender e gerar linguagem natural de maneira eficiente. Ele é capaz de realizar uma ampla gama de tarefas, como tradução, resumo, geração de conteúdo e muito mais.

## 3. O que é LangChain?

LangChain é uma biblioteca que ajuda desenvolvedores a criar aplicativos complexos baseados em modelos de linguagem, permitindo a construção de pipelines, o uso de várias fontes de dados e o gerenciamento de interações com modelos de linguagem. Ele fornece uma estrutura modular para trabalhar com LLMs, facilitando o uso de prompts e cadeias (chains) de execução.

## 4. Bash para copiar e colar:

### Clonar o repositório
```bash
git clone https://github.com/seu-usuario/langchain-openai-summarization.git
cd langchain-openai-summarization
```

### Criar um ambiente virtual e instalar dependências
```bash
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### Criar arquivo `.env` com a chave da API da OpenAI:
```bash
touch .env
echo "OPENAI_KEY=sk-seu-token-aqui" >> .env
```

### Executar o código
```bash
python main.py
```

## 5. Explicação dos fragmentos de código

### Carregar a chave da API
```python
from dotenv import load_dotenv
import os

load_dotenv()
openai_api_key = os.getenv('OPENAI_KEY')
```
Este trecho usa a biblioteca `dotenv` para carregar as variáveis de ambiente do arquivo `.env`, onde a chave da API do OpenAI é armazenada.

### Criar o template de resumo
```python
summary_template = '''
Given the following information about a person: {information}, please create:
1. A short summary
2. Two interesting facts about them
'''
summary_prompt_template = PromptTemplate(input_variables=["information"], template=summary_template)
```
Aqui, o `PromptTemplate` cria um prompt a ser enviado para o modelo. Ele usa a variável `information` como entrada.

### Instanciar o modelo de linguagem
```python
llm = ChatOpenAI(temperature=0, model_name='gpt-3.5-turbo', openai_api_key=openai_api_key)
```
Este trecho inicializa o modelo GPT-3.5 da OpenAI com a chave da API. O parâmetro `temperature=0` significa que o modelo será menos criativo e fornecerá respostas mais consistentes.

### Criar a cadeia de execução (LLMChain)
```python
chain = LLMChain(llm=llm, prompt=summary_prompt_template)
```
`LLMChain` combina o `PromptTemplate` e o modelo de linguagem `ChatOpenAI`, criando uma cadeia de execução para enviar prompts ao LLM e obter respostas.

### Executar o processo
```python
res = chain.run(information=information)
print(res)
```
O método `run()` envia as informações fornecidas (`information`) para a cadeia e imprime o resultado (um resumo e dois fatos interessantes sobre Elon Musk).

## 6. Como copiar o repositório e executar na máquina

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/langchain-openai-summarization.git
   cd langchain-openai-summarization
   ```

2. Crie um ambiente virtual e instale as dependências:
   ```bash
   python -m venv venv
   source venv/bin/activate  # No Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Crie um arquivo `.env` na raiz do projeto e insira sua chave da API da OpenAI:
   ```bash
   touch .env
   echo "OPENAI_KEY=sk-seu-token-aqui" >> .env
   ```

4. Execute o script:
   ```bash
   python main.py
   ```

## Dependências

- [LangChain](https://python.langchain.com/en/latest/)
- [OpenAI Python Client](https://beta.openai.com/docs/)
- [dotenv](https://pypi.org/project/python-dotenv/)

## Conclusão

Este projeto é um exemplo básico de como utilizar modelos de linguagem como o GPT-3.5 da OpenAI com LangChain para gerar resumos automáticos de informações. Sinta-se à vontade para explorar mais e adaptar o código para diferentes usos e tarefas!
