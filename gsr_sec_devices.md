---
theme: default
transition: fade
lineNumbers: true
colorSchema: dark
layout: image
image: /cover.jpg
author: José Roberto Bezerra
description: Gerência e Segurança de Redes
exportFilename: gsr_sec_devices
title: Dispositivos de Segurança de Redes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem
- Conhecer dispositivos e serviços de segurança de rede

---

# Agenda
- Arquitetura em Três Camadas
- Firewalls
- IDS e IPS

---
layout: section
---

# Arquitetura em Três Camadas

---

# Dispositivos de Rede

- Dispositivos finais
- Dispositivos intermediários

---
layout: quote
---

# Projeto de Redes Hierárquico
*Three-layer hierarchical model*

> Modelo hierárquico de redes visa a modularização e a segmentação

---

# Modelo Hierárquico de 3 Camadas

- Acesso
- Distribuição
- Núcleo (*core*)

---

# Modelo Hierárquico de 3 Camadas
Acesso

> Camada de utilização direta dos usuários e seus dispositivos. Fornece serviços básicos de compartilhamento de arquivos, mídia e dispositivos.

---

# Modelo Hierárquico de 3 Camadas
Acesso

- Meios de acesso convenientes ao usuário (*wired*, *wireless*, etc)
- Sistemas finais
    - *Desktops*
    - *Smartphones* e similares
- Dispositivos de rede
    - *Switches* de acesso
    - *Access Points*
- Segurança voltada especialmente para evitar acessos não autorizados
- Redes isoladas

---
layout: quote
---

# Modelo Hierárquico de 3 Camadas
Distribuição

> Com o crescimento da rede surgem demandas de acesso a serviços entre as diversas redes locais existentes. A camada de distribuição possibilita o acesso entre redes de forma segura e controlada.

---

# Modelo Hierárquico de 3 Camadas
Distribuição

- Conecta redes diversas
- Dispositivos de rede
    - Roteadores
    - *Switches* de camada 3 (L3)
- Segurança voltada a proteção ao isolamento das redes e acesso a recursos quando permitido

---

# Modelo Hierárquico de 3 Camadas
Distribuição

- Características desejáveis
    - Roteamento
    - Variedades de meios físicos
    - Mais recursos computacionais (memória e CPU)
    - Portas multi gigabit (100 Gigabit Ethernet, 40G, 25G e similares)
    - Listas de controle de acesso (ACLs)
    - Filtragem de pacotes (*Firewall*)

---

# Modelo Hierárquico de 3 Camadas
Núcleo (*core*)

- Considerada a camada de *backbone* da rede
- Conecta diversos dispositivos da camada de distribuição
- Regula o acesso externo (internet)
- Controle da largura de banda
- Listas de controle de acesso simplificadas
- Redundância
- Segurança resalizada por *Firewalls* diversos
    - *Web Application Firewall*
    - SSl/TLS *offloading* para inspeção de conteúdo
    - Transparentes
    - *Intrusion Detections Systems* (IDS)

---

# Tendência

> Atualmente a tendência moderna é a aplicação da segurança na camada de Distribuição para evitar gargalos na camada Core deixando-a simples e rápida.

---

# Modelo de Duas Camadas

> Embora o modelo hierárquico tenha três camadas, algumas redes corporativas menores podem implementar um design hierárquico de duas camadas unindo o Core e a Distribuição.

---
layout: section
---

# *Designs* de Firewall

---

# Público e Privado

---

# Zona Desmilitarizada (DMZ)


---

# Zone Policy Firewall (ZPFs)

---
layout: section
---

# Tipos de Firewalls

---

# Tipos de Firewalls
*Stateless*

---

# Tipos de Firewalls
*Statefull*

---

# Tipos de Firewalls
*Gateway* ou *Proxy* ou FW de aplicação

---

# Tipos de Firewalls 
*New Generation Firewall* (NGFW)

---
layout: section
---

# Prevenção e Detecção de Intrusão

---
layout: quote
---

# Detecção de Intrusão

> Com o avanço das tecnologias de rede e consequentemente dos ataques, os FWs tradicionais não são mais suficientes para defesa

---

# Detecção de Invasão

> A abordagem moderna inclui dispositivos de detecção de invasão (*Intrusion Detection Systems*, IDS) na infraestrutura de rede

---

# Prevenção de Invasão

> Dispositivos de prevenção a invasões (*Intrusion Prevention Systems, IPS*) podem ser aplicados para bloquear a ação de ataques a infraestrutura de rede.

---

# Referências

- 

---
src: /snippets/end.md
---