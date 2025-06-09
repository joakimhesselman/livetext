Teknisk översikt av index.html

HTML‑filen är en fristående webbapp för tal‑till‑text. Den innehåller både layout, stil och logik.

Gränssnitt och stil
Grundtemat definieras i CSS med variabler för färger och typsnitt, t.ex. svart bakgrund och vitt textfärg

Resultatet visas i #output-container och får särskild hantering i helskärmsläge (teleprompter-mode) där texten visas större och scrollar uppåt

Grundkontroller
Användaren väljer språk (svenska, engelska (US), danska eller norska) via en select

En knapp startar eller stoppar textningen, medan en annan öppnar helskärmsläge (teleprompter)

Anpassningar av texten
Fontstorlek kan ändras med +/-‑knappar och aktuell storlek visas i #font-size-display

Färg väljs med ett färgfält, vilket uppdaterar textfärgen i output-fältet i realtid

Stöd för egna ord och manus
Under “Vanliga ord/namn” kan användaren ange ord eller namn som bör kännas igen bättre. Inmatade rader används när transkripten skrivs ut via funktionen applyVocabulary

Nedladdning och delning
Knappen “Ladda ner .SRT” skapar en undertextfil utifrån talet och hämtar den lokalt

Med “Dela Länk/QR” visas en modal med en QR‑kod som pekar på aktuell URL

Taligenkänning
Web Speech API används för igenkänningen: SpeechRecognition initieras och startas/stoppas via knapparna

Slutlig text och interimresultat hanteras i onresult, där även tidsstämplar samlas för SRT-export

Helskärmsläge (teleprompter)
När teleprompter-knappen klickas begärs helskärm och en särskild klass ger uppåtrullande text. Vid avslutat helskärm återställs läget

Initiering och fel
Vid sidladdning står texten “Väntar på start...” tills användaren startar igenkänningen

En enkel felhantering visar alert om taligenkänningen inte stöds eller om helskärmsförfrågan misslyckas

Sammanfattningsvis erbjuder den uppdaterade index.html:

- Tal-till-text direkt i webbläsaren via Web Speech API
- Val av igenkänningsspråk
- Justerbar textstorlek och textfärg
- Möjlighet att lägga till egna ord/manus
- Helskärmsläge med teleprompterfunktion
- Export av transkription som SRT-fil
- Delning via länk och QR-kod

All logik ligger i en enda HTML-fil och ingen server krävs för att köra appen.
