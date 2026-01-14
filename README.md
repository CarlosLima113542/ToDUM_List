# Relatório do Projeto – ToDUM (ToDo List)

## Identificação
**Alunos:**
- 113542 – Carlos Maia Barbosa Lima  
- 114059 – João Martim Guimarães Costa e Silva  

---

# 1. Descrição Geral da Aplicação

O projeto **ToDUM** consiste no desenvolvimento de uma aplicação de linha de comandos em Python destinada à gestão simples e organizada de tarefas.

O principal objetivo da aplicação é permitir ao utilizador criar, consultar, editar, filtrar e remover tarefas, assegurando simultaneamente a persistência dos dados entre diferentes execuções através de ficheiros no formato JSON.

A aplicação pretende consolidar conhecimentos fundamentais da linguagem Python, nomeadamente:

- Programação orientada a objetos
- Utilização de ciclos e estruturas condicionais
- Validação de dados e tratamento de exceções
- Organização modular do código

---

# 2. Como Executar e Utilizar (Manual do Utilizador)

## 2.1 Requisitos

- Python 3 instalado no sistema  
- Acesso a um terminal  
- Não são necessárias bibliotecas externas adicionais  

## 2.2 Instalação

Para executar a aplicação:

1. Colocar todos os ficheiros `.py` do projeto na mesma pasta  
2. Não é necessária qualquer instalação adicional, uma vez que são utilizadas apenas bibliotecas padrão do Python  

## 2.3 Execução

1. Abrir o terminal na diretoria do projeto  
2. Executar o comando:

```bash
  python main.py
```
---

## 2.4 Utilização

O utilizador interage com a aplicação através de um **menu textual**, escolhendo a opção desejada introduzindo o número correspondente.


A aplicação permite:

- Adicionar novas tarefas

- Listar tarefas existentes

- Atualizar o estado das tarefas

- Editar campos específicos

- Remover tarefas

- Filtrar tarefas segundo vários critérios

- Guardar e carregar tarefas


---


# 3. Implementação das Funcionalidades e Estrutura do Código


## 3.1 Funcionalidades Obrigatórias Implementadas

O desenvolvimento focou-se em cumprir integralmente os requisitos do enunciado, assegurando que a aplicação fosse não só funcional, mas também fiável:

### Listar tarefas
Exibe todos os registos de forma organizada. Optámos por uma visualização tabular no terminal para que o utilizador consiga identificar rapidamente o estado de cada projeto.


### Adicionar nova tarefa
Permite a criação de novos registos. O sistema assume o trabalho de gerar IDs e datas de criação, para que o utilizador se foque apenas na descrição e prioridade.


### Atualizar estado
Essencial para o fluxo de trabalho. Quando uma tarefa passa a "concluída", o código regista o momento exato, garantindo que o histórico de produtividade seja fidedigno.


### Editar campos
Fornece flexibilidade ao utilizador para corrigir descrições ou mudar categorias e prioridades, sem ter de apagar e criar a tarefa de novo.


### Remover tarefa
Uma ação destrutiva que exige o ID correto. Implementámos esta função com cautela para garantir que apenas o registo pretendido seja eliminado.


### Filtrar tarefas
Permite isolar o que é urgente ou o que já terminou. A decisão de filtrar por estado, prioridade ou categoria ajuda a manter o foco em listas longas.


### Persistência de Dados 
Escolhemos o formato JSON para guardar as tarefas. É uma solução prática que garante que, ao reabrir o programa, tudo esteja exatamente como foi deixado.


### Menu Interativo
O programa corre num ciclo contínuo e amigável, guiando o utilizador pelas opções até que este decida encerrar a sessão.


---


## 3.2 Estrutura do Código e Classes

Para manter o código limpo e organizado, utilizámos uma abordagem orientada a objetos que separa a informação da lógica de controlo.


### Classe `Task`

Esta classe funciona como o molde de cada tarefa. Em vez de lidar com dados soltos, agrupamos tudo (ID, descrição, datas, prioridade, categoria e notas) num objeto único. Para tornar a experiência no terminal mais agradável, personalizámos como a tarefa se apresenta visualmente, evitando textos técnicos e confusos.


### Classe `IDGenerator`

Criámos esta classe com o intuito de resolver o problema dos identificadores duplicados. Ela é inteligente o suficiente para verificar quais os IDs já existentes no ficheiro e continuar a sequência corretamente, mesmo após o programa ser reiniciado. A função `next()`, dentro desta classe, cada vez que é utilizada, permite que `uid` aumente numa unidade, para que não haja tarefas com ids iguais, sendo mais fácil aceder a qualquer tarefa.


---


## 3.3 Lógica das Funções e Decisões de Implementação


A organização em funções permitiu-nos criar uma aplicação modular onde cada peça tem o seu papel específico:


- **`menu()` e `input_user()`:** O nosso foco aqui foi a clareza. Usamos cores para destacar o que é importante e validamos cada tecla premida pelo utilizador. Se ele digitar algo errado, o programa explica o erro em vez de simplesmente fechar.

- **`filtrar()`**: O objetivo da função é modularizar as funções detinadas à filtração mais específica das características das tarefas. Se, nessa alteração, a escolha do utilizador for incorreta, nomeadamente na filtração dos parâmentros da prioridade e do estado, o programa faz com que o utilizador entenda o porquê desse mesmo erro. Dentro desta função, são utilizadas outras quatro funções: **`filtrar_estado()`**, **`filtrar_prioridade()`** e **`filtrar_cat()`**. Por último, existe também uma função que filtra os três parâmetros em simultâneo: **`filtrar_todos()`**.


- **`to_do()`:** É o centro de comando. Decidimos centralizar aqui toda a navegação do menu, o que torna muito mais fácil adicionar novas funcionalidades no futuro sem desorganizar o resto do código.


- **`adiciona_tarefa()` e `atualiza_estado()`:** Estas funções gerem a parte "automática" do programa. Decidimos que o utilizador não deve ter a preocupação de inserir datas ou IDs manualmente; o código faz isso por ele, minimizando erros humanos.


- **`remover_tarefa()`**: É a função que permite o utilizador remover tarefas anteriormente criadas. Enquanto não existirem tarefas criadas, é impossível remover qualquer tarefa.


- **`verify_id()`:** Atua como uma camada de segurança. Antes de qualquer edição ou remoção, esta função confirma se o ID existe, evitando falhas de memória ou comportamentos inesperados do programa.


- **`editar_campos()`:** Em vez de forçar o utilizador a reescrever toda a tarefa, criámos uma lógica que permite escolher apenas o que se quer mudar. É uma decisão que respeita o tempo do utilizador e torna a edição muito mais fluida.
  

- **`atualiza_prioridade()`**: Sempre que o utilizador pretender alterar a prioridade de uma tarefa anteriomente definida, por qualquer que seja o motivo, é-lhe permitida essa alteração através da função **`atualiza_prioridade()`**. Esta função está inserida na função **`editar_campos()`**. Para uma melhor leitura do código, achamos mais prático separar a edição das características em pequenas funções como esta.
  
 
- - **`verificar_escolha()`**: Esta função determina se a escolha da característica a alterar em **`editar_campos()`** é válida. Por exemplo, se o utilizador tentar escrever uma característica inexistente, esta função faz com que ele entenda o seu erro. Esta função também se insere na nossa decisão de separar o código em funções menores, permitindo a modularidade.


- **`guardar()` e `carregar()`:** Estas funções tratam da "memória" do ToDUM. Decidimos que o carregamento deve ser automático no início e o salvamento deve ser simples e quando o utilizador pretender, para que a persistência seja algo natural e transparente para quem usa a aplicação.
---

## 3.4 Considerações sobre o Design

- **Ciclos e Condições:** São usados para manter o programa interativo e validar entradas do utilizador.

- **Modularidade:** Funções separadas para cada tarefa tornam o código mais organizado e fácil de seguir.

- **Interface:** Cores e mensagens claras melhoram significativamente a experiência do utilizador.

- **Fiabilidade:** A persistência em JSON mantém os dados entre sessões e torna o sistema confiável.

---

# 4. Funcionalidades Extra Implementadas

Para além dos requisitos base, foram incluídas as seguintes melhorias sugeridas pelo enunciado:

## 4.1 Utilização de Cores e Emojis no Terminal

A aplicação utiliza códigos ANSI, como por exemplo `\033[92m` (verde), para apresentar mensagens no terminal com diferentes cores. Para que sejam apresentados emojis no terminal, como por exemplo o de uma cruz vermelha, a fim de mostrar qualquer erro, são utilizados códigos do tipo `\u274C`. Esta abordagem permite distinguir visualmente menus, mensagens informativas, confirmações de sucesso e mensagens de erro, contribuindo para uma leitura mais clara e uma interação mais intuitiva com o utilizador.

## 4.2 Validação Robusta das Entradas

Foram implementados mecanismos de validação rigorosa das entradas do utilizador, recorrendo à combinação de ciclos `while` com estruturas condicionais e tratamento de exceções (`try/except`). Este método garante que apenas valores válidos são aceites, prevenindo erros de execução e assegurando a estabilidade da aplicação. Permite também que o utilizador verifique a sua escolha antes de ações destrutivas, tais como sair do programa ou remover tarefas. Com a validação robusta de entradas o utilizador também pode decidir se pretende continuar a alterar as características das tarefas na função `editar_campos()`.
Tome-se como exemplo a função `verify_id()`: 

```
def verify_id(tasks):
    if not tasks:
        print ("Nenhuma tarefa foi encontrada.")
        return None
    else:
        while True:
            try:
                id1 = int(input('Escreva o id da tarefa: '))
                if id1 in tasks:
                    return id1
                else:
                    print(f'{red}Erro \u274C{reset} : Esse ID não existe na lista.')
            except ValueError:
                print(f'{red}Erro \u274C{reset}: Por favor, introduza apenas números inteiros.')
```

## 4.3 Função `filtrar_todos()`

A função `filtrar_todos()` permite filtrar tarefas através da combinação simultânea de três critérios: estado, prioridade e categoria. Esta funcionalidade possibilita uma pesquisa mais precisa e detalhada, aumentando a flexibilidade do sistema de filtragem em relação aos filtros simples exigidos.


---

# 5. Considerações Finais

O projeto ToDUM (ToDo List) cumpre de forma eficaz os objetivos definidos no contexto académico universitário, demonstrando a aplicação prática e consistente dos principais conceitos abordados ao longo da unidade curricular.

Ao longo do desenvolvimento do programa, foi possível aplicar conhecimentos fundamentais da linguagem Python, nomeadamente a utilização de programação orientada a objetos, através da criação de classes para modelação de dados, bem como a implementação de funções modulares, que contribuem para a clareza, organização e manutenção do código.

A utilização de ciclos e estruturas condicionais revelou-se essencial para garantir uma interação contínua com o utilizador, permitir a validação rigorosa das entradas e assegurar a correta execução das diferentes funcionalidades do sistema. Adicionalmente, a implementação de tratamento de exceções contribui para a robustez da aplicação, prevenindo falhas inesperadas durante a execução.

A persistência de dados a partir de ficheiros no formato JSON permite guardar e recuperar informação de forma eficiente, tornando a aplicação funcional e reutilizável entre diferentes execuções.

Em suma, o projeto apresenta uma solução funcional, coerente e extensível para a gestão de tarefas em ambiente de consola.
