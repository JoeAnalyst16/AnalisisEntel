<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard Analíticos - Grupo Norte</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #1e3c72, #2a5298, #77c25c);
      background-size: 400% 400%;
      animation: gradientShift 15s ease infinite;
      min-height: 100vh;
      color: #333;
      overflow-x: hidden;
    }

    @keyframes gradientShift {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
      position: relative;
      z-index: 2;
    }

    .header {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      padding: 30px;
      margin-bottom: 30px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .header::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: conic-gradient(from 0deg, transparent, rgba(119, 194, 92, 0.1), transparent);
      animation: rotate 20s linear infinite;
      z-index: -1;
    }

    @keyframes rotate {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .logo-container {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 20px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .logo {
      height: 80px;
      object-fit: contain;
      transition: transform 0.3s ease;
    }

    .logo:hover {
      transform: scale(1.1);
    }

    .mascot {
      height: 100px;
      animation: bounce 2s ease-in-out infinite;
    }

    @keyframes bounce {
      0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
      40% { transform: translateY(-10px); }
      60% { transform: translateY(-5px); }
    }

    .title {
      font-size: 2.5em;
      color: #1e3c72;
      margin-bottom: 10px;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
    }

    .subtitle {
      font-size: 1.2em;
      color: #555;
      margin-bottom: 20px;
      font-weight: 300;
    }

    .tagline {
      font-size: 1.1em;
      color: #77c25c;
      font-weight: 600;
      font-style: italic;
      text-transform: uppercase;
      letter-spacing: 2px;
    }

    .dashboard-section {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      padding: 40px;
      margin-bottom: 30px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    }

    .buttons-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
      margin-bottom: 30px;
    }

    .dashboard-button {
      background: linear-gradient(45deg, #77c25c, #5fa847);
      color: white;
      text-decoration: none;
      padding: 25px 30px;
      border-radius: 15px;
      text-align: center;
      font-size: 1.1em;
      font-weight: 600;
      transition: all 0.3s ease;
      box-shadow: 0 10px 20px rgba(119, 194, 92, 0.3);
      border: none;
      cursor: pointer;
      position: relative;
      overflow: hidden;
    }

    .dashboard-button::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
      transition: left 0.5s;
    }

    .dashboard-button:hover::before {
      left: 100%;
    }

    .dashboard-button:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 30px rgba(119, 194, 92, 0.4);
    }

    .dashboard-button:active {
      transform: translateY(-2px);
    }

    .visualization-preview {
      text-align: center;
      margin: 30px 0;
    }

    .preview-image {
      max-width: 100%;
      height: auto;
      border-radius: 15px;
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
      transition: transform 0.3s ease;
    }

    .preview-image:hover {
      transform: scale(1.02);
    }

    .contacts-section {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      padding: 40px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    }

    .contacts-title {
      font-size: 2em;
      color: #1e3c72;
      margin-bottom: 30px;
      text-align: center;
    }

    .contacts-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
    }

    .contact-card {
      background: linear-gradient(135deg, #f8f9fa, #e9ecef);
      border-radius: 15px;
      padding: 25px;
      border-left: 5px solid #77c25c;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .contact-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
    }

    .contact-name {
      font-size: 1.2em;
      font-weight: 600;
      color: #1e3c72;
      margin-bottom: 5px;
    }

    .contact-position {
      font-size: 0.9em;
      color: #77c25c;
      margin-bottom: 10px;
      font-weight: 500;
    }

    .contact-email {
      color: #555;
      text-decoration: none;
      font-size: 0.9em;
      transition: color 0.3s ease;
    }

    .contact-email:hover {
      color: #77c25c;
    }

    .floating-elements {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    .floating-shape {
      position: absolute;
      border-radius: 50%;
      background: rgba(119, 194, 92, 0.1);
      animation: float 6s ease-in-out infinite;
    }

    .floating-shape:nth-child(1) {
      width: 80px;
      height: 80px;
      top: 20%;
      left: 10%;
      animation-delay: 0s;
    }

    .floating-shape:nth-child(2) {
      width: 60px;
      height: 60px;
      top: 60%;
      right: 10%;
      animation-delay: 2s;
    }

    .floating-shape:nth-child(3) {
      width: 100px;
      height: 100px;
      bottom: 20%;
      left: 20%;
      animation-delay: 4s;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(180deg); }
    }

    .stats-banner {
      background: linear-gradient(45deg, #1e3c72, #2a5298);
      color: white;
      padding: 20px;
      border-radius: 15px;
      margin: 20px 0;
      text-align: center;
    }

    .stats-text {
      font-size: 1.1em;
      font-weight: 300;
      letter-spacing: 1px;
    }

    @media (max-width: 768px) {
      .container {
        padding: 10px;
      }

      .title {
        font-size: 2em;
      }

      .logo-container {
        flex-direction: column;
      }

      .buttons-container {
        grid-template-columns: 1fr;
      }

      .contacts-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="floating-elements">
    <div class="floating-shape"></div>
    <div class="floating-shape"></div>
    <div class="floating-shape"></div>
  </div>

  <div class="container">
    <div class="header">
      <div class="logo-container">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTuCF2FCTVi3KtUgDTtm5fo9L2E7dExWxC1Zw&s" alt="Grupo Norte Logo" class="logo">
        <div style="font-size: 3em; color: #77c25c;">📊</div>
      </div>
      <h1 class="title">Dashboard Analíticos</h1>
      <p class="subtitle">Visualización de datos de colaboradores a nivel nacional</p>
      <p class="tagline">¡Creamos Soluciones!</p>
    </div>

    <div class="stats-banner">
      <p class="stats-text">Análisis en tiempo real • Datos integrados • Decisiones inteligentes</p>
    </div>

    <div class="dashboard-section">
      <h2 style="text-align: center; color: #1e3c72; margin-bottom: 30px; font-size: 2em;">Accede a tus Reportes</h2>
      
      <div class="buttons-container">
        <a href="https://app.powerbi.com/links/m6jrhSKfgr?ctid=474763a9-9dd9-4ea4-8706-a2639fe77865&pbi_source=linkShare&bookmarkGuid=6759a97e-9335-44f2-9a00-e82756ef36c5" class="dashboard-button" target="_blank">
          📊 Informe Power BI
          <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">Análisis interactivo y visualizaciones avanzadas</div>
        </a>
        <a href="https://lookerstudio.google.com/reporting/bee7383c-54aa-46c6-82ec-c4229a477052" class="dashboard-button" target="_blank">
          📈 Informe Looker Studio
          <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">Reportes dinámicos y métricas en tiempo real</div>
        </a>
      </div>

      <div class="visualization-preview">
        <img src="https://blogs.iadb.org/conocimiento-abierto/wp-content/uploads/sites/10/2015/11/Visualizacion-de-datos.jpg" alt="Visualización de datos - Ejemplo" class="preview-image">
      </div>
    </div>

    <div class="contacts-section">
      <h2 class="contacts-title">Equipo de Contacto</h2>
      <div class="contacts-grid">
        <div class="contact-card">
          <div class="contact-name">Paola Zúñiga</div>
          <div class="contact-position">Gerente de Innovación y Proyectos</div>
          <a href="mailto:paola.zuniga@gruponorte.cl" class="contact-email">paola.zuniga@gruponorte.cl</a>
        </div>
        <div class="contact-card">
          <div class="contact-name">Stand by</div>
          <div class="contact-position">Subgerente de Operaciones</div>
          <a href="mailto:@gruponorte.cl" class="contact-email">@gruponorte.cl</a>
        </div>
        <div class="contact-card">
            <div class="contact-name">Ximena</div>
            <div class="contact-position">KAM</div>
            <a href="mailto:ximena.moya@gruponorte.cl" class="contact-email">ximena.moya@gruponorte.cl</a>
          </div>
        <div class="contact-card">
          <div class="contact-name">Francin Aguilera</div>
          <div class="contact-position">Jefa Operacional</div>
          <a href="mailto:francin.aguilera@gruponorte.cl" class="contact-email">francin.aguilera@gruponorte.cl</a>
        </div>
        <div class="contact-card">
          <div class="contact-name">Joe Salas</div>
          <div class="contact-position">Analista Integral</div>
          <a href="mailto:joe.salas@gruponorte.cl" class="contact-email">joe.salas@gruponorte.cl</a>
        </div>
      </div>
    </div>
  </div>

  <script>
    // Añadir interactividad adicional
    document.addEventListener('DOMContentLoaded', function() {
      // Efecto de parallax suave en elementos flotantes
      window.addEventListener('scroll', function() {
        const scrolled = window.pageYOffset;
        const shapes = document.querySelectorAll('.floating-shape');
        shapes.forEach((shape, index) => {
          const speed = 0.1 + (index * 0.05);
          shape.style.transform = `translateY(${scrolled * speed}px)`;
        });
      });

      // Animación de entrada para las tarjetas
      const cards = document.querySelectorAll('.contact-card, .dashboard-button');
      const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
      };

      const observer = new IntersectionObserver(function(entries) {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.style.opacity = '1';
            entry.target.style.transform = 'translateY(0)';
          }
        });
      }, observerOptions);

      cards.forEach(card => {
        card.style.opacity = '0';
        card.style.transform = 'translateY(20px)';
        card.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
        observer.observe(card);
      });
    });
  </script>
</body>
</html>
