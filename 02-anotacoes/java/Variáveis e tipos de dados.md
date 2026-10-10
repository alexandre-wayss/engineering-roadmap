# Variáveis e tipos de dados — Java

> Issue: [#1 — Variáveis e tipos de dados](https://github.com/alexandre-wayss/engineering-roadmap/issues/1)
> Exercício: [CompraProduto.java](https://github.com/alexandre-wayss/java-exercises/blob/main/01-fundamentos/vari%C3%A1veis/CompraProduto.java)

## O que são variáveis?

Variáveis guardam valores para o programa usar. Na declaração, indicamos o tipo, o nome e, opcionalmente, o valor inicial.

```java
String produto = "teclado";
float precoProduto = 350f;
int quantidade = 2;
```

- **String**: texto (é uma classe, não um tipo primitivo).
- **int**: números inteiros.
- **float**: números decimais com precisão menor que `double`; o sufixo `f` indica um literal `float`.
- **double**: números decimais com maior precisão que `float`.
- **boolean**: `true` ou `false`.
- **char**: um caractere, como `'A'`.

## Entrada de dados com Scanner

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.println("Digite a quantidade:");
int quantidade = scanner.nextInt();
scanner.close();
```

- `nextInt()` lê um número inteiro diretamente.
- `nextLine()` lê uma linha como `String`.
- `Integer.parseInt(scanner.nextLine())` lê texto e o interpreta como um inteiro. **Isso não é casting**: é uma conversão feita por um método.
- Fechar o `Scanner` faz sentido quando não haverá mais leituras da entrada naquele programa.

## Operações com variáveis

```java
float precoProduto = 350f;
int quantidade = 2;
float valorCompra = quantidade * precoProduto;
```

O cálculo usa as variáveis, sem precisar escrever o total manualmente. Nessa multiplicação, o `int` é promovido automaticamente para `float` durante a operação.

## Saída formatada

```java
System.out.printf("Total: R$ %.2f%n", valorCompra);
```

- `%s`: texto.
- `%d`: inteiro.
- `%.2f`: número decimal com duas casas.
- `%n`: quebra de linha.

## Casting — ainda não praticado

**Casting** é indicar explicitamente uma conversão de tipo.

```java
double preco = 19.90;
int parteInteira = (int) preco; // resultado: 19
```

O `(int)` descarta a parte decimal, **não arredonda**. Algumas conversões numéricas acontecem automaticamente (por exemplo, `int` para `double`); outras exigem conversão explícita.

**Pendente:** criar um pequeno exemplo próprio com casting e explicar a diferença entre conversão implícita, casting explícito e `Integer.parseInt()`.

## Aplicação prática

No exercício `CompraProduto.java`, pratiquei:

- Declaração e uso de variáveis.
- Tipos `String`, `float` e `int`.
- Leitura de uma quantidade no terminal.
- Multiplicação para obter o valor da compra.
- Exibição do resultado.

**Observação:** a versão mais recente trabalhada localmente utiliza `nextInt()` e `printf()`; publicar essas mudanças no GitHub para atualizar a versão vinculada acima.

## Para revisar depois

- Por que usar `float` ou `double`?
- Qual a diferença entre `nextInt()` e `nextLine()`?
- Como um casting pode causar perda de informação?
- Em sistemas financeiros reais, por que `BigDecimal` costuma ser preferido a `float` e `double`?
