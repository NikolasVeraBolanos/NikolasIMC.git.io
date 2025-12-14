<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de IMC - Nikolas Vera Bolaños</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            background: linear-gradient(135deg, #1a1a1a 0%, #000000 100%);
            color: #ffffff;
            font-family: 'Montserrat', sans-serif;
            margin: 0;
            padding: 0;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        header {
            text-align: center;
            padding: 40px 20px;
            background: rgba(0, 0, 0, 0.7);
            width: 100%;
            box-shadow: 0 4px 10px rgba(0,0,0,0.5);
        }
        h1 {
            font-size: 2.5em;
            margin: 0;
            color: #ff1a1a;
            text-shadow: 0 2px 5px rgba(255,26,26,0.3);
        }
        h2 {
            font-size: 1.3em;
            margin: 10px 0;
            color: #cccccc;
        }
        #logo {
            max-width: 300px;
            margin: 20px auto;
            border-radius: 15px;
            border: 5px solid #ff1a1a;
            box-shadow: 0 0 30px rgba(255,26,26,0.5);
            display: block;
            transition: transform 0.3s;
        }
        #logo:hover {
            transform: scale(1.05);
        }
        .container {
            max-width: 800px;
            width: 90%;
            margin: 40px auto;
            background: rgba(255, 255, 255, 0.05);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.6);
            backdrop-filter: blur(5px);
        }
        form {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-bottom: 30px;
        }
        label {
            font-size: 1.1em;
            font-weight: 600;
        }
        input {
            padding: 15px;
            font-size: 1.1em;
            border: none;
            border-radius: 10px;
            background: rgba(255,255,255,0.1);
            color: white;
            outline: none;
            transition: all 0.3s;
        }
        input:focus {
            background: rgba(255,255,255,0.2);
            box-shadow: 0 0 10px rgba(255,26,26,0.5);
        }
        button {
            padding: 15px 30px;
            font-size: 1.2em;
            font-weight: bold;
            background: #ff1a1a;
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            align-self: center;
        }
        button:hover {
            background: #e60000;
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(255,26,26,0.4);
        }
        #result {
            margin: 30px 0;
            padding: 20px;
            background: rgba(255,26,26,0.15);
            border-radius: 10px;
            font-size: 1.4em;
            font-weight: bold;
        }
        #plan {
            margin-top: 30px;
            line-height: 1.6;
        }
        #plan h3 {
            text-align: center;
            color: #ff1a1a;
            font-size: 1.8em;
        }
        #plan h4 {
            color: #ff4d4d;
            border-bottom: 2px solid #ff1a1a;
            padding-bottom: 5px;
        }
        ul {
            padding-left: 20px;
        }
        li {
            margin: 12px 0;
            padding: 10px;
            background: rgba(255,255,255,0.05);
            border-radius: 8px;
        }
        footer {
            margin-top: auto;
            padding: 20px;
            text-align: center;
            font-size: 0.9em;
            color: #888;
            width: 100%;
        }
        @media (max-width: 600px) {
            h1 { font-size: 2em; }
            #logo { max-width: 250px; }
        }
    </style>
</head>
<body>
    <header>
        <h1>Nikolas Vera Bolaños</h1>
        <h2>Futuro Entrenador de Kickboxing</h2>
        <img id="logo" src="https://i.postimg.cc/HV09yg89/image.png" alt="Nikolas Kickboxing">
    </header>

    <div class="container">
        <p style="text-align:center; font-size:1.2em;">
            Calcula tu IMC y recibe un plan de entrenamiento personalizado de un mes, adaptado al kickboxing según tu condición física.
        </p>

        <form id="imcForm">
            <label for="height">Estatura (en cm):</label>
            <input type="number" id="height" placeholder="Ej: 175" required>

            <label for="weight">Peso (en kg):</label>
            <input type="number" id="weight" placeholder="Ej: 70" required>

            <button type="button" onclick="calculateIMC()">Calcular mi IMC y Plan</button>
        </form>

        <div id="result"></div>
        <div id="plan"></div>
    </div>

    <footer>
        © 2025 Nikolas Vera Bolaños - Todos los derechos reservados
    </footer>

    <script>
        function calculateIMC() {
            const height = parseFloat(document.getElementById('height').value) / 100;
            const weight = parseFloat(document.getElementById('weight').value);
            if (isNaN(height) || isNaN(weight) || height <= 0 || weight <= 0) {
                document.getElementById('result').innerHTML = '<p style="color:#ff8080;">Por favor, ingresa valores válidos.</p>';
                document.getElementById('plan').innerHTML = '';
                return;
            }
            const imc = weight / (height * height);
            const category = getCategory(imc);
            document.getElementById('result').innerHTML = `
                <p>¡Hola Nikolas!</p>
                <p>Tu IMC es <strong>${imc.toFixed(2)}</strong></p>
                <p>Categoría: <strong>${category.category}</strong></p>
            `;
            displayPlan(category.intensity);
        }

        function getCategory(imc) {
            if (imc < 18.5) {
                return { category: 'Bajo peso', intensity: 'baja' };
            } else if (imc < 25) {
                return { category: 'Peso normal', intensity: 'media' };
            } else if (imc < 30) {
                return { category: 'Sobrepeso', intensity: 'alta' };
            } else {
                return { category: 'Obesidad', intensity: 'alta-adaptada' };
            }
        }

        function displayPlan(intensity) {
            let intensidadTexto = '';
            switch(intensity) {
                case 'baja': intensidadTexto = 'Baja (enfoque en ganancia progresiva y técnica)'; break;
                case 'media': intensidadTexto = 'Media (ideal para progreso óptimo)'; break;
                case 'alta': intensidadTexto = 'Alta (máximo rendimiento y quema)'; break;
                case 'alta-adaptada': intensidadTexto = 'Alta adaptada (progresiva y segura)'; break;
            }

            let planHTML = `<h3>Tu Plan de Entrenamiento Personalizado - 1 Mes</h3>`;
            planHTML += `<p><strong>Nikolas Vera Bolaños</strong>, este plan está diseñado específicamente para ti como futuro entrenador de kickboxing. Intensidad: <strong>${intensidadTexto}</strong>.</p>`;
            planHTML += `<p>Entrena 4-5 días por semana. Siempre calienta 10 minutos y enfría con estiramientos.</p>`;

            const weeks = [
                { week: 1, focus: 'Adaptación y base técnica' },
                { week: 2, focus: 'Construcción de fuerza y resistencia' },
                { week: 3, focus: 'Mejora técnica avanzada y potencia' },
                { week: 4, focus: 'Pico de rendimiento y recuperación activa' }
            ];

            weeks.forEach(week => {
                planHTML += `<h4>Semana ${week.week}: ${week.focus}</h4><ul>`;
                planHTML += getDayPlan('Día 1: Fuerza y acondicionamiento', intensity);
                planHTML += getDayPlan('Día 2: Resistencia cardiovascular + sombra', intensity);
                planHTML += getDayPlan('Día 3: Técnica de golpes y patadas', intensity);
                planHTML += getDayPlan('Día 4: Movilidad, core y recuperación activa', intensity);
                planHTML += getDayPlan('Día 5: Sesión completa (sparring ligero opcional)', intensity);
                planHTML += '<li><strong>Días 6-7:</strong> Descanso activo (caminata, yoga o completo descanso).</li></ul>';
            });

            planHTML += '<p style="text-align:center; font-weight:bold; color:#ff1a1a;">¡Consistencia es clave, Nikolas! Tú puedes llegar a ser un gran entrenador.</p>';

            document.getElementById('plan').innerHTML = planHTML;
        }

        function getDayPlan(day, intensity) {
            let details = '';
            switch (intensity) {
                case 'baja':
                    details = `${day}: 30-40 min. Ritmo suave, enfoque en forma correcta y recuperación.`;
                    break;
                case 'media':
                    details = `${day}: 45-60 min. Ritmo moderado-alto, series de 3-4 con buena técnica.`;
                    break;
                case 'alta':
                    details = `${day}: 60-75 min. Alta intensidad, circuitos HIIT, mayor volumen.`;
                    break;
                case 'alta-adaptada':
                    details = `${day}: 45-55 min. Intensidad controlada, ejercicios de bajo impacto alternados con técnica.`;
                    break;
            }
            return `<li>${details}</li>`;
        }
    </script>
</body>
</html>
