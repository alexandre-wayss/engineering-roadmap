## Anatomia de um metodo em java
```java
[modificadores] [tipoRetorno] nomeDoMetodo([parâmetros]) [throws Excecao] {
    // Corpo do método: instruções e lógica
    return valorRetornado;
}
```
## Parâmetros e argumentos de um método 
Parametro existem na declaração do método 
Argumentos residem no momento e no local em que aparecem

```java
// DECLARAÇÃO: 'taxa' e 'meses' são PARÂMETROS (variáveis locais / placeholders)
public double calcularJuros(double taxa, int meses) {
    return Math.pow(1 + taxa, meses);
}

// INVOCACAO: 0.05 e 12 são ARGUMENTOS (os valores concretos passados na execução)
double resultado = calcularJuros(0.05, 12);
```

### Boas práticas para parâmetros
- Padrão lowerCamelCase
- Priorizar intencão sobre tipo (sem notação Húngara) 
- Explicitar unidades de medida em tipos primitivos
- Nomear Boolean com perguntas ou verbos de ação
- Equilibrar contexto com redundância. Exemplo:
	Redundante: `clienteRepository.salvar(Cliente clienteASerSalvo)`  
    Limpo: `clienteRepository.salvar(Cliente cliente)`

## Clean code
### Quantidade ideal de parametros:  
- 0 parâmetros (Niládico): Ideal pela facilidade de leitura e teste.  
- 1 parâmetro (Monádico): Muito comum e intuitivo (`repository.buscarPorId(id)`).  
- 2 parâmetros (Diádico): Aceitável quando há relação natural (`ponto.deslocar(x, y)`).  
- 3 ou mais parâmetros (Triádico / Poliádico): Dificulta a legibilidade na chamada e induz a inversão acidental de argumentos do mesmo tipo. Agrupe-os em um DTO, Record ou Parameter Object.  
    
- Evitar "Flag Arguments": Passar um booleano que divide o método em dois fluxos com lógicas completamente distintas (`processarPagamento(pedido, true)`) costuma violar a responsabilidade única. Prefira dividir em dois métodos: `processarPagamentoAVista(pedido)` e `processarPagamentoParcelado(pedido)`.


## Varargs
É um recurso que permite criar métodos capazes de receberem uma quantidade variavel de argumentos, sem precisar definir antecipadamente quantos serão passados.
Util quando se quer um metodo que aceite zero, um ou varios argumentos do mesmo tipo.

```java
public static int somar(int... numeros) {

    int total = 0;

    for (int numero : numeros) {
        total += numero;
    }

    return total;
}
```

Para unir vararg com outros parametros convencionais, o vararg deve ser obrigatoriamente o ultimo parametro do metodo.

```java
public void exemplo(String nome, int... numeros) {
}
```
## Assinatura do método
É o critério exclusivo que o compilador usa para distinguir métodos dentro de uma mesma classe. Sendo a base para sobrecarga de métodos (overloading).

| Faz parte da assinatura        | NÃO faz parte da assinatura               |
| ------------------------------ | ----------------------------------------- |
| Nome do método                 | Modificadores de acesso (public, private) |
| Quantidade de parâmetros       | Modificadores não-acesso (static, final)  |
| Tipos dos parâmetros           | Tipo de retorno                           |
| Ordem dos tipos dos parâmetros | Nomes dados aos parâmetros                |
|                                | Cláusula throws                           |

### Sobrecarga de Métodos (Method Overloading)
Permite que múltiplos métodos compartilhem o **mesmo nome**, desde que possuam **assinaturas diferentes** (variação no número, tipo ou ordem dos parâmetros):

```java
// Método 1: cálculo com taxa padrão
public double calcularInvestimento(double valor, int meses) {
    return valor * Math.pow(1 + 0.01, meses);
}

// Método 2 (Sobrecarga): cálculo com taxa personalizada
public double calcularInvestimento(double valor, int meses, double taxa) {
    return valor * Math.pow(1 + taxa, meses);
}
```
> [!NOTE]
> Mudar apenas o tipo de retorno (ex: de `double` para `int`) sem alterar os parâmetros **NÃO** é sobrecarga e causa erro de compilação, pois o compilador não teria como saber qual método executar.

## Return vs void
- Usar return quando o método responder a uma pergunta ou executar um cálculo puro. (ex.: `calcularTotal()`, `obterPorId()`, `isValido()`).
- Use void quando o método representa uma ordem/comando ou produz um efeito externo no sistema (ex.: `salvar()`, `deletar()`, `atualizarCache()`, `desenharGrafico()`).

## Passagem por Valor (A Regra de Ouro do Java)
Em Java, **todos os argumentos são passados estritamente por valor (cópia)**. Não existe passagem por referência direta de variáveis.

### 1. Com tipos primitivos (cópia do valor literal):
O método recebe uma cópia do valor primitivo. Qualquer alteração interna **não afeta** a variável de fora:
```java
void incrementar(int x) {
    x = x + 1; // Altera apenas a cópia local do frame
}

int numero = 10;
incrementar(numero);
System.out.println(numero); // Continua sendo 10!
```

### 2. Com objetos e arrays (cópia do endereço de memória):
A variável que guarda um array ou objeto armazena uma **referência** (endereço). Ao passar para um método, o Java copia esse endereço:
- **Alterar o conteúdo interno** (`array[0] = 99`): afeta o objeto real compartilhado na memória.
- **Reatribuir a variável** (`array = new int[5]`): apenas redireciona a cópia local da referência; a variável de fora continua apontando para o objeto original.

```java
void alterarPrimeiroItem(int[] numeros) {
    numeros[0] = 99; // Altera o elemento dentro do array real na Heap
}

int[] valores = {1, 2, 3};
alterarPrimeiroItem(valores);
System.out.println(valores[0]); // Imprime 99!
```

## Modelo de Memória: Stack vs Heap
A JVM organiza a memória de execução do programa em duas regiões principais:

| Característica | Stack (Pilha) | Heap (Monte) |
| :--- | :--- | :--- |
| **O que armazena** | Stack Frames de métodos, variáveis locais e tipos primitivos | Instâncias reais de Objetos e Arrays |
| **Ciclo de vida** | Desalocação automática imediata ao encerrar o método (`LIFO`) | Gerenciada em segundo plano pelo Garbage Collector (GC) |
| **Velocidade** | Acesso ultrarrápido | Acesso ligeiramente mais lento (busca de ponteiros) |
| **Escopo** | Privada de cada Thread de execução | Compartilhada globalmente por toda a aplicação |
| **Erro de estouro** | `StackOverflowError` (ex: recursão infinita) | `OutOfMemoryError` (falta de memória RAM livre) |

- **Stack Frames:** Cada invocação de método empilha um novo bloco com seus parâmetros e variáveis locais. Quando o método retorna, esse bloco é destruído instantaneamente.
- **Garbage Collector:** Objeto na Heap que não possui mais nenhuma referência apontando para ele fica elegível para ser limpo automaticamente pelo coletor de lixo da JVM.