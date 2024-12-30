<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tarot Adventure Game</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #000;
            margin: 0;
            color: #fff;
            background-image: url('https://static.cinemagia.ro/img/db/movie/32/93/741/tarot-628710l.jpg');
            background-size: cover;
            background-position: center;
            height: 100vh;
            width: 100vw;
        }
        #tarot-section {
            position: fixed;
            top: 10%;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 20px;
        }
        .tarot-card {
            transition: transform 0.5s ease;
            cursor: pointer;
        }
        .tarot-card:hover {
            transform: scale(1.1);
        }
        .tarot-card img {
            width: 100%;
            height: 100%;
            border-radius: 10px;
        }
        .tarot-buttons {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }
        .tarot-button {
            padding: 10px;
            background-color: #ff3b3f;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        .tarot-button:hover {
            background-color: #d32f2f;
        }
        #tarot-description {
            position: fixed;
            top: 40%;
            left: 50%;
            transform: translateX(-50%);
            width: 80%;
            max-width: 600px;
            text-align: center;
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
        }
        #new-card-button {
            position: fixed;
            bottom: 220px;
            left: 50%;
            transform: translateX(-50%);
            padding: 10px;
            background-color: #ff3b3f;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        #new-card-button:hover {
            background-color: #d32f2f;
        }
    </style>
</head>
<body>
    <div class="tarot-buttons">
        <button class="tarot-button" onclick="drawTarotCards(1)">O Carte</button>
        <button class="tarot-button" onclick="drawTarotCards(3)">Trei Cărți</button>
        <button class="tarot-button" onclick="drawTarotCards(10)">Crucea Celtică</button>
        <button class="tarot-button" onclick="drawTarotCards(7)">Șapte Cărți</button>
        <button class="tarot-button" onclick="drawTarotCards(12)">Lectura Zodiacală</button>
    </div>

    <div id="tarot-section"></div>
    <div id="tarot-description"></div>
    <button id="new-card-button" onclick="drawTarotCards(1)">Trage o nouă carte</button>

    <script>
    // Tarot Cards Data
    const tarotCards = [
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Magicianul-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Nebunul-2-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Marea-Preoteasa-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Imparateasa-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Imparatul-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Marele-Preot-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Indragostitii-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Faetonul-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Forta-1.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Eremitul-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Roata-Norocului-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Dreptatea-1.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/TAROT-Spanzuratul-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Moartea-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Echilibrul-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Diavolul-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Turnul-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/TAROT-Steaua-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Luna-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Soarele-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Judecata-1-171x300.jpg.webp',
        'https://sloturipetocuri.ro/wp-content/uploads/2022/09/SPT-Lumea-1-171x300.jpg.webp'
    ];

    const tarotDescriptions = [
        'Magicianul - Reprezintă puterea de a manifesta idei și intenții.',
        'Nebunul - Simbolizează noi începuturi și călătorii neașteptate.',
        'Marea Preoteasă - Este un simbol al intuiției și cunoașterii ascunse.',
        'Împărăteasa - Simbolizează fertilitatea, abundența și creativitatea.',
        'Împăratul - Reprezintă autoritatea, structura și controlul.',
        'Marele Preot - Este un simbol al tradiției, educației și înțelepciunii spirituale.',
        'Îndrăgostiții - Simbolizează relațiile, deciziile și parteneriatele.',
        'Faetonul - Reprezintă controlul și determinarea de a merge mai departe.',
        'Forța - Este simbolul curajului, rezistenței și compasiunii.',
        'Eremitul - Reprezintă introspecția și căutarea cunoașterii interioare.',
        'Roata Norocului - Semnifică schimbări și cicluri inevitabile ale vieții.',
        'Dreptatea - Este simbolul echității, adevărului și corectitudinii.',
        'Spânzuratul - Reprezintă sacrificiul și schimbarea perspectivei.',
        'Moartea - Simbolizează transformarea, finalurile și noile începuturi.',
        'Echilibrul - Este simbolul armoniei, răbdării și temperanței.',
        'Diavolul - Reprezintă atașamentele, dependențele și iluzia.',
        'Turnul - Simbolizează schimbări bruște, haos și eliberare.',
        'Steaua - Este simbolul speranței, inspirației și vindecării.',
        'Luna - Reprezintă iluziile, frica și subconștientul.',
        'Soarele - Este simbolul succesului, energiei și optimismului.',
        'Judecata - Semnifică transformarea personală și renașterea.',
        'Lumea - Este simbolul realizării, succesului și împlinirii.'
    ];

    function drawTarotCards(number) {
        const tarotSection = document.getElementById('tarot-section');
        tarotSection.innerHTML = '';
        const tarotDescription = document.getElementById('tarot-description');
        tarotDescription.innerHTML = '';

        const randomCards = [];
        for (let i = 0; i < number; i++) {
            const randomIndex = Math.floor(Math.random() * tarotCards.length);
            randomCards.push(randomIndex);
        }

        randomCards.forEach(index => {
            const card = document.createElement('div');
            card.classList.add('tarot-card');
            card.innerHTML = `<img src="${tarotCards[index]}" alt="Tarot Card">`;
            card.onclick = function() {
                tarotDescription.innerHTML = tarotDescriptions[index];
            };
            tarotSection.appendChild(card);
        });
    }
    </script>
</body>
</html>
