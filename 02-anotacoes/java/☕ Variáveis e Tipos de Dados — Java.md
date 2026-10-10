## 1. O que são variáveis?

Variáveis são espaços na memória utilizados para
armazenar valores que podem ser utilizados pelo programa.

### Sintaxe
```java
tipo nomeVariavel = valor;
```

### Exemplo
```java
String produto = "Teclado";
int quantidade = 2;
float preco = 350f;
```

## 2. Tipos de dados

| Tipo    | Utilização          | Exemplo |
| ------- | ------------------- | ------- |
| int     | Números inteiros    | 10      |
| double  | Números decimais    | 19.90   |
| float   | Números decimais    | 19.90f  |
| boolean | Verdadeiro ou falso | true    |
| char    | Caractere           | 'A'     |
| String  | Textos              | "Java"  |


## 3. Entrada de dados

A classe Scanner permite receber dados digitados
pelo usuário no terminal.

```java
Scanner scanner = new Scanner(System.in);

int quantidade = Integer.parseInt(scanner.nextLine());

scanner.close();
```

## 4. Conversão de tipos

É o processo de transformar um dado de um tipo em outro, sendo divididas em tipos primitivos (implicitas e explicitas) e conversões de texto/objetos.

### Implicita - ocorre automaticamente
Quando é atribuido um tipo menor a um tipo maior, em casos que não perde dados ou precisão
- Ordem: `byte` → `short` → `int` → `long` → `float` → `double`

```java
int inteiro = 100;
double decimal = inteiro; // Automático: decimal vira 100.0

```

### Explicita (Narrowing / casting)
Quando você força manualmente um tipo maior a entrar em um menor de forma ciente.

- Trunca decimal 
```java
double valor = 9.99;
int truncado = (int) valor; // Vira 9

```

- Estouro de capacidade - Overflow 
```java
int numeroGrande = 130;
byte pequeno = (byte) numeroGrande; // Vira -126 (byte só vai de -128 a 127)

```

### Conversões com String

- String para número (parse)
```java
String texto = "42";
int numero = Integer.parseInt(texto);
double preco = Double.parseDouble("19.90");

```
- Número para String
```java
int valor = 10;
String txt1 = String.valueOf(valor); // Recomendado
String txt2 = Integer.toString(valor);

```
## 5. Formatar saída com printf
O printf permite exibir informações formatadas.

```java
System.out.printf("Total: R$ %.2f%n", 350.0);
```

| Código | Significado         |
| ------ | ------------------- |
| %d     | Inteiro             |
| %s     | Texto               |
| %.2f   | Decimal com 2 casas |
| %n     | Nova linha          |

## String

* No java, string é um objeto que representa uma sequência imutável de caracteres, sendo então uma classe e não um tipo primitivo.

```java
String nome = "Java";
nome.toUpperCase(); // Não altera 'nome'
nome = nome.toUpperCase(); // Agora a variável aponta para o novo objeto "JAVA"

```
- String Constant Pool (pool de string), a JVM armazena literais em uma área especial fazendo com que strings com mesmo texto reaproveitem o endereço de memoria

```java
String a = "Oi";
String b = "Oi"; // Aponta para a mesma referência que 'a'
```

- Usar .equals() para comparar Strings pois " == " compara o endereço de memoria. 

### Métodos comuns:
- length() - para pegar tamanho do texto
- toUpperCase() / toLowerCase() - converter para maiuscula ou minuscula
- charAt(int index) - retorna o caracter que está na posição do index
- contains("texto") - retorna true se tiver o trecho
- replace("antigo", "novo") - substitui o antigo pelo novo quando aparecer a palavra
- trim() / strip() - remove espaços em branco do inicio e do final
- split(",") - quebra o texto em um array de partes menores, nesse caso quando encontra uma virgula ele separa em um array.