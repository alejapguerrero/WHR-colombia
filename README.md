<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Felicidad en Colombia - CDAT</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;600;700&family=Source+Serif+4:wght@400;500&display=swap" rel="stylesheet">

    <style>
        html { scroll-behavior: smooth; }
        body {
            margin: 0;
            font-family: 'Source Serif 4', serif;
            background-color: #e8dbca; 
            color: #222;
            line-height: 1.7;
            overflow-x: hidden;
        }

        h1, h2 {
            font-family: 'Playfair Display', serif;
            font-weight: 600;
            letter-spacing: 0.5px;
            color: #271a10; 
        }

        /* 2. EFECTO DE FONDO TRICOLOR (ONDA COLOMBIA) */
        .fondo-onda {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -2;
            pointer-events: none;
            /* La clave son estas variables --x y --y */
            background: radial-gradient(
                circle 150px at var(--x, 50%) var(--y, 50%), 
                rgba(255, 205, 0, 0.4) 20%, 
                rgba(0, 48, 135, 0.25) 15%, 
                rgba(200, 16, 46, 0.15) 30%, 
                transparent 100%
            );
            filter: blur(50px); 
            transition: none !important;
        }
            

        /* 3. HERO / PORTADA (VIDEO) */
        .hero {
            position: relative;
            height: 100vh;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            text-align: center;
            z-index: -1;
        }

        .video-bg {
            position: absolute;
            top: 50%;
            left: 50%;
            min-width: 100%;
            min-height: 100%;
            width: auto;
            height: auto;
            object-fit: cover;
            transform: translate(-50%, -50%);
            z-index: -1;
        }

        .hero-overlay {
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 0, 0.5); 
            z-index: 0;
        }

        .hero h1 {
            position: relative;
            z-index: 2;
            font-size: 3.5em;
            color: white;
            padding: 0 20px;
            max-width: 900px;
            text-shadow: 2px 2px 10px rgba(0,0,0,0.5);
        }

        /* 4. CONTENIDO Y SECCIONES */
        section {
            position: relative;
            z-index: 2; /* Encima del fondo animado */
            padding: 80px 10%;
            max-width: 1000px;
            margin: auto;
        }

        h2 {
            font-size: 2.2em;
            margin-bottom: 25px;
            border-left: 6px solid #411e10;
            padding-left: 20px;
        }
        .imagenes-dobles {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin: 40px 0;
        }

        .imagenes-dobles img {
            width: 100%;
            height: auto;
            border-radius: 14px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .imagenes-dobles img:hover {
            transform: translateY(-5px);
    
        }

        .grafica {
            text-align: center;
            margin: 50px 0;
        }

        .grafica img {
            width: 100%;
            max-width: 900px;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.15);
        }

        footer {
            background-color: #452d19;
            color: rgba(255, 255, 255, 0.8);
            text-align: center;
            padding: 20px 0;
            position: relative;
            z-index: 2;
            font-size: 0.9em;
            border-top: 1px solid rgba(255,255,255,0.1);
        }

        footer p {
            margin: 5px 0;
            display: inline-block;
            padding: 0 15px;
        }

    
        @media(max-width: 768px) {
            .imagenes-dobles { grid-template-columns: 1fr; }
            .hero h1 { font-size: 2.2em; }
            section { padding: 50px 5%; }
            .fondo-onda { width: 250%; height: 250%; top: -75%; left: -75%; } 
        }

        .seccion-video {
            position: relative;
            width: 100%;
            min-height: 60vh; 
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden; 
            color: white;
        }

         .video-fondo-seccion {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100%;
            height: 100%;
            object-fit: cover; 
         transform: translate(-50%, -50%);
           z-index: 0;
        }
        .capa-oscura {
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 0, 0.5); 
            z-index: 1;
        }

        .contenido-video {
            position: relative;
            z-index: 2; 
            text-align: center;
            padding: 40px;
        }

        .contenido-video h2 {
            color: #241a08; 
            border: none;
            font-size: 2.5em;
        }

        .menu-navegacion {
            position: fixed !important;
            top: 20px !important;
            left: 50% !important;
            transform: translateX(-50%) !important;
            width: auto !important; 
            min-width: 600px;
            background-color: rgba(69, 45, 25, 0.85) !important;
            backdrop-filter: blur(10px);
            border-radius: 50px !important;
            padding: 5px 20px !important;
            z-index: 9999 !important; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            border: 1px solid rgba(255,255,255,0.1);
            transition: all 0.4s ease !important;

        }

        .menu-navegacion.reducido {
            top: 5px !important;
            padding: 0px 20px !important; 
            min-width: 450px; !important
            background-color: rgba(40, 25, 15, 0.8) !important; 
            transform: translateX(-50%) scale(0.9) !important; 

        }

        .menu-navegacion.reducido a {
            font-size: 15px !important;
            text-decoration: none !important;
            color: #f7f3ee !important;
            font-weight: 500;
            white-space: nowrap;
        }


        .menu-navegacion ul {
            display: flex !important;
            flex-direction: row !important;
            list-style: none !important;
            list-style-type: none !important;   /* QUITA LOS PUNTOS */
            margin: 0 !important;
            padding: 0 !important;
            align-items: center !important;
            justify-content: center !important;
            height: 40px;
        }

        .menu-navegacion li {
            margin: 0 15px !important; /* Espacio entre palabras */
            list-style: none !important;
            background: none !important;
            padding: 0 !important;
            
        }

        .menu-navegacion a {
            text-decoration: none !important;
            color: #f7f3ee !important;
            font-size: 15px;
            font-weight: 500;
            transition: 0.3s;
            display: block !important;

        }

        .menu-navegacion a:hover {
            color: #473513 !important; 
            background-color: rgba(230, 218, 191, 0.768) !important; 
            transform: translateY(-2px) !important;
        }


    </style>
</head>

<body>

<nav class="menu-navegacion">
    <ul>
        <li><a href="#percepcion">Percepción</a></li>
        <li><a href="#realidad">Felicidad</a></li>
        <li><a href="#desafíos">Desafíos</a></li>
        <li><a href="#evolución">Evolución</a></li>
        <li><a href="#latam">Comparación</a></li>
        <li><a href="#Metodología">Metodología</a></li>
    </ul>
</nav>

<div class="fondo-onda" id="onda"></div>

<header class="hero">
    <video autoplay muted loop playsinline class="video-bg">
        <source src="videos/ctg.mp4" type="video/mp4">
    </video>
    <div class="hero-overlay"></div>
    <h1><strong>¿Es Colombia tan feliz como creemos?</strong></h1>
</header>

<main>
    <section id="percepcion">
        <h2>La Percepción Cultural de la Alegría</h2>
        <p>Tradicionalmente, Colombia ha proyectado una imagen de optimismo y vitalidad. La música, el baile, el fútbol y la vida social ocupan un lugar central en la cotidianidad y fortalecen los vínculos comunitarios, lo que contribuye a una percepción generalizada de alegría y cercanía entre las personas.</p>
        <p>No obstante, aunque estas expresiones culturales influyen positivamente en el bienestar emocional, no siempre se traducen en altos niveles de felicidad cuando se evalúan indicadores estructurales. En este sentido, se hace evidente una diferencia entre la experiencia subjetiva de alegría y las condiciones materiales e institucionales que sostienen el bienestar a largo plazo.</p>

        <div class="imagenes-dobles">
            <img src="imagenes/palenqueras.jpg" alt="Palenqueras en Cartagena">
            <img src="imagenes/sonrisa.jpg" alt="Colombianos orgullosos">
        </div>
    </section>

   <section id="realidad" style="padding:60px 10%;">

    <div style="display:flex; gap:40px; align-items:flex-start; flex-wrap:wrap;">

        <div style="flex:1; min-width:280px;">
            <img src="imagenes/realidad.jpg" alt="Realidad social en Colombia" 
            style="width:100%; max-width:350px; height:auto; object-fit:cover; border-radius:6px; border:8px solid #3E2C23;">
        </div>

        <div style="flex:2; min-width:280px; text-align:left; line-height:1.8;">

            <h2 style="margin-top:0; border:none; padding-left:0; line-height:1.2;">
            Entonces… ¿de qué depende realmente la felicidad en Colombia?
            </h2>

            <p>
            La felicidad no puede entenderse únicamente como una emoción individual o un estado pasajero, sino como el resultado de factores sociales y económicos que influyen en la vida diaria. En Colombia, el ingreso, la estabilidad laboral, el acceso a salud y educación, y la confianza en las instituciones tienen un impacto directo en la percepción de bienestar.
            </p>

            <p>
            Además, la estabilidad política, la seguridad ciudadana y las oportunidades de movilidad social determinan cómo las personas evalúan su calidad de vida. Aunque culturalmente exista optimismo y resiliencia, las limitaciones estructurales pueden afectar esa percepción.
            </p>

            <p>
            Por ello, comprender la felicidad en el país exige mirar más allá de los estereotipos y analizar las condiciones reales que permiten —o dificultan— un bienestar sostenible.
            </p>

        </div>

    </div>

    </section>

    <section class="seccion-video" id="desafíos">
        <video autoplay muted loop playsinline class="video-fondo-seccion">
        <source src="videos/pobreza.mp4" type="video/mp4">
        </video>
         <div class="capa-oscura"></div>

        <div class="contenido-video">
             <h2>Desafíos estructurales y realidad social</h2>
            <p>A pesar de su resiliencia cultural, Colombia enfrenta desafíos estructurales persistentes. La desigualdad económica, la informalidad laboral y las brechas en acceso a servicios básicos limitan la estabilidad y la seguridad de amplios sectores de la población.</p>
            <p>Además, la percepción de corrupción y la polarización política han debilitado la confianza en las instituciones. Según el World Happiness Report, la confianza institucional es uno de los factores más determinantes del bienestar subjetivo, lo que explica por qué la alegría cultural no siempre se traduce en altos niveles de felicidad sostenida.</p>
    
            <div class="imagenes-dobles">
                <img src="imagenes/ayno.jpg" alt="Descripción 1">
                <img src="imagenes/2.jpg" alt="Descripción 2">
            </div>
        </div>
    </section>

    <section id="evolución">
        <h2>Evolución del Coeficiente de Felicidad en Colombia (2011–2024)</h2>
        <div class="grafica">
            <img src="imagenes/grafica_colombia.png" alt="Gráfica felicidad Colombia">
        </div>
         <p>La evolución del coeficiente de felicidad en Colombia evidencia un comportamiento variable a lo largo del periodo analizado. Entre 2011 y 2015 se observa un aumento sostenido del indicador, lo que coincide con un contexto de crecimiento económico relativamente estable y con un clima de expectativas positivas frente a los procesos políticos y sociales del país. Durante estos años, la percepción de bienestar y de estabilidad futura fue más favorable.</p>
         <p>No obstante, a partir de 2016 se inicia una tendencia descendente gradual, asociada a un deterioro progresivo de factores estructurales como la confianza en las instituciones, la percepción de seguridad económica y la cohesión social. Esta disminución se acentúa entre 2019 y 2022, periodo marcado por la pandemia, la crisis económica global y el aumento de tensiones sociales internas, lo que impactó de manera significativa la percepción de bienestar de la población.</p>
         <p>Finalmente, en 2023 y 2024 se observa una recuperación parcial del indicador. Aunque este repunte sugiere una capacidad de adaptación y resiliencia social, los niveles de felicidad aún no alcanzan los máximos registrados en la primera mitad del periodo analizado, lo que pone de manifiesto la persistencia de desafíos estructurales que limitan una recuperación más sólida y sostenida.</p>
        
        </div>
    </section>

    <section id="latam">
        <h2>Comparación Regional: Latinoamérica en 2024</h2>
        
         <p>La gráfica permite observar las diferencias en los niveles de felicidad entre los países latinoamericanos en 2024, así como la contribución relativa de los distintos componentes que explican el puntaje total. En este contexto, Colombia se ubica en una posición intermedia dentro del ranking regional, por debajo de países como Costa Rica, México y Uruguay, pero por encima de otras economías de la región.</p>
         <p>Los países con mayores niveles de felicidad presentan puntajes más altos en variables estructurales como el apoyo social, el ingreso per cápita y la libertad para tomar decisiones, lo que sugiere una mayor estabilidad institucional y mejores condiciones de bienestar general. En contraste, en países con menores niveles de felicidad se observa un mayor peso del componente residual, lo que refleja debilidades estructurales y una menor contribución de factores asociados al desarrollo y la confianza social.</p>
         <p>En el caso de Colombia, el gráfico muestra que el apoyo social y las redes familiares contribuyen de manera significativa al bienestar percibido. Sin embargo, esta fortaleza se ve limitada por menores resultados en variables como ingreso y percepción de corrupción, lo que explica su ubicación intermedia en la región. En conjunto, la comparación regional evidencia que, si bien la cultura y los vínculos sociales son relevantes, la felicidad sostenible depende en gran medida de condiciones estructurales sólidas que garanticen estabilidad, confianza y oportunidades equitativas.</p>
        
         <div class="grafica">
            <img src="imagenes/grafica_latam.jpeg" alt="Comparación Latinoamérica"style="max-height:350px; width:100%; object-fit:contain;">
        </div>
    </section>

    <section id="Metodología">
        <h2>Metodología y Fuentes de Datos</h2>
        <p> Este análisis se basa en información del <a href="https://www.worldhappiness.report/ed/2025/" target="_blank" style="color:#C49A2C; text-decoration:underline; font-style:italic; font-weight:500;">
        World Happiness Report 2025
        </a>, 
        el cual evalúa la felicidad a partir de encuestas globales y seis variables fundamentales.
        </p>
        <p>Las visualizaciones fueron elaboradas utilizando Python y herramientas de análisis de datos, y posteriormente integradas en esta página web para presentar los resultados de forma clara, comparativa y narrativa.</p>
    </section>
</main>

<footer style="background-color:#3E2C23; color:white; padding:45px 20px; text-align:center;">

    <div style="display:flex; justify-content:center; gap:30px; flex-wrap:wrap; margin-bottom:35px;">

        <div style="background-color:#4A352B; padding:18px 22px; border-radius:10px; width:220px;">
            <p style="margin:0 0 8px 0; font-size:16px;">
                <strong>Elías Castro</strong>
            </p>
            <a href="mailto:eliacastro@utb.edu.co" style="color:#F6BD60; text-decoration:none; font-size:13px;">
                eliacastro@utb.edu.co
            </a>
        </div>

        <div style="background-color:#4A352B; padding:18px 22px; border-radius:10px; width:220px;">
            <p style="margin:0 0 8px 0; font-size:16px;">
                <strong>Leidy Velásquez</strong>
            </p>
            <a href="mailto:levelasquez@utb.edu.co" style="color:#F6BD60; text-decoration:none; font-size:13px;">
                levelasquez@utb.edu.co
            </a>
        </div>

        <div style="background-color:#4A352B; padding:18px 22px; border-radius:10px; width:220px;">
            <p style="margin:0 0 8px 0; font-size:16px;">
                <strong>Alejandra Guerrero</strong>
            </p>
            <a href="mailto:aleguerrero@utb.edu.co" style="color:#F6BD60; text-decoration:none; font-size:13px;">
                aleguerrero@utb.edu.co
            </a>
        </div>

        <div style="background-color:#4A352B; padding:18px 22px; border-radius:10px; width:220px;">
            <p style="margin:0 0 8px 0; font-size:16px;">
                <strong>Mathias Franceschi</strong>
            </p>
            <a href="mailto:mfranceschi@utb.edu.co" style="color:#F6BD60; text-decoration:none; font-size:13px;">
                mfranceschi@utb.edu.co
            </a>
        </div>

    </div>

    <div style="display:flex; justify-content:center; gap:70px; flex-wrap:wrap; font-size:14px; opacity:0.9;">
        <p style="margin:0;">
            Proyecto Académico<br>
            <strong>Felicidad en Colombia</strong>
        </p>
        <p style="margin:0;">
            Ciencia de Datos<br>
            <strong>UTB</strong>
        </p>
        <p style="margin:0;">
            <strong>Marzo 2026</strong>
        </p>
    </div>

</footer>


<script>
    const onda = document.getElementById("onda");

    // Escuchamos el movimiento del mouse en todo el documento
    document.addEventListener("mousemove", (e) => {
        if (onda) {
            // clientX y clientY dan la posición exacta del puntero
            onda.style.setProperty('--x', e.clientX + 'px');
            onda.style.setProperty('--y', e.clientY + 'px');
        }
    });

    // Lógica extra para el menú reducido
    const miNav = document.querySelector(".menu-navegacion");
    
    window.addEventListener("scroll", () => {
        
        if (window.scrollY > 50) {
            miNav.classList.add("reducido");
        } else {
            miNav.classList.remove("reducido");
        }
    });
</script>

</body>
</html></P>
</footer>

<script>
    const onda = document.getElementById("onda");

    // Escuchamos el movimiento del mouse en todo el documento
    document.addEventListener("mousemove", (e) => {
        if (onda) {
            // clientX y clientY dan la posición exacta del puntero
            onda.style.setProperty('--x', e.clientX + 'px');
            onda.style.setProperty('--y', e.clientY + 'px');
        }
    });

    // Lógica extra para el menú reducido
    const miNav = document.querySelector(".menu-navegacion");
    
    window.addEventListener("scroll", () => {
        
        if (window.scrollY > 50) {
            miNav.classList.add("reducido");
        } else {
            miNav.classList.remove("reducido");
        }
    });
</script>

</body>
</html>
