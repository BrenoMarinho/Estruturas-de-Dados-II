# Projeto ConectaUDF: minha rede social com grafos

**Estudante:** Breno Silva Marinho **Disciplina:** Estrutura de Dados II 

## 1. O desafio

Você faz parte da equipe que analisa a rede social fictícia **ConectaUDF**. Neste projeto individual, o centro da análise é a sua própria rede: **Breno**, que possui **6 conexões diretas**. Sua missão é representar as amizades em um grafo, realizar cálculos e usar Python para interpretar a estrutura da rede.

## 2. Conceitos essenciais

- **Vértice (ou nó):** representa um usuário.
- **Aresta:** representa uma amizade entre dois usuários.
- **Grau:** quantidade de conexões diretas de um usuário.
- **Caminho:** sequência de usuários em que cada par consecutivo está conectado.
- **Densidade:** proporção entre as amizades existentes e todas as amizades possíveis.

Neste projeto, a amizade é recíproca. Portanto, usamos um **grafo não direcionado**.

## 3. Conheça os usuários

| Código | Usuário |
| --- | --- |
| BS | Breno |
| A | Ana |
| B | Bruno |
| C | Carla |
| D | Diego |
| E | Elisa |
| F | Felipe |

As amizades são (14 no total):

1. Breno — Ana
2. Breno — Bruno
3. Breno — Carla
4. Breno — Diego
5. Breno — Elisa
6. Breno — Felipe
7. Ana — Bruno
8. Ana — Carla
9. Bruno — Carla
10. Bruno — Diego
11. Carla — Elisa
12. Diego — Elisa
13. Diego — Felipe
14. Elisa — Felipe

## 4. Desenho do grafo

<img width="1440" height="1043" alt="grafo_original" src="https://github.com/user-attachments/assets/7a963747-d642-467f-a197-4678d0002b87" />

## 5. Passo a passo: calcule o grau

Conte quantas linhas chegam a cada círculo. Registre o resultado.

| Usuário | Amigos diretos | Grau |
| --- | --- | --- |
| Breno | Ana, Bruno, Carla, Diego, Elisa e Felipe | 6 |
| Ana | Breno, Bruno e Carla | 3 |
| Bruno | Breno, Ana, Carla e Diego | 4 |
| Carla | Breno, Ana, Bruno e Elisa | 4 |
| Diego | Breno, Bruno, Elisa e Felipe | 4 |
| Elisa | Breno, Carla, Diego e Felipe | 4 |
| Felipe | Breno, Diego e Elisa | 3 |

**Pergunta 1:** quem tem mais conexões diretas?

**Resposta:** Breno, com 6 conexões diretas. Em seguida vêm Bruno, Carla, Diego e Elisa, com 4 conexões cada.

## 6. Passo a passo: calcule o número de amizades

Some todos os graus. Como cada amizade conecta dois usuários, cada aresta é contada duas vezes.

**Fórmula:** `Número de arestas = soma dos graus ÷ 2`

1. Soma dos graus: 6 + 3 + 4 + 4 + 4 + 4 + 3 = **28**
2. Divida por 2: 28 ÷ 2 = **14**
3. Quantas amizades existem no grafo? **14**

## 7. Passo a passo: calcule a densidade

A densidade compara as amizades existentes com o total de amizades possíveis.

Para um grafo simples não direcionado:

`D = 2 × E / (V × (V − 1))`

Em que:

- `D` = densidade;
- `E` = número de arestas;
- `V` = número de vértices.

Substitua os valores:

`D = 2 × 14 / (7 × (7 − 1)) = 28 / 42`

- Resultado decimal: **0,66667**
- Resultado percentual: **66,67 %**

**Interprete:** a rede tem poucas ou muitas das conexões possíveis?

A rede tem **muitas** das conexões possíveis: mais da metade das amizades que poderiam existir entre os 7 usuários já existe. Isso acontece porque o Breno está ligado a todos e os amigos dele também se conhecem bastante entre si.

## 8. Passo a passo: represente o grafo em Python

A lista de adjacência registra, para cada usuário, os nomes de seus amigos. Executável no Google Colab.

```python
rede = {
    "Breno": ["Ana", "Bruno", "Carla", "Diego", "Elisa", "Felipe"],
    "Ana": ["Breno", "Bruno", "Carla"],
    "Bruno": ["Breno", "Ana", "Carla", "Diego"],
    "Carla": ["Breno", "Ana", "Bruno", "Elisa"],
    "Diego": ["Breno", "Bruno", "Elisa", "Felipe"],
    "Elisa": ["Breno", "Carla", "Diego", "Felipe"],
    "Felipe": ["Breno", "Diego", "Elisa"]
}

# Quantidade de usuarios
n = len(rede)

# Calcule o grau de cada usuario
for usuario, amigos in rede.items():
    print(usuario, "tem", len(amigos), "conexoes")

# A soma dos graus conta cada amizade duas vezes
soma_graus = sum(len(amigos) for amigos in rede.values())
arestas = soma_graus // 2

print("Total de usuarios:", n)
print("Total de amizades:", arestas)

# Densidade do grafo
densidade = (2 * arestas) / (n * (n - 1))
print(f"Densidade: {densidade:.2%}")
```

**Saída esperada:** Breno com 6 conexões, Ana e Felipe com 3, os demais com 4; 7 usuários; 14 amizades; densidade de 66,67%.

- https://colab.research.google.com/drive/1zLRtVh89SH1p7Z-2qxac6F-U4Iqoesvz#scrollTo=cNg_pQ3HcOyW

### Entenda o código

1. `rede` guarda os usuários e suas listas de amigos.
2. `len(rede)` conta os usuários.
3. `len(amigos)` calcula o grau de cada usuário.
4. `sum(...)` soma os graus.
5. `// 2` divide a soma por dois para contar cada amizade uma única vez.
6. A fórmula final calcula a densidade.

### Opcional: desenhar o grafo com Python

```python
import networkx as nx
import matplotlib.pyplot as plt

G = nx.Graph()
for usuario, amigos in rede.items():
    for amigo in amigos:
        G.add_edge(usuario, amigo)

nx.draw(G, with_labels=True, node_color="lightblue", node_size=1800, font_size=10)
plt.show()
```

## 9. Passo a passo: encontre um caminho

Encontre um caminho de **Ana até Felipe**. Cada passagem por uma linha corresponde a uma aresta.

Exemplo de registro: `Ana → Breno → Felipe`

- **Quantas arestas há no caminho?** 2. Este é o caminho mais curto, pois Ana e Felipe não são amigos diretos e só têm o Breno como amigo em comum.
- **Você encontrou outro caminho? Qual?** Sim, um caminho mais longo, com 3 arestas: `Ana → Carla → Elisa → Felipe`. Outro exemplo: `Ana → Bruno → Diego → Felipe`.

## 10. Desafio individual: amplie a minha rede

**1. Novos usuários fictícios (4):** Gabriela, Heitor, Iago e Janaina.

**2. Novas amizades (7):**

- Ana — Gabriela
- Bruno — Gabriela
- Carla — Iago
- Felipe — Iago
- Felipe — Janaina
- Iago — Heitor
- Iago — Janaina

Observação: os novos usuários ainda não são amigos diretos do Breno. Isso é intencional, para permitir o exercício de recomendação.

**3. Lista de adjacência atualizada:**

```python
rede = {
    "Breno": ["Ana", "Bruno", "Carla", "Diego", "Elisa", "Felipe"],
    "Ana": ["Breno", "Bruno", "Carla", "Gabriela"],
    "Bruno": ["Breno", "Ana", "Carla", "Diego", "Gabriela"],
    "Carla": ["Breno", "Ana", "Bruno", "Elisa", "Iago"],
    "Diego": ["Breno", "Bruno", "Elisa", "Felipe"],
    "Elisa": ["Breno", "Carla", "Diego", "Felipe"],
    "Felipe": ["Breno", "Diego", "Elisa", "Iago", "Janaina"],
    "Gabriela": ["Ana", "Bruno"],
    "Heitor": ["Iago"],
    "Iago": ["Carla", "Felipe", "Heitor", "Janaina"],
    "Janaina": ["Felipe", "Iago"]
}
```

**4. Graus, arestas e densidade recalculados:**

| Usuário | Grau |
| --- | --- |
| Breno | 6 |
| Ana | 4 |
| Bruno | 5 |
| Carla | 5 |
| Diego | 4 |
| Elisa | 4 |
| Felipe | 5 |
| Gabriela | 2 |
| Heitor | 1 |
| Iago | 4 |
| Janaina | 2 |

- Soma dos graus: 6 + 4 + 5 + 5 + 4 + 4 + 5 + 2 + 1 + 4 + 2 = **42**
- Arestas: 42 ÷ 2 = **21**
- Densidade: `2 × 21 / (11 × 10) = 42 / 110 =` **0,38182 (38,18 %)**

**5. Comparação antes e depois:**

|  | Usuários | Arestas | Densidade |
| --- | --- | --- | --- |
| Antes | 7 | 14 | 66,67 % |
| Depois | 11 | 21 | 38,18 % |

A densidade caiu porque o número de usuários cresceu mais rápido do que o número de amizades. Com 11 usuários, existem 55 amizades possíveis, mas só 21 foram criadas. Os novos usuários (principalmente Heitor, com 1 conexão) ainda têm poucos amigos, o que é normal em uma rede em crescimento.

**Comparação dos graus antes e depois:**

| Usuário | Grau antes | Grau depois |
| --- | --- | --- |
| Breno | 6 | 6 |
| Ana | 3 | 4 |
| Bruno | 4 | 5 |
| Carla | 4 | 5 |
| Diego | 4 | 4 |
| Elisa | 4 | 4 |
| Felipe | 3 | 5 |
| Gabriela (novo) | — | 2 |
| Heitor (novo) | — | 1 |
| Iago (novo) | — | 4 |
| Janaina (nova) | — | 2 |

Ana, Bruno, Carla e Felipe ganharam conexões (Felipe ganhou 2). Breno, Diego e Elisa mantiveram o mesmo grau.

**6. Usuários com mais conexões:** **Breno**, com 6 conexões. Logo atrás estão Bruno, Carla e Felipe, com 5 conexões cada.

**7. Como a rede poderia recomendar uma nova amizade para o Breno?**

A rede pode usar **amigos em comum**. Veja os amigos em comum entre o Breno e quem ainda não é amigo dele:

| Possível amizade | Amigos em comum | Quantidade |
| --- | --- | --- |
| Gabriela | Ana e Bruno | 2 |
| Iago | Carla e Felipe | 2 |
| Janaina | Felipe | 1 |
| Heitor | nenhum | 0 |

Gabriela e Iago seriam as melhores sugestões para o Breno, pois cada um tem dois amigos em comum com ele, mas ainda não são amigos. Heitor não seria sugerido, pois não há nenhum amigo em comum.

**Código opcional para gerar recomendações:**

```python
usuario = "Breno"
amigos_dele = set(rede[usuario])

for outro in rede:
    if outro != usuario and outro not in amigos_dele:
        comuns = amigos_dele & set(rede[outro])
        print(outro, "->", len(comuns), "amigos em comum:", sorted(comuns))
```

## 11. Entrega

Entregue:

- **Desenho do grafo:** rede original (7 usuários) e rede ampliada (11 usuários).
- **Tabela com os graus:** seções 5 e 10.
- **Cálculos de arestas e densidade:**
  - Rede original: soma dos graus 28, 28 ÷ 2 = 14 arestas; densidade `2 × 14 / (7 × 6) = 66,67 %`.
  - Rede ampliada: soma dos graus 42, 42 ÷ 2 = 21 arestas; densidade `2 × 21 / (11 × 10) = 38,18 %`.
- **Código Python executável:**

```python
rede = {
    "Breno": ["Ana", "Bruno", "Carla", "Diego", "Elisa", "Felipe"],
    "Ana": ["Breno", "Bruno", "Carla", "Gabriela"],
    "Bruno": ["Breno", "Ana", "Carla", "Diego", "Gabriela"],
    "Carla": ["Breno", "Ana", "Bruno", "Elisa", "Iago"],
    "Diego": ["Breno", "Bruno", "Elisa", "Felipe"],
    "Elisa": ["Breno", "Carla", "Diego", "Felipe"],
    "Felipe": ["Breno", "Diego", "Elisa", "Iago", "Janaina"],
    "Gabriela": ["Ana", "Bruno"],
    "Heitor": ["Iago"],
    "Iago": ["Carla", "Felipe", "Heitor", "Janaina"],
    "Janaina": ["Felipe", "Iago"]
}

# Quantidade de usuarios
n = len(rede)

# Calcule o grau de cada usuario
for usuario, amigos in rede.items():
    print(usuario, "tem", len(amigos), "conexoes")

# A soma dos graus conta cada amizade duas vezes
soma_graus = sum(len(amigos) for amigos in rede.values())
arestas = soma_graus // 2

print("Total de usuarios:", n)
print("Total de amizades:", arestas)

# Densidade do grafo
densidade = (2 * arestas) / (n * (n - 1))
print(f"Densidade: {densidade:.2%}")
```

- https://colab.research.google.com/drive/1zLRtVh89SH1p7Z-2qxac6F-U4Iqoesvz#scrollTo=cNg_pQ3HcOyW

## 12. Pergunta de reflexão

**Duas pessoas ainda não são amigas, mas têm três amigos em comum. Como essa informação poderia ser usada para sugerir uma nova conexão? Quais cuidados de privacidade devem ser considerados ao analisar redes sociais?**

Sim, essa informação poderia ser usada para recomendar uma nova amizade, pois ter três amigos em comum indica que as duas pessoas possuem relações próximas dentro da rede social. Assim, a plataforma poderia sugerir que elas se conectassem, aumentando as possibilidades de interação.

Porém, é importante respeitar a privacidade dos usuários, utilizando apenas informações autorizadas, protegendo seus dados pessoais e permitindo que cada pessoa escolha se deseja aceitar ou não as sugestões de amizade. Além disso, as informações das conexões não devem ser compartilhadas sem consentimento.

## 13. Perguntas para discussão

**Quem é mais conectado? Isso significa que é o mais influente?**

Breno é o mais conectado, com grau 6. Porém, o grau conta apenas a quantidade de conexões diretas. A influência também depende de quem são esses amigos e de a pessoa ligar grupos diferentes. Na rede ampliada, por exemplo, Carla e Felipe são as pontes entre o grupo central e Iago, Heitor e Janaina.

**Como sugerir amizade usando amigos em comum?** Veja a seção 10 (item 7) e a seção 12.

**Que cuidados de privacidade são necessários?** Veja a seção 12.

**Quais outras métricas podem descrever uma rede?**

- **Distância média e diâmetro:** quantas arestas, em média e no máximo, separam dois usuários pelo caminho mais curto.
- **Coeficiente de agrupamento:** mede o quanto os amigos de uma pessoa também são amigos entre si.
- **Centralidade de intermediação:** mede quantos caminhos mais curtos passam por um usuário, ou seja, quem funciona como ponte.
- **Centralidade de proximidade:** mede o quão perto um usuário está de todos os outros.
- **Componentes conectados:** indicam se a rede está toda ligada ou dividida em grupos isolados.

## 14. Conclusão

A rede original de Breno tem 7 usuários e 14 amizades, o que dá densidade de 66,67 %: mais da metade das conexões possíveis existe. Breno é o usuário mais conectado, com 6 conexões diretas, ligado a todos os outros.

Ao ampliar a rede para 11 usuários e 21 amizades, a densidade caiu para 38,18 %. A queda não significa que a rede piorou: o número de conexões possíveis cresceu mais rápido (de 21 para 55) do que o número de amizades criadas, e os novos usuários ainda têm poucos amigos.

O grau de Ana, Bruno, Carla e Felipe aumentou, e Breno continua com o maior grau. A rede poderia sugerir a Breno as amizades com Gabriela e Iago, que têm 2 amigos em comum com ele. Por fim, a análise de redes sociais deve respeitar a privacidade: usar apenas dados autorizados e deixar cada pessoa decidir se aceita as sugestões.
