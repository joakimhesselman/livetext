Live text Irl är en webbaserad app för realtids‑textning. Den använder Tailwind CSS och har en tydlig “neobrutalist” stil. Taligenkänningen bygger på Web Speech API, vilket kontrolleras direkt i början av skriptet där SpeechRecognition initieras.

Grundläggande kontroller
I kontrollpanelen kan användaren välja språk och starta, pausa eller stoppa textningen. Följande språk finns förvalda:

<option value="sv-SE">Svenska</option>
<option value="en-US">Engelska (US)</option>
<option value="da-DK">Danska</option>
<option value="nb-NO">Norska (Bokmål)</option>
<option value="is-IS">Isländska</option>
<option value="fi-FI">Finska</option>
<option value="fr-FR">Franska</option>

Start‑/stopp‑knappen och pausknappen definieras direkt efter språkvalet

Textinställningar och avancerade val
Användaren kan ändra textstorlek och färg via knappar, ett numeriskt fält samt en färgväljare. Under “Avancerade inställningar” går det att ange egna ord eller klistra in ett manus. En kommentar förklarar dock att Web Speech API bara i begränsad utsträckning kan dra nytta av dessa fält.

Nedladdning av undertextfil
Det går att ladda ned transkriptionen som SRT. När användaren klickar på knappen genereras filen via JavaScript. Exempel:

downloadSrtBtn.onclick = () => {
    if (srtEntries.length === 0) return;
    const srtContent = srtEntries.map(entry => `${entry.index}\n${entry.start} --> ${entry.end}\n${entry.text}\n`).join('\n');
    const blob = new Blob([srtContent], { type: 'text/srt;charset=utf-8' });
    ...
    a.download = `livetext_${timestamp}.srt`;
}

Fullskärmsläge och teleprompter
Texten visas i ett “teleprompter”-element. Ett särskilt knappfält gör att man kan gå in i helskärmsläge och justera storlek och färg även där. Vid övergångar till och från helskärm stoppas och startas taligenkänningen automatiskt så att sessionen fortsätter utan problem.

Delning via länk och QR‑kod
Användaren kan dela sin session med en länk eller QR‑kod. Ett klick på “Dela Länk/QR” visar en modal med en genererad QR‑kod:

shareBtn.onclick = () => {
    const currentUrl = window.location.href;
    shareableLinkInput.value = currentUrl;
    qrcodeDisplay.innerHTML = '';
    qrCodeInstance = new QRCode(qrcodeDisplay, { text: currentUrl, width: 200, height: 200, colorDark : "#000000", colorLight : "#ffffff", correctLevel : QRCode.CorrectLevel.H });
    qrModal.classList.remove('hidden');
};

Felhantering
Eventuella fel under taligenkänningen eller vid helskärmsförsök visas i ett särskilt felmodalfönster. Modalens HTML och hjälpfunktioner finns i filen.

Initiering
Vid sidladdning visas meddelandet “Väntar på start...” och knapparnas tillstånd uppdateras beroende på om igenkänningen är aktiv, pausad eller stoppad.

Sammanfattningsvis erbjuder appen möjlighet att:

starta, pausa och stoppa taligenkänning direkt i webbläsaren

välja igenkänningsspråk

ändra textstorlek och färg

visa texten i helskärm med separata kontroller

ladda ned textningen som SRT-fil

dela sessionen via länk eller QR-kod

hantera fel på ett tydligt sätt

All funktionalitet hanteras i en enda HTML-fil med inbäddad JavaScript‑kod och kräver ingen server. Applikationen fungerar bäst i webbläsare som stödjer Web Speech API, exempelvis Chrome eller Edge.
