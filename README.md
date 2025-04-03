# Projeto Intuitive Care
Este projeto foi desenvolvido como parte dos Testes de Nivelamento v.250321 e atende as tarefas solicitadas:

- __Teste de Web Scraping:__ Realização de acesso ao site da ANS, download de anexos de informações e compactação de todos os anexos em um único arquivo.

- __Teste de Transformação de Dados:__ Extração e transformação de dados de arquivos PDF para o formato CSV e compactação do arquivo CSV.

- __Teste de Banco de Dados:__ Criação de scripts SQL para importação e análise de dados, incluindo queries analíticas.

- __Teste de API:__ Desenvolvimento de uma interface web utilizando Vue.js que interage com um servidor Python para realizar buscas textuais na lista de cadastros de operadoras.

O projeto é organizado em três repositórios, cada um com responsabilidades específicas:


## Repositórios
__1. [ic-backend](https://github.com/beatrizlimac/ic-backend/tree/main):__  
- __Descrição:__
Contém a API Python (desenvolvida com Flask) que expõe uma rota para realizar a busca textual na lista de cadastros de operadoras.
Também inclui dois scripts auxiliares:

   - `transforma.py:` Script para transformação de dados (por exemplo, extração e formatação de informações do PDF do rol de procedimentos).

   - `scraping.py:` Script para realizar web scraping, acessando o site da ANS e efetuando o download dos anexos indicados.
       
- __Containerização:__
Possui um Dockerfile que constrói a imagem Docker do backend.

__2. [ic-frontend](https://github.com/beatrizlimac/ic-frontend/tree/main):__  
- __Descrição:__
Contém a aplicação web construída com Vue.js (usando Vite) que consome a API do backend. A interface permite ao usuário inserir um termo de busca e visualizar os registros mais relevantes dos cadastros de operadoras.

- __Containerização:__
Possui um Dockerfile próprio para a construção da imagem Docker do frontend.

__3. intuitive-care:__
- __Descrição:__
Repositório raiz que orquestra os repositórios ic-backend e ic-frontend utilizando o Docker Compose.
Também contém um arquivo .gitignore configurado para ignorar as pastas dos repositórios ic-backend e ic-frontend.

- __Principais arquivos:__

   - `docker-compose.yml:` Define e inicia os containers para o backend, para o frontend e para o mysql.

   - `.gitignore:` Configurado para ignorar arquivos e pastas desnecessárias ou geradas automaticamente.


## Pré-Requisitos
- Docker e Docker Compose instalados.
- Git para clonar os repositórios.


## Instalação e Execução
__1. Clonando os Repositórios:__  

Clone o repositório intuitive-care inicialmente, em seguida clone os repositórios ic-backend e ic-frontend
```
git clone https://github.com/seu-usuario/intuitive-care.git
cd intuitive-care
git clone https://github.com/seu-usuario/ic-backend.git
git clone https://github.com/seu-usuario/ic-frontend.git
```
__2. Executando o Docker Compose:__  

No diretório intuitive-care, execute o comando:
```
docker-compose up --build
```
Esse comando irá:
  - Construir e iniciar o container do ic-backend.
  - Construir e iniciar o container do ic-frontend.

__3. Acessando os serviços:__  

- __API (Backend):__
  
  Teste a API acessando, por exemplo:
  ```
  http://localhost:5001/?q={{ termo }}
  ```
  ou utilizando o Postman.

- __Aplicação Web (Frontend):__

  Acesse a interface em:
  ```
  http://localhost:5173/
  ```

- __Postman:__

  Acesse a coleção do Postman no diretório:
  ```
  intuitive-care/intuitive-care.postman_collection.json
  ```


## Uso e Funcionalidades
- __Busca Textual:__
  
  A aplicação Vue permite a inserção de um termo de busca. Ao submeter, uma requisição é enviada para a API Flask, que retorna os registros mais relevantes dos cadastros de operadoras.

- __Web Scraping e Transformação:__
  
  Os scripts `scraping.py` e `transforma.py` são utilizados para:

  - Acessar o site da ANS e realizar o download dos anexos em PDF.
  - Extrair dados do PDF do rol de procedimentos e eventos em saúde.
  - Transformar e salvar esses dados em um arquivo CSV, com compactação e substituição de abreviações conforme especificado nos testes.

- __Banco de Dados e Análises:__
  
  Embora não esteja detalhado neste README, o projeto também inclui scripts SQL para importar dados e realizar queries analíticas, conforme as tarefas de banco de dados dos testes.

- __Interface e Demonstração:__  

  A interface web, desenvolvida em Vue.js, também permite a demonstração dos resultados por meio de uma coleção no Postman, conforme exigido no teste de API.
