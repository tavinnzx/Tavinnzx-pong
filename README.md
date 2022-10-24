
Jogo Pong tavinnzx

//variaveis da bolinha
  let xBolinha = 275; 
let yBolinha = 185;
let diametro = 22;
let raio = diametro / 2;


//velocidade da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

//variaveis da raquete
let xRaquete = 6;
let yRaquete = 135;
let raqueteComprimento = 9;
let raqueteAltura = 90;

let colidiu = false

//variaveis do oponente 
let xRaqueteOponente = 534;
let yRaqueteOponente = 135;
let velocidadeYOponente ;

//placar do jogo
let meusPontos = 0;
let pontosDoOponente = 0;

//sons do jogo
let raquetada;
let ponto; 
let trilha;

function preload(){
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}

function setup() {
  createCanvas(550, 370);
  trilha.loop();
}

function draw() {
  background(0);
  mostraBolinha();
  movimentoBolinha();
  verificaColisaoBorda(); 
  mostraRaquete(xRaquete,yRaquete);
  movimentaMinhaRaquete();
  verificaColisaoRaquete();
  mostraRaquete(xRaqueteOponente,yRaqueteOponente);
  movimmentoRaqueteOponente();
  verificaColisaoRaqueteBiblioteca(xRaquete,yRaquete);
  verificaColisaoRaqueteBiblioteca(xRaqueteOponente,yRaqueteOponente);
  incluiPlacar();
  marcaPonto();
}
function mostraBolinha(){
  circle(xBolinha,yBolinha,diametro);
}



  
function movimentoBolinha(){
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda(){
  if (xBolinha + raio > width ||
     xBolinha - raio < 0){
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height ||
     yBolinha - raio < 0){
    velocidadeYBolinha *= -1;
  }
}

function mostraRaquete(x,y){
  rect(x,y,raqueteComprimento,
   raqueteAltura);
}

function movimentaMinhaRaquete(){
  if (keyIsDown(UP_ARROW)){
    yRaquete -= 10;
  }
  if (keyIsDown(DOWN_ARROW)){
    yRaquete += 10;
  }
}

function verificaColisaoRaquete(){
  if (xBolinha - raio < xRaquete  + raqueteComprimento && yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio > yRaquete ){
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
}

function movimmentoRaqueteOponente(){
  velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
  yRaqueteOponente += velocidadeYOponente
}

function verificaColisaoRaqueteBiblioteca(x,y){
  colidiu = 
  collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
  if (colidiu){
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
}

function incluiPlacar(){
  stroke(255);
  textAlign(CENTER);
  textSize(17);
  fill(color(255,140,0));
  rect(140,10,40,20);
  fill(255);
  text(meusPontos,160,25);
  fill(color(255,140,0));
  rect(370,10,40,20);
  fill(255);
  text(pontosDoOponente,390,25);
}

function marcaPonto(){
  if (xBolinha > 540){
    meusPontos += 1;
    ponto.play();
  }
  if (xBolinha < 10){
    pontosDoOponente += 1;
    ponto.play();
  }
}



ASS:Tavinnzx
