let drone;
let seeds = [];
let solarPanels = [];
let trees = [];
let techHubs = [];
let score = 0;

function setup() {
  createCanvas(800, 400);
  drone = new Drone();

  // Gerar sementes no campo
  for (let i = 0; i < 5; i++) {
    seeds.push(new Resource(random(50, 300), random(50, 350), 'seed'));
  }

  // Gerar painéis solares na cidade
  for (let i = 0; i < 5; i++) {
    solarPanels.push(new Resource(random(500, 750), random(50, 350), 'solar'));
  }
}

function draw() {
  background(220);

  drawBackground();
  drone.update();
  drone.display();

  // Mostrar e coletar sementes
  for (let i = seeds.length - 1; i >= 0; i--) {
    seeds[i].display();
    if (drone.collect(seeds[i])) {
      seeds.splice(i, 1);
    }
  }

  // Mostrar e coletar painéis
  for (let i = solarPanels.length - 1; i >= 0; i--) {
    solarPanels[i].display();
    if (drone.collect(solarPanels[i])) {
      solarPanels.splice(i, 1);
    }
  }

  // Mostrar árvores plantadas na cidade
  for (let tree of trees) {
    tree.display();
  }

  // Mostrar hubs tecnológicos no campo
  for (let hub of techHubs) {
    hub.display();
  }

  fill(0);
  textSize(16);
  text(`Pontuação: ${score}`, 10, 20);
}

function keyPressed() {
  if (keyCode === 32) { // Espaço para plantar ou instalar
    if (drone.x > width / 2 && drone.holding === 'seed') {
      // Plantar na cidade
      trees.push(new Drop(drone.x, drone.y, 'tree'));
      score += 10;
      drone.holding = null;
    } else if (drone.x < width / 2 && drone.holding === 'solar') {
      // Instalar painel no campo
      techHubs.push(new Drop(drone.x, drone.y, 'hub'));
      score += 10;
      drone.holding = null;
    }
  }
}

function drawBackground() {
  // Campo
  noStroke();
  fill(100, 200, 100);
  rect(0, 0, width / 2, height);

  // Cidade
  fill(180);
  rect(width / 2, 0, width / 2, height);

  // Divisão
  stroke(0);
  line(width / 2, 0, width / 2, height);

  // Prédios
  for (let x = width / 2 + 20; x < width; x += 60) {
    fill(120);
    rect(x, height - 100, 40, 100);
  }
}

// Classe do Dron
class Drone {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.speed = 3;
    this.holding = null;
  }

  update() {
    if (keyIsDown(LEFT_ARROW)) this.x -= this.speed;
    if (keyIsDown(RIGHT_ARROW)) this.x += this.speed;
    if (keyIsDown(UP_ARROW)) this.y -= this.speed;
    if (keyIsDown(DOWN_ARROW)) this.y += this.speed;

    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }

  display() {
    fill(80, 80, 200);
    ellipse(this.x, this.y, 30, 30);
    if (this.holding) {
      fill(this.holding === 'seed' ? 'green' : 'orange');
      ellipse(this.x, this.y - 20, 10, 10);
    }
  }

  collect(resource) {
    let d = dist(this.x, this.y, resource.x, resource.y);
    if (d < 20 && !this.holding) {
      this.holding = resource.type;
      return true;
    }
    return false;
  }
}

// Classe para sementes e painéis
class Resource {
  constructor(x, y, type) {
2
let seeds = [];
    this.x = x;
    this.y = y;
    this.type = type;
  }

  display() {
    fill(this.type === 'seed' ? 'green' : 'orange');
    ellipse(this.x, this.y, 12, 12);
  }
}

// Classe para árvores e hubs tecnológicos
class Drop {
  constructor(x, y, kind) {
    this.x = x;
    this.y = y;
    this.kind = kind;
  }

  display() {
    if (this.kind === 'tree') {
      fill('green');
      triangle(this.x - 10, this.y, this.x + 10, this.y, this.x, this.y - 20);
    } else {
      fill('blue');
      rect(this.x - 5, this.y - 5, 10, 10);
    }
  }
}
