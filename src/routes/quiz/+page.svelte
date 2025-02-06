<script>
  
    let respostas = [];

    let quizConcluido = false;
    
    
    let perguntas = [
      {
        id: 1,
        pergunta: "Qual sua cor favorita?",
        opcoes: ["Rosa", "Azul", "Preto", "Vermelho", "Verde", "Roxo", "Laranja", "Outro/Todas", "Nenhuma"],
        imagens: {
          Rosa: "babygirl.jpg",
          Azul: "newyork.jpg",
          Preto: "party.jpg",
          Vermelho: "savage.jpg",
          Verde: "brat.jpg",
          Roxo: "lido.jpg",
          Laranja: "angel.jpg",
          "Outro/Todas": "cocaine.jpg",
          Nenhuma: "toxic.jpg"
        }
      },
      {
        id: 2,
        pergunta: "Qual desses artistas você prefere?",
        opcoes: ["Lana Del Rey", "Taylor Swift", "The Weeknd", "The Smiths", "Outro", "Odeio todos os da lista"],
        imagens: {
          "Lana Del Rey": "daddy.jpg", 
          "Taylor Swift": "tropic.jpg",
          "The Weeknd": "breed.jpg" , 
          "The Smiths": "princess.jpg" ,
          Outro:"candyfloss.jpg", 
          "Odeio todos os da lista": "many.jpg"
        }
      },
      {
        id: 3,
        pergunta: "Você é introvertido, extrovertido ou ambivertido?",
        opcoes: ["Introvertido", "Extrovertido", "Ambivertido"],
        imagens: {
          Introvertido: "illuminate.jpg", 
          Extrovertido:  "glitz.jpg", 
          Ambivertido: "gold.jpg" 
        }
      },
      {
        id: 4,
        pergunta: "Qual estação do ano você prefere?",
        opcoes: ["Verão", "Inverno", "Outono", "Primavera"],
        imagens: {
          Verão: "moonshine.jpg", 
          Inverno: "night.jpg" , 
          Outono: "cairo.jpg" ,
          Primavera: "paris.jpg"
        }
      },
      {
        id: 5,
        pergunta: "Qual desses tipos de cores você prefere?",
        opcoes: ["Vibrantes", "Neutras"],
        imagens: {
          Vibrantes: "desire.jpg", 
          Neutras: "whore.jpg" 
        }
      },
      {
        id: 6,
        pergunta: "Costuma se maquiar ou não?",
        opcoes: ["Sim", "Não"],
        imagens: {
          Sim: "flight.jpg" , 
          Não: "eyes.jpg"
        }
      }
    ];




    function responder(idPergunta, escolha) {
      respostas[idPergunta - 1] = escolha; 
    }
    
    
    function verificarConclusao() {
      return respostas.length === perguntas.length && !respostas.includes(undefined);
    }
    
    
    function gerarPaleta() {
      return respostas.map((resposta, index) => {
        const pergunta = perguntas[index];
        return pergunta.imagens[resposta] || "https://via.placeholder.com/100"; 
      }).slice(0, 6); 
    }
  

    function reiniciarQuiz() {
      respostas = [];
      quizConcluido = false;
    }
  </script>
  
  
  <style>
    

    .quiz-container {
      margin: 20px;
      font-family: Arial, sans-serif;
    }
  
   
    .titulo {
      text-align: center; 
      font-size: 24px;
      margin-bottom: 20px;
    }
  
    .pergunta {
      color: black;
      margin-bottom: 20px;
      font-size: medium;
    }
  
    .opcoes {
      color: black;
      display: flex;
      gap: 10px;
    }
  
    .opcao {
      padding: 10px 15px;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s, border-color 0.3s;
    }
  
    .opcao:hover {
      background-color: #f0f0f0;
      border-color: #bbb;
    }
  
    .paleta {
  display: grid;
  grid-template-columns: repeat(2, 1fr); 
  gap: 0; 
  margin-top: 0;
  padding: 0;
  max-width: 400px;
  margin: 0 auto;
}

.quadradinho {
  width: 100%;
  height: auto; 
  overflow: hidden;
}

.quadradinho img {
  width: 100%;
  height: auto; 
  object-fit: cover; 
}




  
    .btn-reiniciar {
      margin-top: 10px; 
      padding: 10px 15px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
      display: block;
      margin-left: auto;
      margin-right: auto; 
    }
  
    .btn-reiniciar:hover {
      background-color: #0056b3;
    }
  
    .btn-terminar {
      margin-top: 20px;
      padding: 10px 15px;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
  
    .btn-terminar:disabled {
      background-color: #6c757d;
      cursor: not-allowed;
    }
  </style>
  
  <div class="quiz-container">
    <div class="titulo"><p style="color: #d47988;"><b>Descubra a sua paleta!</b></p></div> 
  
    {#each perguntas as pergunta}
      <div class="pergunta">
        <h3>{pergunta.pergunta}</h3>
        <div class="opcoes">
          {#each pergunta.opcoes as opcao}
            <button
              class="opcao"
              on:click={() => responder(pergunta.id, opcao)}
              disabled={respostas[pergunta.id - 1] !== undefined}
            >
              {opcao}
            </button>
          {/each}
        </div>
      </div>
    {/each}
  
    <button
      class="btn-terminar"
      on:click={() => quizConcluido = verificarConclusao()}
      disabled={!verificarConclusao()}
    >
      Terminar
    </button>
  
    {#if quizConcluido}
      <div class="paleta">
        {#each gerarPaleta() as imagem}
          <div class="quadradinho">
            <img src={imagem} alt="Cor da sombra" />
          </div>
        {/each}
      </div>
      <button class="btn-reiniciar" on:click={reiniciarQuiz}>Reiniciar Quiz</button>
    {/if}
  </div>
  
