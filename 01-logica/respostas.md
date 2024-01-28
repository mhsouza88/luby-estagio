# ✩ Lista 01: Lógica de Programação ✩
## Obs.: Os exercícios foram resolvidos usando Javascript.
### 01) Implemente a função abaixo para calcular fatorial de um número.
````csharp
    // Exemplo:
    // 5! = 5 · 4 · 3 · 2 · 1 = 120
    CalcularFatorial(5) == 120//true
````

````javascript
const calcularFatorial = (numero) => {
  if (numero === 0 || numero === 1) {
    return 1;
  } else {
    return numero * calcularFatorial(numero - 1);
  }
};

console.log(calcularFatorial(5) === 120); // resultado: true
````

### 02) Implemente a função abaixo que calcula o valor total do prêmio somando fator do tipo do prêmio conforme valores:
    - Tipo: "basic" fator multiplicação do prêmio: 1
    - Tipo: "vip" fator multiplicação do prêmio: 1.2
    - Tipo: "premium" fator multiplicação do prêmio: 1.5
    - Tipo: "deluxe" fator multiplicação do prêmio: 1.8
    - Tipo: "special" fator multiplicação do prêmio: 2
    
- **Regras**
    - A função também deverá provir um parâmetro para que seja passado fator de multiplicação próprio.
    - Quando parâmetro de fator de multiplicação próprio for informado e válido o mesmo deve sobrescrever o cálculo do tipo de prêmio.
    - O prêmio nunca deve ter um valor negativo ou igual a zero.

````csharp
// Exemplo
CalcularPremio(100, "vip", null) == 120.00;//true
CalcularPremio(100, "basic", 3) == 300.00;//true
````

````javascript
const calcularPremio = (valor, tipo, fatorProprio) => {
  const fatores = {
    basic: 1,
    vip: 1.2,
    premium: 1.5,
    deluxe: 1.8,
    special: 2,
  };

  let fatorFinal =
    fatorProprio && fatorProprio > 0 ? fatorProprio : fatores[tipo];

  let premioFinal = valor * fatorFinal;
  return premioFinal > 0 ? premioFinal : 0;
};

console.log(calcularPremio(100, "vip", null) === 120.0); // resultado: true
console.log(calcularPremio(100, "basic", 3) === 300.0); // resultado: true
````

### 03) Implemente a função abaixo para contar quantos números primos existe até o número informado.
````csharp
// Exemplo
//Número primo: 2
//Número primo: 3
//Número primo: 5
//Número primo: 7
//Total de números primos: 4
ContarNumerosPrimos(10) == 4//true
````

````javascript
const ehPrimo = (numero) => {
  if (numero <= 1) return false;
  if (numero <= 3) return true;

  if (numero % 2 === 0 || numero % 3 === 0) return false;

  for (let i = 5; i * i <= numero; i += 6) {
    if (numero % i === 0 || numero % (i + 2) === 0) return false;
  }

  return true;
};

const contarNumerosPrimos = (valor) => {
  let contador = 0;
  for (let i = 2; i <= valor; i++) {
    if (ehPrimo(i)) contador++;
  }
  return contador;
};

console.log(contarNumerosPrimos(10) === 4); // resultado: true
````

### 04) Implemente a função abaixo que conta e calcula a quantidade de vogais dentro de uma string.
````csharp
CalcularVogais("Luby Software") == 4//true
````
    
````javascript
const calcularVogais = (texto) => {
    const vogais = ['a', 'e', 'i', 'o', 'u'];
    let contador = 0;

    for (let letra of texto.toLowerCase()) {
        if (vogais.includes(letra)) {
            contador++;
        }
    }

    return contador;
};

console.log(calcularVogais("Luby Software") === 4); // resultado: true
````

### 05) Implemente a função abaixo que aplica uma porcentagem de desconto a um valor e retorna o resultado. 
- Lembre-se que as entradas e saídas dos dados são strings que devem ser tratadas.
````csharp
CalcularValorComDescontoFormatado("R$ 6.800,00", "30%") == "R$ 4.760,00"; //true 
````

````javascript
const calcularValorComDescontoFormatado = (valor, desconto) => {
  let valorNumerico = parseFloat(
    valor.replace("R$", "").replace(/\./g, "").replace(",", ".")
  );
  let percentualDesconto = parseFloat(desconto.replace("%", "")) / 100;

  let valorComDesconto = valorNumerico - valorNumerico * percentualDesconto;

  return `R$ ${valorComDesconto
    .toFixed(2)
    .replace(".", ",")
    .replace(/\B(?=(\d{3})+(?!\d))/g, ".")}`;
};

console.log(
  calcularValorComDescontoFormatado("R$ 6.800,00", "30%") === "R$ 4.760,00"
); // resultado: true
````

### 06) Implemente a função abaixo que obtém duas string de datas e calcula a diferença de dias entre elas.
````csharp
CalcularDiferencaData("10122020", "25122020") == 15; //true 
````

````javascript
const calcularDiferencaData = (data1, data2) => {
  const converterData = (strData) =>
    new Date(
      parseInt(strData.substring(4, 8)), // ano
      parseInt(strData.substring(2, 4)) - 1, // mês (0-11)
      parseInt(strData.substring(0, 2)) // dia
    );

  const dataConvertida1 = converterData(data1);
  const dataConvertida2 = converterData(data2);

  // diferença em milissegundos e conversão para dias
  const diferencaTempo = Math.abs(dataConvertida2 - dataConvertida1);
  return diferencaTempo / (1000 * 60 * 60 * 24);
};

console.log(calcularDiferencaData("10122020", "25122020") === 15); // resultado: true
````

### 07) Implemente a função abaixo que retorna um novo vetor com todos elementos pares do vetor informado.
````csharp
int[] vetor = new int[] { 1,2,3,4,5 };
ObterElementosPares(vetor) == new int { 2, 4 }; //true 
````

````javascript
const obterElementosPares = (vetor) => {
  return vetor.filter((elemento) => elemento % 2 === 0);
};

const arraysSaoIguais = (arr1, arr2) => {
  if (arr1.length !== arr2.length) return false;
  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i] !== arr2[i]) return false;
  }
  return true;
};

let vetor = [1, 2, 3, 4, 5];
let resultadoEsperado = [2, 4];
console.log(arraysSaoIguais(obterElementosPares(vetor), resultadoEsperado)); // resultado: true
````

### 08) Implemente a função abaixo que deve buscar um ou mais elementos no vetor que contém o valor ou parte do valor informado na busca.
````csharp
string[] vetor = new string[] {
  "John Doe",
  "Jane Doe",
  "Alice Jones",
  "Bobby Louis",
  "Lisa Romero"
};

BuscarPessoa(vetor, "Doe") == new string[] { "John Doe", "Jane Doe" };//true
BuscarPessoa(vetor, "Alice") == new string[] { "Alice Jones" };//true
BuscarPessoa(vetor, "James") == new string[] { };//true
````

````javascript
const buscarPessoa = (vetor, busca) => {
  return vetor.filter((pessoa) => pessoa.includes(busca));
};

const arraysSaoIguais = (arr1, arr2) => {
  if (arr1.length !== arr2.length) return false;
  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i] !== arr2[i]) return false;
  }
  return true;
};

let vetor = [
  "John Doe",
  "Jane Doe",
  "Alice Jones",
  "Bobby Louis",
  "Lisa Romero",
];

console.log(arraysSaoIguais(buscarPessoa(vetor, "Doe"), ["John Doe", "Jane Doe"])); // resultado: true
console.log(arraysSaoIguais(buscarPessoa(vetor, "Alice"), ["Alice Jones"])); // resultado: true
console.log(arraysSaoIguais(buscarPessoa(vetor, "James"), [])); // resultado: true
````

### 09) Implemente a função abaixo que obtém uma string com números separados por vírgula e transforma em um array de array de inteiros com no máximo dois elementos.
````csharp
TransformarEmMatriz("1,2,3,4,5,6") == new int[][] { new int[] { 1, 2 }, new int[] { 3, 4 }, new int[] { 5, 6 } }; //true 
````

````javascript
const transformarEmMatriz = (strNumeros) => {
  let numeros = strNumeros.split(",").map(Number);
  let matriz = [];

  for (let i = 0; i < numeros.length; i += 2) {
    matriz.push(numeros.slice(i, i + 2));
  }

  return matriz;
};

const arraysDeArraysSaoIguais = (arr1, arr2) => {
  if (arr1.length !== arr2.length) return false;
  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i].length !== arr2[i].length) return false;
    for (let j = 0; j < arr1[i].length; j++) {
      if (arr1[i][j] !== arr2[i][j]) return false;
    }
  }
  return true;
};

let resultadoEsperado = [
  [1, 2],
  [3, 4],
  [5, 6],
];
console.log(
  arraysDeArraysSaoIguais(transformarEmMatriz("1,2,3,4,5,6"), resultadoEsperado)
); // resultado: true
````

### 10) Implemente a função abaixo que compara dois vetores e cria um novo vetor com os elementos faltantes de ambos.
````csharp
// Exemplo
// faltam elementos no vetor2
int[] vetor1 = new int[] { 1,2,3,4,5 };
int[] vetor2 = new int[] { 1,2,5 };
ObterElementosFaltantes(vetor1, vetor2) == new int[] { 3, 4 }; //true 

// faltam elementos no vetor3
int[] vetor3 = new int[] { 1,4,5 };
int[] vetor4 = new int[] { 1,2,3,4,5 };
ObterElementosFaltantes(vetor3, vetor4) == new int[] { 2, 3 }; //true
  
// faltam elementos em ambos vetores
int[] vetor5 = new int[] { 1,2,3,4 };
int[] vetor6 = new int[] { 2,3,4,5 };
ObterElementosFaltantes(vetor5, vetor6) == new int[] { 1, 5 }; //true

// não faltam items
int[] vetor7 = new int[] { 1,3,4,5 };
int[] vetor8 = new int[] { 1,3,4,5 };
ObterElementosFaltantes(vetor7, vetor8) == new int[] { }; //true
````

````javascript
const obterElementosFaltantes = (vetor1, vetor2) => {
  let faltandoEmVetor1 = vetor1.filter(
    (elemento) => !vetor2.includes(elemento)
  );
  let faltandoEmVetor2 = vetor2.filter(
    (elemento) => !vetor1.includes(elemento)
  );

  return faltandoEmVetor1.concat(faltandoEmVetor2);
};

const arraysSaoIguais = (arr1, arr2) => {
  if (arr1.length !== arr2.length) return false;
  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i] !== arr2[i]) return false;
  }
  return true;
};

console.log(
  arraysSaoIguais(obterElementosFaltantes([1, 2, 3, 4, 5], [1, 2, 5]), [3, 4])
); // resultado: true
console.log(
  arraysSaoIguais(obterElementosFaltantes([1, 4, 5], [1, 2, 3, 4, 5]), [2, 3])
); // resultado: true
console.log(
  arraysSaoIguais(obterElementosFaltantes([1, 2, 3, 4], [2, 3, 4, 5]), [1, 5])
); // resultado: true
console.log(
  arraysSaoIguais(obterElementosFaltantes([1, 3, 4, 5], [1, 3, 4, 5]), [])
); // resultado: true
````
