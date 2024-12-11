<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App con Service Worker</title>
    <link rel="stylesheet" href="styles.css">
    
</head>
<body>
    <h1>Bienvenido a nuestra App</h1>
    <p>Esta página está optimizada para funcionar offline.</p>
    <img src="images/logo.png" alt="Logo">
    <script src="script.js"></script>
    <title>Planificación de Fiesta</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background: url('') no-repeat center center fixed;
            background-size: cover;
            color: #333;
        }

        img {
            max-width: 200px;
            margin-top: 10px;
            display: none;
        }

        h2 {
            color: #0056b3;
        }

        #resultado {
            font-weight: bold;
            margin-top: 20px;
        }

        .thank-you {
            margin-top: 20px;
            font-size: 1.2em;
            color: #28a745;
        }

        .thank-you-events-mayte {
            margin-top: 20px;
            font-size: 1.2em;
            color: #007bff;
        }

        .btn {
            padding: 10px 20px;
            background-color: #0056b3;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 1em;
        }

        .btn:hover {
            background-color: #003d7a;
        }

        input[type="text"], select {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            font-size: 1em;
        }

        input[type="file"] {
            margin: 10px 0;
        }

        .form-section {
            margin-bottom: 20px;
        }

        .form-section h2 {
            font-size: 1.5em;
        }

        #social-links {
            margin-top: 20px;
        }

        #social-links input {
            width: 80%;
            margin-right: 10px;
        }

        /* Paleta de colores */
        .color-swatch {
            display: inline-block;
            width: 50px;
            height: 50px;
            margin: 5px;
            border: 1px solid #ccc;
            vertical-align: middle;
        }

        .color-label {
            display: inline-block;
            margin-left: 10px;
            vertical-align: middle;
        }
    </style>
    <script>
        function mostrarSeleccion() {
            // Obtener los valores seleccionados
            var tematica = document.getElementById("tematica").value;
            var banquete = document.getElementById("banquete").value;
            var bebida = document.getElementById("bebida").value;
            var postre = document.getElementById("postre").value;
            var musica = document.getElementById("musica").value;

            // Mostrar el mensaje de confirmación
            var confirmacion = "La temática será " + tematica + 
                               ", la bebida " + bebida + 
                               ", el postre " + postre + 
                               ", el banquete " + banquete + 
                               ", y la música " + musica + ".";

            if (confirm(confirmacion + " ¿Es correcto?")) {
                // Mostrar el mensaje final con la selección
                document.getElementById("resultado").innerText = confirmacion;
                document.getElementById("thank-you-message").style.display = "block";
                document.getElementById("thank-you-events-mayte").style.display = "block";
            } else {
                alert("Puedes volver a hacer los cambios.");
            }
        }

        function mostrarImagenes(input, imgId) {
            const file = input.files[0];
            const reader = new FileReader();

            reader.onload = function(e) {
                document.getElementById(imgId).src = e.target.result;
                document.getElementById(imgId).style.display = "block";
            }

            reader.readAsDataURL(file);
        }

        function establecerFondo(input) {
            const file = input.files[0];
            const reader = new FileReader();

            reader.onload = function(e) {
                document.body.style.backgroundImage = "url('" + e.target.result + "')";
            }

            reader.readAsDataURL(file);
        }

        function resetearFormulario() {
            window.location.reload();
        }
    </script>
</head>
<body>
    <h1>Planificación de la Fiesta</h1>

    <!-- Ingreso del título y teléfono de la empresa -->
    <h2>Ingresa el título de tu empresa:</h2>
    <input type="text" id="tituloEmpresa" placeholder="Título de la empresa">
    <h2>Ingresa el teléfono celular de la empresa:</h2>
    <input type="text" id="telefonoEmpresa" placeholder="Teléfono de la empresa">

    <!-- Carga de portada como fondo -->
    <h2>Subir fondo de pantalla:</h2>
    <input type="file" id="portada" accept="image/*" onchange="establecerFondo(this)">

    <!-- Formulario de datos de contacto del usuario -->
    <h2>Datos de contacto del usuario:</h2>
    <input type="text" id="nombreUsuario" placeholder="Tu nombre">
    <input type="text" id="telefonoUsuario" placeholder="Tu teléfono">
    
    <!-- Selección de Temática -->
    <h2>Elige la temática de la fiesta:</h2>
    <form onsubmit="event.preventDefault(); mostrarSeleccion();">
        <label for="tematica">Temática:</label>
        <select id="tematica" name="tematica">
            <option value="Halloween">Halloween</option>
            <option value="Navidad">Navidad</option>
            <option value="Verano">Fiesta de Verano</option>
            <option value="Fantasía">Fantasía</option>
            <option value="Elegante">Elegante</option>
            <option value="Boda">Boda</option>
            <option value="Fiesta Infantil">Fiesta Infantil</option>
            <option value="Graduación Escolar">Graduación Escolar</option>
            <option value="Bautizo">Bautizo</option>
            <option value="Granja">Granja</option>
            <option value="SuperHéroes">SuperHéroes</option>
            <option value="Paw Patrol">Paw Patrol</option>
            <option value="Marvel">Marvel</option>
            <option value="Tinkerbell">Tinkerbell</option>
            <option value="Mario Bros">Mario Bros</option>
            <option value="Princesita Sofia">Princesita Sofia</option>
            <option value="Shrek ">Shrek</option>
            <option value="Piratas Del Caribe">Piratas Del Caribe</option>
            <option value="Tortugas Ninjas">Tortugas Ninjas</option>
        </select>
        <input type="file" id="imgTematica" accept="image/*" onchange="mostrarImagenes(this, 'imgTematicaPreview')">
        <img id="imgTematicaPreview">

        <!-- Selección de Banquete -->
        <h2>Elige el banquete:</h2>
        <label for="banquete">Banquete:</label>
        <select id="banquete" name="banquete">
            <option value="Barbacoa">Barbacoa</option>
            <option value="Buffet">Buffet</option>
            <option value="Vegetariano">Vegetariano</option>
            <option value="Mariscos">Mariscos</option>
            <option value="Carnitas">Carnitas</option>
            <option value="Mole">Mole</option>
            <option value="Pechuga de Pollo">Pechuga de Pollo</option>
            <option value="Nugetts de Pollo">Nugetts de Pollo</option>
            <option value="Pizza">Pizza </option>
        </select>
        <input type="file" id="imgBanquete" accept="image/*" onchange="mostrarImagenes(this, 'imgBanquetePreview')">
        <img id="imgBanquetePreview">

        <!-- Selección de Bebida -->
        <h2>Elige la bebida:</h2>
        <label for="bebida">Bebida:</label>
        <select id="bebida" name="bebida">
            <option value="Vino">Vino</option>
            <option value="Refrescos">Refrescos</option>
            <option value="Cerveza">Cerveza</option>
            <option value="Cócteles">Cócteles</option>
            <option value="Agua">Agua</option>
            <option value="Agua De Sabor">Agua de Sabor</option>
        </select>
        <input type="file" id="imgBebida" accept="image/*" onchange="mostrarImagenes(this, 'imgBebidaPreview')">
        <img id="imgBebidaPreview">

        <!-- Selección de Postre -->
        <h2>Elige el postre:</h2>
        <label for="postre">Postre:</label>
        <select id="postre" name="postre">
            <option value="Pastel">Pastel</option>
            <option value="Helado">Helado</option>
            <option value="Cheesecake">Cheesecake</option>
            <option value="Flan">Flan</option>
            <option value="Cupcakes">Cupcakes</option>
            <option value="Pay">Pay</option>
        </select>
        <input type="file" id="imgPostre" accept="image/*" onchange="mostrarImagenes(this, 'imgPostrePreview')">
        <img id="imgPostrePreview">

        <!-- Selección de Música -->
        <h2>Elige la música:</h2>
        <label for="musica">Música:</label>
        <select id="musica" name="musica">
            <option value="DJ">DJ</option>
            <option value="Banda">Banda</option>
            <option value="Ñorteño ">Ñorteño</option>
            <option value="Sonidero  ">Sonidero</option>
            <option value="Norteño Banda">Norteño Banda</option>
            <option value="Conjunto Musical">Conjunto Musical</option>
        </select>

    </select>
        <input type="file" id="imgMusica" accept="image/*" onchange="mostrarImagenes(this, 'imgMusicaPreview')">
        <img id="imgMusicaPreview">

        <!-- Botón de confirmación -->
        <br><br>
        <button type="button" class="btn" onclick="mostrarSeleccion()">Confirmar selección</button>
    </form>

    <!-- Resultado -->
    <div id="resultado"></div>
    <div id="thank-you-message" class="thank-you">
        ¡Gracias por tu selección!
    </div>
    <div id="thank-you-events-mayte" class="thank-you-events-mayte">
        ¡Gracias de nuevo por elegir Eventos Mayte para organizar tu fiesta!
    </div>

    <!-- Enlaces de redes sociales -->
    <div id="social-links">
        <h2>Enlaces de redes sociales:</h2>
        <input type="text" id="facebook" placeholder="Enlace a Facebook">
        <input type="text" id="instagram" placeholder="Enlace a Instagram">
        <input type="text" id="twitter" placeholder="Enlace a Twitter">
        <input type="text" id="whatsapp" placeholder="Enlace a WhatsApp">
    </div>

    <!-- Paleta de colores -->
    <h2>Selecciona los colores para tu evento:</h2>
    <div class="color-swatch" style="background-color: #ff5733;"></div>
    <div class="color-label">#ff5733</div>
    <div class="color-swatch" style="background-color: #33c1ff;"></div>
    <div class="color-label">#33c1ff</div>
    <div class="color-swatch" style="background-color: #ff33d4;"></div>
    <div class="color-label">#ff33d4</div>
    <div class="color-swatch" style="background-color: #8aff33;"></div>
    <div class="color-label">#8aff33</div>
    <div class="color-swatch" style="background-color: #ffb833;"></div>
    <div class="color-label">#ffb833</div>

    
    <!-- Botón para resetear -->
    <div class="color-and-button">
        <button type="button" class="btn" onclick="resetearFormulario()">Resetear formulario</button>
    </div>
    </body>
</html>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App con Service Worker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #0056b3;
        }
        p {
            font-size: 1.2em;
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Bienvenido a Eventos Mayte</h1>
    <p>Esta página está optimizada para funcionar incluso sin conexión.</p>
    <script>
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/service-worker.js')
                .then((registration) => {
                    console.log('Service Worker registrado correctamente:', registration.scope);
                })
                .catch((error) => {
                    console.error('Error al registrar el Service Worker:', error);
                });
        }
    </script>
</body>
</html>
// Nombre del caché
const CACHE_NAME = 'eventos-mayte-v1';

// Archivos a cachear
const FILES_TO_CACHE = [
    '/',          // El archivo index.html
    '/index.html' // El mismo archivo index.html por redundancia
];

// Evento de instalación: Cachear recursos esenciales
self.addEventListener('install', (event) => {
    event.waitUntil(
        caches.open(CACHE_NAME).then((cache) => {
            console.log('Archivos cacheados correctamente.');
            return cache.addAll(FILES_TO_CACHE);
        })
    );
    self.skipWaiting(); // Activa el SW inmediatamente
});

// Evento de activación: Limpiar cachés antiguas
self.addEventListener('activate', (event) => {
    event.waitUntil(
        caches.keys().then((cacheNames) => {
            return Promise.all(
                cacheNames.map((cache) => {
                    if (cache !== CACHE_NAME) {
                        console.log('Eliminando caché antigua:', cache);
                        return caches.delete(cache);
                    }
                })
            );
        })
    );
    self.clients.claim(); // Reclama el control de los clientes activos
});

// Evento fetch: Estrategia Cache First con fallback a red
self.addEventListener('fetch', (event) => {
    event.respondWith(
        caches.match(event.request).then((cachedResponse) => {
            // Devuelve desde caché si existe
            if (cachedResponse) {
                return cachedResponse;
            }
            // Si no está en caché, busca en la red
            return fetch(event.request).catch(() => {
                // En caso de error de red, muestra un mensaje por consola
                console.error('Error al buscar en red: ', event.request.url);
            });
        })
    );
});
