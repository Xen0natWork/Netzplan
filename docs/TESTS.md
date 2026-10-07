# Project tests

- Syntax-Check: `node --check app.js` und `node --check netzplan-core.js`
- Core-Logik testen (Node, ohne Browser): siehe README.md Abschnitt "Tests"
- Manuelles UI-Testen: `index.html` im Browser öffnen, "Beispiel laden" klicken,
  erwartete Werte: Projektdauer 14, kritischer Pfad B→D→E→G
- Kein Build-Schritt, kein Package-Manager nötig (reines Vanilla JS/HTML/CSS)
