# 🧩 Jogo Didático: HeapSort

> **Aprenda fazendo:** Um jogo interativo de terminal para dominar o algoritmo HeapSort na prática.

Projeto desenvolvido para a disciplina de **Estruturas de Dados II** do curso de **Ciência da Computação**.

---

## 🎯 Sobre o Projeto

O aprendizado de algoritmos complexos costuma ser apenas passivo e visual. Este projeto inverte essa dinâmica: aqui, **você toma as decisões**.

Inspirado no modelo acadêmico *Sortia 2.0*, desenvolvemos uma versão em Python que exibe visualmente a árvore binária e transfere a responsabilidade da ordenação para o jogador. O estudante não apenas assiste, mas interage, corrige e compreende a relação direta entre um vetor plano e uma estrutura de árvore hierárquica.

## ⚙️ Como Funciona

O jogo guia o estudante por duas etapas práticas:

### 1. Construção da Max-Heap

O sistema gera um vetor (aleatório ou digitado pelo usuário) e exibe sua estrutura lógica. A missão é analisar a árvore de baixo para cima e indicar as trocas necessárias para garantir a regra fundamental:

> **Regra da Max-Heap:** Todo nó pai deve ser **maior ou igual** aos seus filhos.
> *Em um vetor, para o índice `i`: Filho esquerdo = `2i + 1` | Filho direito = `2i + 2*`

### 2. Ordenação (HeapSort)

Com a estrutura da Max-Heap pronta, o maior valor estará sempre no topo (raiz). O ciclo de ordenação começa:

1. Troque a raiz com o último elemento da região não ordenada.
2. A região ativa da *heap* diminui visualmente.
3. Realize novas trocas para restaurar a regra da Max-Heap na região ativa.
4. Repita o processo até o vetor estar 100% ordenado.

---

## 🕹️ Dinâmica e Pontuação

Você interage digitando os índices que deseja trocar (ex: `1 4`). O sistema avalia sua escolha em tempo real e calcula seu desempenho:

| Ação | O que acontece | Impacto no Placar |
| --- | --- | --- |
| ✅ **Acerto** | A troca é validada, o vetor é atualizado e o jogo avança. | **+ 10 pontos** |
| ❌ **Erro** | O sistema explica por que a troca não restaura a *heap*. | **- 2 pontos** |
| 💡 **Dica** | Digitando `dica`, o sistema indica o próximo passo ideal. | **- 1 ponto** |

*Nota: A pontuação final reflete sua precisão e nunca será menor que zero.*

---

## 🚀 Como Executar

Desenvolvido em Python puro (apenas as bibliotecas nativas `random` e `dataclasses`), o projeto foi encapsulado em um *Jupyter Notebook* para facilitar o uso sem a necessidade de configurações complexas.

**Via Google Colab (Recomendado)**

1. Baixe o arquivo `Jogo_Heapsort-Sortia.ipynb`.
2. Acesse o [Google Colab](https://colab.research.google.com/) e faça o *upload* do arquivo.
3. Execute as células sequencialmente e jogue diretamente pela saída do console.

**Localmente**
Abra o arquivo `.ipynb` em sua IDE preferida (como VS Code ou JupyterLab), execute as células e interaja pelo terminal integrado.

---

## 📦 Estrutura de Arquivos

* **`Jogo_Heapsort-Sortia.ipynb`:** Motor do jogo. Contém a lógica de validação, renderização visual da árvore por níveis, sistema de dicas e interface via console.
* **`Guia de Atividade Prática do Estudante.pdf`:** Documentação oficial com o diagnóstico pedagógico, propostas e mapeamento dos conceitos de estruturas de dados.
* **`README.md`:** Apresentação do projeto.

---

## 👤 Desenvolvido por

**Breno Silva Marinho**
*18/09/2026*
