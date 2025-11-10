# Artify Me

## Description du projet

**Artify Me** est un outil web interactif réalisé avec **p5.js**, qui permet de transformer une image importée selon différents **courants artistiques emblématiques**.  
Chaque style repose sur un principe visuel unique, réinterprété par le code :

- **Impressionnisme** → touches de couleur légères, effet de mouvement et de lumière.  
- **Cubisme** → déstructuration géométrique et fragmentation visuelle.  
- **Pop Art** → aplats saturés, trames et contrastes marqués.  
- **Pointillisme** → composition en points colorés inspirée de la peinture divisionniste.

L’utilisateur peut importer une image, choisir un style, ajuster plusieurs paramètres (taille, densité, opacité, palette), et enregistrer son œuvre finale.

---

## Fonctionnalités principales

- Importation d’image (fichier local ou drag & drop)  
- Sélection du style artistique (Impressionnisme / Cubisme / Pop Art / Pointillisme)  
- Réglages :
  - taille des formes ou points,  
  - densité de rendu,  
  - opacité,  
  - palette de couleurs.  
- Sauvegarde du rendu en image (.png)  
- Option *Randomize* pour générer un résultat aléatoire  
- Bouton *Clear* pour réinitialiser la toile  

---

## Références artistiques et conceptuelles

### Inspirations visuelles :
- **Claude Monet** – pour la lumière et la touche impressionniste  
- **Georges Seurat** – pour le pointillisme et la couleur par fragmentation  
- **Pablo Picasso & Georges Braque** – pour la géométrisation cubiste  
- **Roy Lichtenstein & Andy Warhol** – pour l’esthétique du Pop Art  

### Inspirations techniques :
- *p5.js image manipulation examples*  
- *Generative Art with p5.js* — Matt DesLauriers  
- *The Coding Train* — Daniel Shiffman (tutoriels sur la manipulation d’images et de pixels)  

---

## Snippets de code utilisés

### Import d’image
```js
let img;

function setup() {
  createCanvas(900, 600);
  noLoop();

  const btnImport = createButton('Importer une image');
  btnImport.position(20, 160);
  btnImport.mousePressed(() => {
    const input = createFileInput(handleFile);
    input.elt.click();
  });
}

function handleFile(file) {
  if (file.type === 'image') {
    loadImage(file.data, (loaded) => {
      img = loaded;
      img.resize(800, 0); 
      redraw();
    });
  }
}

```
### Impressionisme
```js
function renderImpressionism() {
  const step = 10; 
  img.loadPixels();
  noStroke();
  for (let y = 0; y < img.height; y += step) {
    for (let x = 0; x < img.width; x += step) {
      const c = img.get(x, y);
      fill(c[0], c[1], c[2], random(120, 180)); 
      const sz = random(6, 12); 
      ellipse(x + random(-4, 4), y + random(-4, 4), sz, sz * 0.8);
    }
  }
}
```
### Cubisme
```js
function renderCubism() {
  const step = 40; 
  img.loadPixels();
  noStroke();
  for (let y = 0; y < img.height; y += step) {
    for (let x = 0; x < img.width; x += step) {
      const c = img.get(x, y);
      fill(c);
      push();
      translate(x, y);
      rotate(radians(random(-10, 10))); 
      rect(0, 0, step, step);
      pop();
    }
  }
}
```
### Pop Art
```js
function renderPopArt() {
  const step = 15; 
  img.loadPixels();
  for (let y = 0; y < img.height; y += step) {
    for (let x = 0; x < img.width; x += step) {
      const c = img.get(x, y);
      const bright = brightness(color(c)); 
      if (bright > 50) {
        fill(255, 0, 0);
      } else {
        fill(0, 0, 255); 
      }
      ellipse(x, y, step, step); 
    }
  }
}
```
### Pointillisme
```js
function renderPointillism() {
  const step = 8; 
  img.loadPixels();
  noStroke();
  for (let y = 0; y < img.height; y += step) {
    for (let x = 0; x < img.width; x += step) {
      const c = img.get(x, y);
      fill(c[0], c[1], c[2], 200);
      const size = random(3, 8);
      circle(x, y, size);
    }
  }
}
```
### Sauvegarde du rendu 
```js
function keyPressed() {
  if (key === 's' || key === 'S') {
    saveCanvas('artifyMe_result', 'png');
  }
}
```