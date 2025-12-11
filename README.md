<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Esercizio di Vocabolario Italiano (Livello A2/B1)</title>
    <style>
        :root {
            --primary-color: #00897B; /* Teal */
            --secondary-color: #80CBC4; /* Light Teal */
            --background-color: #F4F6F6;
            --container-bg: #FFFFFF;
            --correct-color: #4CAF50;
            --incorrect-color: #F44336;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: var(--background-color);
            color: #333;
            line-height: 1.6;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background-color: var(--container-bg);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 25px;
            font-size: 2em;
        }

        h2 {
            color: #004D40;
            border-bottom: 2px solid var(--secondary-color);
            padding-bottom: 5px;
            margin-top: 30px;
        }

        /* --- Navigation --- */
        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 30px;
        }

        .nav-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 600;
            transition: all 0.3s ease;
            background: #E0F2F1;
            color: var(--primary-color);
        }

        .nav-buttons button.active,
        .nav-buttons button:hover {
            background: var(--primary-color);
            color: white;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }

        .section {
            padding: 20px 0;
            border-top: 1px solid #EEE;
            display: none;
        }

        .section.active {
            display: block;
        }

        /* --- Scoreboard --- */
        #score-display {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 1.1em;
            font-weight: 600;
            color: var(--primary-color);
            background: var(--secondary-color);
            padding: 8px 15px;
            border-radius: 5px;
        }

        /* --- Vocabulary List --- */
        .vocab-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin-bottom: 10px;
            border-bottom: 1px dashed var(--secondary-color);
        }

        .vocab-item:last-child {
            border-bottom: none;
        }

        .vocab-word-details {
            flex-grow: 1;
        }

        .word {
            font-weight: 700;
            color: var(--primary-color);
            font-size: 1.2em;
        }

        .context {
            font-style: italic;
            color: #777;
            font-size: 0.9em;
            margin-left: 10px;
        }

        .explanation, .example {
            margin-top: 5px;
            font-size: 0.95em;
        }

        .speak-button {
            background: var(--secondary-color);
            color: var(--primary-color);
            border: none;
            padding: 8px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: background 0.2s;
        }

        .speak-button:hover {
            background: var(--primary-color);
            color: white;
        }

        /* --- Word Bank Styling --- */
        .word-bank {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 10px;
            background: linear-gradient(135deg, #E8F5E9 0%, #B9F6CA 100%);
            border: 1px solid var(--correct-color);
            justify-content: center;
            font-weight: 600;
            color: #1B5E20;
        }

        .word-bank span {
            padding: 5px 12px;
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        /* --- Fill in the Gaps (Writing) --- */
        .gap-sentence {
            padding: 10px 0;
            border-bottom: 1px dotted #CCC;
            margin-bottom: 15px;
        }

        .gap-sentence input[type="text"] {
            padding: 8px;
            border: 1px solid var(--secondary-color);
            border-radius: 5px;
            font-size: 1em;
            width: 150px;
            text-align: center;
            margin: 0 5px;
            transition: border-color 0.3s;
        }

        .gap-sentence input:focus {
            border-color: var(--primary-color);
            outline: none;
        }

        .feedback {
            margin-left: 15px;
            font-weight: 600;
        }

        .writing-controls {
            display: flex;
            gap: 15px;
            margin-top: 20px;
            justify-content: center;
        }

        .writing-controls button {
            padding: 10px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 700;
            transition: background 0.3s;
        }

        #check-writing {
            background: var(--primary-color);
            color: white;
        }

        #check-writing:hover {
            background: #00695C;
        }

        #reset-writing {
            background: #EEE;
            color: #333;
        }

        #reset-writing:hover {
            background: #DDD;
        }

        /* --- Match Definitions --- */
        .match-container {
            display: flex;
            justify-content: space-around;
            gap: 20px;
        }

        .match-column {
            flex-basis: 48%;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .match-item {
            padding: 12px;
            border: 2px solid var(--secondary-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            user-select: none;
            min-height: 40px;
            display: flex;
            align-items: center;
            background-color: var(--container-bg);
        }

        .match-word {
            font-weight: 700;
            color: var(--primary-color);
        }

        .match-definition {
            font-style: italic;
        }

        .match-selected {
            border-color: var(--primary-color) !important;
            background-color: #E0F7FA;
            box-shadow: 0 0 10px rgba(0, 137, 123, 0.3);
        }

        .match-correct {
            background-color: var(--correct-color) !important;
            color: white;
            border-color: var(--correct-color) !important;
            cursor: default;
            box-shadow: none;
        }

        .match-incorrect {
            animation: shake 0.5s;
            border-color: var(--incorrect-color) !important;
            background-color: #FFEBEE;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-5px); }
            40%, 80% { transform: translateX(5px); }
        }

        /* --- Fill in the Gaps (Pronunciation) - ITALIAN VERSION --- */
        .pron-sentence {
            display: flex;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px dotted #CCC;
            margin-bottom: 15px;
        }

        .pron-sentence p {
            flex-grow: 1;
            margin: 0;
            display: flex;
            align-items: center;
        }

        .pron-blank {
            display: inline-block;
            width: 150px;
            height: 25px;
            line-height: 25px;
            text-align: center;
            border-bottom: 2px dashed #999;
            margin: 0 5px;
            font-weight: 600;
            color: var(--primary-color);
        }

        .pron-correct {
            border-bottom: 2px solid var(--correct-color);
            color: var(--correct-color);
        }

        .mic-button {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.5em;
            padding: 5px;
            transition: transform 0.2s;
        }

        .mic-button:hover {
            transform: scale(1.1);
        }
        
        .mic-listening {
            color: var(--incorrect-color);
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .pron-feedback {
            margin-left: 15px;
            font-size: 0.9em;
            font-style: italic;
        }

    </style>
</head>
<body>

    <div id="score-display">Punteggio: 0 / 24</div>

    <div class="container">
        <h1>Esercizio di Vocabolario Italiano</h1>
        <p>Pratica le seguenti parole e frasi in italiano.</p>

        <div class="nav-buttons">
            <button onclick="showSection('vocab-list', this)" class="active">📚 Lista Vocabolario</button>
            <button onclick="showSection('writing-gaps', this)">✍️ Completa le Frasi</button>
            <button onclick="showSection('match-defs', this)">🧠 Abbina Definizioni</button>
            <button onclick="showSection('pronunciation-gaps', this)">🗣️ Pronuncia</button>
        </div>

        <div id="vocab-list" class="section active">
            <h2>📚 Lista Vocabolario & Esempi</h2>
            <div id="vocab-items-container">
                </div>
        </div>

        <div id="writing-gaps" class="section">
            <h2>✍️ Completa le Frasi</h2>
            <p>Usa le parole del riquadro per completare le frasi. Scrivi la parola o frase esattamente come appare.</p>
            <div id="writing-word-bank" class="word-bank">
                </div>
            <div id="writing-sentences-container">
                </div>
            <div class="writing-controls">
                <button id="check-writing" onclick="checkWritingGaps()">Controlla Risposte</button>
                <button id="reset-writing" onclick="resetWritingGaps()">Azzera</button>
            </div>
        </div>

        <div id="match-defs" class="section">
            <h2>🧠 Abbina Definizioni</h2>
            <p>Clicca una parola a sinistra, poi clicca la sua corretta definizione a destra.</p>
            <div class="match-container" id="match-container">
                <div class="match-column" id="match-words-container">
                    </div>
                <div class="match-column" id="match-definitions-container">
                    </div>
            </div>
        </div>

        <div id="pronunciation-gaps" class="section">
            <h2>🗣️ Pronuncia e Riempi gli Spazi</h2>
            <p>Premi il microfono e pronuncia la parola mancante per completare la frase. (Lingua: Italiano).</p>
            <div id="pron-word-bank" class="word-bank">
                </div>
            <div id="pron-sentences-container">
                </div>
        </div>

    </div>

    <script>
        // --- DATA ---
        const vocabData = [
            {
                word: "Come va?",
                english: "How are you? / How's it going?",
                explanation: "Espressione colloquiale usata per chiedere lo stato di salute o il procedere delle cose.",
                example: "Ciao Marco! Come va? Tutto bene con il lavoro?",
                writingSentence: "Quando incontri un amico, puoi salutarlo dicendo: ___",
                pronSentence: "Domani sera vado a trovare Luigi. Spero che ___ tutto bene per lui.",
                definition: "Domanda informale usata per chiedere 'come stai' o 'come procedono le cose'.",
            },
            {
                word: "senza",
                english: "without",
                explanation: "Preposizione che indica la mancanza o l'assenza di qualcosa o qualcuno.",
                example: "Non posso bere il caffè senza zucchero, è troppo amaro.",
                writingSentence: "Ho dovuto fare la spesa ___ la lista e ho dimenticato molte cose.",
                pronSentence: "Non guidare mai l'auto ___ cintura di sicurezza, è pericoloso.",
                definition: "Preposizione che indica la mancanza o l'esclusione di qualcosa.",
            },
            {
                word: "dopo",
                english: "after / afterwards",
                explanation: "Avverbio o preposizione che indica un momento successivo nel tempo.",
                example: "Prima andiamo a cena, dopo guardiamo un film a casa.",
                writingSentence: "Ti chiamo ___ la riunione; ora sono occupato.",
                pronSentence: "Facciamo i compiti subito, così ___ possiamo giocare.",
                definition: "In un momento successivo rispetto a un altro evento o tempo.",
            },
            {
                word: "penso",
                english: "I think",
                explanation: "Prima persona singolare del presente indicativo del verbo 'pensare' (formulare un'opinione o credere).",
                example: "Penso che domani pioverà, quindi porterò l'ombrello.",
                writingSentence: "___ che sia un'ottima idea andare al mare questo fine settimana.",
                pronSentence: "Non sono sicuro, ma ___ che il treno parta dal binario 5.",
                definition: "Verbo (prima persona singolare) che significa formulare un'idea o credere in qualcosa.",
            },
            {
                word: "dottorato",
                english: "PhD (Doctorate)",
                explanation: "Il titolo accademico più elevato, ottenuto dopo anni di ricerca universitaria (abbreviato in PhD).",
                example: "Sta lavorando al suo dottorato in fisica quantistica da quattro anni.",
                writingSentence: "Per insegnare all'università, spesso è necessario completare un ___.",
                pronSentence: "Dopo la laurea magistrale, ha deciso di continuare gli studi con il ___.",
                definition: "Il più alto titolo di studio universitario, conseguito con un periodo di ricerca (PhD).",
            },
            {
                word: "piove",
                english: "it is raining",
                explanation: "Terza persona singolare del presente indicativo del verbo 'piovere' (fenomeno meteorologico).",
                example: "Guarda fuori, piove forte! Dobbiamo rimandare la nostra passeggiata.",
                writingSentence: "Se ___ , dovremo annullare la partita di calcio all'aperto.",
                pronSentence: "Non voglio uscire perché ___ e non ho l'ombrello con me.",
                definition: "Verbo impersonale che descrive il fenomeno meteorologico della caduta della pioggia.",
            },
            {
                word: "costosa",
                english: "expensive (feminine)",
                explanation: "Aggettivo femminile per descrivere qualcosa che ha un prezzo elevato (maschile: 'costoso').",
                example: "Quella borsa di marca è molto bella, ma è anche estremamente costosa.",
                writingSentence: "L'ultima auto che ha comprato è davvero troppo ___ per le sue finanze.",
                pronSentence: "La riparazione dell'orologio antico è stata più ___ del previsto.",
                definition: "Che ha un prezzo alto; che richiede una grande spesa di denaro (forma femminile).",
            },
            {
                word: "marito",
                english: "husband",
                explanation: "L'uomo unito a una donna dal vincolo del matrimonio.",
                example: "Mio marito è un ingegnere e lavora a Milano.",
                writingSentence: "Mia sorella e suo ___ hanno comprato una casa nuova l'anno scorso.",
                pronSentence: "Il ___ della mia amica le ha regalato un bellissimo anello.",
                definition: "L'uomo con cui una donna è sposata.",
            }
        ];

        let totalVocabulary = vocabData.length;
        let totalPossibleScore = totalVocabulary * 3;
        let currentScore = 0;
        let writingCorrectCount = 0;
        let matchingCorrectCount = 0;
        let pronCorrectCount = 0;

        let selectedWordMatch = null;
        let selectedDefinitionMatch = null;
        const matchingAnswers = {}; // wordId -> definitionId

        const pronResults = {}; // word -> true/false

        // La lingua per il riconoscimento vocale è impostata su 'it-IT'
        const recognitionFallback = ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window);

        // --- UTILITY FUNCTIONS ---
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function varToHex(variable) {
            const style = getComputedStyle(document.documentElement);
            const value = style.getPropertyValue(variable).trim();
            return value || '#333333';
        }

        function updateScore() {
            currentScore = writingCorrectCount + matchingCorrectCount + pronCorrectCount;
            document.getElementById('score-display').innerText = `Punteggio: ${currentScore} / ${totalPossibleScore}`;
        }

        function showSection(id, button) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            document.getElementById(id).classList.add('active');

            document.querySelectorAll('.nav-buttons button').forEach(btn => {
                btn.classList.remove('active');
            });
            button.classList.add('active');
        }

        // --- 1. LISTA VOCABOLARIO ---
        function generateVocabList() {
            const container = document.getElementById('vocab-items-container');
            container.innerHTML = '';
            vocabData.forEach(item => {
                const div = document.createElement('div');
                div.className = 'vocab-item';
                div.innerHTML = `
                    <div class="vocab-word-details">
                        <span class="word">${item.word}</span> <span class="context">(${item.english})</span>
                        <p class="explanation"><strong>Spiegazione:</strong> ${item.explanation}</p>
                        <p class="example"><strong>Esempio:</strong> <em>"${item.example}"</em></p>
                    </div>
                    <button class="speak-button" onclick="speak('${item.word}', 'it-IT')">▶️ Ascolta</button>
                `;
                container.appendChild(div);
            });
        }

        function speak(text, lang) {
            if ('speechSynthesis' in window) {
                const u = new SpeechSynthesisUtterance(text);
                u.lang = lang;
                speechSynthesis.speak(u);
            } else {
                alert("La sintesi vocale non è supportata nel tuo browser.");
            }
        }


        // --- 2. COMPLETA LE FRASI (SCRITTURA) ---
        function generateWritingGaps() {
            const container = document.getElementById('writing-sentences-container');
            const bank = document.getElementById('writing-word-bank');
            container.innerHTML = '';
            bank.innerHTML = '';

            // Genera Word Bank
            shuffleArray([...vocabData]).forEach(item => {
                const span = document.createElement('span');
                span.innerText = item.word;
                bank.appendChild(span);
            });

            // Genera Frasi (Mischiare)
            shuffleArray([...vocabData]).forEach((item, index) => {
                const sentence = item.writingSentence;
                const expectedWord = item.word;
                // La sostituzione è sensibile, l'input deve essere vuoto
                const sentenceHTML = sentence.replace('___', `<input type="text" data-expected="${expectedWord}" id="write-gap-${index}">`);

                const div = document.createElement('div');
                div.className = 'gap-sentence';
                div.innerHTML = `
                    <p>${sentenceHTML}<span id="write-feedback-${index}" class="feedback"></span></p>
                `;
                container.appendChild(div);
            });
        }

        function checkWritingGaps() {
            let correctCount = 0;
            document.querySelectorAll('#writing-sentences-container input').forEach((input, index) => {
                const expected = input.getAttribute('data-expected').toLowerCase().trim();
                const actual = input.value.toLowerCase().trim();
                const feedbackSpan = document.getElementById(`write-feedback-${index}`);

                if (input.disabled) {
                    if (actual === expected) correctCount++;
                    return; // Già corretta, non rivalutare
                }

                if (actual === expected) {
                    feedbackSpan.innerHTML = '✔️ Corretto!';
                    feedbackSpan.style.color = varToHex('--correct-color');
                    input.style.borderColor = varToHex('--correct-color');
                    input.disabled = true;
                    correctCount++;
                } else {
                    feedbackSpan.innerHTML = '❌ Riprova.';
                    feedbackSpan.style.color = varToHex('--incorrect-color');
                    input.style.borderColor = varToHex('--incorrect-color');
                }
            });

            writingCorrectCount = correctCount;
            updateScore();
        }

        function resetWritingGaps() {
            document.querySelectorAll('#writing-sentences-container input').forEach((input, index) => {
                input.value = '';
                input.style.borderColor = varToHex('--secondary-color');
                input.disabled = false;
                document.getElementById(`write-feedback-${index}`).innerHTML = '';
            });
            writingCorrectCount = 0;
            updateScore();
        }

        // --- 3. ABBINAMENTO DEFINIZIONI ---
        function generateMatchDefs() {
            const wordsContainer = document.getElementById('match-words-container');
            const defsContainer = document.getElementById('match-definitions-container');
            wordsContainer.innerHTML = '';
            defsContainer.innerHTML = '';
            selectedWordMatch = null;
            selectedDefinitionMatch = null;
            matchingCorrectCount = 0;
            updateScore();

            // Creare oggetti con ID univoci per l'abbinamento
            const words = shuffleArray(vocabData.map((item, index) => ({ id: `word-${index}`, text: item.word, answer: `def-${index}` })));
            const definitions = shuffleArray(vocabData.map((item, index) => ({ id: `def-${index}`, text: item.definition, answer: `word-${index}` })));

            words.forEach(item => {
                const div = document.createElement('div');
                div.className = 'match-item match-word';
                div.id = item.id;
                div.setAttribute('data-answer', item.answer);
                div.setAttribute('onclick', 'selectMatchItem(this, "word")');
                div.innerText = item.text;
                wordsContainer.appendChild(div);
            });

            definitions.forEach(item => {
                const div = document.createElement('div');
                div.className = 'match-item match-definition';
                div.id = item.id;
                div.setAttribute('data-answer', item.answer);
                div.setAttribute('onclick', 'selectMatchItem(this, "definition")');
                div.innerText = item.text;
                defsContainer.appendChild(div);
            });
        }

        function selectMatchItem(element, type) {
            if (element.classList.contains('match-correct')) return;

            // Pulisci la selezione precedente dello stesso tipo
            document.querySelectorAll(`.match-${type}`).forEach(item => item.classList.remove('match-selected', 'match-incorrect'));

            element.classList.add('match-selected');

            if (type === 'word') {
                selectedWordMatch = element;
            } else {
                selectedDefinitionMatch = element;
            }

            if (selectedWordMatch && selectedDefinitionMatch) {
                checkMatch();
            }
        }

        function checkMatch() {
            const word = selectedWordMatch;
            const definition = selectedDefinitionMatch;

            if (word.getAttribute('data-answer') === definition.id) {
                // Abbinamento Corretto
                word.classList.add('match-correct');
                definition.classList.add('match-correct');
                matchingCorrectCount++;
                updateScore();
            } else {
                // Abbinamento Errato
                word.classList.add('match-incorrect');
                definition.classList.add('match-incorrect');
                setTimeout(() => {
                    word.classList.remove('match-incorrect');
                    definition.classList.remove('match-incorrect');
                }, 800);
            }

            // Pulisci le selezioni
            selectedWordMatch = null;
            selectedDefinitionMatch = null;
            setTimeout(() => {
                document.querySelectorAll('.match-item').forEach(item => item.classList.remove('match-selected'));
            }, 500);
        }

        // --- 4. PRONUNCIA ---
        function generatePronunciationGaps() {
            const container = document.getElementById('pron-sentences-container');
            const bank = document.getElementById('pron-word-bank');
            container.innerHTML = '';
            bank.innerHTML = '';
            pronCorrectCount = 0;
            updateScore();
            Object.keys(pronResults).forEach(key => pronResults[key] = false); // Azzera i risultati

            // Genera Word Bank
            shuffleArray([...vocabData]).forEach(item => {
                const span = document.createElement('span');
                span.innerText = item.word;
                bank.appendChild(span);
            });

            // Genera Frasi (Mischiare)
            shuffleArray([...vocabData]).forEach((item, index) => {
                const sentence = item.pronSentence;
                const expectedWord = item.word;
                const blankPlaceholder = `<span class="pron-blank" id="pron-gap-${index}">?</span>`;
                const sentenceHTML = sentence.replace('___', blankPlaceholder);

                const div = document.createElement('div');
                div.className = 'pron-sentence';
                div.innerHTML = `
                    <p>
                        ${sentenceHTML}
                    </p>
                    <button class="mic-button" data-expected="${expectedWord}" data-index="${index}" onclick="startSpeechRecognition(this)">🎙️</button>
                    <span id="pron-feedback-${index}" class="pron-feedback"></span>
                `;
                container.appendChild(div);
                pronResults[expectedWord] = false;
            });

            if (!recognitionFallback) {
                console.warn("Il riconoscimento vocale non è supportato in questo browser.");
            }
        }

        let recognition = null;
        let isListening = false;
        let currentMicButton = null;

        function startSpeechRecognition(button) {
            if (!recognitionFallback) {
                alert("Il riconoscimento vocale non è supportato nel tuo browser.");
                return;
            }

            if (isListening) {
                // Se è già in ascolto, ferma la sessione corrente
                if (recognition) recognition.stop();
                return;
            }

            const expectedWord = button.getAttribute('data-expected');
            const index = button.getAttribute('data-index');
            const gapElement = document.getElementById(`pron-gap-${index}`);
            const feedbackElement = document.getElementById(`pron-feedback-${index}`);

            // Se è già corretto, non fare nulla
            if (pronResults[expectedWord]) return;

            // Resetta l'interfaccia utente per il nuovo tentativo
            gapElement.innerText = '?';
            gapElement.classList.remove('pron-correct');
            feedbackElement.innerText = '';
            
            // Evidenzia il pulsante
            currentMicButton = button;
            currentMicButton.classList.add('mic-listening');
            isListening = true;

            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            recognition = new SpeechRecognition();
            recognition.continuous = false;
            recognition.interimResults = false;
            recognition.lang = 'it-IT'; // Imposta la lingua italiana

            recognition.onresult = (event) => {
                let transcript = event.results[0][0].transcript.toLowerCase().trim();
                
                // Trattamento speciale per "Come va?" che può essere riconosciuto con o senza punto interrogativo
                let cleanTranscript = transcript.replace(/[^a-z0-9\s]/g, '').replace(/\s/g, ''); 
                let cleanExpected = expectedWord.toLowerCase().trim().replace(/[^a-z0-9\s]/g, '').replace(/\s/g, '');
                
                if (cleanTranscript === cleanExpected) {
                    if (!pronResults[expectedWord]) {
                        pronResults[expectedWord] = true;
                        pronCorrectCount++;
                        updateScore();
                    }
                    gapElement.innerText = expectedWord;
                    gapElement.classList.add('pron-correct');
                    feedbackElement.innerText = '✅ Successo!';
                    feedbackElement.style.color = varToHex('--correct-color');
                } else {
                    feedbackElement.innerText = `❌ Ascoltato: "${transcript}". Riprova.`;
                    feedbackElement.style.color = varToHex('--incorrect-color');
                }
            };

            recognition.onerror = (event) => {
                console.error('Errore nel riconoscimento vocale:', event.error);
                feedbackElement.innerText = `⚠️ Errore: ${event.error}. Assicurati che il microfono sia attivo.`;
                feedbackElement.style.color = '#FF9800';
                stopListeningUI();
            };

            recognition.onend = () => {
                stopListeningUI();
            };

            recognition.start();
            feedbackElement.innerText = '...In ascolto...';
            feedbackElement.style.color = varToHex('--primary-color');
        }

        function stopListeningUI() {
            if (currentMicButton) {
                currentMicButton.classList.remove('mic-listening');
            }
            isListening = false;
            currentMicButton = null;
        }

        // --- INIZIALIZZAZIONE ---
        document.addEventListener('DOMContentLoaded', () => {
            generateVocabList();
            generateWritingGaps();
            generateMatchDefs();
            generatePronunciationGaps();
            updateScore();
            showSection('vocab-list', document.querySelector('.nav-buttons button:first-child'));
        });
    </script>
</body>
</html>
