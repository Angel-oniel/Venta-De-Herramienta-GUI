<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Venta de Herramientas - Ferretería Online</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        header {
            text-align: center;
            padding: 20px;
            background-color: #007bff; /* Cambiado a azul */
            color: white;
        }
        .auth-container {
            display: flex;
            justify-content: center;
            margin-top: 30px;
            flex-wrap: wrap;
        }
        .auth-form {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            margin: 10px;
            transition: transform 0.2s;
        }
        .auth-form:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
        }
        .menu {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            margin: 20px 0;
            display: none; /* Ocultar menú por defecto */
        }
        .menu-item {
            background: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin: 10px;
            padding: 15px;
            width: 200px;
            text-align: center;
            transition: transform 0.3s;
        }
        .menu-item:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
        }
        img {
            width: 100%;
            border-radius: 8px;
        }
        button {
            padding: 10px 15px;
            margin-top: 10px;
            border: none;
            border-radius: 5px;
            background-color: #28a745;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #218838;
        }
        footer {
            text-align: center;
            margin-top: 20px;
            padding: 10px;
            background-color: #007bff; /* Cambiado a azul */
            color: white;
        }
        .hidden {
            display: none;
        }
        .menu h2 {
            width: 100%;
            text-align: center;
        }
        .cart {
            margin-top: 20px;
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .cart-item {
            display: flex;
            justify-content: space-between;
            margin: 5px 0;
        }
        .user-info {
            margin-top: 10px;
            font-size: 1.2em;
            color: white;
        }
        .about-section, .contact-section {
            margin-top: 30px;
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .loader {
            display: none;
            margin: 20px auto;
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 4px solid #007bff; /* Cambiado a azul */
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .login-feedback {
            color: red;
            margin-top: 10px;
        }
        .button-container {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }
        .input-group {
            margin-bottom: 15px;
        }
        .input-group input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            transition: border-color 0.3s;
        }
        .input-group input:focus {
            border-color: #007bff; /* Cambiado a azul */
        }
        .forgot-password {
            text-align: right;
            font-size: 0.9em;
            color: #007bff; /* Cambiado a azul */
            cursor: pointer;
        }
        .forgot-password:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

<header>
    <h1>Ferretería Online</h1>
    <p>¡Las mejores herramientas a un clic de distancia!</p>
    <div class="user-info" id="userInfo"></div>
</header>

<div class="auth-container">
    <div class="auth-form">
        <h2>Registro</h2>
        <div class="loader" id="loader"></div>
        <form id="registerForm" onsubmit="registrarUsuario(event)">
            <div class="input-group">
                <input type="text" id="regUsername" placeholder="Nombre de usuario" required>
            </div>
            <div class="input-group">
                <input type="password" id="regPassword" placeholder="Contraseña" required>
            </div>
            <div class="button-container">
                <button type="submit">Registrarse</button>
            </div>
        </form>
    </div>
    <div class="auth-form">
        <h2>Login</h2>
        <form id="loginForm" onsubmit="loginUsuario(event)">
            <div class="input-group">
                <input type="text" id="loginUsername" placeholder="Nombre de usuario" required>
            </div>
            <div class="input-group">
                <input type="password" id="loginPassword" placeholder="Contraseña" required>
            </div>
            <div class="forgot-password" onclick="mostrarRecuperar()">¿Olvidaste tu contraseña?</div>
            <div class="button-container">
                <button type="submit">Iniciar sesión</button>
            </div>
        </form>
        <div id="loginFeedback" class="login-feedback"></div>
        <div id="recuperarForm" class="hidden">
            <input type="email" id="recuperarEmail" placeholder="Tu correo" required>
            <button onclick="recuperarContrasena()">Recuperar</button>
            <div id="recuperarFeedback" class="login-feedback"></div>
        </div>
    </div>
</div>

<button onclick="toggleMenu()" id="menuButton" class="hidden">Ver Menú</button>

<div class="menu" id="menu">
    <h2>Menú</h2>
    <div class="menu-item">
        <img src="https://imgs.search.brave.com/j_Z0J-3sRNF6bdicJsHu7cnJXzNPbXbgjQU2JfUkpII/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9tLm1l/ZGlhLWFtYXpvbi5j/b20vaW1hZ2VzL0kv/NzE4R21qaXdiQUwu/anBn" alt="Martillo">
        <h3>Martillo</h3>
        <p>Martillo de acero inoxidable.</p>
        <p><strong>Precio: $10.00</strong></p>
        <button onclick="agregarAlCarrito('Martillo', 10)">Agregar al carrito</button>
    </div>
    <div class="menu-item">
        <img src="https://imgs.search.brave.com/u2KArDm26j5GsycbW9H83jGhx7f3HVWNzrDtztF2wOc/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly93d3cu/d3VydGguY29tLmFy/L2ltZy9wcm9kdWN0/b3MvNDgxNDktY2gt/ZGVzdG9ybmlsbGFk/b3ItdHgxMC1yZWQt/bGluZS5qcGc" alt="Destornillador">
        <h3>Destornillador</h3>
        <p>Destornillador de precisión.</p>
        <p><strong>Precio: $6.00</strong></p>
        <button onclick="agregarAlCarrito('Destornillador', 6)">Agregar al carrito</button>
    </div>
    <div class="menu-item">
        <img src="https://imgs.search.brave.com/5n1nZNoUjS3_o0fWyTNXze8xQTGwQBLJjJpP5-MMMZU/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly93d3cu/b2Nob2EuY29tLmRv/L21lZGlhL3Byb2R1/Y3QvMi0yOC0zMTAy/Mi5qcGc" alt="Alicate">
        <h3>Alicate</h3>
        <p>Alicate multifuncional.</p>
        <p><strong>Precio: $7.00</strong></p>
        <button onclick="agregarAlCarrito('Alicate', 7)">Agregar al carrito</button>
    </div>
    <div class="menu-item">
        <img src="https://imgs.search.brave.com/s2wW6b7QbhpoYeKeJS9Z9o4LNt4-TwGcit37Q78CxbI/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly93d3cu/ZGVtYXF1aW5hc3lo/ZXJyYW1pZW50YXMu/Y29tL3dwLWNvbnRl/bnQvdXBsb2Fkcy8y/MDE3LzAyL0JhaGNv/LUFyY28tZGUtc2ll/cnJhLWp1bmlvci5q/cGc" alt="Sierra">
        <h3>Sierra</h3>
        <p>Sierra circular eléctrica de 1350W.</p>
        <p><strong>Precio: $9.00</strong></p>
        <button onclick="agregarAlCarrito('Sierra', 9)">Agregar al carrito</button>
    </div>
    <div class="menu-item">
        <img src="https://imgs.search.brave.com/PSEPt5uPjKGkEaU93ig6coNBwwG3vdd14F_47trcsCo/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9kb2pp/dzJtOXR2djA5LmNs/b3VkZnJvbnQubmV0/LzM5OTk5L3Byb2R1/Y3QvTV9mbGc5MzE2/NzUyMC5qcGc_MTcm/dGltZT0xNzI1OTkz/NjEx" alt="Cinta métrica">
        <h3>Cinta métrica</h3>
        <p>Cinta métrica de 5 metros.</p>
        <p><strong>Precio: $8.00</strong></p>
        <button onclick="agregarAlCarrito('Cinta métrica', 8)">Agregar al carrito</button>
    </div>
</div>

<div class="cart hidden" id="cart">
    <h2>Carrito de Compras</h2>
    <div id="cartItems"></div>
    <p id="totalPrice"><strong>Total: $0.00</strong></p>
    <button onclick="finalizarCompra()">Finalizar Compra</button>
</div>

<div class="about-section">
    <h2>Sobre Nosotros</h2>
    <p>En Ferretería Online, nos apasiona ofrecer las mejores herramientas para todos tus proyectos. Desde 2020, hemos estado brindando productos de alta calidad a precios competitivos. ¡Explora nuestro catálogo y encuentra lo que necesitas!</p>
</div>

<div class="contact-section">
    <h2>Contacto</h2>
    <p>Teléfono: (555) 123-4567</p>
    <p>Email: contacto@ferreteriaonline.com</p>
    <p>Dirección: Calle Falsa 123, Ciudad Imaginaria, País Soñado</p>
    <form onsubmit="enviarFormulario(event)">
        <input type="text" placeholder="Tu nombre" required>
        <input type="email" placeholder="Tu correo" required>
        <textarea placeholder="Tu mensaje" required></textarea>
        <button type="submit">Enviar</button>
    </form>
</div>

<footer>
    <p>&copy; 2024 Ferretería Online. Todos los derechos reservados.</p>
</footer>

<script>
    const usuarios = JSON.parse(localStorage.getItem('usuarios')) || [];
    const carrito = [];
    let usuarioActual = null;

    function registrarUsuario(event) {
        event.preventDefault();
        document.getElementById('loader').style.display = 'block'; // Mostrar el loader
        const username = document.getElementById('regUsername').value;
        const password = document.getElementById('regPassword').value;

        setTimeout(() => { // Simular una carga
            if (usuarios.some(user => user.username === username)) {
                alert('El nombre de usuario ya está en uso.');
                document.getElementById('loader').style.display = 'none'; // Ocultar el loader
                return;
            }

            usuarios.push({ username, password });
            localStorage.setItem('usuarios', JSON.stringify(usuarios));
            alert('Usuario registrado exitosamente.');
            document.getElementById('registerForm').reset();
            document.getElementById('loader').style.display = 'none'; // Ocultar el loader
        }, 2000);
    }

    function loginUsuario(event) {
        event.preventDefault();
        const username = document.getElementById('loginUsername').value;
        const password = document.getElementById('loginPassword').value;
        const feedback = document.getElementById('loginFeedback');

        const user = usuarios.find(user => user.username === username && user.password === password);
        if (user) {
            usuarioActual = user.username;
            document.getElementById('userInfo').innerText = `Usuario conectado: ${usuarioActual}`;
            alert('Inicio de sesión exitoso.');
            feedback.innerText = ''; // Limpiar mensajes de error
            document.getElementById('loginForm').reset();
            document.getElementById('menu').style.display = 'flex'; // Mostrar menú
            document.getElementById('menuButton').style.display = 'block'; // Mostrar botón de menú
            document.getElementById('cart').classList.remove('hidden'); // Mostrar carrito
        } else {
            feedback.innerText = 'Nombre de usuario o contraseña incorrectos.';
        }
    }

    function mostrarRecuperar() {
        document.getElementById('recuperarForm').classList.toggle('hidden');
    }

    function recuperarContrasena() {
        const email = document.getElementById('recuperarEmail').value;
        const feedback = document.getElementById('recuperarFeedback');

        setTimeout(() => {
            feedback.innerText = 'Si el correo está registrado, se enviará un enlace para recuperar la contraseña.';
            document.getElementById('recuperarEmail').value = ''; // Limpiar campo
        }, 1000);
    }

    function agregarAlCarrito(item, precio) {
        carrito.push({ item, precio });
        actualizarCarrito();
        alert(item + ' ha sido agregado al carrito.');
    }

    function actualizarCarrito() {
        const cartItemsContainer = document.getElementById('cartItems');
        cartItemsContainer.innerHTML = '';

        let total = 0;
        carrito.forEach((producto, index) => {
            total += producto.precio;
            cartItemsContainer.innerHTML += `<div class="cart-item">
                ${producto.item} - $${producto.precio.toFixed(2)}
                <button onclick="eliminarDelCarrito(${index})">Eliminar</button>
            </div>`;
        });

        document.getElementById('totalPrice').innerHTML = `<strong>Total: $${total.toFixed(2)}</strong>`;
        document.getElementById('cart').classList.remove('hidden');
    }

    function eliminarDelCarrito(index) {
        carrito.splice(index, 1);
        actualizarCarrito();
    }

    function finalizarCompra() {
        alert('Compra finalizada. ¡Gracias por tu pedido!');
        carrito.length = 0; // Vaciar carrito
        actualizarCarrito();
    }

    function enviarFormulario(event) {
        event.preventDefault();
        alert('Mensaje enviado. Nos pondremos en contacto contigo pronto.');
        document.querySelector('.contact-section form').reset();
    }

    function toggleMenu() {
        const menu = document.getElementById('menu');
        menu.style.display = menu.style.display === 'flex' ? 'none' : 'flex';
    }
</script>
</body>
</html>
