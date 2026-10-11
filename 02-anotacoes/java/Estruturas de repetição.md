## FOR
quando sabe previamente o número de repetições.
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

```

## WHILE
quando o loop depende de uma condição lógica e o número de repetições é desconhecido; testa a condição antes de executar.
```java
int contador = 0;
while (contador < 5) {
    System.out.println(contador);
    contador++;
}


```

## DO-WHILE
semelhante ao `while`, mas garante que o bloco execute ao menos uma vez, pois avalia a condição no final.
```java
int numero = 0;
do {
    System.out.println(numero);
    numero++;
} while (numero < 5);

```

## FOR EACH
Simplifica a iteração direta sobre arrays e coleções sem precisar de um índice manual.

```java
String[] frutas = {"Maçã", "Banana", "Uva"};
for (String fruta : frutas) {
    System.out.println(fruta);
}

- **Somente leitura:** Não permite alterar os elementos diretamente no array ou coleção.
- **Sem índice:** Não disponibiliza a posição numérica (`i`). Se for necessário saber o índice do elemento (ex: exibir `"Item 1"`, `"Item 2"`), utilize o `for` tradicional.

## Loops Infinitos
Ocorrem quando a condição de parada nunca se torna falsa:

- **Erro acidental:** Esquecer de atualizar a variável de controle (ex: esquecer o `contador++` no `while`), travando a execução e consumindo CPU indefinidamente.
- **Padrão intencional (`while (true)`):** Muito utilizado em menus de console, servidores e daemons que devem rodar continuamente até uma ação explícita de saída:
  ```java
  while (true) {
      System.out.println("Digite 0 para sair:");
      int opcao = scanner.nextInt();
      if (opcao == 0) {
          System.out.println("Saindo...");
          break; // Interrompe o loop infinito
      }
  }
  ```

## BREAK e CONTINUE e ROTULOS
- break: Interrompe e encerra o laço por completo. O controle sai do bloco do loop imediatamente.  
    
- continue: Pula o restante da iteração atual e avança direto para a próxima repetição (ou para o teste de condição).

- Por padrão, `break` e `continue` atuam apenas no laço mais interno. Para controlar um laço externo a partir de um interno, usa-se um rótulo (label):
```java
externo:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (i == 2 && j == 2) {
            break externo; 
        }
        System.out.println("i: " + i + ", j: " + j);
    }
} // o break sai para aqui

```