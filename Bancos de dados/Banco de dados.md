## Dado vs Informação

O dado é a menor parte de uma banco de dados, um banco de dados é feito para armazenar dados. O dado é o elemento bruto geralmente proveniente de uma entrada do usuário ou de outros sistemas.

A informação é um elemento já processado constituído de dados, sendo proveniente do processamento de dados.

![[dado_vs_informacao|100%]]

## Banco de dados relacional vs Não relacional

Os bancos de dados relacionais são conhecidos como bancos SQL. Isso se dá porque o SQL, que vem de Structured Query Language ou Linguagem de Consulta Estruturada, é a linguagem que se usa para se comunicar com bancos relacionais.
Já os bancos não relacionais são conhecidos como NoSQL (Not Only SQL), pois podem ou não usar a linguagem SQL.

## Bancos de dados relacionais

Conceito criado por Edgar Frank Codd em 1970, baseado no modelo relacional, onde os dados estão guardados entre tabelas que por sua vez podem ou não estar relacionadas.

### Pontos fortes

Os SGBD - Sistemas Gerenciadores de Bancos de Dados, oferecem aos usuário processos de validação, verificação e garantia de integridade dos dados. Além de oferecer controle de concorrência, recuperação de falhas e segurança, controle de transações, otimização de consultas, dentre outras.

### Pontos fracos

Dificuldade de conciliar o modelo relacional com a demanda por escalabilidade cada vez mais frequente. Dificuldade em se organizar os dados em um sistema distribuído trabalhando com particionamento de dados.

## Bancos de dados não relacionais

O termo NoSQL surgiu em 1998, partindo de uma solução de banco de dados que não oferencia uma interface SQL, mas ainda assim estava baseado inicialmente na arquitetura relacional. Posteriormente, o termo passou a representar soluções que promoviam uma alternativa ao modelo relacional, tornando-se uma abreviação de Not Only SQL - Não Apenas SQL. O maior diferencial desse tipo de banco é a performance, pois por não utilizar um modelo estruturado em tabelas, consegue-se trabalhar com dados de forma muito mais rápida.

### Características comuns

Como não se baseiam no modelo relacional, promovem alta disponibilidade e maior escalabilidade.

### Algumas implementações oferecem

- Parcitionamento e replicação de dados;
- Sistemas baseados em armazenamento de chave/valor;
- Sistemas orientados a documentos;
- SIstemas orientaods a colunas;
- Sistemas baseados em grafos.

![[exemplificacao|100%]]
## Principais bancos relacionais

