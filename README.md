HTML
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Consulta Tu Número - Sorteos Diarios (Colores)</title>
  <style>
    :root {
      --primary: #16a34a; /* Verde principal para acentos */
      --primary-dark: #15803d;
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --text: #0f172a;

      /* === COLORES DE ESTADOS === */
      /* AZUL: PAGADO */
      --pagado-bg: #dbeafe; /* Azul muy claro */
      --pagado-text: #1d4ed8; /* Azul fuerte */

      /* ROJO: NO PAGADO */
      --nopagado-bg: #fee2e2; /* Rojo muy claro */
      --nopagado-text: #991b1b; /* Rojo fuerte */

      /* VERDE: DISPONIBLE */
      --disponible-bg: #dcfce7; /* Verde muy claro */
      --disponible-text: #166534; /* Verde fuerte */

      /* GRIS: RESERVADO (POR DEFECTO/GRUPO) */
      --reservado-bg: #f1f5f9; /* Gris muy claro */
      --reservado-text: #475569; /* Gris fuerte */
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: system-ui, -apple-system, sans-serif; }
    body { background-color: var(--bg); color: var(--text); padding: 15px; }
    .container { max-width: 800px; margin: 0 auto; }

    /* Header & Timer */
    header { text-align: center; margin-bottom: 20px; }
    h1 { font-size: 2.2rem; color: var(--primary-dark); margin-bottom: 10px; font-weight: 800; } 
    
    .timer-box {
      background: var(--card-bg);
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 20px;
      text-align: center;
    }
    .timer-title { font-weight: bold; font-size: 0.9rem; color: #64748b; text-transform: uppercase; }
    .draw-schedule { 
      font-size: 1.4rem; 
      font-weight: bold; 
      color: var(--primary); 
      margin-top: 6px; 
    }

    /* Search Bar */
    .search-box {
      display: flex;
      gap: 8px;
      margin-bottom: 20px;
    }
    .search-box input {
      flex: 1;
      padding: 12px 16px;
      border: 1px solid #cbd5e1;
      border-radius: 8px;
      font-size: 1rem;
      outline: none;
    }
    .search-box button {
      padding: 12px 18px;
      background: #64748b;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
    }

    /* Grid layout */
    .section-title { font-size: 1.1rem; margin-bottom: 10px; font-weight: bold; }
    .grid-container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(65px, 1fr));
      gap: 8px;
      background: var(--card-bg);
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 20px;
    }
    .grid-item {
      padding: 8px 4px;
      border-radius: 6px;
      text-align: center;
      font-size: 0.85rem;
      font-weight: bold;
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    /* === ESTILOS CSS PARA CADA ESTADO === */
    .grid-item.PAGADO { background: var(--pagado-bg); color: var(--pagado-text); border: 1px solid var(--pagado-text); }
    .grid-item.NO_PAGADO { background: var(--nopagado-bg); color: var(--nopagado-text); border: 1px solid var(--nopagado-text); }
    .grid-item.DISPONIBLE { background: var(--disponible-bg); color: var(--disponible-text); border: 1px solid var(--disponible-text); }
    .grid-item.RESERVADO_GRUPO { background: var(--reservado-bg); color: var(--reservado-text); border: 1px solid var(--reservado-text); }

    .grid-item .contact { font-size: 0.65rem; font-weight: normal; opacity: 0.8; word-break: break-all; }

    /* Table */
    .table-container {
      background: var(--card-bg);
      border-radius: 12px;
      overflow-x: auto;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 20px;
    }
    table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.9rem; }
    th, td { padding: 12px 16px; border-bottom: 1px solid #e2e8f0; }
    th { background: #f1f5f9; color: #475569; font-weight: bold; }
    
    /* Badges de tabla */
    .badge {
      display: inline-block;
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 0.75rem;
      font-weight: bold;
    }
    .badge.PAGADO { background: var(--pagado-bg); color: var(--pagado-text); }
    .badge.NO_PAGADO { background: var(--nopagado-bg); color: var(--nopagado-text); }
    .badge.DISPONIBLE { background: var(--disponible-bg); color: var(--disponible-text); }

    /* CTA Button */
    .cta-btn {
      display: block;
      width: 100%;
      text-align: center;
      background: #25d366;
      color: white;
      text-decoration: none;
      padding: 14px;
      font-size: 1.1rem;
      font-weight: bold;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(37, 211, 102, 0.3);
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <h1>🍀 FAMILIA LL 2 🍀<br>Consulta Tu Número</h1>
    </header>

    <!-- Próximo Sorteo (Hora Fija) -->
    <div class="timer-box">
      <div class="timer-title">Próximo Sorteo</div>
      <div class="draw-schedule">Sábado - 10:30 PM</div>
    </div>

    <!-- Buscador -->
    <div class="search-box">
      <input type="text" id="searchInput" placeholder="Buscar por Número, Nombre de Usuario o Celular..." onkeyup="filterData()">
      <button onclick="resetSearch()">Limpiar</button>
    </div>

    <!-- Matriz Visual de Números -->
    <div class="section-title">Disponibilidad y Pagos</div>
    <div class="grid-container" id="numbersGrid"></div>

    <!-- Tabla Detallada -->
    <div class="section-title">Listado de Reservas</div>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Número</th>
            <th>Contacto</th>
            <th>Estado</th>
            <th>Precio</th>
          </tr>
        </thead>
        <tbody id="tableBody"></tbody>
      </table>
    </div>

    <!-- Botón a WhatsApp -->
    <a href="https://chat.whatsapp.com/CmF7B6TZZq7FeYTDwHJDR5?s=sw&p=a&mlu=4&ilr=4" target="_blank" class="cta-btn">
      📲 UNIRSE AL GRUPO DE WHATSAPP
    </a>
  </div>

  <script>
    // 1. Datos del Sorteo
    const PRECIO_BOLETO = "$2.000";
    
    let baseData = [
      { num: "00", contacto: "Chachi Benitaz", estado: "PAGADO" },  
      { num: "01", contacto: "Lupita", estado: "NO_PAGADO" },
      { num: "02", contacto: "LIBRE", estado: "DISPONIBLE" },        
      { num: "03", contacto: "Kevin Correa", estado: "PAGADO" },    
      { num: "04", contacto: "Kevin Correa", estado: "NO_PAGADO" },
      { num: "05", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "06", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "07", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "08", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "09", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "10", contacto: "LIBRE", estado: "DISPONIBLE" },  
      { num: "11", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "12", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "13", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "14", contacto: "LIBRE", estado: "DISPONIBLE" },      
      { num: "15", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "16", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "17", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "18", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "19", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "20", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "21", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "22", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "23", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "24", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "25", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "26", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "27", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "28", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "29", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "30", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "31", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "32", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "33", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "34", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "35", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "36", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "37", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "38", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "39", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "40", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "41", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "42", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "43", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "44", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "45", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "46", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "47", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "48", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "49", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "50", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "51", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "52", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "53", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "54", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "55", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "56", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "57", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "58", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "59", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "60", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "61", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "62", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "63", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "64", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "65", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "66", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "67", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "68", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "69", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "70", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "71", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "72", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "73", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "74", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "75", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "76", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "77", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "78", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "79", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "80", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "81", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "82", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "83", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "84", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "85", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "86", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "87", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "88", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "89", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "90", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "91", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "92", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "93", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "94", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "95", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "96", contacto: "Kevin Correa", estado: "PAGO" }, 
      { num: "97", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "98", contacto: "LIBRE", estado: "DISPONIBLE" }, 
      { num: "99", contacto: "LIBRE", estado: "DISPONIBLE" }, 
    ];

    // Lógica para rellenar del 00 al 99
    const finalData = [];
    const definedNumbers = new Map(baseData.map(item => [item.num, item]));

    for (let i = 0; i < 100; i++) {
      const numStr = i.toString().padStart(2, '0');
      if (definedNumbers.has(numStr)) {
        finalData.push(definedNumbers.get(numStr));
      } else {
        finalData.push({ num: numStr, contacto: "RESERVADO GRUPO", estado: "RESERVADO_GRUPO" });
      }
    }

    // 2. Renderizar cuadrícula y tabla
    function render(data) {
      const grid = document.getElementById("numbersGrid");
      const tbody = document.getElementById("tableBody");
      grid.innerHTML = "";
      tbody.innerHTML = "";

      data.forEach(item => {
        let displayEstadoTable = item.estado;
        if(item.estado === "RESERVADO_GRUPO") displayEstadoTable = "RESERVADO";

        const gridItem = document.createElement("div");
        gridItem.className = `grid-item ${item.estado}`; 
        gridItem.innerHTML = `
          <span>${item.num}</span>
          <span class="contact">${item.contacto}</span>
        `;
        grid.appendChild(gridItem);

        if(item.estado === "PAGADO" || item.estado === "NO_PAGADO") {
          const row = document.createElement("tr");
          row.innerHTML = `
            <td><strong>${item.num}</strong></td>
            <td>${item.contacto}</td>
            <td><span class="badge ${item.estado}">${item.estado.replace('_', ' ')}</span></td>
            <td>${PRECIO_BOLETO}</td>
          `;
          tbody.appendChild(row);
        }
      });
    }

    // 3. Función de búsqueda
    function filterData() {
      const query = document.getElementById("searchInput").value.toLowerCase();
      const filtered = finalData.filter(item => 
        item.num.includes(query) || item.contacto.toLowerCase().includes(query)
      );
      render(filtered);
    }

    function resetSearch() {
      document.getElementById("searchInput").value = "";
      render(finalData);
    }

    // Inicializar
    render(finalData);
  </script>
</body>
</html>
