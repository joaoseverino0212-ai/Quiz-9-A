# Quiz-9-A
Quiz 9°A
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Profissional - 9°A</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #6a0dad, #000000, #ffffff);
    color: #fff;
    text-align: center;
    margin: 0;
    padding: 0;
    animation: bgShift 15s infinite alternate;
  }

  @keyframes bgShift {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
  }

  .container {
    max-width: 700px;
    margin: 50px auto;
    background: linear-gradient(to bottom, #7b1fa2, #000000, #ffffff);
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0 25px #4a0072;
    overflow: hidden;
    position: relative;
  }

  h1, h2 {
    color: #fff;
    text-shadow: 0 0 10px #000;
  }

  .options button {
    display: block;
    width: 100%;
    margin: 12px 0;
    padding: 15px;
    font-size: 16px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    background: linear-gradient(90deg, #9c27b0, #000000, #ffffff);
    color: #fff;
    transition: transform 0.3s, box-shadow 0.3s;
    box-shadow: 0 0 10px #9c27b0, 0 0 20px #000, 0 0 30px #fff;
  }

  .options button:hover {
    transform: scale(1.08);
    box-shadow: 0 0 15px #9c27b0, 0 0 25px #000, 0 0 35px #fff;
  }

  .result {
    font-size: 20px;
    margin-top: 20px;
    line-height: 1.5;
  }

  .result-image {
    width: 60%;
    max-width: 300px;
    margin-top: 20px;
    border-radius: 15px;
    animation: pulse 2s infinite;
    box-shadow: 0 0 15px #000, 0 0 25px #9c27b0, 0 0 35px #fff;
  }

  @keyframes pulse {
    0% { transform: scale(1); box-shadow: 0 0 15px #000, 0 0 25px #9c27b0, 0 0 35px #fff; }
    50% { transform: scale(1.05); box-shadow: 0 0 25px #000, 0 0 35px #9c27b0, 0 0 45px #fff; }
    100% { transform: scale(1); box-shadow: 0 0 15px #000, 0 0 25px #9c27b0, 0 0 35px #fff; }
  }

  /* Fade animation para perguntas */
  .fade {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s, transform 0.6s;
  }
  .fade.show {
    opacity: 1;
    transform: translateY(0);
  }
</style>
</head>
<body>
<div class="container">
  <h1>Quiz Profissional - 9°A</h1>
  <div id="quiz" class="fade"></div>
</div>

<script>
const quizData = [
  { question: "O que você mais gosta de fazer no dia a dia?", options: ["Resolver problemas de lógica ou mexer em tecnologia","Conversar, ajudar e ouvir pessoas","Criar coisas novas, desenhar ou inventar histórias","Cuidar da saúde e do bem-estar","Fazer experimentos, pesquisar e descobrir coisas novas"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Qual ambiente de trabalho você prefere?", options: ["Escritório moderno com computadores","Lugar cheio de pessoas para conversar","Ateliê ou palco criativo","Hospital, clínica ou academia","Laboratório ou centro de pesquisas"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Se você fosse participar de uma feira escolar, em qual parte gostaria de estar?", options: ["Na organização com planilhas e computadores","Recebendo visitantes e explicando o projeto","Apresentando algo criativo (teatro, cartaz, arte)","Mostrando como algo pode melhorar a saúde","Explicando um experimento científico"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Que tipo de matéria escolar você mais curte?", options: ["Matemática e informática","História e sociologia","Artes e literatura","Biologia e educação física","Química e física"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Como você prefere resolver problemas?", options: ["Usando lógica e raciocínio rápido","Conversando com as pessoas e mediando situações","Criando uma nova forma ou ideia diferente","Encontrando soluções que melhorem a saúde ou bem-estar","Testando hipóteses e experimentando"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Qual dessas frases combina mais com você?", options: ["Adoro mexer com tecnologia.","Gosto de ajudar e liderar pessoas.","Sou cheio(a) de ideias criativas.","Quero cuidar e salvar vidas.","Tenho curiosidade de como as coisas funcionam."], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Qual profissão te parece mais legal?", options: ["Programador(a) ou engenheiro(a)","Psicólogo(a) ou professor(a)","Estilista, designer ou artista","Médico(a), enfermeiro(a) ou nutricionista","Cientista ou pesquisador(a)"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Você gosta mais de trabalhar:", options: ["Com máquinas e computadores","Com pessoas e grupos","Com a criatividade e expressão","Com saúde e bem-estar","Com ciência e descobertas"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Como você gostaria de ser reconhecido(a) no futuro?", options: ["Como alguém que criou soluções tecnológicas","Como alguém que ajudou muitas pessoas","Como alguém criativo e inovador","Como alguém que salvou vidas","Como alguém que fez descobertas científicas"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] },
  { question: "Se fosse para escolher uma missão agora, qual seria?", options: ["Criar um aplicativo novo","Organizar uma campanha social","Produzir uma peça de teatro ou moda","Ajudar alguém doente","Inventar algo no laboratório"], area: ["Tecnológica","Comunicação","Criativa","Saúde","Científica"] }
];

let current = 0;
let scores = { "Tecnológica":0, "Comunicação":0, "Criativa":0, "Saúde":0, "Científica":0 };

function loadQuestion(){
  const quiz = document.getElementById("quiz");
  quiz.classList.remove("show");
  setTimeout(() => {
    if(current < quizData.length){
      const q = quizData[current];
      quiz.innerHTML = `
        <h2>Pergunta ${current+1}: ${q.question}</h2>
        <div class="options">
          ${q.options.map((opt,i)=> `<button onclick="selectOption('${q.area[i]}')">${opt}</button>`).join("")}
        </div>
      `;
    } else { showResult(); }
    quiz.classList.add("show");
  }, 300);
}

function selectOption(area){
  scores[area]++;
  current++;
  loadQuestion();
}

function showResult(){
  const quiz = document.getElementById("quiz");
  let maxArea = Object.keys(scores).reduce((a,b)=> scores[a] > scores[b]? a:b);
  let description = "";
  let resultImage = "";

  switch(maxArea){
    case "Tecnológica": 
      description="Área Tecnológica: Trabalhos com tecnologia, programação e engenharia. Possíveis profissões: programador(a), engenheiro(a), desenvolvedor(a)."; 
      resultImage="https://upload.wikimedia.org/wikipedia/commons/3/35/Computer_icon.png"; 
      break;
    case "Comunicação": 
      description="Área de Comunicação e Atendimento: Trabalhar com pessoas, ensino e suporte. Possíveis profissões: professor(a), psicólogo(a), assistente social."; 
      resultImage="https://upload.wikimedia.org/wikipedia/commons/2/2c/Communication_icon.png"; 
      break;
    case "Criativa": 
      description="Área Criativa e Artística: Explorar arte, moda e design. Possíveis profissões: estilista, designer, artista."; 
      resultImage="https://upload.wikimedia.org/wikipedia/commons/6/6d/Creativity_icon.png"; 
      break;
    case "Saúde": 
      description="Área da Saúde e Bem-Estar: Cuidar de pessoas e promover saúde. Possíveis profissões: médico(a), enfermeiro(a), nutricionista."; 
      resultImage="https://upload.wikimedia.org/wikipedia/commons/3/35/Medical_icon.png"; 
      break;
    case "Científica": 
      description="Área Científica e de Laboratórios: Pesquisar e descobrir novas informações. Possíveis profissões: cientista, pesquisador(a), químico(a)."; 
      resultImage="https://upload.wikimedia.org/wikipedia/commons/8/85/Einstein_Emoji.png"; 
      break;
  }

  quiz.classList.remove("show");
  setTimeout(() => {
    quiz.innerHTML = `
      <h2>Seu resultado: ${maxArea}</h2>
      <p class="result">${description}</p>
      <img src="${resultImage}" alt="${maxArea}" class="result-image">
      <p class="result"><strong>Amostra científica da Escola Estadual Dr. Manoel Dantas dos alunos do 9°A: Emilly Camilo, Sara Geovana, Melyssa Gabrielle, Ana Clara e Severino Pedro</strong></p>
    `;
    quiz.classList.add("show");
  }, 300);
}

// Iniciar o quiz
loadQuestion();
</script>
</body>
</html>
