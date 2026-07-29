<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Iniciativa de Intercambio Cultural y Voluntariado</title>
  <!-- Supabase CDN -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
  <style>
    :root {
      --bg-dark: #121212;
      --card-bg: #1e1e1e;
      --accent: #2563eb;
      --accent-hover: #1d4ed8;
      --text-main: #f3f4f6;
      --text-muted: #9ca3af;
      --border: #374151;
      --success: #10b981;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background-color: var(--bg-dark);
      color: var(--text-main);
      padding-bottom: 70px;
    }

    header {
      background-color: var(--card-bg);
      padding: 1rem;
      text-align: center;
      border-bottom: 1px solid var(--border);
      position: sticky;
      top: 0;
      z-index: 10;
    }

    header h1 {
      font-size: 1.25rem;
      color: #fff;
    }

    main {
      padding: 1rem;
      max-width: 600px;
      margin: 0 auto;
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .card {
      background-color: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1rem;
      margin-bottom: 1rem;
    }

    .card h2 {
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
      color: #fff;
    }

    .card p {
      color: var(--text-muted);
      font-size: 0.9rem;
      margin-bottom: 0.75rem;
    }

    .btn {
      display: inline-block;
      width: 100%;
      background-color: var(--accent);
      color: white;
      border: none;
      padding: 0.75rem;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      text-align: center;
      font-size: 0.95rem;
    }

    .btn:hover {
      background-color: var(--accent-hover);
    }

    .btn-secondary {
      background-color: transparent;
      border: 1px solid var(--border);
      color: var(--text-main);
      margin-top: 0.5rem;
    }

    input, select, textarea {
      width: 100%;
      padding: 0.75rem;
      background-color: #2b2b2b;
      border: 1px solid var(--border);
      border-radius: 8px;
      color: white;
      margin-bottom: 0.75rem;
      font-size: 0.9rem;
    }

    nav.bottom-nav {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      background-color: var(--card-bg);
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-around;
      padding: 0.5rem 0;
      z-index: 20;
    }

    .nav-item {
      background: none;
      border: none;
      color: var(--text-muted);
      font-size: 0.75rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      cursor: pointer;
    }

    .nav-item.active {
      color: var(--accent);
      font-weight: bold;
    }

    .badge {
      display: inline-block;
      padding: 0.25rem 0.5rem;
      border-radius: 4px;
      font-size: 0.75rem;
      background-color: #374151;
      color: #fff;
    }

    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.8);
      z-index: 30;
      align-items: center;
      justify-content: center;
      padding: 1rem;
    }

    .modal.active {
      display: flex;
    }

    .modal-content {
      background: var(--card-bg);
      padding: 1.5rem;
      border-radius: 12px;
      width: 100%;
      max-width: 400px;
    }
  </style>
</head>
<body>

  <header>
    <h1>Voluntariado e Intercambio</h1>
  </header>

  <main>
    <!-- Tab Inicio -->
    <section id="tab-inicio" class="tab-content active">
      <div class="card">
        <h2>Aprende y Conecta</h2>
        <p>Aprende idiomas con voluntarios nativos o comparte tus conocimientos con personas de todo el mundo.</p>
        <button class="btn" onclick="switchTab('tutores')">Buscar Tutores</button>
        <button class="btn btn-secondary" onclick="openModal('modal-tutor')">Postularse como Tutor</button>
      </div>
    </section>

    <!-- Tab Tutores -->
    <section id="tab-tutores" class="tab-content">
      <h2 style="margin-bottom: 1rem;">Tutores Disponibles</h2>
      <div id="lista-tutores">
        <p style="color: var(--text-muted);">Cargando tutores...</p>
      </div>
    </section>

    <!-- Tab Sesiones -->
    <section id="tab-sesiones" class="tab-content">
      <h2 style="margin-bottom: 1rem;">Solicitudes y Sesiones</h2>
      <div id="lista-solicitudes">
        <p style="color: var(--text-muted);">Cargando solicitudes...</p>
      </div>
    </section>

    <!-- Tab Perfil -->
    <section id="tab-perfil" class="tab-content">
      <div class="card">
        <h2>Mi Perfil</h2>
        <p>Gestiona tu cuenta y tus preferencias de aprendizaje.</p>
        <input type="text" id="nombre-usuario" placeholder="Tu Nombre Completo" value="Usuario Activo">
        <input type="text" id="pais-usuario" placeholder="Tu País" value="Nicaragua">
        <button class="btn" onclick="alert('Perfil actualizado correctamente')">Guardar Cambios</button>
      </div>
    </section>
  </main>

  <!-- Modal Solicitar Tutoría -->
  <div id="modal-solicitud" class="modal">
    <div class="modal-content">
      <h2>Solicitar Tutoría</h2>
      <p id="solicitud-tutor-nombre" style="font-weight: bold; color: #fff;"></p>
      <input type="text" id="estudiante-nombre" placeholder="Tu Nombre">
      <input type="text" id="estudiante-pais" placeholder="Tu País">
      <input type="text" id="estudiante-idioma" placeholder="Idioma que deseas practicar">
      <button class="btn" onclick="enviarSolicitud()">Enviar Solicitud</button>
      <button class="btn btn-secondary" onclick="closeModal('modal-solicitud')">Cancelar</button>
    </div>
  </div>

  <!-- Modal Registro de Tutor -->
  <div id="modal-tutor" class="modal">
    <div class="modal-content">
      <h2>Postularse como Tutor</h2>
      <input type="text" id="tutor-nombre" placeholder="Nombre Completo">
      <input type="text" id="tutor-idioma" placeholder="Idioma que enseñas">
      <input type="text" id="tutor-pais" placeholder="Tu País">
      <textarea id="tutor-desc" placeholder="Breve descripción sobre ti"></textarea>
      <button class="btn" onclick="guardarTutor()">Registrarme como Tutor</button>
      <button class="btn btn-secondary" onclick="closeModal('modal-tutor')">Cancelar</button>
    </div>
  </div>

  <!-- Navegación Inferior -->
  <nav class="bottom-nav">
    <button class="nav-item active" onclick="switchTab('inicio')">Inicio</button>
    <button class="nav-item" onclick="switchTab('tutores')">Tutores</button>
    <button class="nav-item" onclick="switchTab('sesiones')">Sesiones</button>
    <button class="nav-item" onclick="switchTab('perfil')">Perfil</button>
  </nav>

  <script>
    // Inicializar Supabase con tus credenciales
    const SUPABASE_URL = 'https://jvppioynydoustjevsmc.supabase.co';
    const SUPABASE_KEY = 'Sb_publishable_xdv_OPu80dHdIbWITHR2WA_9ZyaCFhL';
    const _supabase = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

    let tutorSeleccionado = '';

    function switchTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
      document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
      
      document.getElementById(`tab-${tabId}`).classList.add('active');
      event.currentTarget?.classList.add('active');

      if (tabId === 'tutores') cargarTutores();
      if (tabId === 'sesiones') cargarSolicitudes();
    }

    function openModal(id) {
      document.getElementById(id).classList.add('active');
    }

    function closeModal(id) {
      document.getElementById(id).classList.remove('active');
    }

    // Cargar Tutores desde Supabase
    async function cargarTutores() {
      const contenedor = document.getElementById('lista-tutores');
      contenedor.innerHTML = '<p style="color: var(--text-muted);">Cargando tutores...</p>';

      const { data, error } = await _supabase.from('tutores').select('*');

      if (error || !data || data.length === 0) {
        contenedor.innerHTML = '<p style="color: var(--text-muted);">No hay tutores registrados aún. ¡Sé el primero en postularte!</p>';
        return;
      }

      contenedor.innerHTML = '';
      data.forEach(t => {
        contenedor.innerHTML += `
          <div class="card">
            <h2>${t.nombre} <span class="badge">${t.pais}</span></h2>
            <p><strong>Enseña:</strong> ${t.idioma}</p>
            <p>${t.descripcion || ''}</p>
            <button class="btn" onclick="prepararSolicitud('${t.nombre}')">Solicitar Tutoría</button>
          </div>
        `;
      });
    }

    // Guardar un nuevo Tutor en Supabase
    async function guardarTutor() {
      const nombre = document.getElementById('tutor-nombre').value;
      const idioma = document.getElementById('tutor-idioma').value;
      const pais = document.getElementById('tutor-pais').value;
      const descripcion = document.getElementById('tutor-desc').value;

      if (!nombre || !idioma || !pais) {
        alert('Por favor completa todos los campos requeridos.');
        return;
      }

      const { error } = await _supabase.from('tutores').insert([
        { nombre, idioma, pais, descripcion }
      ]);

      if (error) {
        alert('Error al guardar: ' + error.message);
      } else {
        alert('¡Te has registrado como tutor con éxito!');
        closeModal('modal-tutor');
        switchTab('tutores');
      }
    }

    // Abrir modal de solicitud
    function prepararSolicitud(nombreTutor) {
      tutorSeleccionado = nombreTutor;
      document.getElementById('solicitud-tutor-nombre').innerText = `Tutor: ${nombreTutor}`;
      openModal('modal-solicitud');
    }

    // Enviar Solicitud de Tutoría a Supabase
    async function enviarSolicitud() {
      const estNombre = document.getElementById('estudiante-nombre').value;
      const estPais = document.getElementById('estudiante-pais').value;
      const estIdioma = document.getElementById('estudiante-idioma').value;

      if (!estNombre || !estPais || !estIdioma) {
        alert('Por favor completa los campos.');
        return;
      }

      const { error } = await _supabase.from('solicitudes').insert([
        {
          tutor_nombre: tutorSeleccionado,
          estudiante_nombre: estNombre,
          estudiante_pais: estPais,
          estudiante_idioma: estIdioma,
          estado: 'Pendiente'
        }
      ]);

      if (error) {
        alert('Error al enviar la solicitud: ' + error.message);
      } else {
        alert('¡Solicitud enviada al tutor exitosamente!');
        closeModal('modal-solicitud');
        switchTab('sesiones');
      }
    }

    // Cargar Solicitudes en vivo desde Supabase
    async function cargarSolicitudes() {
      const contenedor = document.getElementById('lista-solicitudes');
      contenedor.innerHTML = '<p style="color: var(--text-muted);">Cargando solicitudes...</p>';

      const { data, error } = await _supabase.from('solicitudes').select('*');

      if (error || !data || data.length === 0) {
        contenedor.innerHTML = '<p style="color: var(--text-muted);">No hay solicitudes o sesiones pendientes.</p>';
        return;
      }

      contenedor.innerHTML = '';
      data.forEach(s => {
        contenedor.innerHTML += `
          <div class="card">
            <h2>Solicitud de ${s.estudiante_nombre}</h2>
            <p><strong>Tutor solicitado:</strong> ${s.tutor_nombre}</p>
            <p><strong>País:</strong> ${s.estudiante_pais} | <strong>Idioma:</strong> ${s.estudiante_idioma}</p>
            <p><strong>Estado:</strong> <span class="badge" style="background-color: var(--accent);">${s.estado}</span></p>
            <button class="btn" onclick="alert('Abriendo chat con ${s.estudiante_nombre}...')">Iniciar Chat</button>
            <button class="btn btn-secondary" onclick="alert('Iniciando sala de videollamada...')">Iniciar Videollamada</button>
          </div>
        `;
      });
    }

    // Cargar al iniciar
    cargarTutores();
  </script>
</body>
</html>

