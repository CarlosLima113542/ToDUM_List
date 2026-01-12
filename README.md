# ToDUM – Gestor de Tarefas em Python

---

## Nome e número dos alunos
113542 – Carlos Maia Barbosa Lima  
114059 – João Martim Guimarães Costa e Silva

---

## Como correr o programa

1. Verifique se tem o Python 3 instalado no seu sistema.  
2. Coloque todos os ficheiros `.py` do projeto na mesma pasta.  
3. Abra o terminal nessa diretoria.  
4. Execute o comando:

   ```
   python main.py
   ```

5. Após a execução, o menu interativo será apresentado no ecrã, permitindo iniciar a utilização da aplicação.

---

## 1. Enquadramento e Objetivos

O projeto **ToDUM** consiste no desenvolvimento de uma aplicação de linha de comandos em Python destinada à gestão simples e organizada de tarefas. Este trabalho enquadra‑se no contexto académico e tem como principais objetivos:

- Consolidar conhecimentos fundamentais da linguagem Python;  
- Aplicar princípios de programação orientada a objetos;  
- Desenvolver uma solução modular, clara e facilmente reutilizável;  
- Implementar mecanismos de validação e tratamento de exceções;  
- Assegurar a persistência de dados através de ficheiros.

A aplicação permite ao utilizador criar, consultar, editar, filtrar e remover tarefas, além de guardar e carregar informação em formato JSON, garantindo continuidade entre sessões.

---

## 2. Estrutura Geral do Programa

O programa foi organizado de forma a separar responsabilidades e facilitar a manutenção. A estrutura base integra:

- Um **menu interativo**, que centraliza a comunicação com o utilizador;  
- A classe **`Task`**, responsável pela representação de cada tarefa;  
- A classe **`IDGenerator`**, que assegura a atribuição de identificadores únicos;  
- Funções dedicadas à **gestão de tarefas** (criação, edição, remoção e listagem);  
- Funções de **filtragem**, permitindo consultas específicas;  
- Funções de **persistência de dados**, encarregues de guardar e carregar ficheiros.

---

## 3. Menu e Interação com o Utilizador

O menu principal apresenta nove opções, permitindo ao utilizador escolher a operação pretendida:

1. Listar tarefas  
2. Adicionar tarefa  
3. Atualizar estado  
4. Editar campos  
5. Remover tarefa  
6. Filtrar tarefas  
7. Guardar tarefas  
8. Carregar tarefas  
9. Sair  

A função `input_user()` valida as entradas, garantindo que apenas valores inteiros dentro do intervalo permitido são aceites, prevenindo erros e interrupções inesperadas.

Adicionalmente, o programa recorre à utilização de **cores no terminal**, através de códigos ANSI, com o objetivo de melhorar a legibilidade e a experiência do utilizador. Diferentes cores são utilizadas para distinguir menus, mensagens informativas, confirmações de sucesso e mensagens de erro, permitindo uma identificação visual imediata do tipo de informação apresentada.

Esta abordagem contribui para uma interação mais intuitiva e organizada, facilitando a utilização da aplicação em ambiente de consola. A utilização de cores, embora não seja essencial para a lógica do programa, demonstra preocupação com a usabilidade e com a clareza da comunicação com o utilizador, reforçando a qualidade global da aplicação.

---

## 4. Utilização de Ciclos e Estruturas Condicionais

O programa **ToDUM** recorre de forma extensiva a **ciclos** e **estruturas condicionais**, fundamentais para garantir o correto funcionamento da aplicação, a interação contínua com o utilizador e a validação de dados.

### 4.1 Ciclos (`while` e `for`)

#### Ciclo `while`

O ciclo `while` é utilizado principalmente para:

- Manter o programa em execução até o utilizador optar por sair;
- Repetir pedidos de entrada sempre que o utilizador introduz dados inválidos;
- Permitir múltiplas operações consecutivas sem reiniciar o programa.

Exemplos de utilização incluem:

- O ciclo principal da função `to_do()`, que mantém o menu ativo até o utilizador escolher a opção de saída;
- A validação de opções no menu e nos filtros, garantindo que apenas valores válidos são aceites;
- A função `editar_campos()`, que permite ao utilizador realizar várias alterações consecutivas à mesma tarefa.

Este tipo de ciclo é essencial para assegurar uma interação contínua e controlada com o utilizador.

#### Ciclo `for`

O ciclo `for` é utilizado sempre que é necessário percorrer coleções de dados, nomeadamente o dicionário que armazena as tarefas.

É utilizado, por exemplo, para:

- Listar todas as tarefas existentes;
- Aplicar filtros por estado, prioridade ou categoria;
- Guardar e carregar tarefas a partir de ficheiros JSON.

A utilização do ciclo `for` permite percorrer todas as tarefas de forma eficiente e organizada.

---

### 4.2 Estruturas Condicionais (`if`, `elif`, `else`)

As estruturas condicionais desempenham um papel central na lógica do programa, permitindo a tomada de decisões com base nas escolhas do utilizador ou no estado das tarefas.

São utilizadas, entre outros contextos, para:

- Executar diferentes funcionalidades consoante a opção escolhida no menu;
- Verificar se existem tarefas antes de executar operações sobre elas;
- Atualizar automaticamente a data de conclusão quando uma tarefa é marcada como concluída;
- Apresentar mensagens informativas ou de erro conforme a situação.

A estrutura `if / elif / else` permite que o programa reaja de forma adequada a cada situação, garantindo robustez e prevenindo erros de execução.

---

### 4.3 Validação de Dados com Ciclos e Condições

A combinação de ciclos com estruturas condicionais é utilizada para validar todas as entradas do utilizador. Sempre que um valor inválido é introduzido, o programa solicita novamente a entrada correta, evitando falhas ou comportamentos inesperados.

Este mecanismo é aplicado, por exemplo, na validação de:

- Opções do menu;
- Estados das tarefas;
- Prioridades;
- Identificadores de tarefas.

Esta abordagem contribui para a fiabilidade e estabilidade da aplicação.

---

### 4.4 Importância na Estrutura do Programa

O uso adequado de ciclos e condições permite que o programa:

- Seja interativo e dinâmico;
- Evite encerramentos inesperados;
- Garanta coerência nos dados;
- Proporcione uma melhor experiência ao utilizador.

Desta forma, estas estruturas constituem elementos essenciais na implementação do projeto **ToDUM**, demonstrando a correta aplicação dos conceitos fundamentais de programação abordados na unidade curricular.

---

## 5. Modelação das Tarefas – Classe `Task`

A classe `Task` representa cada tarefa individual e inclui os seguintes atributos:

- `estado`: estado atual da tarefa (*por fazer*, *em progresso* ou *concluída*);  
- `desc`: descrição da tarefa;  
- `data_cr`: data e hora de criação;  
- `data_cl`: data e hora de conclusão;  
- `prioridade`: prioridade atribuída (*baixa*, *média* ou *alta*);  
- `notas`: observações adicionais;  
- `categoria`: categoria associada.

O método `__repr__()` foi implementado para apresentar a tarefa de forma clara e organizada no terminal, facilitando a leitura.

---

## 6. Gestão de Identificadores – Classe `IDGenerator`

A classe `IDGenerator` garante que cada tarefa recebe um identificador único e sequencial. Sempre que uma nova tarefa é criada, o método `next()` incrementa automaticamente o ID.

Quando tarefas são carregadas a partir de um ficheiro, o gerador ajusta‑se ao maior identificador encontrado, evitando duplicações e assegurando consistência.

---

## 7. Funcionalidades Principais

### 7.1 Listagem de Tarefas

Apresenta todas as tarefas existentes, ordenadas por identificador.  
Se não existirem tarefas registadas, o utilizador é informado.

### 7.2 Adição de Tarefas

Permite criar uma nova tarefa, solicitando:

- Descrição  
- Categoria  
- Prioridade  
- Notas  

A data de criação é registada automaticamente.

### 7.3 Atualização do Estado

Permite alterar o estado de uma tarefa.  
Quando esta é marcada como *concluída*, a data de conclusão é automaticamente registada.

### 7.4 Edição de Campos

O utilizador pode editar individualmente:

- Descrição  
- Prioridade  
- Categoria  
- Notas  

É possível realizar várias alterações seguidas sem regressar ao menu principal.

### 7.5 Remoção de Tarefas

Remove definitivamente uma tarefa após validação do respetivo identificador.

---

## 8. Filtragem de Tarefas

O sistema permite filtrar tarefas com base em:

- Estado  
- Prioridade  
- Categoria  
- Combinação simultânea dos três critérios  

Se não forem encontradas tarefas que correspondam ao filtro aplicado, o utilizador é devidamente informado.

---

## 9. Persistência de Dados

### 9.1 Guardar Tarefas

As tarefas podem ser guardadas num ficheiro JSON.  
Cada objeto `Task` é convertido num dicionário através de `vars()`, garantindo uma serialização correta.

### 9.2 Carregar Tarefas

Permite recuperar tarefas previamente guardadas.  
O programa inclui tratamento de exceções para lidar com:

- Ficheiros inexistentes  
- Ficheiros vazios  
- Ficheiros corrompidos  

As tarefas carregadas são reconstruídas como objetos `Task`.

---

## 10. Validação de Dados e Tratamento de Erros

Ao longo do programa, são aplicados mecanismos de validação que evitam:

- Introdução de valores inválidos  
- Seleção de identificadores inexistentes  
- Escolha de opções fora do intervalo permitido  

Sempre que ocorre um erro, o utilizador recebe mensagens claras e informativas, garantindo uma utilização segura e intuitiva.

---

## 11. Conclusão

O projeto **ToDUM – Gestor de Tarefas em Python** cumpre de forma eficaz os objetivos definidos no contexto académico universitário, demonstrando a aplicação prática e consistente dos principais conceitos abordados ao longo da unidade curricular.

Ao longo do desenvolvimento do programa, foi possível aplicar conhecimentos fundamentais da linguagem Python, nomeadamente a utilização de **programação orientada a objetos**, através da criação de classes para modelação de dados, bem como a implementação de **funções modulares**, que contribuem para a clareza, organização e manutenção do código.

A utilização de **ciclos e estruturas condicionais** revelou-se essencial para garantir uma interação contínua com o utilizador, permitir a validação rigorosa das entradas e assegurar a correta execução das diferentes funcionalidades do sistema. Adicionalmente, a implementação de **tratamento de exceções** contribui para a robustez da aplicação, prevenindo falhas inesperadas durante a execução.

A persistência de dados através de ficheiros no formato **JSON** permite guardar e recuperar informação de forma eficiente, tornando a aplicação funcional e reutilizável entre diferentes execuções.

Em suma, o projeto apresenta uma solução funcional, coerente e extensível para a gestão de tarefas em ambiente de consola. Constitui uma base sólida para futuras melhorias, como a introdução de novos critérios de organização, otimização da interface com o utilizador ou desenvolvimento de uma interface gráfica, reforçando assim o seu valor enquanto trabalho académico e enquanto aplicação prática.

---


