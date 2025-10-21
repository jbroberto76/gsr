---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image-right
image: /mona-bernhardsen-1s9OyG6YkfI-unsplash.jpg
title: Cifras de Fluxo
description: Gerência e Segurança de Redes
author: José Roberto Bezerra
exportFilename: gsr_aula6_fluxo
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem

- Conhecer o conceito de cifra de fluxo

---

# Agenda 

1. Estrutura
2. Cifras de Bloco x Cifras de Fluxo
3. Cifras Típicas
4. Aplicações
5. Vulnerabilidades

---
layout: section
---

# Estrutura

---

# Estrutura
Cifras de fluxo

- Criptografa um byte por vez
- Comumente aplica a canais de comunicação ou aplicações cliente/servidor
- Estrutura básica:
    - Chave de entrada ($K$)
    - Fluxo de bits, ou fluxo de chave ($k$)
    - XOR
    - Texto claro
    - Texto cifrado

---
image: /cifra_fluxo.png
layout: image
backgroundSize: contain
---

---

# Exemplo

|     | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | Texto claro    |
|-----|---|---|---|---|---|---|---|---|----------------|
|     | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | Fluxo de chave |
| XOR | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | Texto cifrado  |
|     |   |   |   |   |   |   |   |   |                |
|     | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | Texto cifrado  |
|     | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | Fluxo de chave |
| XOR | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | Texto claro    |

---
layout: quote
---

# Fluxo de chave
*Key stream*

> Um fluxo **pseudo-aleatório** é imprevisível sem conhecimento da chave de entrada

---
layout: quote
---

# Fluxo de chave
*Key stream*

> Um fluxo genuinamente **aleatório** é aquele que é totalmente imprevisível. *One Time Pad*.

---
layout: fact
---

# Por que utilizar um fluxo pseudo-aleatório?

---

# Cifras de Fluxo
Características

- O gerador de números pseudo-aleatório utiliza funções determinísticas e periódicas para geração do fluxo
- Quanto maior o período, maior a dificuldade de criptoanálise
- Quanto mais próximo do fluxo genuinamente aleatório, maior a dificuldade de criptoanálise
- Chave $K$ de pelo menos 128 bits
- Segurança das Cifras de Fluxo é comparável às Cifras de Bloco

---

# Cifras de Fluxo
Vantagens

- Implementação simplificada
- Baixa demanda computacional
    - DES, 9Mbps
    - 3DES, 3Mbps
    - RC4, 45Mbps
- Reutilização de chaves

---

# Cifras de Fluxo
Aplicações

- Canais de comunicação
- Cliente/Servidor
- Criptografia de unidades de armazenamento

---
layout: section
---

# Cifras Típicas

---

# Cifras de Fluxo
Exemplos

- Cifra de *Vernam*
- Salsa20
- RC4

---

# Cifra de *Vernam*

- Uma das primeiras CF (*Gilbert Vernam*, 1917)
- Chave e texto claro do mesmo tamanho
- XOR bit a bit entre texto claro e chave
- Generalização do OTP

---

# Salsa20

- CF proposta por *Daniel Bernstein* em 2005
- Segurança e eficiência
- Chaves de 128, 192 e 256 bits
- Fundamenta-se no uso de *nonces*

---
layout: quote
---

# Salsa20
*Number used Once*

> Número aleatório utilizado uma única vez em um algoritmo criptográfico

---

# Salsa20

- Utiliza um *nonce* de 64 bits como entrada junto com uma chave secreta

$$
\begin{aligned}
ChaveSecreta + nonce &= FluxoDeChaves \\
FluxoDeChaves \oplus TextoClaro &= TextoCifrado
\end{aligned}
$$

---

# RC4
*Rivest Cipher 4*

- Criado por *Ron Rivest* para RSA em 1994
- Tamanho de chave variável
- Fundamenta-se na permutação aleatória
- Baixa demanda computacional
    - 8 a 16 operações de processador por *byte* de saída

---

# RC4
Aplicações

- TLS 1.0
- WEP (*Wired Equivalent Privacy*)
- WPA (*WiFi Protected Access*)

---
layout: image-right
image: /rc4.png
backgroundSize: contain
---

# RC4
Funcionamento

- Chave $K$ possui tamanho variável entre 1 a 256 bytes (8 a 2048 bits)
- A chave inicializa o vetor de estados $S$ de 256 bytes

$$
\begin{aligned}
S[0] &= 0,\\S[1] &= 1,\\ ... ,\\ S[255] &= 255
\end{aligned}
$$

---

# RC4
$T$

- Se $K$ tem 256 bytes, um vetor temporário, $T$, é inicializado com o valor de $S$
- Caso contrário, $K$ é replicado em $T$ até que tenha o mesmo tamanho de $S$
- Resumo em pseudo-código:

```c {*}{class:'!children:text-xl'}
for i = 0 to 255
    S[i] = i;
    T[i] = K[i mod keylen];
```

---

# RC4
Permutações

- A função de $T$ é causar permutações em $S$, conforme abaixo

```c {*}{class:'!children:text-xl'}
j = 0;
for i = 0 to 255 do
    j = (j + S[i] + T[i]) mod 256;
    Swap (S[i], S[j])
```

---

# RC4
Fluxo de chaves

- O fluxo é gerado percorrendo cada elemento de $S$ e realizando as permutações

```c {*}{class:'!children:text-xl'}
i, j = 0;
while True
    i = (i + 1) mod 256;
    j = (j + S[i]) mod 256;
Swap (S[i], S[j])
t = (S[i] + S[j]) mod 256;
k = S[t]
```

---
layout: image
image: https://blog.cloudflare.com/content/images/rc4.gif
backgroundSize: contain
---

# RC4
Animação com State de 32 bytes


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
src: /snippets/end.md
---