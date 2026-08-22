# ICP - Leitor de Dados do Módulo ICP

App desenvolvido com Streamlit para leitura, análise e comparação de sinais a partir de arquivos CSV gerados pelo módulo ICP.

## 🚀 Como rodar o projeto

1. **Crie o ambiente virtual**:
   ```
   python -m venv venv
   ```

2. **Ative o ambiente virtual**:
   - Windows (CMD): `venv\Scripts\activate`
   - Linux/Mac: `source venv/bin/activate`
   - Bash no Windows: `source venv/Scripts/activate`

3. **Instale as dependências**:
   ```
   pip install -r requirements.txt
   ```

4. **Execute o aplicativo**:
   ```
   streamlit run app.py
   ```

## Organização do Projeto

O repositório está organizado da seguinte maneira:

- `app.py`: Arquivo principal da aplicação Streamlit. Contém a lógica de interface, upload e plotagem dos gráficos.
- `pages/`: Diretório contendo páginas adicionais da aplicação (multipage app do Streamlit).
- `requirements.txt`: Lista de dependências e bibliotecas Python necessárias para rodar o projeto.
- `venv/`: Ambiente virtual contendo os pacotes instalados isoladamente.
- `README.md`: Este arquivo de documentação.

## Requisitos do Arquivo de Dados e Funcionalidades

A aplicação espera receber os dados provenientes do módulo ICP e fornece uma interface de visualização interativa.

### O que o código espera receber

Para que o aplicativo processe os dados corretamente, o arquivo enviado deve seguir estas características:

- **Formato do Arquivo**: Deve obrigatoriamente ter a extensão `.csv` (Comma Separated Values).
- **Estrutura (Cabeçalhos)**: A primeira linha do arquivo deve conter o cabeçalho (nomes das colunas), por exemplo: `Tempo`, `Sinal 1`, `Sinal 2`, etc. Esses nomes serão capturados automaticamente e disponibilizados como opções para a seleção dos eixos X e Y.
- **Tipos de Dados nas Colunas**: Abaixo dos cabeçalhos, os dados devem ser valores numéricos correspondentes às leituras do módulo. O código realiza a leitura destas colunas usando a biblioteca Pandas.

### O que o código gera

Após o usuário realizar o upload do arquivo CSV com sucesso, o sistema analisa os dados e gera na tela as seguintes visualizações:

1. **Pré-visualização dos Dados (Tabela)**: Exibe uma tabela interativa contendo os dados brutos carregados do CSV, para que o usuário possa conferir se a importação ocorreu conforme o esperado.
2. **Informações Gerais**: Calcula e exibe o número total de linhas e colunas (dimensões da tabela), dando uma noção imediata do volume de amostras.
3. **Gráfico de Série Única (Eixo Y)**: Disponibiliza um menu onde o usuário escolhe qualquer coluna lida. A aplicação então gera um gráfico de linha dessa variável, utilizando como eixo X simplesmente o índice das linhas do arquivo.
4. **Gráfico Comparativo (X vs Y)**: Oferece dois menus suspensos onde é possível configurar os eixos independentemente.
   - O primeiro menu escolhe qual coluna ditará o **Eixo X** (por exemplo, a coluna de `Tempo`).
   - O segundo menu escolhe a coluna do **Eixo Y**. O código é inteligente o suficiente para remover do segundo menu a coluna que já foi selecionada para o Eixo X.
   - Um segundo gráfico de linha é então gerado, traçando com precisão a relação entre as duas variáveis escolhidas.
