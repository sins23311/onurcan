<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Blackjack Kart Takibi</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }
    .controls {
      margin-bottom: 20px;
    }
    .card {
      display: inline-block;
      margin: 10px;
      padding: 10px;
      background-color: #fff;
      border: 1px solid #ccc;
      border-radius: 8px;
      cursor: pointer;
      user-select: none;
      text-align: center;
      width: 100px;
    }
    .card img {
      width: 60px;
      height: auto;
      display: block;
      margin: 0 auto 5px;
    }
    .card:hover {
      background-color: #e0e0e0;
    }
    .summary {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Blackjack Kart Takibi</h1>  <div class="controls">
    <label>Deste Sayısı:
      <input type="number" id="deck-count" value="4" min="1" max="8">
    </label>
    <button onclick="initializeCards()">Sıfırla</button>
  </div>  <div>
    <label>Elindeki Toplam Puan:
      <input type="number" id="hand-value" min="1" max="21" value="12">
    </label>
    <button onclick="calculateOdds()">Patlama Oranı Hesapla</button>
  </div>  <div id="card-container"></div>  <div class="summary">
    <p><strong>Kalan Toplam Kart:</strong> <span id="total-remaining">0</span></p>
    <p><strong>Patlama Oranı:</strong> <span id="bust-chance">-</span></p>
    <p><strong>Güvenli Kart Oranı:</strong> <span id="safe-chance">-</span></p>
  </div>  <script>
    const cardValues = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
    const cardCounts = {};
    let deckCount = 4;

    function cardPoint(card) {
      if (card === 'A') return 1;
      if (['J','Q','K'].includes(card)) return 10;
      return parseInt(card);
    }

    function initializeCards() {
      deckCount = parseInt(document.getElementById('deck-count').value);
      cardValues.forEach(card => cardCounts[card] = deckCount * 4);
      renderCards();
      updateSummary();
    }

    function renderCards() {
      const container = document.getElementById('card-container');
      container.innerHTML = '';
      cardValues.forEach(card => {
        const count = cardCounts[card];
        const cardEl = document.createElement('div');
        cardEl.className = 'card';

        const img = document.createElement('img');
        const code = card === '10' ? '0' : card;
        img.src = `https://raw.githubusercontent.com/hayeah/playing-cards-assets/master/png/${code}S.png`;
        img.alt = card;

        const text = document.createElement('div');
        text.textContent = `${card}: ${count}`;

        cardEl.appendChild(img);
        cardEl.appendChild(text);

        cardEl.onclick = () => {
          if (cardCounts[card] > 0) {
            cardCounts[card]--;
            renderCards();
            updateSummary();
          }
        };

        container.appendChild(cardEl);
      });
    }

    function updateSummary() {
      let total = 0;
      cardValues.forEach(card => total += cardCounts[card]);
      document.getElementById('total-remaining').textContent = total;
    }

    function calculateOdds() {
      const handValue = parseInt(document.getElementById('hand-value').value);
      let bustTotal = 0, totalCards = 0;

      cardValues.forEach(card => {
        const value = cardPoint(card);
        const count = cardCounts[card];
        if (handValue + value > 21) bustTotal += count;
        totalCards += count;
      });

      const bustChance = totalCards > 0 ? ((bustTotal / totalCards) * 100).toFixed(2) : 0;
      const safeChance = (100 - bustChance).toFixed(2);

      document.getElementById('bust-chance').textContent = bustChance + '%';
      document.getElementById('safe-chance').textContent = safeChance + '%';
    }

    // Başlangıçta çalıştır
    initializeCards();
  </script></body>
</html>
