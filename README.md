# voluntariado-
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Language Exchange Initiative</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: #121212;
            color: #ffffff;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* Header */
        header {
            background-color: #1e1e1e;
            padding: 16px;
            text-align: center;
            border-bottom: 1px solid #2d2d2d;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        header h1 {
            font-size: 1.1rem;
            color: #4da6ff;
            font-weight: 600;
        }

        /* Main Container */
        main {
            flex: 1;
            padding: 20px 16px 80px 16px;
            max-width: 600px;
            margin: 0 auto;
            width: 100%;
        }

        /* Tab Content */
        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Cards Style */
        .card {
            background-color: #1e1e1e;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 16px;
            border: 1px solid #2d2d2d;
        }

        .card h2 {
            font-size: 1.3rem;
            margin-bottom: 8px;
            color: #ffffff;
        }

        .card p {
            color: #a0a0a0;
            font-size: 0.95rem;
            line-height: 1.4;
            margin-bottom: 16px;
        }

        .btn {
            background-color: #2c2c2e;
            color: #ffffff;
            border: none;
            padding: 10px 18px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 0.9rem;
            width: 100%;
            cursor: pointer;
            transition: background 0.2s;
            text-align: center;
            text-decoration: none;
            display: inline-block;
        }

        .btn-primary {
            background-color: #007aff;
            color: #ffffff;
        }

        .btn:active {
            opacity: 0.8;
        }

        /* Forms */
        .form-group {
            margin-bottom: 14px;
        }

        .form-group label {
            display: block;
            font-size: 0.85rem;
            color: #a0a0a0;
            margin-bottom: 6px;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px;
            background-color: #2c2c2e;
            border: 1px solid #3a3a3c;
            border-radius: 8px;
            color: #ffffff;
            font-size: 0.95rem;
        }

        /* Tutor Profile Header */
        .tutor-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 12px;
        }

        .avatar {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background-color: #007aff;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.2rem;
        }

        /* Bottom Navigation Bar */
        nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: #1e1e1e;
            border-top: 1px solid #2d2d2d;
            display: flex;
            justify-content: space-around;
            padding: 10px 0;
            z-index: 100;
        }

        .nav-item {
            background: none;
            border: none;
            color: #757575;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            font-size: 0.75rem;
            cursor: pointer;
            width: 25%;
        }

        .nav-item.active {
            color: #007aff;
        }

        .nav-icon {
            font-size: 1.2rem;
        }
    </style>
</head>
<body>

    <header>
        <h1>Language Exchange Initiative</h1>
    </header>

    <main>
        <!-- TAB 1: INICIO -->
        <section id="tab-inicio" class="tab-content active">
            <div class="card">
                <h2>Aprende</h2>
                <p>Encuentra el tutor perfecto para ti. Aplica y empieza a aprender hoy mismo sin ningún costo.</p>
                <button class="btn btn-primary" onclick="switchTab('tutores')">Ver tutores</button>
            </div>

            <div class="card">
                <h2>Enseña</h2>
                <p>Comparte tu idioma nativo como voluntario. Crea sesiones, sube materiales y conecta con estudiantes motivados.</p>
                <button class="btn" onclick="openModal('tutor-form')">Configurar perfil de tutor</button>
            </div>

            <div class="card">
                <h2>Tus sesiones</h2>
                <p>Accede a tus clases, chats privados y materiales compartidos. Todo en un solo lugar.</p>
                <button class="btn" onclick="switchTab('sesiones')">Mis sesiones</button>
            </div>
        </section>

        <!-- TAB 2: TUTORES -->
        <section id="tab-tutores" class="tab-content">
            <h2 style="margin-bottom: 16px;">Tutores Disponibles</h2>
            
            <div class="card">
                <div class="tutor-header">
                    <div class="avatar">E</div>
                    <div>
                        <h3>Equipo Voluntario</h3>
                        <span style="font-size: 0.8rem; color: #4da6ff;">Español • Nativo</span>
                    </div>
                </div>
                <p>¡Hola! Ofrecemos sesiones de práctica, lecciones gramaticales y conversación fluida para principiantes.</p>
                <button class="btn btn-primary" onclick="openStudentModal('Equipo Voluntario')">Solicitar Tutoría</button>
            </div>
        </section>

        <!-- TAB 3: SESIONES -->
        <section id="tab-sesiones" class="tab-content">
            <h2 style="margin-bottom: 16px;">Tus Sesiones y Chats</h2>
            <div class="card">
                <h3>Chat Privado y Materiales</h3>
                <p>Accede al canal seguro para interactuar por texto, compartir archivos de video/audio y coordinar videollamadas.</p>
                <a href="https://discord.com" target="_blank" class="btn btn-primary">Abrir Chat Privado / Discord</a>
            </div>
            <div class="card">
                <h3>Aula de Videollamada</h3>
                <p>Inicia tu clase en vivo cuando acuerdes el horario con tu tutor/estudiante.</p>
                <a href="https://meet.jit.si/VoluntariadoIdiomasRoom" target="_blank" class="btn">Entrar a Videollamada (Jitsi)</a>
            </div>
        </section>

        <!-- TAB 4: PERFIL -->
        <section id="tab-perfil" class="tab-content">
            <h2 style="margin-bottom: 16px;">Mi Perfil</h2>
            <div class="card">
                <p><strong>Rol:</strong> Usuario / Voluntario</p>
                <p><strong>Estado:</strong> Activo</p>
                <button class="btn" onclick="alert('Configuración guardada')">Editar Perfil</button>
            </div>
        </section>

        <!-- MODAL / FORMULARIO ESTUDIANTE -->
        <div id="modal-estudiante" class="card" style="display: none; position: fixed; top: 10%; left: 5%; right: 5%; z-index: 200; background: #1e1e1e; border: 2px solid #007aff;">
            <h2>Solicitud de Estudiante</h2>
            <p id="tutor-selected-text">Envía tu solicitud al tutor.</p>
            <form onsubmit="event.preventDefault(); submitApplication();">
                <div class="form-group">
                    <label>Tu Nombre:</label>
                    <input type="text" required placeholder="Ej. Alex">
                </div>
                <div class="form-group">
                    <label>¿De qué país eres?</label>
                    <input type="text" required placeholder="Ej. Estados Unidos">
                </div>
                <div class="form-group">
                    <label>¿Qué idioma hablas nativamente?</label>
                    <input type="text" required placeholder="Ej. Inglés">
                </div>
                <button type="submit" class="btn btn-primary" style="margin-bottom: 8px;">Enviar Solicitud</button>
                <button type="button" class="btn" onclick="closeStudentModal()">Cancelar</button>
            </form>
        </div>
    </main>

    <!-- NAVEGACIÓN INFERIOR -->
    <nav>
        <button class="nav-item active" onclick="switchTab('inicio')">
            <span class="nav-icon">🏠</span>
            <span>Inicio</span>
        </button>
        <button class="nav-item" onclick="switchTab('tutores')">
            <span class="nav-icon">👥</span>
            <span>Tutores</span>
        </button>
        <button class="nav-item" onclick="switchTab('sesiones')">
            <span class="nav-icon">📖</span>
            <span>Sesiones</span>
        </button>
        <button class="nav-item" onclick="switchTab('perfil')">
            <span class="nav-icon">👤</span>
            <span>Perfil</span>
        </button>
    </nav>

    <script>
        function switchTab(tabId) {
            // Ocultar todos los contenidos
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            // Quitar clase activa de botones
            document.querySelectorAll('.nav-item').forEach(btn => {
                btn.classList.remove('active');
            });

            // Mostrar el seleccionado
            document.getElementById('tab-' + tabId).classList.add('active');
            
            // Marcar icono activo
            const indexMap = {'inicio': 0, 'tutores': 1, 'sesiones': 2, 'perfil': 3};
            document.querySelectorAll('.nav-item')[indexMap[tabId]].classList.add('active');
        }

        function openStudentModal(tutorName) {
            document.getElementById('tutor-selected-text').innerText = "Solicitud para: " + tutorName;
            document.getElementById('modal-estudiante').style.display = 'block';
        }

        function closeStudentModal() {
            document.getElementById('modal-estudiante').style.display = 'none';
        }

        function submitApplication() {
            alert("¡Solicitud enviada con éxito! El tutor revisará tus datos para iniciar la sesión.");
            closeStudentModal();
            switchTab('sesiones');
        }

        function openModal(type) {
            alert("Opción para registrar nuevo tutor activada.");
        }
    </script>
</body>
</html>
