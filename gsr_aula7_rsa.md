---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image-right
image: /cover.jpg
title: Cifras Assimétricas e RSA
description: Gerência e Segurança de Redes
author: José Roberto Bezerra
exportFilename: gsr_aula7_rsa
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem

- Conhecer o conceito de cifras assimétricas e suas aplicações

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

> Tratar o problema de distribuição de chaves na criptografia simétrica

> Criar um método para garantir que ambas as partes de uma comunicação, Emissor e Receptor, tenham certeza das respectivas identidades

---

# Algoritmos

> Diversos algoritmos de criptografia assimétrica podem ser aplicados em situações distintas. Os principais são:
- RSA
- *Diffie-Hellman*
- Curva elíptica
- DSS

---
layout: quote
---

# Concepções Incorretas
CA é mais segura

<v-clicks>

> A criptografia assimétrica é mais segura contra criptoanálise do que a criptografia simétrica.

A segurança dos sistemas criptográficos está relacionada ao tamanho de chaves e o esforço computacional envolvido na quebra de cifras

</v-clicks>

---
layout: quote
---

# Concepções Incorretas
Hoje se utiliza apenas CA

<v-clicks>

> A criptografia assimétrica é uma técnica de uso geral que tornou a criptografia simétrica obsoleta.

Na verdade, a CA acrescenta uma grande sobrecarga computacional abrindo espaço para CS. Logo, ambas se complementam.

</v-clicks>

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

1. Texto claro
2. Algoritmos de criptografia/decriptografia
3. Par de chaves assimétricas (pública/privada)
4. Texto cifrado

---

# Criptosistemas de Chave Pública
Etapas (encriptação com chave pública)

1. Cada usuário gera um par de chaves para criptografia/decriptografia
2. Cada usuário coloca uma das chaves (a pública) num repositório publicamente acessível
3. Se Bob deseja enviar mensagem para Alice, Bob criptografa a mensagem usando a chave pública de Alice
4. Quando Alice recebe a mensagem, ela a decriptografa usando sua chave privada. Nenhum outro destinatário é capaz de decriptografar, pois não tem acesso a chave privada (confidencialidade é garantida)

---
image: /criptog_chave_pub.png
layout: image
backgroundSize: contain
---

---

# Criptosistemas de Chave Pública
Etapas (encriptação com chave privada)

1. Cada usuário gera um par de chaves para criptografia/decriptografia
2. Cada usuário coloca uma das chaves (a pública) num repositório publicamente acessível
3. Bob utiliza sua chave privada para encriptar a mensagem e enviar para Alice
4. Quando Alice recebe a mensagem, ela a decriptografa usando a chave pública de Bob, a única capaz de realizar essa tarefa. Não há confidencialidade. É possível garantir a autenticidade.

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

- Chave única para criptografia e decriptografia
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

# Aplicações de CA

- Criptografia/Decriptografia
- Assinatura digital
- Troca de chaves

---

# Algoritmos Típicos

| **Algoritmo**    | **Enc/Dec** | **Assinatura Digital** | **Troca de Chaves** |
|------------------|-------------|------------------------|---------------------|
| RSA              |  sim        |  sim                   | sim                 |
| Curva Elíptica   |  sim        |  sim                   | sim                 |
| *Diffie-Hellman* |  não        |  não                   | sim                 |
| DSS              |  não        |  sim                   | não                 |

---
layout: image-right
image: /crip_decrip_1.png
backgroundSize: contain
---

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

- A mensagem $X$ apenas pode ser decriptografada pelo par da chave $PU_b$, a chave $PR_b$
- A chave $PR_b$ é secreta e de conhecimento apenas de B, logo a confidencialidade é garantida

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

- A mensagem $X$ apenas pode ser decriptografada pela chave $PU_b$, porém essa chave não é secreta. É de conhecimento de todos, logo a confidencialidade não é garantida.
- A autenticidade pode ser garantida nesse esquema

---
layout: image-right
image: /crip_decrip_3.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

> O esquema mostrado garante confidencialidade? E a autenticidade?

---
layout: image-right
image: /crip_decrip_3.png
backgroundSize: contain
---

# Aplicações de CS
Criptografia/decriptografia

- Ambas as propriedades são garantidas nesse esquema, confidencialidade e autenticidade.

---
layout: quote
---

# Aplicações de CS
Assinatura digital

> Garante a autenticidade, autoria ou identificação das partes envolvidas

---
image: https://www.diegomacedo.com.br/assinatura-e-certificacao-digital/
layout: image-right
backgroundSize: contain
---

# Aplicações de CS
Assinatura digital

- Elementos
    - Par de chaves
    - Algoritmo criptográfico
    - Texto claro (mensagem)
    - Texto cifrado
    - Função de *hash*

---
image: https://i0.wp.com/www.diegomacedo.com.br/wp-content/uploads/2012/03/Autenticidade.png?w=744&ssl=1
layout: image-right
backgroundSize: contain
---

# Aplicações de CS
Assinatura digital

> A assinatura digital isoladamente não garante a confidencialidade da mensagem

---

# Certificados Digitais

> O certificado digital é um documento eletrônico assinado digitalmente que tem a função de associar uma pessoa, instituição, equipamento a uma chave pública. As informações públicas contidas num certificado digital são o que possibilita colocá-lo em repositórios públicos.

---

# Certificados Digitais
ICP Brasil

> A Infraestrutura de Chaves Públicas Brasileira (ICP-Brasil) é uma cadeia hierárquica de confiança que viabiliza a emissão de certificados digitais para a identificação virtual do cidadão.

---

# ICP Brasil
Estrutura

[Instituto Nacional de Tecnologia da Informação](https://estrutura.iti.gov.br/)

---
layout: quote
---

# Aplicações de CS
Funções de *hash*

> São funções matemáticas que recebem uma entrada qualquer tamanho e transformam em um sequência de caracteres de tamanho fixo

---

# Funções de *Hash*
Algorítmos típicos

- MD5 (*Message Digest 5*), 128 bits, obsoleto
- SHA-1 (*Secure Hash Algorithm*), 160 bits, obsoleto
- SHA-2 ou SHA-256, 256 bits
- SHA-3 variante do SHA-2

---
image: https://media.kasperskydaily.com/wp-content/uploads/sites/94/2014/04/06143603/HASH.png
layout: image
backgroundSize: contain
---

---

# Aplicações de CS
Troca de chaves

> *Key Exchange* é o processo que permite que duas partes estabeleçam uma chave secreta compartilhada sem a necessidade de transmiti-la diretamente

---

# Troca de chaves
Principais algorítmos

- *Diffie-Hellman*
- RSA

---

# Criptografia Assimétrica
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

# Criptoanálise de Chave Pública

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
Algoritmo



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

# Referências

- [O que é criptografia assimétrica](https://www.ibm.com/br-pt/think/topics/asymmetric-encryption)
- [Obter certificado digital](https://www.gov.br/pt-br/servicos/obter-certificacao-digital)

---

# Referências

- Capítulo 9. Criptografia e Segurança de Redes. *William Stallings*. 6ª. Edição. Editora Pearson.

- Capítulo 9. Criptografia e Segurança de Redes. *William Stallings*. 4ª. Edição. Editora Pearson.

---
src: /snippets/end.md
---