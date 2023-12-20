# Qualidade de Código 

### Característica 1: Simplicidade

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| A simplicidade em um projeto de software refere-se à ausência de complexidade desnecessária. Um código simples é fácil de entender, manter e modificar. Ele possui uma estrutura clara e direta, evitando abstrações complicadas e lógica desnecessariamente intrincada |  - **Long Method (Método Longo)**: Métodos extensos podem ser complexos e difíceis de compreender. A simplificação envolve a extração de métodos menores para reduzir o tamanho. <br> - **Complex Conditional Statements (Declarações Condicionais Complexas)**: Simplificar condicionais complexos pode envolver a decomposição dessas estruturas em métodos menores ou a aplicação de técnicas como Decompose Conditional | **Extrair Método:** Identificar trechos de código complexos e transformá-los em métodos menores, cada um realizando uma tarefa específica. Isso reduz a complexidade e facilita a compreensão |

## Exemplo de implementação em código

```java

// Código sem simplificação: Utiliza um algoritmo simples (e custoso) para verificar se o numero eh primo

public class Classe1 {

    public static void main(String[] args) {
        int valor = 10;

        if (valor > 1) {
            for (int i = 2; i < valor; i++) {  
                if (valor % i == 0) { 
                    System.out.println("Não é primo...");
                    return;
                }
            }

            System.out.println("É primo!");
        } else {
            System.out.println("Não é primo...");
        }
    }
}

// Código simplificado: Utiliza o mesmo algoritmo para verificar se o numero eh primo, porem em um metodo dedicado
// que apenas eh chamado no metodo principal

public class Classe1 {

    public static void main(String[] args) {
        int valor = 10;

        if (valor > 1) {
            if (ehPrimo(valor)) {
                System.out.println("É primo!");
            } else {
                System.out.println("Não é primo...");
            }
        } else {
            System.out.println("Não é primo...");
        }
    }

    private static boolean ehPrimo(int valor) {
        for (int i = 2; i * i < valor; i++) {
            if (valor % i == 0) {
                return false;
            }
        }

        return true;
    }
} 

```


### Característica 2: Boas Interfaces

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
|Boas interfaces em um projeto de software referem-se à forma como os diferentes módulos, classes e componentes se comunicam. Interfaces claras e bem definidas facilitam a interação entre partes do sistema, promovendo a reutilização e a compreensão | **Inappropriate Intimacy (Intimidade Inadequada):** Classes que se comunicam em excesso podem indicar uma falta de clareza nas interfaces. Refatorações como Move Method ou Move Field podem ser aplicadas para melhorar a situação.| **Mover Método / Mover Campo:** Para reduzir a intimidade inadequada entre duas classes, movendo métodos ou campos para uma classe mais apropriada. Isso ajuda a definir interfaces mais claras.|

## Exemplo de implementação em código

```java

// Código com intimidade inadequada: Classe2 depende de imprimir() da Classe1, o que pode levar a 
// ambiguidade nos resultados da impressao e acesso desnecessario de classes externas a metodos da Classe1

public class Classe1 {

    private int valor;

    public Classe1(int valor) {
        this.valor = valor;
    }

    public int getValor() {
        return valor;
    }

    public void setValor(int valor) {
        this.valor = valor;
    }

    public void imprimir() {
        System.out.println("O valor é " + valor);
    }
}

public class Classe2 {

    public static void main(String[] args) {
        Classe1 classe1 = new Classe1(10);

        classe1.imprimir();

        classe1.setValor(20);

        classe1.imprimir();
    }
}

// Código refatorado: Com o metodo imprimirClasse1 em um metodo dedicado em uma classe separada, Classe2 agora
// nao acessa mais diretamente metodos internos de Classe1 diretamente

public class Classe1 {

    private int valor;

    public Classe1(int valor) {
        this.valor = valor;
    }

    public int getValor() {
        return valor;
    }

    public void setValor(int valor) {
        this.valor = valor;
    }
}

public class ImprimirClasse1 {

    public static void imprimir(Classe1 classe1) {
        System.out.println("O valor é " + classe1.getValor());
    }
}

public class Classe2 {

    public static void main(String[] args) {
        Classe1 classe1 = new Classe1(10);

        ImprimirClasse1.imprimir(classe1);

        classe1.setValor(20);

        ImprimirClasse1.imprimir(classe1);
    }
}

```


### Característica 3: Modularidade (Baixo Acoplamento e Alta Coesão)

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
|Modularidade refere-se à capacidade de dividir o sistema em módulos independentes. Baixo acoplamento significa que esses módulos são pouco dependentes entre si, enquanto alta coesão significa que os elementos dentro de um módulo estão fortemente relacionados|**Feature Envy (Inveja de Recursos):** Métodos que frequentemente acessam dados de outras classes podem indicar acoplamento inadequado. A refatoração pode envolver o movimento desses métodos para as classes apropriadas.|**Mover Método:** Para resolver o problema de Feature Envy, movendo métodos para a classe correta e reduzindo o acoplamento entre classes|

## Exemplo de implementação em código


```java

// Codigo que define uma classe Calculadora com quatro métodos.
// Todos esses quatro métodos acessam os campos valor1 e valor2 da classe Calculadora e dependem da
// implementacao da classe como um todo

public class Calculadora {

    private int valor1;
    private int valor2;

    public Calculadora(int valor1, int valor2) {
        this.valor1 = valor1;
        this.valor2 = valor2;
    }

    public int somar() {
        return valor1 + valor2;
    }

    public int subtrair() {
        return valor1 - valor2;
    }

    public int multiplicar() {
        return valor1 * valor2;
    }

    public int dividir() {
        return valor1 / valor2;
    }
}

public class Recibo {

    public static void main(String[] args) {
        Calculadora calculadora = new Calculadora(10, 20);

        System.out.println(calculadora.somar());
        System.out.println(calculadora.subtrair());
        System.out.println(calculadora.multiplicar());
        System.out.println(calculadora.dividir());
    }
}

// Código refatorado: Com os quatro metodos de operacoes na classe dedicada e separada Operacoes, agora
// outras classes podem utilizar os metodos sem conhecer o funcionamento interno de Calculadora por completo
// Alem de manter a coesao utilizando getters ao inves de acesso direto a valor1 e valor2 

public class Calculadora {

    private int valor1;
    private int valor2;

    public Calculadora(int valor1, int valor2) {
        this.valor1 = valor1;
        this.valor2 = valor2;
    }
    
    public int getValor1() {
        return valor1;
    }

    public int getValor2() {
        return valor1;
    }
}

public class Operacoes {

    public static int somar(int valor1, int valor2) {
        return valor1 + valor2;
    }

    public static int subtrair(int valor1, int valor2) {
        return valor1 - valor2;
    }

    public static int multiplicar(int valor1, int valor2) {
        return valor1 * valor2;
    }

    public static int dividir(int valor1, int valor2) {
        return valor1 / valor2;
    }
}

public class Recibo {
    private Calculadora calculadora = new Calculadora(10, 20);

    public static void imprimeRecibo() {
        System.out.println(Operacoes.somar(calculadora.getValor1(), calculadora.getValor2()));
        System.out.println(Operacoes.subtrair(calculadora.getValor1(), calculadora.getValor2()));
        System.out.println(Operacoes.multiplicar(calculadora.getValor1(), calculadora.getValor2()));
        System.out.println(Operacoes.dividir(calculadora.getValor1(), calculadora.getValor2()));
    }
}

```

### Característica 4: Ausência de Duplicidades

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| A ausência de duplicidades refere-se à eliminação de código redundante. Cada parte do código deve ter uma única representação, evitando repetições que aumentam a dificuldade de manutenção | **Duplicated Code (Código Duplicado)**: Duplicação de código é um mau cheiro significativo. Refatorações como Extract Method ou Extract Class podem ser aplicadas para eliminar duplicações | **Extrair Método / Extrair Classe**: Para eliminar duplicações de código, identificando trechos semelhantes e criando métodos ou classes compartilhadas |

## Exemplo de implementação em código


```java

// Codigo com duplicidade de codigo: Ambos os metodos hello1 e hello2 realizam uma funcao muito parecida, que consiste em
// imprimir "Hello world!" no std output. Eh um exemplo simples em que fica evidente que esse codigo pode ser refatorado
// de modo a implementar a reutilizacao e reduzir a duplicidade

public class Hello {
    public void hello1() {
        System.out.println("Olá, mundo!");
        System.out.println("Olá, mundo!");
        System.out.println("Olá, mundo!");
    }

    public void hello2() {
        System.out.println("Olá, mundo!");
    }
}

// Código refatorado: Agora tanto hello1 quanto hello2 apenas reutilizam o metodo dedicado printHello() e hello1 apenas
// o chama em um loop de 3 repeticoes, que eh mais um exemplo de reducao da duplicidade de codigo que existia anteriormente

public class Hello {
    public void hello1() {
        for(int i = 0; i < 3; i++) {
            printHello();
        }
    }

    public void hello2() {
        printHello();
    }

    private static void printHello() {
        System.out.println("Olá, mundo!");
    }
}

```

### Característica 5: Boa Documentação

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| Boa documentação no código ajuda na compreensão e manutenção. Comentários claros, nomes de variáveis significativos e documentação de código facilitam o entendimento do propósito e funcionamento de cada componente | **Comments (Comentários em Excesso)**: Código excessivamente comentado pode indicar falta de clareza. Refatorações podem envolver a melhoria da legibilidade do código, tornando os comentários menos necessários | **Renomear Variáveis / Extrair Método**: Para melhorar a clareza do código, escolhendo nomes significativos para variáveis e métodos. Isso reduz a necessidade de comentários explicativos |

## Exemplo de implementação em código


```java

// Codigo com documentacao excessiva: Os nomes das variaveis e dos metodos nao sao nada intuitivos e 
// consequentemente demandam uma quantidade alta de comentarios descritivos

public class ClasseXYZXPTOn23 {
    // Metodo lp (de loop) que itera 3 vezes e printa a iteracao incrementada com 1
    public static void lp() {
        // Declara uma variável inteira chamada `i` e a inicializa com o valor 0.
        int i = 0;

        // Define a condição de parada do loop.
        // O loop continuará a ser executado enquanto o valor de `i` for menor que 3.
        while (i < 3) {

            // Atualiza o valor da variável `i` em 1 após cada iteração do loop.
            i++;

            // Imprime a mensagem "Iteração " + (i + 1) no console.
            System.out.println("Iteração " + (i + 1));
        }
    }
}

// Código refatorado: Com nomes mais auto descritivos tanto para as variaveis quanto para a classe e metodo
// nao existe a necessidade da quantidade elevada de comentarios no meio do codigo

public class ClasseIteradora {

    public static void itera3Vezes(String[] args) {
        // Declara e inicializa uma variável `iteracao` com o valor 0.
        int iteracao = 0;

        // Itera 3 vezes, imprimindo a mensagem "Iteração " + iteração incrementada com 1 no console.
        for (iteracao = 0; iteracao < 3; iteracao++) {
            System.out.println("Iteração " + iteração + 1);
        }
    }
}

```