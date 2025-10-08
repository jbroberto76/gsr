---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image-right
image: /img/mona-bernhardsen-1s9OyG6YkfI-unsplash.jpg
title: Advanced Encryption Standard
exportFilename: gsr_aula5_aes
author: José Roberto Bezerra
description: Gerência e Segurança de Redes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem

- Conhecer o *Advanced Encryption Standard*

---

# Agenda 

1. Características
2. Estrutura geral
3. Detalhamento
2. Open SSL

---
layout: section
---

# Advanced Encryption Standard

---

# AES
*Advanced Encryption Standard*

- Publicado pelo NIST em 2001 em substituição ao DES como padrão de cifra de bloco
- Complexidade bastante superior ao DES, RSA, etc
- Padrão atual para cifra de bloco

---
layout: quote
---

# NIST

> The Advanced Encryption Standard (AES) specifies a FIPS-approved cryptographic algorithm that can be used to protect electronic data. The AES algorithm is a symmetric block cipher that can encrypt (encipher) and decrypt (decipher) information.

[FIPS 197](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)

---

# Características AES
Blocos

- Blocos de 128 bits (16 bytes)
- O bloco de entrada é definido como uma matriz quadrada de *bytes* (4x4) chamado de *State*
- Ao longo da execução, o *State* vai sendo modificado até o estágio final se tornar o texto cifrado

---

# Características AES
Chaves

- Versões com chaves de 128, 192 ou 256 bits (AES-128, AES-192 ou AES-256)
- A chave também é vista como uma matriz quadrada de *bytes* (4x4)
- A chave passa por um processo de expansão passando a ser de 44 *words* de 4 *bytes*

---

# Características AES
Rodadas

- A cifra é executada em diversas rodadas, segundo o tamanho da chave:
  - 10 rodadas, chave de 16 bytes (128bits)
  - 12 rodadas, chave de 24 bytes (192bits)
  - 16 rodadas, chave de 32 bytes (256bits)
- Em cada rodada são aplicadas 4 funções de transformação:
  - `SubBytes`
  - `ShiftRows`
  - `MixColumns`
  - `AddRoundKey`

---
layout: section
---

# Estrutura Geral

---

# Estrutura
Funções de transformação

- A primeira rodada aplica `AddRoundKey` ao texto claro
- As 9 rodadas seguintes aplicam as 3 funções de transformação
- Apenas `AddRoundKey` utiliza-se da chave
- As outras funções acrescentam confusão, difusão e não linearidade

---
image: /img/aes_rounds.png
layout: image
backgroundSize: contain
---


---

# `SubBytes`

- Transformação de substituição de *bytes*
- Define uma matriz de 16x16 *bytes* (S-Box) para permutações de todos os valores de 8 bits possíveis
- Cada byte de *State* é mapeado para um novo valor
  - 4 bits à esquerda representam as linhas
  - 4 bits à direita representam as colunas

---
layout: image-right
image: /img/subbytes.png
backgroundSize: contain
---

# `SubBytes`

- Por exemplo, o valor hexadecimal `{95}` referencia a linha 9, coluna 5 da S-box, que contém o valor `{2A}`.
- Logo, o valor `{95}` é mapeado para o `{2A}`

---

# `SubBytes`

- S-Box é projetada para ser resistente a ataques de criptoanálise
- A saída não pode ser descrita como uma função matemática simples da entrada (não linear)
- S-Box é inversível, mas não é autoinversível
  - Por exemplo, S-box({95}) = {2A}
  - Mas, IS-box({95}) = {AD}

---

# `SubBytes`
Como a S-Box é construída?

1. É inicializada com valores em byte em sequência crescente linha por linha. A primeira linha contém $\{00\}, \{01\}, \{02\}, ..., \{0F\}$, a segunda linha contém $\{10\}, \{11\}$, etc.; e assim por diante. Desse modo, o valor do byte na linha $y$, coluna $x$ é $\{yx\}$.
2. Cada *byte* na S-box é mapeado com seu inverso multiplicativo no corpo finito $GF(2^8)$; o valor $\{00\}$ é mapeado consigo mesmo.

---

# `SubBytes`
Como a S-Box é construída?

3. Considere que cada *byte* na S-box consiste em 8 bits rotulados $\{b_7, b_6, b_5, b_4, b_3, b_2, b_1, b_0\}$. Aplique a seguinte transformação a cada *bit* de cada *byte* na S-box:

$$
\begin{aligned}
b_{i}^{*} &= b_i \oplus b_{(i+4)\mod{8}} \oplus b_{(i+5)\mod{8}} \oplus b_{(i+6)\mod{8}} \oplus b_{(i+7)\mod{8}} \oplus c_i \\
&Onde:\\
&c = \{63\} = \{01100110\}
\end{aligned}
$$

---
image: /img/s_box_4x4.png
layout: image-right
backgroundSize: contain
---

# S-Box
Exemplo 4x4

---

# `ShiftRows`

- Transformação de deslocamento de *bytes*
- Recebe o *State* como entrada
  - Mantém 1a. linha intacta
  - Desloca a 2a. linha 1 byte à esquerda
  - Desloca a 3a. linha 2 bytes à esquerda
  - Desloca a 4a. linha 3 bytes à esquerda
- Garante que os 4 bytes de uma coluna sejam espalhados em quatro colunas diferentes

---
image: /img/shiftrows.png
layout: image-right
backgroundSize: contain
---

# `ShiftRows`
Exemplo

---

# `MixColumns`

- Transformação de embaralhamento de colunas
- Opera sobre cada coluna de *State*
- Cada *byte* de uma coluna é mapeado para um novo valor que é determinado em função de todos os quatro *bytes* nessa coluna

---

# `MixColumns`

- Os coeficientes da matriz são baseados em um código linear que garante um bom embaralhamento entre os *bytes* de cada coluna
- A transformação de embaralhamento de colunas combinada com a de deslocamento de linhas garante que, após algumas rodadas, todos os *bits* da saída dependam de todos os *bits* da entrada.

---
image: /img/mix_columns.png
layout: image-right
backgroundSize: contain
---

# `MixColumns`
Diagrama


---

# `AddRoundKey`

- Transformação direta de adição de chave de rodada
- Os 128 *bits* de *State* passam por um XOR com os 128 *bits* da chave da rodada
- A transformação de adição de chave da rodada é a mais simples e afeta **cada** *bit* de *State*.
- A complexidade da expansão de chave da rodada, mais a dos outros estágios do AES, garantem a sua segurança.

---
image: /img/addroundkey.png
layout: image-right
backgroundSize: contain
---

# `AddRoundKey`

---
image: /img/addroundkey_bytes.png
layout: image-right
backgroundSize: contain
---

# `AddRoundKey`
Byte a byte

---

# Expansão da Chave
Características

- Utiliza como entrada uma chave de 4 *words* (16 *bytes*) e produz um array linear de 44 *words* (176 *bytes*)
- Fornece uma chave da rodada de 4 *words* para o estágio `AddRoundKey` inicial e para cada uma das 10 rodadas da cifra
- A chave original é copiada para as 4 primeiras posições da chave expandida

---

# Expansão da Chave
Raciocínio

- A expansão da chave acontece da seguinte forma:
  - Cada *word*, $w[i]$ depende da *word* imediatamente anterior, $w[i-1]$, e da *word* quatro posições atrás, $w[i-4]$
    - $w[i] = w[i-4] \oplus w[i-1]$
  - Em três das quatro *words* da rodada é aplicada a operação XOR
  - Na quarta é aplicada uma função complexa, `RotWord`

---

# Expansão da Chave
`RotWord`

1. Realiza um deslocamento circular de um *byte* à esquerda em uma *word*. Uma *word* de entrada $[B_0, B_1, B_2, B_3]$ é transformada em $[B_1, B_2, B_3, B_0]$
2. Realiza uma substituição *byte* a *byte* utilizando S-Box
3. O resultado de 1. e 2. passa por um XOR

---

```c
KeyExpansion (byte key[16], word w[44])
{
  word temp
  for (i = 0; i < 4; i++) 
    w[i] = (key[4*i], key[4*i+1],
    key[4*i+2],
    key[4*i+3]);
  
  for (i = 4; i < 44; i++)
  {
    temp = w[i – 1];
    if (i mod 4 = 0) 
      temp = SubWord (RotWord (temp)) XOR Rcon[i/4];
    w[i] = w[i-4] XOR temp
  }
}
```

---
layout: quote
---

> Caso uma pequena alteração na chave ou no texto claro produzisse uma pequena mudança no texto cifrado correspondente, isso poderia ser usado para reduzir de forma significativa o tamanho do espaço de textos claros (ou chaves) possíveis a ser pesquisado.

---
layout: quote
---

# Efeito Avalanche
No AES

> O que é desejado é o efeito avalanche, em que uma pequena mudança no texto claro ou na chave produz uma grande alteração no texto cifrado.

---
image: /img/avalanche_msg.png
layout: image-right
backgroundSize: contain
---

# Efeito Avalanche no AES
Texto claro

- Aplica o AES em textos claros que diferem em apenas 1 *bit* com a mesma chave

---
layout: quote
---

# Efeito Avalanche no AES
Texto claro

> Ao selecionar dois textos claros ao acaso,espera-se que eles difiram em cerca de metade das posições de *bits* e os dois textos cifrados também se diferenciem em mais ou menos **metade** das posições.

---
image: /img/avalanche_chave.png
layout: image-right
backgroundSize: contain
---

# Efeito Avalanche no AES
Chave

- Aplica AES com textos claros idênticos e chaves que diferem em um único *bit*

---
layout: quote
---

# Efeito Avalanche no AES
Chave

> Uma rodada produz uma mudança significativa e a magnitude de alteração após todas as rodadas subsequentes é cerca de **metade** dos *bits*.

---
layout: section
---

# OpenSSL

---
layout: quote
---

# OpenSSL

> The OpenSSL Project develops and maintains the OpenSSL software - a robust, commercial-grade, full-featured toolkit for general-purpose cryptography and secure communication.

---

# OpenSSL Help

- Dentre os diversos comandos disponíveis, `openssl enc` realiza a encriptação de arquivos
- Diversas cifras estão disponíveis
- `openssl help`

---

# ECB
*Electronic Codebook Mode*
 
- A encriptação é aplicada diretamente a cada bloco
- Encriptação e Decriptação podem acontecer em paralelo
- Mensagens com tamanho múltiplo do tamanho do bloco
- Vulnerável a ataques, pois a mesma chave gera as mesmas cifras, sempre

---

# CBC
*Cipher Block Chaining Mode*

- A operação de encriptação não pode ser realizada em paralelo
- Como na decriptação os blocos já disponibilizados simultaneamente, a operação de decriptação pode ocorrer em paralelo
- Um dos mais usados

---

# `openssl enc -aes-256-cbc`

- Utiliza o comando `enc` do OpenSSL para encriptação e decriptação utilizando AES com chave de 256 *bits* no modo CBC
- Opções de cifras disponíveis com AES

```bash
roberto@m2JRB ~ % openssl enc -list | grep aes   
-aes-128-cbc               -aes-128-cfb               -aes-128-cfb1             
-aes-128-cfb8              -aes-128-ctr               -aes-128-ecb              
-aes-128-ofb               -aes-192-cbc               -aes-192-cfb              
-aes-192-cfb1              -aes-192-cfb8              -aes-192-ctr              
-aes-192-ecb               -aes-192-ofb               -aes-256-cbc              
-aes-256-cfb               -aes-256-cfb1              -aes-256-cfb8             
-aes-256-ctr               -aes-256-ecb               -aes-256-ofb              
-aes128                    -aes128-wrap               -aes128-wrap-pad          
-aes192                    -aes192-wrap               -aes192-wrap-pad          
-aes256                    -aes256-wrap               -aes256-wrap-pad          
-id-aes128-wrap            -id-aes128-wrap-pad        -id-aes192-wrap           
-id-aes192-wrap-pad        -id-aes256-wrap            -id-aes256-wrap-pad
```

---

# `openssl enc -aes-256-cbc`
Demais opções

- `-in`, arquivo com texto claro
- `-out`, arquivo com a mensagem cifrada
- `-pbkdf2`, utiliza PBKDF2 (*Password-Based Key Derivation Function 2*)
- `-pass`, senha para a geração da chave

---

# PBKDF2
*Password-Based Key Derivation Function 2*

> Uma função de derivação de chave baseada em senha, amplamente usada para criptografia e para aumentar a segurança das senhas. A técnica foi definida no padrão de criptografia de chave pública PKCS#5 da *RSA Laboratories* em 2000 e se tornou uma das principais ferramentas para proteção de dados sensíveis.

---

# PBKDF2
Características

- Transforma senhas em chaves criptográficas
- Combina a senha dada com um valor de sal (*Salt*) e aplica repetidamente uma função *hash* para geração da chave (fortalecimento de chave)
- Aumenta significativamente o custo computacional e o tempo necessário para quebrar a senha, oferecendo uma defesa eficaz contra ataques de força bruta

---

# PBKDF2
Características

- Flexível e configurável
  - *hash* (SHA-256 ou SHA-512)
  - número de iterações

> O uso de um valor de sal garante que, mesmo que dois usuários tenham a mesma senha, as chaves geradas serão únicas, aumentando a singularidade e segurança das senhas.

<!-- No campo da segurança digital, o PBKDF2 é amplamente aplicado em vários cenários, como criptografia de arquivos, controle de acesso a bancos de dados e proteção de senhas de contas online. Ele é mais do que uma ferramenta de criptografia, sendo um framework de segurança completo, oferecendo uma proteção robusta para o tratamento de dados sensíveis. -->

---
image: https://www.feistyduck.com/library/openssl-cookbook/assets/image-main-view.png
layout: image-right
backgroundSize: contain
---

# Referências

- [OpenSSL](https://www.openssl.org/)
- [OpenSSL Cookbook](https://www.feistyduck.com/library/openssl-cookbook/online/)
- [PBKDF-2](https://cryptobook.nakov.com/mac-and-key-derivation/pbkdf2)

---

# Referências

- Capítulo 5. Criptografia e Segurança de Redes. William Stallings. 6ª. Edição. Editora Pearson. 
  - **Seções 5.2, 5.3, 5.4 e 5.5.**

---
src: /src/end.md
---