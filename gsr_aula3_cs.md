---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image-right
image: /img/mona-bernhardsen-1s9OyG6YkfI-unsplash.jpg
title: Conceitos de Segurança da Informação
exportFilename: gsr_aula3_cs
author: José Roberto Bezerra
description: Gerência e Segurança de Redes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem 

- Conhecer o conceito de cifra simétrica
- Conhecer as técnicas clássicas relacionadas a CS

---

# Agenda 

- Modelo
- Técnicas de substituição
- Técnicas de transposição
- Máquinas de rotor

---
layout: section
---

# Cifra simétrica
Modelo

---
layout: image
image: /img/modelo_sc.png
backgroundSize: contain
---

# Cifra simétrica
Elementos

- Texto claro (mensagem ou dados)
- Algoritmo de encriptação/decriptação
    - Realiza substituições e transformações para tornar a mensagem ilegível
- Chave secreta
    - Entrada para o algoritmo que modifica a mensagem original
- Texto cifrado
    - Mensagem embaralhada produzida pelo algoritmo

---

# Requisitos Uso Seguro
Primeiro

> Um oponente deverá ser incapaz de decifrar o texto
cifrado ou descobrir a chave, mesmo que possua
diversos textos cifrados com seus respectivos textos
claros

---

# Requisitos Uso Seguro
Segundo

> Emissor e Receptor precisam ter obtido a chave
secreta de forma segura. Se um oponente descobrir
a chave e o algoritmo a comunicação está
comprometida

---

# Requisitos Uso Seguro
Observação

> O sigilo do algoritmo de encriptação/decriptação
não é determinante para a segurança

---
layout: image
image: /img/modelo_sc2.png
backgroundSize: contain
---

---

# Tipos de Ataques Criptoanalíticos

| Tipo de Ataque | Conhecido pelo Criptoanalista | Objetivo | Dificuldade |
|----------------|------------------------------|----------|-------------|
| **Ciphertext-Only Attack** | Apenas o texto cifrado | Recuperar a chave ou texto claro | Alta |
| **Known-Plaintext Attack** | Pares de texto claro e texto cifrado correspondente | Determinar a chave de cifragem | Média |
| **Chosen-Plaintext Attack** | Pode escolher textos claros e obter seus textos cifrados | Descobrir a chave usada para cifrar | Baixa-Média |
| **Chosen-Ciphertext Attack** | Pode escolher textos cifrados e obter seus textos claros | Determinar a chave de decifragem | Baixa-Média |
| **Adaptive Chosen-Plaintext** | Pode adaptar escolhas baseado em resultados anteriores | Obter informações sobre a chave eficientemente | Baixa |
| **Related-Key Attack** | Conhece cifras com chaves relacionadas | Explorar relações matemáticas entre chaves | Variável |
| **Side-Channel Attack** | Informações físicas (tempo, consumo de energia) | Extrair a chave através de vazamentos | Dependente da implementação |
| **Brute-Force Attack** | Algoritmo de cifra (às vezes texto cifrado) | Testar todas as chaves possíveis | Muito Alta |
| **Dictionary Attack** | Texto cifrado e dicionário de entradas prováveis | Quebrar cifras com conjunto limitado de entradas | Variável |
| **Man-in-the-Middle** | Pode interceptar e modificar comunicação | Obter chaves ou informações trocadas | Média |

---

# Ciphertext-Only Attack
- **Cenário mais comum em interceptações passivas**
- Criptoanalista possui apenas as mensagens cifradas
- **Exemplo**: Análise de tráfego de rede criptografado

---

# Known-Plaintext Attack
- **Situação comum em protocolos estruturados**
- Criptoanalista conhece alguns pares texto claro ↔ texto cifrado
- **Exemplo**: Ataque a cifras que usam cabeçalhos padrão

---

# Chosen-Plaintext Attack
- **Cenário de ataque muito poderoso**
- Atacante pode escolher textos arbitrários para cifrar
- **Exemplo**: Ataque a sistemas onde o atacante tem acesso temporário

---

# Chosen-Ciphertext Attack
- **Ataque similar ao chosen-plaintext, mas na decifragem**
- Atacante pode decifrar textos cifrados de sua escolha
- **Exemplo**: Ataque a protocolos de autenticação

---

# Adaptive Chosen-Plaintext
- **Versão mais sofisticada do chosen-plaintext**
- Escolhas são adaptadas baseadas nos resultados anteriores
- **Exemplo**: Ataques diferenciais e lineares

---

# Related-Key Attack
- **Explora relações matemáticas entre chaves**
- Criptoanalista conhece cifras com chaves relacionadas
- **Exemplo**: Ataques a esquemas de derivação de chaves

---

# Side-Channel Attack
- **Explora implementações físicas, não a teoria matemática**
- Baseia-se em vazamentos de informação durante o processamento
- **Exemplos**: Análise de tempo, consumo de energia, emissões eletromagnéticas

---

# 💪 Brute-Force Attack
- **Ataque por força bruta**
- Testa exaustivamente todas as chaves possíveis
- **Eficácia**: Dependente do tamanho da chave

---

# 📚 Dictionary Attack
- **Utiliza um dicionário de entradas prováveis**
- Eficaz quando o texto claro vem de um conjunto limitado
- **Exemplo**: Ataque a senhas comuns

---

# 👥 Man-in-the-Middle
- **Ataque ativo à comunicação**
- Atacante se posiciona entre duas partes legítimas
- **Objetivo**: Interceptar e possivelmente modificar comunicação

---

# Classificação por Complexidade

| Complexidade | Tipos de Ataque |
|--------------|-----------------|
| **Baixa** | Adaptive Chosen-Plaintext, Side-Channel |
| **Média** | Known-Plaintext, Chosen-Plaintext, Chosen-Ciphertext, Man-in-the-Middle |
| **Alta** | Ciphertext-Only, Brute-Force |
| **Variável** | Related-Key, Dictionary |

---

# Encriptação Computacionalmente Segura

1. Custo para quebrar a cifra ultrapassa o valor da informação encriptada
2. Tempo exigido para quebrar a cifra supera o tempo de vida útil da informação

---

# Classificação

- Tipo
    - Substituição ou Transposição
- Quantidade de chaves
    - Simétrica ou assimétrica
- Modo de processamento
    - Bloco ou Fluxo

---

# Ataque de Força Bruta

- Metade das chaves precisa ser experimentada
- Texto claro em idioma conhecido facilita a quebra da chave
- Arquivos numéricos e/ou compactados dificultam a quebra da chave

---
layout: quote
---

# Cifra de César

> Uma das primeiras técnicas de criptografia que se tem conhecimento. Consiste em deslocar um alfabeto uma quantidade fixa de caracteres.

---
layout: image-right
image: https://www.researchgate.net/profile/Izanete-Souza/publication/366839658/figure/fig2/AS:11431281110995061@1672835218554/Figura-2-Representacao-visual-da-Cifra-de-Cesar.png
backgroundSize: contain
---

# Cifra de César

---
layout: image-right
image: /img/cifra_cesar2.png
backgroundSize: contain
---

# Cifra de César

---
layout: image-right
image: /img/criptoanalise.png
backgroundSize: contain
---

# Criptoanálise
Cifra de César

---

# Criptoanálise
Cifra de César

- Algoritmos conhecidos
- Chave fraca
- Mensagem em texto claro identificável

---
layout: image-right
image: /img/zip.png
backgroundSize: contain
---

# Criptoanálise
Texto compactado

- Zip de um arquivo de texto claro
- Chave de 168 bits 

---
layout: quote
---

# Cifras Monoalfabéticas

> A cifra de César respeita a sequência do alfabeto cifrado criando 25 possibilidades de chave. As cifras monoalfabéticas trazem um aprimoramento substituindo cada letra por QUALQUER outra letra

$a \rightarrow Q\\$
$b \rightarrow W\\$
$c \rightarrow E\\$
$d \rightarrow R\\$

---

# Cifras Monoalfabéticas

- Chaves de cifras de substituição monoalfabéticas possuem $25!$ possibilidades (permutação)

$$
\begin{aligned}
&S = \{ a, b, c\}\\
&\underbrace{abc, acb, bac, bca, cab, cba}_{3!}\\
\end{aligned}
$$

---

# Cifras Monoalfabéticas

- Aparenta segurança comparada a Cifra de César
- Mesmo com pequena quantidade de texto, a cifra pode ser quebrada com estratégias de propriedades estatísticas de idiomas/texto

---
layout: image
image: /img/texto_cifrado.png 
backgroundSize: contain
---

# Exemplo de Texto Cifrado

---
image: /img/stats.png
layout: image-right
backgroundSize: contain
---

# Frequência Relativa

- Considerando que o texto é em Inglês
- Extrair a frequência relativa do texto cifrado
- Comparar com a frequência do idioma

---

# Frequência Relativa

- É provável que P e Z correspondam a 'e' e 't'
- É provável S, U, O, M e H correspondam ao conjunto {a, h, i, n, o, r, s}
- A, B, G, Y, I, J devem pertencer ao conjunto {b, j, k, q, v, x, z}

---

# Frequência Relativa

- Busca pelo digrama mais frequente em inglês: *th*
    - Corresponde ao ZW
- Busca pelo trigrama mais frequente: *the*
    - Corresponde ao ZWP
- A sequência ZWSZ na primeira linha corresponde a 'th?t'
    Fazendo uma tentativa de atribuição a *that*, teríamos S = 'a'

---
layout: image
image: /img/quatro_letras.png
backgroundSize: contain
---

# Frequência Relativa
A partir de 4 letras

---
layout: image
image: /img/texto_decifrado.png
backgroundSize: contain
---

# Frequência Relativa
Texto Decifrado

---

# Frequência Relativa
Digramas mais frequentes (pt-br)

- DE - (Artigo "de")
- ES - (Sufixo de plural, "os", "as" -> "es" em muitas palavras)
- EN - (Presente em muitas palavras como "então", "mente")
- TE - (Sufixo verbal "-te", "mente")
- DO - (Artigo contraído "do")
- DA - (Artigo contraído "da")
- OS - (Artigo "os")
- AS - (Artigo "as")
- EM - (Preposição "em")

---

# Frequência Relativa
Trigramas mais frequentes (pt-br)

- QUE - (Conjunção e pronome extremamente comum)
- ENT - (Presente em "entre", "então", "mente", "entidade")
- ADE - (Final de palavras como "idade", "dade", "ade")
- MEN - (Principalmente do sufixo "-mente")
- DES - (Prefixos "des-", "dis-")
- PAR - ("para", "parte", "par")
- TRA - ("tra", "trás", "trabalho")
- ÇÃO - (Sufixo nominal extremamente comum)
- COM - (Preposição "com")
- EST - ("estar", "este", "está")

---

# Frequência Relativa
Ordem aproximada das letras mais frequentes (pt-br)

A, E, O, S, R, I, D, N, M, T, C, U, L, P, V, G, F, B, H, Q, J, Z, X, Y, K, W.

---

# Frequência Relativa
Palavras curtas comuns (pt-br)

- **1 letra**: A (artigo), E (conjunção), O (artigo)
- **2 letras**: DE, DO, DA, EM, OS, AS, SE, AO, ÀS, UM, UMA, É, É.
- **3 letras**: QUE, COM, PARA, POR, SEM, UMA, NAS, DOS, DAS, ENT, TEM, SUA, SER.

---
layout: quote
---

# John the Ripper

> Ferramentas como o *John the Ripper* (com seu modo --substring) ou o *Criptool* possuem algoritmos que calculam estatísticas de n-gramas (digramas, trigramas, tetragramas) e usam tentativa e erro otimizado para encontrar a chave de substituição que maximiza a "pontuação" do texto decifrado, ou seja, que o torna mais parecido com um texto legível em português ou outro idioma.

[Openwall](https://www.openwall.com/john/)

---

# Cifras de Substituição

- A frequência do alfabeto original se reflete no alfabeto da cifra, facilitando sua quebra
- Uma melhoria da CS consiste em utilizar vários alfabetos de cifra (Cifras Polialfabéticas)
- Outra possível melhoria seria o uso de homófonos
    - Atribuir vários símbolos diferentes em rodízio para mesma letra
    - Cifra *Playfair*
    - Cifra de *Hill*

---
layout: image-right
image: /img/vigenere.png
backgroundSize: contain
---

# Cifras Polialfabéticas

- Utilizam um conjunto de regras monoalfabéticas simultaneamente
- Uma chave determina a regra específica
- Cifra de *Vigenère*
    - Utiliza 26 cifras de César
- É necessário utilizar uma chave tão grande quanto a mensagem para tornar a cifra segura (repete-se uma palavra-chave)

---
layout: image-right
image: /img/vigenere.png
backgroundSize: contain
---

# Cifra de *Vigenère*
Fragilidades

- As informações de frequência do texto são ocultados, mas não são totalmente perdidas
- É possível determinar o tamanho da palavra chave buscando padrões de repetição no texto

---
layout: image-right
image: /img/otp.png
backgroundSize: contain
---

# One Time Pad

- Chave do mesmo tamanho da mensagem
- Chave descartada após o uso
- Uso de XOR entre o texto claro e a chave
- Sistema inquebrável
    - Produz uma saída com nenhuma relação estatística com a entrada

---

# One Time Pad
Fragilidades

- Sistema inquebrável, porém pouco prático
- A largura de banda exigida para as chaves é similar aos dados
- Problema de distribuição de chaves

---
layout: section
---

# Cifras de Transposição

---
layout: image-right
image: /img/railfence.png
backgroundSize: contain
---

# Cifras Transposição

- Técnicas que envolvem a permutação das letras do texto claro
- *Rail fence*
    Exemplo de texto de claro: *Meet after the toga party*

---
layout: image-right
image: /img/railfence2.png
backgroundSize: contain
---

# *Rail Fence*

---

# Cifras Transposição

- Criptoanálise explora as CT através das estatísticas de frequência aplicadas as cifras alfabéticas
- Melhorias são obtidas aplicando múltiplos estágios de transposição

---
layout: section
---

# Máquinas de Rotor

---

# Máquinas de Rotor

- Aplica várias etapas de encriptação
- Precursor da encriptação DES
- Conjunto de cilindros independentes
- 26 pinos de entrada + 26 pinos de saída

---
layout: image
image: /img/rotores.png
backgroundSize: contain
---


---

# Máquinas de Rotor

- Aplicando 3 rotores com 26 letras cada tem-se 17.576 alfabetos possíveis
- Com 4 rotores 456.976 alfabetos
- Uma máquina com 5 rotores é equivalente a uma Cifra de *Vigenère* com chave de tamanho maior que 11 milhões de letras
- *Enigma* e *Purple* foram máquinas usadas na segunda guerra

---

# Como funciona a *Enigma*?

<Youtube id="5w3zDa7bgLU" />

---

# Como a *Enigma* foi Quebrada?

<Youtube id="E0YX8BC4RLo" />

---

# Referências 

- **Capítulo 2**  . Criptografia e Segurança de Redes. William Stallings. 4a. Ed. Editora Pearson.
- [Como funciona a *Enigma*?](https://www.youtube.com/watch?v=5w3zDa7bgLU)
- [Como a *Enigma* foi Quebrada?](https://www.youtube.com/watch?v=5w3zDa7bgLU)

---
src: /src/end.md
---