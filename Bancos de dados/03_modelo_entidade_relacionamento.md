# Modelo Entidade Relacionamento (MER)

Abaixo temos um exemplo de uam modelagem para o fluxo de emissão de nota fiscal:
![Exemplo de modelo entidade relacionamento para um fluxo de emissão de nota fiscal](../Imagens/bancos_de_dados/der_nota_fiscal.png)

Algumas conclusões importantes que podemos tirar do diagrama:

- Temos as entidades Nota Fiscal, Cliente, Produto e Produto da Nota Fiscal;
- A entidade Produto da Nota Fiscal tem relação com as entidades Nota Fiscal e Produto, criando um vínculo entre essas duas entidades;
- Um Produto da Nota Fiscal pode conter um único Produto e só pode estar em uma única Nota Fiscal;
- Já um Produto pode estar em múltiplos Produtos da Nota Fiscal e uma Nota Fiscal pode conter múltiplos produtos;
- Por fim, uma nota fiscal precisa ter um cliente e só pode conter um único cliente, porém o Cliente pode possuir múltiplas Notas Fiscais.