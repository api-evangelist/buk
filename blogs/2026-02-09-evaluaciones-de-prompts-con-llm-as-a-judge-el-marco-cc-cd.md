---
title: "Evaluaciones de prompts con LLM-as-a-Judge: el marco CC/CD en Buk"
url: "https://buk.engineering/2026/02/09/evaluaciones-de-prompts-con-llm-as-a-judge-el-marco-cc-cd-en-buk.html"
date: "2026-02-09"
author: "aboneto"
feed_url: "https://buk.engineering/feed.xml"
---
Cuando trabajas con software “clásico”, la mayor parte de tus controles de calidad viven en tests deterministas y en un pipeline de CI/CD: compilas, ejecutas tests , haces deploy (despliegue). En cambio, cuando tu producto depende de Large Language Models (LLM), tu sistema se vuelve parcialmente no determinista: para un mismo input (entrada), puedes observar distintos outputs (salidas). Esto cambia la forma de iterar.
