## Estruturas de Decisão: if, else if e else
Permitem desviar o fluxo de execução com base em expressões booleanas (`true` ou `false`). São ideais para testar **faixas de valores** ou condições lógicas compostas.

```java
double nota = 8.5;

if (nota >= 9.0) {
    System.out.println("Excelente! Conceito A");
} else if (nota >= 7.0) {
    System.out.println("Aprovado! Conceito B");
} else if (nota >= 5.0) {
    System.out.println("Recuperação! Conceito C");
} else {
    System.out.println("Reprovado! Conceito D");
}
```

- **Avaliação em cascata:** O Java avalia de cima para baixo. Assim que a primeira condição verdadeira é atendida, seu bloco é executado e todas as seguintes são ignoradas.
- **O bloco `else`:** É opcional e serve como comportamento padrão caso nenhuma condição anterior seja satisfeita.

### Escopo de Variáveis em Blocos `{ }`
Variáveis declaradas dentro de um bloco condicional só existem **dentro** daquelas chaves:

```java
if (autorizado) {
    int codigoAcesso = 1234; // Criada e visível apenas dentro deste if
    System.out.println(codigoAcesso);
}

// System.out.println(codigoAcesso); // ERRO de compilação: variável inacessível fora do bloco
```
Se precisar usar o valor fora do bloco, declare a variável **antes** da estrutura condicional:
```java
int codigoAcesso = 0;
if (autorizado) {
    codigoAcesso = 1234;
}
System.out.println(codigoAcesso); // Funciona normalmente
```

## Switch Classico
```java
int dia = 2;

switch (dia) {
    case 1:
        System.out.println("Domingo");
        break;
    case 2:
        System.out.println("Segunda");
        break;
    default:
        System.out.println("Dia inválido");
        break;
}

```

- fall-through: se esquecer o comando break a execução continua rodando o bloco abaixo até encontrar um break ou o final do switch.
- Tipos permitidos no switch: `byte`, `short`, `char`, `int` (e seus respectivos wrappers `Byte`, `Short`, `Character`, `Integer`), `String` e `enum`. Tipos como `double`, `float` e `long` não são permitidos.

## Switch Expression
```java
int dia = 2;

// Usando como expressão com retorno:
String nomeDia = switch (dia) {
    case 1 -> "Domingo";
    case 2 -> "Segunda";
    case 3, 4, 5, 6, 7 -> "Outro dia";
    default -> "Inválido";
};

```
- Cada bloco encerra automaticamente sem transbordar para o próximo (sem fall-through).
- Múltiplos valores podem ser agrupados por vírgula no mesmo `case`.
- **Blocos com múltiplas instruções (`yield`):** Se um `case` precisar de mais de uma linha de código, usa-se chaves `{}` e a palavra-chave `yield` para devolver o valor resultante:
  ```java
  String status = switch (codigo) {
      case 1 -> "Ativo";
      case 2 -> {
          System.out.println("Registrando tentativa pendente...");
          yield "Pendente";
      }
      default -> "Desconhecido";
  };
  ```

## IFs aninhados:
O problema do IF aninhado é que torna o código difícil de ler, testar e manter, conhecido como *Pyramid of Doom* ou *Arrow Anti-pattern*, em que o dev precisa ficar memorizando o estado de condições anteriores abertas para deduzir o que acontece no meio do bloco ou em um `else` futuro. Cada nível de aninhamento multiplica a quantidade de caminhos de execução possíveis, o que exige uma quantidade desproporcional de testes unitários. O *Happy Path* da funcionalidade fica espremido e escondido no ponto mais profundo da indentação ao invés de ficar visível logo no início.

### Soluções possiveis:
#### Early Return:
inverter a logica para checar os casos de erro ou saida primeiro e interromper o metodo com return ou throw.

#### Combinar condições (usar && e || )
Agrupar validacoes que levem ao mesmo resultado em uma unica linha usando esses operadores logicos com curto-circuito.

#### Extrair metodos menores
Mover validacoes e regras compostas para metodos com nomes autoexplicativos

#### Operador ternario
Substituir blocos grandes por atribuições simples

#### Polimorfismo / Strategy
Substituir condicionais de tipo ou comportamento por classes distintas que compartilham uma interface comum.