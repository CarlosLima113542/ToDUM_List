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

---

## 4. Modelação das Tarefas – Classe `Task`

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

## 5. Gestão de Identificadores – Classe `IDGenerator`

A classe `IDGenerator` garante que cada tarefa recebe um identificador único e sequencial. Sempre que uma nova tarefa é criada, o método `next()` incrementa automaticamente o ID.

Quando tarefas são carregadas a partir de um ficheiro, o gerador ajusta‑se ao maior identificador encontrado, evitando duplicações e assegurando consistência.

---

## 6. Funcionalidades Principais

### 6.1 Listagem de Tarefas

Apresenta todas as tarefas existentes, ordenadas por identificador.  
Se não existirem tarefas registadas, o utilizador é informado.

### 6.2 Adição de Tarefas

Permite criar uma nova tarefa, solicitando:

- Descrição  
- Categoria  
- Prioridade  
- Notas  

A data de criação é registada automaticamente.

### 6.3 Atualização do Estado

Permite alterar o estado de uma tarefa.  
Quando esta é marcada como *concluída*, a data de conclusão é automaticamente registada.

### 6.4 Edição de Campos

O utilizador pode editar individualmente:

- Descrição  
- Prioridade  
- Categoria  
- Notas  

É possível realizar várias alterações seguidas sem regressar ao menu principal.

### 6.5 Remoção de Tarefas

Remove definitivamente uma tarefa após validação do respetivo identificador.

---

## 7. Filtragem de Tarefas

O sistema permite filtrar tarefas com base em:

- Estado  
- Prioridade  
- Categoria  
- Combinação simultânea dos três critérios  

Se não forem encontradas tarefas que correspondam ao filtro aplicado, o utilizador é devidamente informado.

---

## 8. Persistência de Dados

### 8.1 Guardar Tarefas

As tarefas podem ser guardadas num ficheiro JSON.  
Cada objeto `Task` é convertido num dicionário através de `vars()`, garantindo uma serialização correta.

### 8.2 Carregar Tarefas

Permite recuperar tarefas previamente guardadas.  
O programa inclui tratamento de exceções para lidar com:

- Ficheiros inexistentes  
- Ficheiros vazios  
- Ficheiros corrompidos  

As tarefas carregadas são reconstruídas como objetos `Task`.

---

## 9. Validação de Dados e Tratamento de Erros

Ao longo do programa, são aplicados mecanismos de validação que evitam:

- Introdução de valores inválidos  
- Seleção de identificadores inexistentes  
- Escolha de opções fora do intervalo permitido  

Sempre que ocorre um erro, o utilizador recebe mensagens claras e informativas, garantindo uma utilização segura e intuitiva.

---

## 10. Conclusão

O projeto **ToDUM** cumpre os objetivos definidos, demonstrando a aplicação prática de conceitos essenciais de programação em Python, como orientação a objetos, modularização, validação e persistência de dados.

---


