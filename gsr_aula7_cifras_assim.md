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
exportFilename: gsr_aula7_cifras_assim
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem

- Conhecer o conceito de cifras assimnétricas

---

# Agenda 

- Por que usar cifras assimétricas?
- Princípios e elementos
- Aplicações
- Vulnerabilidades

---
layout: section
---

#  Por que usar cifras assimétricas?

---
layout: quote
---

# Objetivos

> Tratar o problema de distribuição de chaves para criptografia simétrica

> Criar um método para garantir que ambas as partes de uma comunicação, Emissor e Receptor, tenham certeza das respectivas identidades

---
layout: section
---

# Princípios e Elementos

---

# Criptosistemas de Chave Pública
Princípios

- É computacionalmente inviável determinar a chave de decriptografia dado apenas o conhecimento do algoritmo e chave de criptografia
- Qualquer uma das chaves relacionadas pode ser usada para criptografia, com outra usada para a decriptografia

---

# Criptosistemas de Chave Pública
Elementos

- Texto claro
- Algoritmos de criptografia/decriptografia
- Par de chaves assimétricas (pública/privada)
- Texto cifrado

---

# Criptosistemas de Chave Pública
Etapas

1. Cada usuário gera um par de chaves para criptografia/decriptografia
2. Cada usuário coloca uma das chaves num repositório publicamente acessível
3. Se Bob deseja enviar mensagem para Alice, Bob criptografa a mensagem usando a chave pública de Alice
4. Quando Alice recebe a mensagem, ela a decriptografa usando sua chave privada. Nenhum outro destinatário é capaz de decriptografar, pois não tem acesso a chave privada

---
image: /criptog_chave_pub.png
layout: image
backgroundSize: contain
---

---
image: /criptog_chave_priv.png
layout: image
backgroundSize: contain
---


---
layout: two-cols-header
---

# Criptografia Simétrica x Assimétrica

:: left ::

- Chave única para cirptografia e decriptografia
- Compartilhamento de chave
- Chave deve permanecer secreta
- O conhecimento do algoritmo e amostras de texto cifrado não deve ser suficiente para determinar a chave

:: right ::

- Chaves distintas para criptografia e decriptografia
- Emissor e receptor precisam ter acesso a apenas uma das chaves do par
- Uma das chaves permanece secreta
- O conhecimento do algoritmo e amostras de texto cifrado não deve ser suficiente para determinar a chave

---
layout: section
---

# Aplicações

---

# Aplicações de CS

- Criptografia/Decriptografia
- Assinatura digital
- Troca de chaves

---
layout: image-right
image: /crip_decrip_1.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

> O esquema mostrado garante confidencialidade?

---
layout: image-right
image: /crip_decrip_1.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

- 

---
layout: image-right
image: /crip_decrip_2.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

> O esquema mostrado garante confidencialidade?

---
layout: image-right
image: /crip_decrip_2.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

- 



---
layout: image-right
image: /crip_decrip_3.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

> O esquema mostrado garante confidencialidade? E a autenticidade?

---



---
layout: image-right
image: /crip_decrip_3.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

- 

---

# Aplicações de CS
Assinatura digital

---

# Aplicações de CS
Troca de chaves

---

# Criptorgrafia Assimétrica
*Diffie-Hellman*

> *Whitifield Diffie* e *Martin Hellman* postularam um sistema criptográfico baseado em duas chaves em 1976 e estabeleceram as condições que um algoritmo para implementar esse sistema deveria atender.

> Entretanto, os pesquisadores não demonstraram a existência de tal algoritmo

---

# Criptografia Assimétrica
Requisitos

1. Ser computacionalmente fácil gerar um par de chaves pública e
privada
2. Ser computacionalmente fácil para um emissor A, de posse da chave pública de um receptor $B$, gerar texto difrado $C$ referente a uma mensagem $M$

$$
C = E(Pub_B, M)
$$

---

# Criptografia Assimétrica
Requisitos

3. Ser computacionalmente fácil para B decriptografar o texto cifrado, $C$, resultante usando a chave privada para recuperar a mensagem M

$$
M = D(Priv_B, C)
$$

4. Ser computacionalmente inviável para um adversário, conhecendo a chave pública de B, determinar a chave privada de B, $Priv_B$
5. Ser computacionalmente inviável para um adversário, conhecendo $Pub_B$ e um texto cifrado $C$, recuperar a mensagem original

---

# Criptoanálise de Chave Pública

- Vulneráveis a ataques de força bruta
- Uso de chaves de tamanho adequado
    - Chaves demasiadamente grandes exigem capacidade computacional que cresce exponencialmente
    - Chaves muito pequenas expõe o algoritmo a ataques de força bruta

---

# Criptoanálise de Chave Pública

- Encontrar a chave privada a partir da chave pública
    - Ainda não há provas matemáticas que isso é inviável
    - Ainda não há relatos de que isso foi realizado
    - Logo, algoritmos de chave assimétrica ainda são “suspeitos”

---

# Criptoanálise de Chave Pública

- Vulneráveis a ataques de mensagem provável
    - Quando se usa como mensagem uma chave simétrica de 56 bits (DES, por exemplo)
    - Um adversário poderia criptografar todas as possíveis chaves de 56 bits usando a chave pública para encontrar a chave criptografada em combinação com o texto cifrado capturado
    - Para qualquer tamanho de chave assimétrica, o ataque é reduzido a um ataque de força bruta de 56 bits

---

> Depois do artigo pioneiro de *Diffie* e *Hellman* (1976) iniciou-se uma corrida para criar um algoritmo que atendesse aos requisitos proposto pelos autores

> Em 1978, *Ron Rivest*, *Adi Shamir* e *Len Adleman*, pesquisadores do MIT, publicaram uma das primeiras propostas e a mais aplicada até hoje

---
layout: section
---

# RSA

---

# RSA
Características

- Cifra de blocos
- Tamanho dos blocos dependente do tamanho da chave

$$
Bloco (bytes) = Chave (bits) - 11
$$

- Blocos típicos:
    - Chave de 1024 bits, blocos de até 117 bytes
    - Chave de 2048 bits, blocos de até 245 bytes
    - Chave de 4096 bits, blocos de até 501 bytes

---

# RSA
Abordagem dos ataques

- Força bruta
- Ataques matemáticos
- Ataques de temporização (*timing attack*)
- Ataques de texto cifrado escolhido

---

# RSA
Ataques de força bruta

> A contramedida é utilizar chaves de tamanho adequado através do compromisso entre segurança e agilidade do sistema

---

# RSA
Ataques matemáticos

- O algoritmos RSA fundamenta-se na escolha de números primos $p$ e $q$
$$
n = p \cdot q
$$

- As chaves são geradas a partir de $n$
- As estratégias de ataque consistem em artifícios matemáticos para encontrar $n$

---

# RSA
*Timing attacks*

> Buscam estimar $n$ através do tempo de processamento das operações multiplicação modular para e assim fazer suposições sobre o valor de $n$

---




---

# Referências

- [NIST Terms `nonce`](https://csrc.nist.gov/glossary/term/nonce)
- [UUID Generator](https://www.uuidgenerator.net/version4)
- [RC4 no WEP](https://www.researchgate.net/publication/224981600_Analise_Critica_da_Implementacao_da_Cifra_RC4_no_Protocolo_WEP)

---

# Referências

- Capítulo 7. Criptografia e Segurança de Redes. William Stallings. 6ª. Edição. Editora Pearson. **Capítulo 9**

- Capítulo 6. Criptografia e Segurança de Redes. William Stallings. 4ª. Edição. Editora Pearson. **Capítulo 9**

---
src: /snippets/end.md
---