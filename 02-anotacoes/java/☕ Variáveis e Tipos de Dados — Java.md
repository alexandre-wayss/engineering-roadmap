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

### String → int

```java
String numero = "10";
int quantidade = Integer.parseInt(numero);
```

### Casting

```java
double preco = 19.90;
int valorInteiro = (int) preco;
```

O casting para int descarta a parte decimal.

## 5. Saída formatada

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


