# ✩ Desafio em Orientação a Objetos ✩
## Obs.: O exercício foi resolvido utilizando Typescript. Para rodar, siga as instruções abaixo:
>   1. Instalar o Node.js (https://nodejs.org/)
>   2. Criar um arquivo Javascript, copiar e colar o código da resolução e salvar o arquivo (exemplo: maquinaDeVendas.js)
>   3. Instalar o Typescript globalmente [npm install -g typescript].
>   4. Compilar o arquivo de Typescript para Javascript usando o comando [tsc maquinaDeVendas.ts].
>   5. Executar o arquivo Javascript resultante com o Node.js no terminal usando [node maquinaDeVendas.js].
### AVISO: Como foi pedido no enunciado da lista de exercícios, nenhuma biblioteca ou dependência externa foi usada. Entretanto, ao usar o Typescript sem a dependência necessária, a visualização do menu e a interação com o usuário foram comprometidas. Ou seja, é uma visualização estática apenas.

### 01) Desenvolver programa que rode uma **Vending Machine (Máquina de venda de bebidas em lata)** utilizando orientação objetos conforme as regras abaixo.
> - Crie uma interface de usuário simples para execução da máquina. (Utilizando Console por exemplo)
> - A máquina deverá possuir um estoque de produtos com valor e quantidade de cada produto. 
>   A quantidade de produto no estoque da máquina deve ser alterado conforme realização de vendas dos produtos.
> - A máquina deverá ter opção para visualizar estoque e quantidade disponível.
> - A máquina só pode vender produtos com quantidade em estoque disponível.
> - A máquina deverá contabilizar as vendas e mostrar o valor total das vendas realizadas.
> - Uma venda só poderá ser concluída ao inserir o valor total do produto.
> - A máquina deverá contabilizar e solicitar o valor faltante para finalizar a venda, caso haja valor de troco para deverá informar o valor.
> - A máquina não necessita de lógica de contagem de notas, será apenas necessário informar os valores.
> - Caso necessário crie um documento simples com informações de como executar o programa.

#### Resolução:
````typescript
class Produto {
  constructor(
    public nome: string,
    public preco: number,
    public quantidade: number
  ) {}
}

class MaquinaDeVendas {
  private vendas: number = 0;
  private produtos: Map<string, Produto> = new Map();

  adicionarProduto = (produto: Produto): void => {
    this.produtos.set(produto.nome, produto);
  };

  mostrarProdutos = (): void => {
    console.log("\nProdutos Disponíveis:");
    this.produtos.forEach((produto) => {
      console.log(
        `${produto.nome}: R$${produto.preco.toFixed(2)}, Quantidade: ${
          produto.quantidade
        }`
      );
    });
  };

  comprarProduto = (nomeProduto: string, valorPago: number): void => {
    const produto = this.produtos.get(nomeProduto);
    if (!produto) {
      console.log("Produto não encontrado!");
      return;
    }
    if (produto.quantidade <= 0) {
      console.log("Produto esgotado!");
      return;
    }
    if (valorPago < produto.preco) {
      console.log(
        `Valor insuficiente! Por favor, adicione mais R$${(
          produto.preco - valorPago
        ).toFixed(2)}.`
      );
      return;
    }

    produto.quantidade--;
    this.vendas += produto.preco;
    const troco = valorPago - produto.preco;
    console.log(`Comprou ${produto.nome}. Troco: R$${troco.toFixed(2)}`);
  };

  mostrarVendas = (): void => {
    console.log(`\nTotal de Vendas: R$${this.vendas.toFixed(2)}`);
  };
}

// Saídas desejadas ao comprar um produto
let maquina = new MaquinaDeVendas();
maquina.adicionarProduto(new Produto("Sukita", 2.5, 10));
maquina.adicionarProduto(new Produto("Pepsi", 2.0, 15));

// Mais algumas ações
maquina.mostrarProdutos();
maquina.comprarProduto("Sukita", 3.0);
maquina.mostrarVendas();
````
