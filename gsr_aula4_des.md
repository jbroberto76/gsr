---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image-right
image: /img/mona-bernhardsen-1s9OyG6YkfI-unsplash.jpg
title: Data Encryption Standard
exportFilename: gsr_aula4_des
author: José Roberto Bezerra
description: Gerência e Segurança de Redes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem 

- Distinguir cifras de bloco e de fluxo
- Conhecer o *Data Encryption Standard*

---

# Agenda 

- Cifras de fluxo e de bloco
- Cifra de Feistel
- DES
- Modos de Operação
- Open SSL

---
layout: section
---

# Cifras de Fluxo e de Bloco

---

# Cifras de Fluxo
*Stream ciphers*

- Encripta um fluxo de dados digital **bit a bit ou byte a byte**
- O fluxo de chaves (*key stream*), $k_i$, tem o tamanho do fluxo de bits de texto claro ($p_i$)
- Para chaves aleatórias, a cifra é inquebrável (*One Time Pad*)
- Problema de compartilhamento de chaves

---
layout: image
image: /img/modelo_cifra_fluxo.png
backgroundSize: contain
---


---

# Cifras de Fluxo

- Geração de fluxo de bits feita via função algorítmica no emissor e receptor (**pseudo aleatória**)
- O algoritmo é afetado pela chave
- O fluxo de bits deve ser criptograficamente forte

---

# Cifras de Bloco

- O texto claro é tratado como um todo ou em **partes de tamanho fixo**
- Blocos de 64 ou 128 bits
- Emissor e receptor compartilham uma chave simétrica

---
layout: image
image: /img/modelo_cifra_bloco.png
backgroundSize: contain
---

---
layout: two-cols-header
---

# Cifra de Bloco Ideal

::left::

- Mapeamento reversível
- Para blocos de $n$ bits existem:
    - $2^n$ blocos possíveis
    - $2^n!$ mapeamentos reversíveis 

::right::

| Texto Claro | Texto Cifrado |
|:---------------:|:-----------------:|
| 00              | 11                |
| 01              | 10                |
| 10              | 00                |
| 11              | 01                |

---

# Mapeamento Irreversível

| Texto Claro     |     Texto Cifrado |
|:---------------:|:-----------------:|
| 00              | 11                |
| 01              | 10                |
| 10              | 01                |
| 11              | 01                |

---
layout: image-right
image: /img/cifra_ideal_4bits.png
backgroundSize: contain
---

# Cifra de Bloco Ideal

- Cifra reversível
- Mapeamentos de encriptação e decriptação definidos por tabulação
- Exemplo, cifra de substituição de 4 bits ($n=4$)

---

# Cifra de Bloco Ideal
Fragilidades

- Para $n$ pequeno a CBI equivale a cifra de substituição, logo sujeita a **análise estatística da texto**
- Considerando $n$ suficientemente grande e uma substituição reversível, as características estatísticas do texto são mascaradas
- Porém, uma cifra de bloco com $n$ suficiente grande é **impraticável**

---

# Cifra de Bloco Ideal
Fragilidades

- O mapeamento coincide com a própria chave
- Para o exemplo de 4 bits é necessário uma chave de 4 bits x 16 linhas = 64 bits
- Regra geral:
    - Tamanho do bloco: $n$
    - Tamanho da chave: $n \cdot 2^n$

---
layout: section
---

# Cifra de Feistel

---
layout: quote
---

# Cifra de Feistel

> Conceito de uma cifra de produto, (execução de duas ou mais cifras simples em sequência) tornando o resultado ou produto final criptograficamente mais forte do que qualquer uma das cifras componentes.

---

# Cifra de Feistel
Características

- Cifra de bloco com chave de tamanho $k$ bits + bloco de $n$ bits
    - Transformações: $2^k$
-  Cifra de bloco ideal
    - Transformações: $2^n!$
- Alternância entre permutações e substituições

---
layout: quote
---

# Cifra de Feistel
Substituições

> Cada elemento de texto claro ou grupo de elementos é substituído exclusivamente por um elemento ou grupo de elementos de texto cifrado correspondente.

---
layout: quote
---

# Cifra de Feistel
Permutações

> Uma sequência de elementos de texto claro é permutada, ou seja, nenhum elemento é acrescentado, removido ou substituído na sequência, mas a ordem em que os elementos aparecem é modificada.

---

# Difusão e Confusão

- A cifra de Feistel é uma aplicação prática de uma proposta de *Claude Shannon* (1949) para uma cifra de produto que alterne funções de confusão e difusão
- Difusão e confusão são os ingredientes básicos para qualquer sistema criptográfico para frustrar a criptoanálise estatística

---

# Difusão

- Dissipa a estrutura estatística do texto
- Cada digíto do texto claro afeta vários dígitos do texto cifrado
- Seja uma mensagem $M = m_1 + m_2 + m_3 + \dots$
- Cada caractere, $y_n$, do texto cifrado é dado por:

$$
y_n = \sum_{i=1}^k{m_{n+i}}mod26
$$

---

# Difusão
Principais técnicas

- Permutações (Transposições), através da reorganização dos bits/bytes dentro do bloco para espalhar a influência de cada bit de entrada por todo o bloco de saída
- Operações de Deslocamento (*Shifting*), disseminar bits para posições distantes
- Múltiplas operações XOR
- Redes de *Feistel*

---

# Confusão

- Agrega complexidade ao relacionamento estatístico entre o texto claro e o texto cifrado
- Mesmo que o atacante tenha alguma ideia das estatísticas do texto a complexidade conferida pela confusão impede a dedução da chave

---
layout: quote
---

> A confusão refere-se à complexidade da relação entre a chave secreta e o texto cifrado. O objetivo é tornar essa relação tão complexa e não-linear que seja praticamente impossível para um atacante deduzir informações sobre a chave a partir do texto cifrado

---

# Confusão 

- Um observador que veja o texto cifrado não deve ser capaz de deduzir a chave usada
- Cada bit do texto cifrado deve depender de múltiplos bits da chave de forma complexa
- A relação chave/texto cifrado deve ser estatisticamente indetectável

---

# Confusão
Principais técnicas

- Operações não lineares:
    - S-boxes (Caixas de Substituição): Tabelas que introduzem não-linearidade
    - Operações modulares com números primos
    - Funções matemáticas complexas

---
layout: image-right
image: /img/feistel1.png
backgroundSize: contain
---

# Cifra de *Feistel*
Estrutura (**encriptação**)

---
layout: image-right
image: /img/feistel2.png
backgroundSize: contain
---

# Cifra de *Feistel*
Estrutura (**decriptação**)

---
layout: image-right
image: /img/feistel_single.png
backgroundSize: contain
---

# Cifra de *Feistel*
Estrutura

| Entrada | Bloco de texto claro com 2w bits dividido em LE0 e RE0 |
|:-------:|--------------------------------------------------------|
| Saída   | LE1 e RE1, são a entrada da próxima rodada             |
| Rodadas | N rodadas                                              |
| Função  | XOR                                                    |
| Chave   | K, modificada a cada rodada                            |

---

# Cifra de *Feistel*
Parâmetros

| Bloco    | Maior segurança com blocos maiores                     |
|:--------:|--------------------------------------------------------|
|          | Maior custo computacional                              |
|          | Blocos de 64 bits são razoáveis                        |
| Rodadas  | Mais rodas, maior segurança                            |
| Função   | XOR                                                    |

---

# Cifra de *Feistel*
Parâmetros

| Chave    | Maior segurança com maiores chaves                     |
|:--------:|--------------------------------------------------------|
|          | Maior custo computacional                              |
| Algoritmo de subchave e $F$ | Aumentam a dificuldade da criptoanálise |

---
layout: section
---

# *Data Encription Standard*

---

# DES
*Data Encription Standard*

- Criptografia mais utilizada antes do AES (2001)
- Adotado pelo NIST em 1977
- Reafirmado em 1994
- Substituído pelo *Triple*$* DES em 1999
- *$*Triple* DES substituído pelo AES em 2001

---

# DES
Características

- Blocos de dados de 64 bits
- Chave de 56 bits
- 16 rodadas

---
layout: section
---

# Modos de Operação

---
layout: quote
---

> Como utilizar cifras de bloco para um conjunto de dados maior do que o tamanho do bloco?

---

# Modos de Operação

- Descrevem como aplicar cifras de bloco a mensagens mais longas
    - *Electronic Codebook Mode* (ECB)
    - *Cipherblock Chaining Mode* (CBC)
    - *Cipher Feedback Mode*
    - *Output Feedback Mode*
    - *Counter Mode* (*Galois*)

---
layout: image-right
image: https://www.jmunixusers.org/presentations/cryptography/images/block-ecb.png
backgroundSize: contain
---

# ECB
*Electronic Code Book*

- O texto claro é dividido em blocos de 64 bits
- Cada bloco é criptografado de forma independente com a mesma chave
- Esta estratégia fragiliza a cifra, pois blocos idênticos de texto claro produzem blocos idênticos de texto cifrado
- Cria padrões "visíveis" na cifra (ECB *Penguin*)

---
layout: image
image: https://www.jmunixusers.org/presentations/cryptography/images/block-ecb-penguin.png
backgroundSize: contain
---

---
layout: image-right
image: https://www.jmunixusers.org/presentations/cryptography/images/block-cbc.png
backgroundSize: contain
---

# CBC
*Cipher Block Chaining*

- Cada bloco de texto claro é combinado (usando um XOR) com o texto cifrado do bloco anterior antes de ser criptografado
- No primeiro bloco utiliza-se um vetor de inicialização (IV)
- Evita a repetição de padrões do EBC
- Sensível a propagação de erros

---
layout: image-right
image: https://cdn-images.postach.io/dbabb368-8101-471e-8db0-891899ecc396/447564dd-a88d-4769-9a56-22deaae1f819/b0f0252b-17ed-4d53-9f73-fe1c7452f6e2.png
backgroundSize: contain
---

# Counter Mode
*Galois*

- Um contador é usado para gerar uma sequência de blocos de chave única combinados com os dados de entrada para serem criptografados juntos
- Acrescenta um código de autenticação para cada bloco
- Realiza criptografia e autenticação em um processo único
- Evita propagação de erros
- Dificulta falsificação

---
layout: quote
---

# OpenSSL

---

> OpenSSL é uma biblioteca de *software* de código aberto e uma ferramenta de linha de comando usada para implementar os protocolos SSL e TLS para comunicações seguras.

---

# OpenSSL

- Implementação de algoritmos criptográficos
- Geração de chaves
- Geração e verficação de Certificados
- Funções de *Hash* (*message digest*)

---
layout: quote
---

# SSL
*Secure Socket Layer*

> SSL é um protocolo de segurança da Internet baseado em criptografia desenvolvido pela Netscape em 1995, com o objetivo de garantir a privacidade, autenticação e integridade de dados nas comunicações da Internet.

---

# SSL ou TLS?
*Transport Layer Security*

> O SSL é o antecessor direto de outro protocolo chamado TLS. Em 1999, o IETF (*Internet Engineering Task Force*) propôs uma atualização do SSL

---
layout: image
image: https://cheapsslweb.com/blog/wp-content/uploads/2025/06/tls-version-history-1024x480.webp
backgroundSize: contain
---

---

# OpenSSL
Como usar?

- Linha de comando
- `openssl` + Subcomando + Opções
- Exemplos
    - `openssl help`

---
image: /img/ssl_commands.png
layout: image-right
backgroundSize: contain
---

# OpenSSL
Comandos

---
image: /img/ssl_md.png
layout: image-right
backgroundSize: contain
---

# OpenSSL
*Message Digests*

---
image: /img/ssl_ciphers.png
layout: image-right
backgroundSize: contain
---

# OpenSSL
Algorítmos criptográficos

---

# OpenSSL
Exemplos

- Criptografia

`openssl enc -aes-256-cbc -in file.txt -out file.enc`

- Chave Privada

`openssl genpkey -algorithm RSA -out private_key.pem -aes256`

- Verificando informação em um certificado

`openssl x509 -in certificate.pem -text -noout`

---
layout: fact
---

# Perguntas

---

# Referências 
- Criptografia e Segurança de Redes. *Stallings, W.* Capítulo 3. **Seções: 3.1 a 3.3.** 
- [O que é OpenSSL?](https://www.ssldragon.com/pt/blog/que-e-openssl/)
- [SSL e TLS](https://www.cloudflare.com/pt-br/learning/ssl/what-is-ssl/)

---
src: /src/end.md
---