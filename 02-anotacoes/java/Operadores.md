## Operadores Aritméticos
Realizam operações matemáticas básicas sobre valores numéricos:

| Operador | Significado | Exemplo | Resultado |
| -------- | ----------- | ------- | --------- |
| +        | Adição (ou concatenação de Strings) | 10 + 5  | 15        |
| -        | Subtração   | 10 - 5  | 5         |
| *        | Multiplicação | 10 * 5  | 50        |
| /        | Divisão     | 10 / 4  | 2 (inteira) |
| %        | Módulo (resto da divisão) | 10 % 3  | 1         |

- **Divisão inteira vs decimal:** Se ambos os operandos forem inteiros, o Java trunca e descarta as casas decimais (`5 / 2` resulta em `2`). Para obter resultado decimal, ao menos um operando precisa ser decimal (`5.0 / 2` resulta em `2.5`).
- **Módulo (`%`):** Muito utilizado para verificar se um número é par ou ímpar (`numero % 2 == 0`) ou limitar intervalos cíclicos.

## Operadores de Atribuição
Atribuem um valor a uma variável, podendo combinar operações matemáticas diretamente (atribuição composta):

| Operador | Equivalente a | Descrição |
| -------- | ------------- | --------- |
| =        | x = y         | Atribuição simples |
| +=       | x = x + y     | Soma e atribui |
| -=       | x = x - y     | Subtrai e atribui |
| *=       | x = x * y     | Multiplica e atribui |
| /=       | x = x / y     | Divide e atribui |
| %=       | x = x % y     | Calcula o resto e atribui |

## Operadores de Incremento e Decremento
Aumentam ou diminuem em 1 o valor de uma variável:

- `++` (Incremento): adiciona 1 ao valor.
- `--` (Decremento): subtrai 1 do valor.

### Pré-fixado vs Pós-fixado
- **Pós-fixado (`x++` / `x--`):** O valor atual é **utilizado primeiro** na expressão e somente depois a variável é incrementada.
  ```java
  int a = 5;
  int b = a++; // b recebe 5, depois 'a' passa a valer 6
  ```
- **Pré-fixado (`++x` / `--x`):** A variável é **incrementada primeiro** e o novo valor é utilizado na expressão.
  ```java
  int a = 5;
  int b = ++a; // 'a' passa a valer 6 primeiro, depois 'b' recebe 6
  ```

## Operadores Relacionais
Comparam dois valores e retornam sempre um valor booleano (`true` ou `false`):

| Operador | Significado      | Exemplo | Retorno |
| -------- | ---------------- | ------- | ------- |
| ==       | Igual a          | 5 == 5  | true    |
| !=       | Diferente de     | 5 != 3  | true    |
| >        | Maior que        | 7 > 10  | false   |
| <        | Menor que        | 3 < 8   | true    |
| >=       | Maior ou igual a | 5 >= 5  | true    |
| <=       | Menor ou igual a | 4 <= 2  | false   |
> [!NOTE]
> O operador `==` compara o endereço de memória (referência) de objetos, não o conteúdo (para objetos como `String`, utilize `.equals()`).

## Operadores Logicos
Conectam expressões booleanas para retornar true ou false.

- && (AND logico) - retorna true se ambas as condicões forem verdadeiras.
- || (OR logico) - retorna true se pelo menos uma das condiçoes forem verdadeiras
- ! (NOT logico) - Inverte o valor booleano, ou seja se era true vira false, false vira true.
- ^ (XOR logico) - retorna true se apenas uma das condições for verdadeira, e false se ambas forem iguais.

&& e || são operadores que funcionam COM CURTO-CIRCUITO que é basicamente dar o resultado sem avaliar a segunda condiçãp por exemplo no AND se a primeira condição for false ele nem avalia a segunda.

Operadores BITWISE (& e |) funcionam como o AND e o OR mas sem o curto-circuito, avaliando sempre ambas as condições.

## Operador Ternario
Uma forma simplificada de escrever if-else que sempre retorna um valor

```java
condicao ? expressaoSeVerdadeiro : expressaoSeFalso;
```

- Obrigação de retorno: O ternário é uma expressão, não uma instrução de controle de fluxo pura. Você precisa atribuir seu resultado a uma variável, passá-lo como argumento para um método ou retorná-lo em uma função.
- Compatibilidade de tipos: Ambas as expressões de retorno precisam ser compatíveis com o tipo esperado pelo destino.
- Encadeamento: É possível aninhar múltiplos ternários, mas isso costuma prejudicar a legibilidade:
  ```java
  String resultado = nota >= 7 ? "Aprovado" : nota >= 5 ? "Recuperação" : "Reprovado";
  ```

## Precedencia dos operadores
| Ordem | Operadores                       | Descrição                    | Associatividade |
| ----- | -------------------------------- | ---------------------------- | --------------- |
| 1     | [] . () ++ (pós) -- (pós)        | Acesso, chamada, pós-fixados | ->              |
| 2     | ++ (pré) -- (pré) + - ! ~ (cast) | Unários, negações, cast      | <-              |
| 3     | * / %                            | Multiplicativos              | ->              |
| 4     | + -                              | Aditivos e concatenação      | ->              |
| 5     | << >> >>>                        | Deslocamento (shift)         | ->              |
| 6     | < <= > >= instanceof             | Relacionais                  | ->              |
| 7     | == !=                            | Igualdade                    | ->              |
| 8     | &                                | AND bitwise / booleano       | ->              |
| 9     | ^                                | XOR bitwise / booleano       | ->              |
| 10    | \|                               | OR bitwise / booleano        | ->              |
| 11    | &&                               | AND lógico (curto-circuito)  | ->              |
| 12    | \|                               | OR lógico (curto-circuito)   | ->              |
| 13    | ? :                              | Ternário                     | <-              |
| 14    | = += -= *= /= %= ...             | Atribuições                  | <-              |
