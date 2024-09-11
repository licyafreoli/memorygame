<script>
	import { onMount } from "svelte";
	import { writable } from "svelte/store";
  
	let cards = [];
	let flippedCards = [];
	let matchedCards = [];
	let score = 0;
	let timer = 0;
	let interval;
	let difficulty = "easy";
	let bestScore = localStorage.getItem('bestScore') || 0;
	let bestTime = localStorage.getItem('bestTime') || Infinity;
  
	// URLs das imagens para as cartas
	const cardImages = {
		easy: [
  'https://unsplash.com/pt-br/fotografias/gato-persa-laranja-sentado-13ky5Ycf0ts',
  'https://unsplash.com/pt-br/fotografias/cao-preto-sentado-no-barco-no-corpo-da-agua-ShLDezSsZJk',
  'https://unsplash.com/pt-br/fotografias/foto-de-animal-marrom-de-4-patas-jgJ3rDPcOjc',
  'https://unsplash.com/pt-br/fotografias/urso-pardo-selvagem-que-caminha-na-taiga-finlandesa-verde-FziCFoC3kxU'
  ],

medium: [
	'https://unsplash.com/pt-br/fotografias/um-cavalo-branco-em-um-campo-ACE44MRalyc',
	'https://unsplash.com/pt-br/fotografias/gato-tabby-marrom-em-escadas-brancas-mJaD10XeD7w',
	'https://unsplash.com/pt-br/fotografias/cordeiro-em-um-caminho-5SpKDV3p_gY',
	'https://unsplash.com/pt-br/fotografias/cardeal-empoleirado-l1H0sF8-v0k',
	'https://unsplash.com/pt-br/fotografias/pinguim-branco-e-preto-na-agua-aRD43BMqAp8',
	'https://unsplash.com/pt-br/fotografias/um-golden-retriever-vestindo-uma-bandana-e-soprando-bolhas-Q8Tn-jYIuTs',

  ],

hard: [
 'https://unsplash.com/pt-br/fotografias/close-up-foto-de-preto-e-branco-cao-husky-siberiano-NKN25UfGfkQ',
 'https://unsplash.com/pt-br/fotografias/cao-segurando-flor-2s6ORaJY6gI',
 'https://unsplash.com/pt-br/fotografias/cao-marrom-de-pelagem-longa-KZv7w34tluA',
 'https://unsplash.com/pt-br/fotografias/raposa-vermelha-cercada-de-flores-roxas-pAiwxxJVh0I',
 'https://unsplash.com/pt-br/fotografias/white-fox-sitting-on-snow-during-daytime-xgTMSz6kegE',
 'https://unsplash.com/pt-br/fotografias/um-pequeno-coelho-esta-deitado-em-uma-cama-21ECgy7wzoc' ,
 'https://unsplash.com/pt-br/fotografias/golfinho-saltando-do-mar-durante-o-dia-dgBOx1e3Mbs',
 'https://unsplash.com/pt-br/fotografias/tartaruga-marrom-nadando-debaixo-dagua-L-2p8fapOA8',
],
	};
  
	function shuffle(array) {
	  for (let i = array.length - 1; i > 0; i--) {
		const j = Math.floor(Math.random() * (i + 1));
		[array[i], array[j]] = [array[j], array[i]];
	  }
	}
  
	function startGame() {
	  matchedCards = [];
	  score = 0;
	  flippedCards = [];
	  timer = 0;
	  if (interval) clearInterval(interval);
	  interval = setInterval(() => {
		timer++;
	  }, 1000);
  
	  cards = [...cardImages[difficulty], ...cardImages[difficulty]];
	  shuffle(cards);
	}
  
	function flipCard(index) {
	  if (flippedCards.length < 2 && !flippedCards.includes(index) && !matchedCards.includes(index)) {
		flippedCards = [...flippedCards, index];
	  }
  
	  if (flippedCards.length === 2) {
		if (cards[flippedCards[0]] === cards[flippedCards[1]]) {
		  matchedCards = [...matchedCards, ...flippedCards];
		  score++;
		  if (matchedCards.length === cards.length) {
			clearInterval(interval);
			if (score > bestScore) {
			  bestScore = score;
			  localStorage.setItem('bestScore', score);
			}
			if (timer < bestTime) {
			  bestTime = timer;
			  localStorage.setItem('bestTime', timer);
			}
			alert(`Você ganhou! Pontuação: ${score}, Tempo: ${timer}s`);
		  }
		}
		setTimeout(() => {
		  flippedCards = [];
		}, 1000);
	  }
	}
  
	function setDifficulty(level) {
	  difficulty = level;
	  startGame();
	}
  
	onMount(() => {
	  startGame();
	});
  </script>
  
  <style>
	* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

h1 {
  margin: 20px 0;
  font-size: 3em;
  color: #f5f5f5;
  text-shadow: 0 4px 6px rgba(0,0,0,0.8);
  font-weight: 700;
}

.button-container {
  margin-bottom: 30px;
}

button {
  background: linear-gradient(135deg, #1e88e5, #1565c0);
  border: none;
  color: #e0e0e0;
  padding: 15px 30px;
  margin: 0 10px;
  border-radius: 12px;
  font-size: 1.2em;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease;
  box-shadow: 0 8px 16px rgba(0,0,0,0.5);
}

button:hover {
  background: linear-gradient(135deg, #1565c0, #1e88e5);
}

button:active {
  transform: scale(0.95);
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 20px;
  margin: 20px;
  width: 90%;
  max-width: 1200px;
}

.card {
  position: relative;
  width: 100%;
  padding-bottom: 100%;
  background: #333;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.6s ease, box-shadow 0.4s ease;
  box-shadow: 0 8px 16px rgba(0,0,0,0.7);
  perspective: 1000px;
}

.card.flipped {
  transform: rotateY(180deg);
}

.card.matched {
  background: #4caf50;
  box-shadow: 0 10px 20px rgba(0,0,0,0.8);
  transform: scale(1.05);
}

.card img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  backface-visibility: hidden;
  transition: opacity 0.6s ease;
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  color: #e0e0e0;
  border-radius: 12px;
  transition: opacity 0.6s ease;
  backface-visibility: hidden;
  transform: rotateY(180deg);
}

.card.flipped::before {
  opacity: 0;
}

.card img {
  opacity: 0;
}

.card.flipped img {
  opacity: 1;
}



  </style>
  
  <div>
	<h1>Jogo da Memória</h1>
	<div class="button-container">
	  <button on:click={() => setDifficulty("easy")}>Fácil</button>
	  <button on:click={() => setDifficulty("medium")}>Médio</button>
	  <button on:click={() => setDifficulty("hard")}>Difícil</button>
	</div>
  
	<div class="grid">
	  <!-- svelte-ignore a11y-click-events-have-key-events -->
	  {#each cards as card, index}
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<div class="card {matchedCards.includes(index) ? 'matched' : ''} {flippedCards.includes(index) ? 'flipped' : ''}" on:click={() => flipCard(index)}>
		  {#if flippedCards.includes(index) || matchedCards.includes(index)}
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img src={card} alt="Card Image" />
		  {/if}
		</div>
	  {/each}
	</div>
  
	<div class="stats">
	  <h2>Pontuação: {score}</h2>
	  <h2>Tempo: {timer}s</h2>
	  <h2>Melhor Pontuação: {bestScore}</h2>
	  <h2>Melhor Tempo: {bestTime}s</h2>
	</div>
  </div>
  