---
title: CIFRAS DE BLOCO (AES)
subtitle: Gerência e Segurança de Redes
---

# Objetivos de Aprendizagem

- Apresentar o Advanced Encryption Standard

---

# Agenda

1. Advanced Encryption Standard
2. Open SSL

---

# Advanced Encryption Standard

---

# Advanced Encryption Standard

- Publicado pelo NIST em 2001 em substituição ao DES como padrão de cifra de bloco
- Complexidade bastante superior ao DES, RSA, etc
- Padrão atual para cifra de bloco

---

# Características AES

- Blocos de 128 bits (16 bytes)
- O bloco de entrada é definido como uma matriz quadrada de bytes (4x4) chamado de State
- Ao longo da execução State vai sendo modificado até no estágio final se tornar o texto cifrado

---

# Características AES

- Chave de 128, 192 ou 256 bits (AES-128, AES-192 ou AES-256)
- A chave também é vista como uma matriz quadrada de bytes (4x4)
- A chave passa por um processo de expansão passando a ser de 44 words de 4 bytes

---

# Características AES

- A cifra é executada em diversas rodadas, segundo o tamanho da chave:
  - 10 rodadas, chave de 16 bytes (128bits)
  - 12 rodadas, chave de 24 bytes (192bits)
  - 16 rodadas, chave de 32 bytes (256bits)
- Em cada rodada são aplicadas 4 funções de transformação:
  - SubBytes
  - ShiftRows
  - MixColumns
  - AddRoundKey

---

# Estrutura Geral AES

---

# Estrutura Detalhada AES

---

# Estrutura Detalhada

- A primeira rodada aplica AddRoundKey ao texto claro
- As 9 rodadas seguintes aplicam as 4 funções de transformação
- Apenas AddRoundKey utiliza-se da chave
- As outras funções acrescentam confusão, difusão e não linearidade

---

# Rodada Individual

---

# SubBytes

- Transformação de substituição de bytes
- Define uma matriz de 16x16 bytes (S-Box) para permutações de todos os valores de 8bits possíveis
- Cada byte de State é mapeado para um novo valor
  - 4 bits à esquerda representam as linhas
  - 4 bits à direita representam as colunas

---

# SubBytes

- Por exemplo, o valor hexadecimal `{95}` referencia a linha 9, coluna 5 da S-box, que contém o valor `{2A}`.
- Logo, o valor `{95}` é mapeado para o `{2A}`

---

# SubBytes

- S-Box é projetada para ser resistente a ataques de criptoanálise
- A saída não pode ser descrita como uma função matemática simples da entrada (não linear)
- S-Box é inversível, mas não é autoinversível
  - Por exemplo, S-box({95}) = {2A}
  - Mas, IS-box({95}) = {AD}

---

# ShiftBytes

- Transformação de deslocamento de bytes
- Recebe o State como entrada
  - Mantém 1ª linha intacta
  - Desloca a 2ª linha 1 byte à esquerda
  - Desloca a 3ª linha 2 bytes à esquerda
  - Desloca a 4ª linha 3 bytes à esquerda
- Garante que os 4 bytes de uma coluna sejam espalhados em quatro colunas diferentes

---

# MixColumns

- Transformação de embaralhamento de colunas
- Opera sobre cada coluna de State
- Cada byte de uma coluna é mapeado para um novo valor que é determinado em função de todos os quatro bytes nessa coluna

---

# MixColumns

- Os coeficientes da matriz são baseados em um código linear que garante um bom embaralhamento entre os bytes de cada coluna
- A transformação de embaralhamento de colunas combinada com a de deslocamento de linhas garante que, após algumas rodadas, todos os bits da saída dependam de todos os bits da entrada.

---

# AddRoundKey

- Transformação direta de adição de chave de rodada
- Os 128 bits de State passam por um XOR com os 128 bits da chave da rodada
- A transformação de adição de chave da rodada é a mais simples e afeta cada bit de Estado.
- A complexidade da expansão de chave da rodada, mais a dos outros estágios do AES, garantem a sua segurança.

---

# OpenSSL

---

# OpenSSL

- The OpenSSL Project develops and maintains the OpenSSL software - a robust, commercial-grade, full-featured toolkit for general-purpose cryptography and secure communication.

---

# OpenSSL Help

- Dentre os diversos comandos disponíveis, `openssl enc` realiza a encriptação de arquivos
- Diversas cifras estão disponíveis
- `openssl help`

---

# Electronic Codebook Mode

- ECB
- A encriptação é aplicada diretamente a cada bloco
- Encriptação e Decriptação podem acontecer em paralelo
- Mensagens com tamanho múltiplo do tamanho do bloco
- Vulnerável a ataques, pois a mesma chave gera as mesmas cifras, sempre

---

# Cipher Block Chaining Mode

- CBC
- A operação de encriptação não pode ser realizada em paralelo
- Como na decriptação os blocos já disponibilizados simultaneamente, a operação de decriptação pode ocorrer em paralelo
- Um dos mais usados

---

# openssl enc aes-256-cbc

---

# Referências

- https://www.openssl.org/
- https://www.feistyduck.com/library/openssl-cookbook/online/
- https://wiki.openssl.org/index.php/Enc

---

# Referências

- Capítulo 5. Criptografia e Segurança de Redes. William Stallings. 6ª. Edição. Editora Pearson.

---

# FIM

Prof. José Roberto Bezerra  
jbroberto@ifce.edu.br  
IFCE – Campus Fortaleza