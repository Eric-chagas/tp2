# Qualidade de Código 

### Característica 1: Simplicidade

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| A simplicidade em um projeto de software refere-se à ausência de complexidade desnecessária. Um código simples é fácil de entender, manter e modificar. Ele possui uma estrutura clara e direta, evitando abstrações complicadas e lógica desnecessariamente intrincada |  - **Long Method (Método Longo)**: Métodos extensos podem ser complexos e difíceis de compreender. A simplificação envolve a extração de métodos menores para reduzir o tamanho. <br> - **Complex Conditional Statements (Declarações Condicionais Complexas)**: Simplificar condicionais complexos pode envolver a decomposição dessas estruturas em métodos menores ou a aplicação de técnicas como Decompose Conditional | **Extrair Método:** Identificar trechos de código complexos e transformá-los em métodos menores, cada um realizando uma tarefa específica. Isso reduz a complexidade e facilita a compreensão |


### Característica 2: Boas Interfaces

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
|Boas interfaces em um projeto de software referem-se à forma como os diferentes módulos, classes e componentes se comunicam. Interfaces claras e bem definidas facilitam a interação entre partes do sistema, promovendo a reutilização e a compreensão | **Inappropriate Intimacy (Intimidade Inadequada):** Classes que se comunicam em excesso podem indicar uma falta de clareza nas interfaces. Refatorações como Move Method ou Move Field podem ser aplicadas para melhorar a situação.| **Mover Método / Mover Campo:** Para reduzir a intimidade inadequada entre duas classes, movendo métodos ou campos para uma classe mais apropriada. Isso ajuda a definir interfaces mais claras.|


### Característica 3: Modularidade (Baixo Acoplamento e Alta Coesão)

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
|Modularidade refere-se à capacidade de dividir o sistema em módulos independentes. Baixo acoplamento significa que esses módulos são pouco dependentes entre si, enquanto alta coesão significa que os elementos dentro de um módulo estão fortemente relacionados|**Feature Envy (Inveja de Recursos):** Métodos que frequentemente acessam dados de outras classes podem indicar acoplamento inadequado. A refatoração pode envolver o movimento desses métodos para as classes apropriadas.|**Mover Método:** Para resolver o problema de Feature Envy, movendo métodos para a classe correta e reduzindo o acoplamento entre classes|


### Característica 4: Ausência de Duplicidades

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| A ausência de duplicidades refere-se à eliminação de código redundante. Cada parte do código deve ter uma única representação, evitando repetições que aumentam a dificuldade de manutenção | **Duplicated Code (Código Duplicado)**: Duplicação de código é um mau cheiro significativo. Refatorações como Extract Method ou Extract Class podem ser aplicadas para eliminar duplicações | **Extrair Método / Extrair Classe**: Para eliminar duplicações de código, identificando trechos semelhantes e criando métodos ou classes compartilhadas |


### Característica 5: Boa Documentação

| Descrição da Característica | Relação com Maus-Cheiros de Código de Martin Fowler | Operação de Refatoração |
| -- | -- | -- |
| Boa documentação no código ajuda na compreensão e manutenção. Comentários claros, nomes de variáveis significativos e documentação de código facilitam o entendimento do propósito e funcionamento de cada componente | **Comments (Comentários em Excesso)**: Código excessivamente comentado pode indicar falta de clareza. Refatorações podem envolver a melhoria da legibilidade do código, tornando os comentários menos necessários | **Renomear Variáveis / Extrair Método**: Para melhorar a clareza do código, escolhendo nomes significativos para variáveis e métodos. Isso reduz a necessidade de comentários explicativos |
