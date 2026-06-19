<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Capacitación TICs - Colegio de Bachilleres</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700;900&family=Space+Grotesk:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  :root {
    --azul: #0f4c81;
    --azul-claro: #1a6bb5;
    --cian: #00b4d8;
    --oscuro: #0a0e1a;
    --gris: #1c2230;
    --texto: #e8eaf0;
    --texto-sec: #8a94a6;
    --acento: #00e5ff;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    font-family: 'Inter', sans-serif;
    background: var(--oscuro);
    color: var(--texto);
    overflow-x: hidden;
  }

  /* AUDIO */
  #audio-ctrl {
    position: fixed; bottom: 24px; right: 24px; z-index: 9999;
    background: rgba(0,180,216,0.15);
    border: 1px solid var(--cian);
    border-radius: 50%;
    width: 48px; height: 48px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; backdrop-filter: blur(8px);
    transition: all 0.3s;
  }
  #audio-ctrl:hover { background: rgba(0,180,216,0.3); transform: scale(1.1); }
  #audio-ctrl svg { width: 22px; height: 22px; fill: var(--cian); }

  /* NAV */
  nav {
    position: fixed; top: 0; width: 100%; z-index: 1000;
    background: rgba(10,14,26,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(0,180,216,0.15);
    padding: 0 5%;
    display: flex; align-items: center; justify-content: space-between;
    height: 64px;
  }
  .nav-logo {
    display: flex; align-items: center; gap: 10px;
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 700; font-size: 1.1rem;
    color: var(--acento);
    letter-spacing: -0.02em;
  }
  .nav-logo span { color: var(--texto); font-weight: 400; }
  nav ul { list-style: none; display: flex; gap: 2rem; }
  nav a {
    color: var(--texto-sec); text-decoration: none;
    font-size: 0.9rem; font-weight: 500;
    transition: color 0.2s;
  }
  nav a:hover { color: var(--acento); }

  /* HERO */
  #inicio {
    min-height: 100vh;
    display: flex; align-items: center;
    padding: 80px 5% 40px;
    position: relative;
    overflow: hidden;
  }
  .hero-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px; align-items: center;
    max-width: 1200px; margin: 0 auto; width: 100%;
  }
  .hero-tag {
    display: inline-block;
    background: rgba(0,180,216,0.1);
    border: 1px solid rgba(0,180,216,0.3);
    color: var(--cian);
    padding: 6px 16px; border-radius: 100px;
    font-size: 0.78rem; font-weight: 500;
    letter-spacing: 0.06em; text-transform: uppercase;
    margin-bottom: 24px;
  }
  .hero-titulo {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(2.2rem, 4.5vw, 3.8rem);
    font-weight: 700;
    line-height: 1.1;
    letter-spacing: -0.03em;
    margin-bottom: 12px;
  }
  .hero-titulo .gradiente {
    background: linear-gradient(135deg, var(--cian), #a78bfa);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .hero-sub {
    font-size: 1.05rem; color: var(--texto-sec);
    line-height: 1.7; margin-bottom: 36px;
    max-width: 480px;
  }
  .hero-btns { display: flex; gap: 16px; flex-wrap: wrap; }
  .btn-primario {
    background: var(--cian);
    color: var(--oscuro);
    padding: 13px 28px; border-radius: 8px;
    font-weight: 700; font-size: 0.92rem;
    text-decoration: none; transition: all 0.2s;
    cursor: pointer;
    border: none;
    display: inline-block;
  }
  .btn-primario:hover { background: var(--acento); transform: translateY(-2px); }
  .btn-secundario {
    border: 1px solid rgba(0,180,216,0.4);
    color: var(--cian);
    padding: 13px 28px; border-radius: 8px;
    font-weight: 500; font-size: 0.92rem;
    text-decoration: none; transition: all 0.2s;
    cursor: pointer;
    background: transparent;
    display: inline-block;
  }
  .btn-secundario:hover { background: rgba(0,180,216,0.1); }
  .hero-img-wrap {
    position: relative;
  }
  .hero-img-wrap img {
    width: 100%; border-radius: 16px;
    object-fit: cover; height: 420px;
    border: 1px solid rgba(0,180,216,0.2);
  }
  .hero-badge {
    position: absolute; bottom: -20px; left: -20px;
    background: rgba(10,14,26,0.9);
    border: 1px solid rgba(0,180,216,0.3);
    border-radius: 12px;
    padding: 14px 20px;
    backdrop-filter: blur(8px);
  }
  .hero-badge p { font-size: 0.75rem; color: var(--texto-sec); }
  .hero-badge strong { font-size: 1.2rem; color: var(--acento); font-family: 'Space Grotesk', sans-serif; }

  /* BG deco */
  .deco-circle {
    position: absolute; border-radius: 50%;
    filter: blur(80px); pointer-events: none; opacity: 0.12;
  }
  .deco-1 { width: 600px; height: 600px; background: var(--cian); top: -200px; right: -100px; }
  .deco-2 { width: 400px; height: 400px; background: #7c3aed; bottom: -100px; left: -100px; }

  /* ACTIVIDADES */
  #actividades {
    padding: 100px 5%;
    max-width: 1200px; margin: 0 auto;
  }
  .section-eyebrow {
    color: var(--cian); font-size: 0.78rem;
    font-weight: 600; letter-spacing: 0.1em;
    text-transform: uppercase; margin-bottom: 12px;
  }
  .section-titulo {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(1.8rem, 3vw, 2.6rem);
    font-weight: 700; letter-spacing: -0.02em;
    margin-bottom: 14px;
  }
  .section-sub {
    color: var(--texto-sec); font-size: 1rem;
    line-height: 1.7; max-width: 520px; margin-bottom: 56px;
  }
  .cards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 20px;
  }
  .card {
    background: var(--gris);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 14px;
    padding: 28px 24px;
    transition: all 0.3s;
    position: relative; overflow: hidden;
  }
  .card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 3px; height: 100%;
    background: var(--cian);
    opacity: 0; transition: opacity 0.3s;
  }
  .card:hover { border-color: rgba(0,180,216,0.3); transform: translateY(-4px); }
  .card:hover::before { opacity: 1; }
  .card-icon {
    width: 44px; height: 44px;
    background: rgba(0,180,216,0.12);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 18px;
    font-size: 1.4rem;
  }
  .card h3 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 1.05rem; font-weight: 600;
    margin-bottom: 10px; color: var(--texto);
  }
  .card p { font-size: 0.88rem; color: var(--texto-sec); line-height: 1.65; }

  /* GALERÍA */
  #galeria {
    padding: 100px 5%;
    background: rgba(255,255,255,0.02);
  }
  .galeria-inner { max-width: 1200px; margin: 0 auto; }
  .galeria-header { margin-bottom: 48px; }
  .masonry {
    columns: 3;
    column-gap: 16px;
  }
  .masonry-item {
    break-inside: avoid;
    margin-bottom: 16px;
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    cursor: pointer;
  }
  .masonry-item img {
    width: 100%; display: block;
    transition: transform 0.4s;
  }
  .masonry-item:hover img { transform: scale(1.04); }
  .masonry-item .overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.5), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .masonry-item:hover .overlay { opacity: 1; }

  /* LIGHTBOX */
  .lightbox {
    display: none;
    position: fixed; inset: 0; z-index: 9998;
    background: rgba(0,0,0,0.9);
    align-items: center; justify-content: center;
    backdrop-filter: blur(4px);
  }
  .lightbox.open { display: flex; }
  .lightbox img {
    max-width: 90vw; max-height: 88vh;
    border-radius: 12px; object-fit: contain;
  }
  .lightbox-close {
    position: absolute; top: 24px; right: 28px;
    color: #fff; font-size: 2rem; cursor: pointer;
    background: none; border: none; line-height: 1;
  }

  /* CONTACTO */
  #contacto {
    padding: 100px 5%;
    max-width: 700px; margin: 0 auto;
    text-align: center;
  }
  .contacto-card {
    background: var(--gris);
    border: 1px solid rgba(0,180,216,0.2);
    border-radius: 20px;
    padding: 56px 48px;
    margin-top: 40px;
  }
  .contacto-info { margin-bottom: 32px; }
  .contacto-info p {
    color: var(--texto-sec); font-size: 0.92rem;
    margin-bottom: 10px;
  }
  .contacto-info a {
    color: var(--cian); text-decoration: none;
    font-weight: 500; font-size: 1rem;
  }
  .contacto-info a:hover { text-decoration: underline; }
  form { display: flex; flex-direction: column; gap: 14px; text-align: left; }
  form input, form textarea {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 8px;
    padding: 13px 16px;
    color: var(--texto);
    font-size: 0.92rem; font-family: 'Inter', sans-serif;
    transition: border-color 0.2s;
    outline: none;
  }
  form input:focus, form textarea:focus {
    border-color: var(--cian);
  }
  form textarea { min-height: 110px; resize: vertical; }
  form button {
    background: var(--cian);
    color: var(--oscuro);
    font-weight: 700; font-size: 0.95rem;
    padding: 14px; border-radius: 8px;
    border: none; cursor: pointer;
    transition: all 0.2s;
  }
  form button:hover { background: var(--acento); transform: translateY(-2px); }
  .wa-btn {
    display: inline-flex; align-items: center; gap: 8px;
    margin-top: 20px;
    border: 1px solid rgba(0,180,216,0.3);
    color: var(--cian);
    padding: 12px 24px; border-radius: 8px;
    font-weight: 500; font-size: 0.92rem;
    text-decoration: none; transition: all 0.2s;
  }
  .wa-btn:hover { background: rgba(0,180,216,0.1); }

  /* FOOTER */
  footer {
    border-top: 1px solid rgba(255,255,255,0.07);
    padding: 32px 5%;
    text-align: center;
    color: var(--texto-sec); font-size: 0.83rem;
  }

  .success-message {
    display: none;
    background: rgba(0, 200, 100, 0.2);
    border: 1px solid rgba(0, 200, 100, 0.5);
    color: #00c864;
    padding: 12px 16px;
    border-radius: 8px;
    margin-bottom: 14px;
    text-align: center;
  }

  @media(max-width: 768px) {
    .hero-grid { grid-template-columns: 1fr; }
    .hero-img-wrap { display: none; }
    nav ul { display: none; }
    .masonry { columns: 2; }
    .contacto-card { padding: 36px 24px; }
  }
  @media(max-width: 480px) {
    .masonry { columns: 1; }
  }
</style>
</head>
<body>

<!-- AUDIO -->
<audio id="bgaudio" loop>
  <source src="https://upload.wikimedia.org/wikipedia/commons/transcoded/b/b5/Jeff_Buckley_-_Lover%2C_You_Should%27ve_Come_Over.ogg/Jeff_Buckley_-_Lover%2C_You_Should%27ve_Come_Over.ogg.mp3" type="audio/mpeg">
</audio>
<div id="audio-ctrl" onclick="toggleAudio()" title="Reproducir / Pausar música">
  <svg id="play-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M8 5v14l11-7z"/></svg>
  <svg id="pause-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" style="display:none"><path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/></svg>
</div>

<!-- NAV -->
<nav>
  <div class="nav-logo">TICs <span>Bonfil · Plantel Cancún 3</span></div>
  <ul>
    <li><a href="#inicio">Inicio</a></li>
    <li><a href="#actividades">Actividades</a></li>
    <li><a href="#galeria">Galería</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="inicio">
  <div class="deco-circle deco-1"></div>
  <div class="deco-circle deco-2"></div>
  <div class="hero-grid">
    <div>
      <div class="hero-tag">COBAQROO · Capacitación TICs 2026</div>
      <h1 class="hero-titulo">
        Más tecnología,<br>
        <span class="gradiente">más posibilidades.</span>
      </h1>
      <p class="hero-sub">Capacitación en Tecnologías de la Información y Comunicación para estudiantes del Colegio de Bachilleres del plantel Cancún Tres Bonfil.</p>
      <div class="hero-btns">
        <a href="#actividades" class="btn-primario">Ver actividades</a>
        <a href="#contacto" class="btn-secundario">Contáctanos</a>
      </div>
    </div>
    <div class="hero-img-wrap">
      <img src="https://juliohdez74.github.io/asesorIA/images/laboratorio/c3lince.png" alt="Plantel Cancún Tres" onerror="this.src='https://placehold.co/600x420/0a0e1a/00b4d8?text=Plantel+Cancun+3'">
      <div class="hero-badge">
        <p>Plantel activo</p>
        <strong>Cancún 3 Bonfil</strong>
      </div>
    </div>
  </div>
</section>

<!-- ACTIVIDADES -->
<section id="actividades">
  <div class="section-eyebrow">Lo que aprenderás</div>
  <h2 class="section-titulo">Actividades de la Capacitación</h2>
  <p class="section-sub">Habilidades digitales demandadas en el mundo actual, desde electrónica hasta inteligencia artificial.</p>
  <div class="cards-grid">
    <div class="card">
      <div class="card-icon">⚡</div>
      <h3>Programación de Arduino</h3>
      <p>Aprende a programar microcontroladores y crear proyectos electrónicos interactivos.</p>
    </div>
    <div class="card">
      <div class="card-icon">📊</div>
      <h3>Hojas de Cálculo</h3>
      <p>Domina Excel, análisis de datos, gráficos avanzados y automatización de procesos.</p>
    </div>
    <div class="card">
      <div class="card-icon">🎨</div>
      <h3>Diseño Digital</h3>
      <p>Crea gráficos, diseños web y contenido visual profesional con herramientas modernas.</p>
    </div>
    <div class="card">
      <div class="card-icon">📱</div>
      <h3>Gestión de Redes Sociales</h3>
      <p>Estrategias de marketing digital y administración de contenido profesional.</p>
    </div>
    <div class="card">
      <div class="card-icon">🌐</div>
      <h3>Instalación de Redes</h3>
      <p>Fundamentos de redes de computadoras, configuración y administración.</p>
    </div>
    <div class="card">
      <div class="card-icon">🖥️</div>
      <h3>Mantenimiento de Equipos</h3>
      <p>Diagnóstico, reparación y mantenimiento preventivo de computadoras.</p>
    </div>
    <div class="card">
      <div class="card-icon">💻</div>
      <h3>Diseño de Páginas Web</h3>
      <p>Crea sitios web responsivos usando HTML, CSS, JavaScript y frameworks modernos.</p>
    </div>
    <div class="card">
      <div class="card-icon">🤖</div>
      <h3>Inteligencia Artificial</h3>
      <p>Explora el mundo de la IA, machine learning y herramientas de IA aplicadas.</p>
    </div>
  </div>
</section>

<!-- GALERÍA -->
<section id="galeria">
  <div class="galeria-inner">
    <div class="galeria-header">
      <div class="section-eyebrow">Nuestro trabajo</div>
      <h2 class="section-titulo">Galería de Actividades</h2>
      <p class="section-sub">Imágenes reales de nuestros estudiantes trabajando y aprendiendo.</p>
    </div>
    <div class="masonry" id="galeria-grid">
      <!-- Las fotos se inyectan dinámicamente -->
    </div>
  </div>
</section>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox" onclick="cerrarLightbox(event)">
  <button class="lightbox-close" onclick="document.getElementById('lightbox').classList.remove('open')">✕</button>
  <img src="" alt="" id="lightbox-img">
</div>

<!-- CONTACTO -->
<section id="contacto">
  <div class="section-eyebrow">Escríbenos</div>
  <h2 class="section-titulo">¡Contáctanos!</h2>
  <p class="section-sub" style="margin:0 auto 0;text-align:center;">¿Preguntas o quieres unirte? Nos encantaría escucharte.</p>
  <div class="contacto-card">
    <div class="contacto-info">
      <p>📧 <a href="mailto:jesuspool23b@cancuntresbonfil.edu.mx">jesuspool23b@cancuntresbonfil.edu.mx</a></p>
      <p>🏫 Colegio de Bachilleres — Plantel Cancún Tres Bonfil</p>
    </div>
    <div id="success-message" class="success-message">
      ¡Mensaje enviado con éxito! Nos pondremos en contacto pronto.
    </div>
    <form onsubmit="enviarForm(event)">
      <input type="text" id="nombre" placeholder="Tu nombre" required>
      <input type="email" id="email" placeholder="Tu correo electrónico" required>
      <textarea id="mensaje" placeholder="Tu mensaje..."></textarea>
      <button type="submit">Enviar mensaje</button>
    </form>
    <div style="text-align:center;margin-top:16px;">
      <a href="https://wa.me/529982149358" class="wa-btn" target="_blank">
        💬 Escríbenos por WhatsApp
      </a>
    </div>
  </div>
</section>

<footer>
  <p>© 2026 Capacitación TICs — Colegio de Bachilleres, Plantel Cancún Tres Bonfil. Todos los derechos reservados.</p>
</footer>

<script>
  // ========== GALERÍA - Imágenes de ejemplo ==========
  const fotos = [
    'https://placehold.co/400x300/0a0e1a/00b4d8?text=Estudiante+1',
    'https://placehold.co/400x400/0a0e1a/00b4d8?text=Estudiante+2',
    'https://placehold.co/400x350/0a0e1a/00b4d8?text=Estudiante+3',
    'https://placehold.co/400x380/0a0e1a/00b4d8?text=Estudiante+4',
    'https://placehold.co/400x320/0a0e1a/00b4d8?text=Estudiante+5',
    'https://placehold.co/400x390/0a0e1a/00b4d8?text=Estudiante+6'
  ];

  // Inyectar fotos en la galería
  function cargarGaleria() {
    const galeriaGrid = document.getElementById('galeria-grid');
    galeriaGrid.innerHTML = '';
    
    fotos.forEach((foto, index) => {
      const item = document.createElement('div');
      item.className = 'masonry-item';
      item.innerHTML = `
        <img src="${foto}" alt="Foto ${index + 1}" onclick="abrirLightbox('${foto}')">
        <div class="overlay"></div>
      `;
      galeriaGrid.appendChild(item);
    });
  }

  // ========== AUDIO ==========
  function toggleAudio() {
    const audio = document.getElementById('bgaudio');
    const playIcon = document.getElementById('play-icon');
    const pauseIcon = document.getElementById('pause-icon');
    
    if (audio.paused) {
      audio.play();
      playIcon.style.display = 'none';
      pauseIcon.style.display = 'block';
    } else {
      audio.pause();
      playIcon.style.display = 'block';
      pauseIcon.style.display = 'none';
    }
  }

  // ========== LIGHTBOX ==========
  function abrirLightbox(src) {
    const lightbox = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightbox-img');
    lightboxImg.src = src;
    lightbox.classList.add('open');
  }

  function cerrarLightbox(event) {
    // Solo cerrar si se hace clic en el fondo, no en la imagen
    if (event.target.id === 'lightbox') {
      document.getElementById('lightbox').classList.remove('open');
    }
  }

  // ========== FORMULARIO ==========
  function enviarForm(event) {
    event.preventDefault();
    
    const nombre = document.getElementById('nombre').value;
    const email = document.getElementById('email').value;
    const mensaje = document.getElementById('mensaje').value;
    
    // Validación básica
    if (!nombre.trim() || !email.trim() || !mensaje.trim()) {
      alert('Por favor completa todos los campos');
      return;
    }
    
    // Aquí normalmente enviarías los datos a un servidor
    // Por ahora, mostramos un mensaje de éxito
    console.log({
      nombre: nombre,
      email: email,
      mensaje: mensaje,
      fecha: new Date().toLocaleString('es-ES')
    });
    
    // Mostrar mensaje de éxito
    const successMessage = document.getElementById('success-message');
    successMessage.style.display = 'block';
    
    // Limpiar formulario
    document.querySelector('form').reset();
    
    // Ocultar mensaje después de 5 segundos
    setTimeout(() => {
      successMessage.style.display = 'none';
    }, 5000);
  }

  // ========== INICIALIZAR AL CARGAR LA PÁGINA ==========
  document.addEventListener('DOMContentLoaded', function() {
    cargarGaleria();
  });
</script>

</body>
</html>
