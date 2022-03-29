# O que vamos aprender ?
hoje vamos aprender o que são **Algoritimos de ordenação e algoritimos de busca** vamos implemanetar soluções interaveis e recursivas
assim como aplicaremos o "dividir e conquistar" ou até mesmo a "força bruta". Faremos uma análise de complexidade de cada um deles entendendo quando será a melhor ocasião para utilizá-los.

# sera capaz de;
- Implementar algorimos de busca cusca linear e busca binaria
- escrever algoritimo de ordenação, como por exemplo, ordenação por bolha , inserção, seleção com
- utilizar tecnicas de "força bruta" e "dividir para conquistar"
- Analisar a complexidade e escolher o algoritimo adequado para o problema

# Isso é importante por ;
No dia a dia como pessoa programadora, você será confrontada com diversos problemas. Seu papel será analisá-los e buscar uma solução eficiente. Se destacam aquelas pessoas que conseguem entender o problema e propor os melhores algoritmos para aquele caso. Por isso é muito comum em entrevistas de emprego, empresas cobrarem o conhecimento destes algoritmos. Não quer dizer que na sua rotina de trabalho irá utilizar aqueles algoritmos o tempo todo, mas o conhecimento técnico deles e as técnicas empregadas em suas soluções podem ser utilizadas em outras resoluções.
O exercício de analise de complexidade sobre estes algoritmos também é algo que deve ser destacado, pois é algo bastante útil de ser aplicado em outros tipos de algoritmos.

## coteudo
### Algoritmos de Ordenação
Algoritmo de ordenação ( sorting algorithms ) são uma categoria de algoritmos que buscam colocar elementos de uma sequência em uma determinada ordem definida. Esta ordem pode ser numérica, lexicográfica ou por qualquer outra característica. As razões para se ordenar uma sequência podem variar desde facilitar a visualização até facilitar uma busca.
Imagine uma coleção de músicas onde queremos exibi-las em ordem alfabética, ou ordenadas pelo número de vezes em que foram tocadas. Ou talvez uma lista telefônica ao qual precisamos buscar um nome, não seria mais fácil se estivesse ordenada em ordem alfabética? Lidando com arrays, matrizes e outras coleções, numéricas ou não, muitas vezes teremos de utilizar a ordenação.
Faremos a implementação e análise de alguns dos algoritmos existentes (os mais populares). Existem vários outros e basta uma busca por algoritmos de ordenação ( sorting algorithms ) para obter uma lista extensa de algoritmos deste estilo.

### Algoritmos de ordenação que usam força bruta

Como visto na aula anterior, a força bruta caracteriza-se por ser uma técnica que se testa todas as possibilidades existentes para resolver um problema.
Por exemplo, imagine que você tem um cadeado com 4 dígitos, cada um de 0-9. Você esqueceu sua combinação, mas não quer comprar outro cadeado. Como você não consegue se lembrar de nenhum dos dígitos, é necessário usar um método de força bruta para abrir a fechadura. Portanto, você define todos os números de volta para 0 e os tenta um por um: 0001 , 0002 , 0003 e assim por diante até que seja aberto. Na pior das hipóteses, seriam necessárias 10⁴ ou 10.000 tentativas para encontrar sua combinação.

### Selection Sort
A ordenação por seleção ( selection sort em inglês), divide o array em duas partes, uma já ordenada e outra de itens a serem ordenados. Em seguida, selecionaremos o menor elemento na lista não ordenada e o incluiremos na lista ordenada. Isto será feito continuamente até que nossa lista de elementos não ordenados se esgote, e logo teremos uma lista com os itens ordenados.
Como funciona o algoritmo?

```
# Vamos supor os números não ordenados
- ordenados =
- não ordenados = 3 6 1 7

# Buscamos entre os elementos não ordenados o menor elemento
- menor = 1

# Vamos adicioná-lo a lista de elementos ordenados
- ordenados = 1
- não ordenados = 6 3 7

# Agora repetimos o passo de busca
- menor = 3

# Assim teremos
- ordenados = 1 3
- não ordenados = 6 7

# Como ainda não esgotamos os números a serem ordenados repetiremos a busca
menor = 6

# Agora temos quase todos os elementos ordenados
- ordenados = 1 3 6
- não ordenados = 7

# Faremos a busca pelo menor elemento novamente (único)
- menor = 7

# Esgotamos as possibilidades e temos nossa lista ordenada
- ordenados = 1 3 6 7
```
Vamos ver um exemplo de implementação:

```
def selection_sort(array):
    # como um algoritmo de força bruta
    # percorre a estrutura exaustivamente
    for i in range(len(array)):
        minimum = i

        # itera sobre os elementos não ordenados
        for j in range(i + 1, len(array)):
            # seleciona o menor valor
            if array[j] < array[minimum]:
                minimum = j

        # após encontrar o menor valor
        # ao invés de criar um novo array (o que aumenta complexidade de espaço)
        # realizamos a substituição entre o menor elemento
        # e a posição i que corresponde ao primeiro elemento não ordenado
        # que consequentemente passará a ser o último ordenado
        array[minimum], array[i] = array[i], array[minimum]

    return array

print(selection_sort([100, 4, 6, 33, 56, 67]))
```
Analisando a complexidade deste algoritmo, vemos que independente de todos os elementos estarem ordenados (ou não), ou parcialmente ordenados, sempre teremos que percorrer o array completamente e também n - 1 elementos a cada iteração. Isto nos leva a uma complexidade O(n²) para todos os casos (pior, médio, melhor).
Como criamos apenas algumas variáveis de controle e não criamos um array auxiliar, nosso algoritmo tem uma complexidade de espaço constante, ou seja, não muda seja para 10, 1000 ou 10.000 elementos.

#### Insertion Sort
A ordenação por inserção ( insertion sort ), tem esse nome por inserir um elemento de cada vez em sua posição correta. Fazendo uma analogia a um jogo de cartas, onde sua "mão" esteja ordenada, é como se a cada nova carta recebida fossemos movendo ela até achar a posição correta e a inserimos ali, e faremos isso sucessivamente até que não tenha novas cartas e por consequência, nossa mão esteja ordenada. É mais eficiente que a ordenação por seleção e também considerada mais simples.
Como funciona o algoritmo?

```
# Vamos supor os números não ordenados
- coleção = 3 2 1 7

# vamos pegar o primeiro elemento e movê-lo até sua posição
- elemento = 3

# como não há elementos a esquerda de 3 não o movemos
- coleção = 3 2 1 7

# agora vamos pegar o segundo elemento
- elemento = 2

# vamos movê-lo à esquerda, enquanto seu valor for menor
# que o elemento a sua esquerda
             ⤺
- coleção = 2 3 1 7

# próximo elemento da coleção
- elemento = 1

# vamos inseri-lo na  posição correta,
# movendo para a esquerda enquanto seu valor for menor
# que o elemento a esquerda
             ⤺ ⤺
- coleção = 1 2 3 7

# por fim verificamos o último elemento
- elemento = 7

# não há elementos menores a esquerda
# e a coleção está ordenada
- coleção = 1 2 3 7
```

Vamos ver um exemplo de implementação:

```
def insertion_sort(array):
    # itera sobre cada valor do array
    for i in range(len(array)):
        current_value = array[i]
        current_position = i
        # enquanto o valor da posição for menor que os elementos a sua esquerda
        while (
            current_position > 0
            and array[current_position - 1] > current_value
        ):
            # move as posições para a direita
            array[current_position] = array[current_position - 1]
            current_position = current_position - 1
        # colocamos o elemento em sua nova posição
        array[current_position] = current_value
    return array

print(insertion_sort([100, 4, 6, 33, 56, 67]))
```
Como precisamos percorrer cada um dos elementos, e depois percorrer comparando os elementos à esquerda do mesmo, em um pior caso, onde o array esteja inversamente ordenado, teremos uma complexidade de O(n²) . Isto se repete também em média, para arrays parcialmente ordenados. Porém se inicialmente o array estiver ordenado, este algoritmo terá complexidade O(n) , pois só fara a iteração de todos os elementos, e não precisará ficar movendo os elementos.
Assim como na ordenação por seleção, como criamos apenas algumas variáveis de controle e não criamos um array auxiliar, nosso algoritmo tem uma complexidade de espaço constante, ou seja, não muda, seja para 10, 1000 ou 10.000 elementos.

#### Algoritmos de ordenação que usam soluções iterativas

Soluções iterativas consistem na realização de uma ou mais operações repetidas vezes, por meios de comandos de repetição. As ordenações demonstradas acima (seleção, inserção), são consideradas iterativas, pois estamos realizando operações de comparação e troca de elementos repetidas vezes, por meios de comandos de repetição ( for ).
💡 Toda solução iterativa pode ser reescrita de forma recursiva.

### Bubble Sort
ambém conhecido como ordenação por bolha ( bubble sort ), têm esse nome, pois a movimentação dos elementos lembra o movimento das bolhas em um refrigerante. São realizadas múltiplas iterações sobre a coleção, sempre comparando o valor ao item adjacente e realizando a troca daqueles que estão fora de ordem. A cada iteração o próximo maior valor é colocado em sua posição correta, ou seja, cada item se desloca como uma bolha para a posição a qual pertence.
Como funciona o algoritmo?

```
# Vamos supor os números não ordenados
- coleção = 7 5 1 2

# vamos realizar a primeira iteração.
# Comparamos os dois primeiros elementos (índices 0 e 1)
- 7 > 5 ?

# como o 7 é maior 5, faremos a troca de posição

           ⤺
- coleção = 5 7 1 2
           ⤻
# Agora comparamos os elementos dos índices 1 e 2

- 7 > 1?

# Novamente faremos a troca
             ⤺
- coleção = 5 1 7 2
             ⤻

# Depois, comparamos os índices 2 e 3

- 7 > 2

# Mais uma vez faremos a troca
               ⤺
- coleção = 5 1 2 7
               ⤻

# Como houveram trocas, vamos iterar mais uma vez nossa coleção
# O elemento 7, como uma bolha, foi subindo até sua posição
- coleção = 5 1 2 7

# Comparamos os primeiros elementos e faremos a troca
           ⤺
- coleção = 1 5 2 7
           ⤻

# Em seguida comparamos os próximos elementos e faremos a troca novamente

             ⤺
- coleção = 1 2 5 7
             ⤻
# Como houveram trocas precisamos iterar novamente a nossa coleção
- coleção = 1 2 5 7

# Porém desta vez não há trocas e nossa coleção está ordenada
```

```
def bubble_sort(array):
    # variável utilizado na iteração
    # para marcar se houve ou não trocas naquela iteração
    # Quando falsa, indica que o array está ordenado
    has_swapped = True

    # armazena o número de iterações para evitar
    # a iteração sobre índices já ordenados
    num_of_iterations = 0

    # Enquanto ainda não está ordenado (ocorreram trocas na iteração)
    while has_swapped:
        has_swapped = False

        # percorra o array até o ultimo índice não ordenado
        for i in range(len(array) - num_of_iterations - 1):
            # caso a posição corrente seja maior que a posterior
            if array[i] > array[i + 1]:
                # realiza a troca entre as posições
                array[i], array[i + 1] = array[i + 1], array[i]
                # marca que tivemos trocas nesta iteração
                has_swapped = True
        num_of_iterations += 1

    return array


print(bubble_sort([100, 4, 6, 33, 56, 67]))
```
### Algoritmos de ordenação que usam dividir e conquistar
Algoritmos que utilizam da técnica de dividir e conquistar , consistem em dividir um problema grande em partes menores, encontrar soluções para as partes menores, e então combinar as soluções obtidas em uma solução global. Esta técnica produz um algoritmo eficiente, caso a divisão e conquista sejam eficientes.
💡 Os algoritmos abaixo foram implementados de forma recursiva, mas lembre-se, toda solução recursiva pode ser reescrita de forma iterativa.

### Merge sort

