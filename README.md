<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Reemplazo de Palabras</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
      margin-bottom: 20px;
    }
    .container {
      display: flex;
      gap: 20px;
      margin-bottom: 20px;
    }

    .botonera {
      display: flex;
      justify-content: flex-end; /* Los manda a la derecha */
      gap: 10px; /* Espacio entre ellos (ajustalo como quieras) */
      margin-bottom: 20px;
    
    }

    textarea {
      width: 100%;
      height: 180px;
      padding: 10px;
      resize: vertical;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 14px;
    }
    #resultado {
      height: 260px;
      background: #fff;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      border: none;
      border-radius: 6px;
      background: #da25a3;
      color: #fff;
      cursor: pointer;
    }
    button:hover {
      background: #9e35c8;
    }
      .tooltip {
    position: relative;
    display: inline-block;
    cursor: pointer;
  }

  .tooltip .tooltip-text {
    visibility: hidden;
    width: 140px;
    background-color: #333;
    color: #fff;
    text-align: center;
    padding: 6px;
    border-radius: 6px;

    position: absolute;
    z-index: 1;
    bottom: 125%; 
    left: 50%;
    transform: translateX(-50%);

    opacity: 0;
    transition: opacity 0.25s;
  }

  .tooltip:hover .tooltip-text {
    visibility: visible;
    opacity: 1;
  }

  </style>
</head>
<body>
  <h1>Reemplazo de Palabras</h1>

  <div class="container">
    <textarea id="textoOriginal" placeholder="Texto original..."></textarea>
  </div>
  
  <div class="botonera"> 
    <button  title="Borra el texto que aparece en Texto original" onclick="limpiarCampos()">Limpiar campos</button>
  </div>
 
<div class="container">
  <textarea id="buscar" placeholder="Palabras a buscar (una por línea)"></textarea>
  <textarea id="reemplazar" placeholder="Palabras reemplazo (una por línea)"></textarea>
  </div>
 
  <textarea id="resultado" placeholder="Resultado..." readonly></textarea>
  
  <div class="botonera">
    <button onclick="procesar()">Reemplazar</button>
    <button onclick="copiarResultado()">Copiar resultado</button>
  </div>

  <script>
    function procesar() {
      const original = document.getElementById('textoOriginal').value;
      const buscar = document.getElementById('buscar').value.split(/\r?\n/);
      const reemplazar = document.getElementById('reemplazar').value.split(/\r?\n/);

      let resultado = original;

      for (let i = 0; i < buscar.length; i++) {
        const palabraBuscar = buscar[i].trim();
        const palabraReemplazo = reemplazar[i] ? reemplazar[i].trim() : '';
        if (palabraBuscar) {
          const regex = new RegExp(palabraBuscar.replace(/[.*+?^${}()|[\]\\]/g, '\\$&'), 'g');
          resultado = resultado.replace(regex, palabraReemplazo);
        }
      }

      document.getElementById('resultado').value = resultado;
    }
      function limpiarCampos() {
      document.getElementById('textoOriginal').value = '';
      document.getElementById('resultado').value = '';
    }

    function copiarResultado() {
      const resultado = document.getElementById('resultado');
      resultado.select();
      document.execCommand('copy');
      alert('Texto copiado al portapapeles');
    }
  </script>
</body>
</html>
