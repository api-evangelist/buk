---
title: "Actualizar una gema no debería mover 74 líneas del Gemfile.lock"
url: "https://buk.engineering/2026/10/05/bundle-update-conservativo-por-defecto.html"
date: "2026-10-05"
author: "jpacheco"
feed_url: "https://buk.engineering/feed.xml"
---
Cualquiera que haya mantenido una aplicación Ruby on Rails medianamente grande conoce la escena. Necesitas actualizar una gema —digamos, rails — para aplicar un parche de seguridad o agarrar un bug fix. Ejecutas lo más obvio: $ bundle update rails && git diff --stat Gemfile.lock Gemfile.lock | 74 +++++++++++++++++++++++----------------------- Setenta y cuatro líneas.
