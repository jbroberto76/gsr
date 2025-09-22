---
theme: default
trasition: fade
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

# Referências 

- Capítulo 1 . Criptografia e Segurança de Redes. William Stallings. 4a. Ed. Editora Pearson.
- 

---
src: /src/end.md
---