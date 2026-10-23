---
title: "AG-UI en Ruby: la gema ag‑ui‑protocol"
url: "https://buk.engineering/2026/02/16/ag-ui-en-ruby-la-gema-ag-ui-protocol.html"
date: "2026-02-16"
author: "aboneto"
feed_url: "https://buk.engineering/feed.xml"
---
En Buk veníamos construyendo experiencias conversacionales con agentes, pero con una realidad típica en equipos que se mueven rápido: gran parte de la comunicación entre agente y frontend terminaba quedando como acuerdos “de facto” (eventos armados a mano, payloads que cambian, edge cases (casos borde) que se descubren tarde). Para resolverlo, decidimos adoptar el protocolo AG-UI , que estandariza la comunicación agent-to-UI usando un modelo orientado a eventos. Y como nuestro stack principal es Ruby on Rails y aún no existía un SDK Ruby oficial, aportamos a la comunidad creando la gema ag-ui-
