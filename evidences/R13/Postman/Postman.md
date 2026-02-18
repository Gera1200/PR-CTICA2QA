1. Post http://localhost:8000/login

username ---- deaj1
password -----Deaj123!

<!doctype html>
<html lang="es">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Trámites QA Demo</title>
    <link rel="stylesheet" href="/static/app.css">
</head>

<body>
    <header class="topbar">
        <div class="brand">Trámites QA (Demo)</div>

        <nav class="nav">
            <a href="/">Inicio</a>




            <a href="/deaj/tramites">Bandeja DEAJ</a>


            <a href="/logout">Salir (deaj1)</a>
        </nav>

    </header>

    <main class="container">

        <h1>Inicio (DEAJ)</h1>
        <div class="grid">
            <div class="card">
                <h3>ENVIADO</h3>
                <div class="big">0</div>
            </div>
            <div class="card">
                <h3>EN_REVISION</h3>
                <div class="big">0</div>
            </div>
            <div class="card">
                <h3>APROBADO</h3>
                <div class="big">1</div>
            </div>
            <div class="card">
                <h3>RECHAZADO</h3>
                <div class="big">0</div>
            </div>
        </div>
        <p><a class="btn" href="/deaj/tramites">Ir a bandeja DEAJ</a></p>

    </main>

    <footer class="footer">
        Demo para práctica QA: login + trámites + adjuntos PDF + validación DEAJ + auditoría.
    </footer>
</body>

</html>

2.GET http://localhost:8000/tramites/1

Internal Server Error

