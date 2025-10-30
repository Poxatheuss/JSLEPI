[index.html.html](https://github.com/user-attachments/files/23243456/index.html.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gestão de EPI</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --light-gray: #f5f5f5;
            --border-color: #ddd;
            --table-header: #2c3e50;
            --low-risk: #d4edda;
            --medium-risk: #fff3cd;
            --high-risk: #f8d7da;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Calibri', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f9f9f9;
            color: #333;
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
        }
        
        h1 {
            text-align: center;
            color: var(--primary-color);
            margin-bottom: 25px;
            font-size: 28px;
            padding: 15px;
            background: linear-gradient(135deg, #1a3a5f 0%, #2c3e50 100%);
            color: white;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .dashboard-card {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            text-align: center;
            border-top: 4px solid var(--secondary-color);
        }
        
        .dashboard-card.warning {
            border-top-color: var(--warning-color);
        }
        
        .dashboard-card.danger {
            border-top-color: var(--accent-color);
        }
        
        .dashboard-card h3 {
            font-size: 14px;
            color: #7f8c8d;
            margin-bottom: 10px;
        }
        
        .dashboard-card .value {
            font-size: 28px;
            font-weight: bold;
            color: var(--primary-color);
        }
        
        .dashboard-card .subtext {
            font-size: 12px;
            color: #95a5a6;
            margin-top: 5px;
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid var(--border-color);
            flex-wrap: wrap;
        }
        
        .tab {
            padding: 12px 24px;
            cursor: pointer;
            background: #f8f9fa;
            border: 1px solid var(--border-color);
            border-bottom: none;
            margin-right: 5px;
            border-radius: 5px 5px 0 0;
            font-weight: 500;
            transition: all 0.3s;
        }
        
        .tab.active {
            background: white;
            border-bottom: 1px solid white;
            margin-bottom: -1px;
            font-weight: bold;
            color: var(--secondary-color);
        }
        
        .tab:hover {
            background: #e9ecef;
        }
        
        .tab-content {
            display: none;
            padding: 20px 0;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            margin-right: 10px;
            transition: all 0.3s;
            font-size: 14px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }
        
        .btn-primary {
            background: linear-gradient(to right, #3498db, #2980b9);
            color: white;
        }
        
        .btn-primary:hover {
            background: linear-gradient(to right, #2980b9, #1c6ea4);
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
        }
        
        .btn-success {
            background: linear-gradient(to right, #27ae60, #219653);
            color: white;
        }
        
        .btn-success:hover {
            background: linear-gradient(to right, #219653, #1e7e34);
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
        }
        
        .btn-danger {
            background: linear-gradient(to right, #e74c3c, #c0392b);
            color: white;
        }
        
        .btn-danger:hover {
            background: linear-gradient(to right, #c0392b, #a93226);
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
        }
        
        .btn-warning {
            background: linear-gradient(to right, #f39c12, #e67e22);
            color: white;
        }
        
        .btn-warning:hover {
            background: linear-gradient(to right, #e67e22, #d35400);
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
        }
        
        .btn-sm {
            padding: 8px 15px;
            font-size: 12px;
        }
        
        .actions {
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .search-box {
            display: flex;
            margin-bottom: 20px;
        }
        
        .search-box input {
            flex: 1;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 4px 0 0 4px;
            font-size: 14px;
        }
        
        .search-box button {
            padding: 12px 20px;
            background: var(--secondary-color);
            color: white;
            border: none;
            border-radius: 0 4px 4px 0;
            cursor: pointer;
        }
        
        .table-container {
            overflow-x: auto;
            margin-bottom: 25px;
            border: 1px solid var(--border-color);
            border-radius: 5px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.1);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
        }
        
        th, td {
            border: 1px solid var(--border-color);
            padding: 12px;
            text-align: left;
        }
        
        th {
            background: linear-gradient(to bottom, #3a5795, #2c3e50);
            color: white;
            font-weight: bold;
            position: sticky;
            top: 0;
        }
        
        tr:nth-child(even) {
            background-color: var(--light-gray);
        }
        
        .status-badge {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }
        
        .status-valid {
            background-color: var(--low-risk);
            color: #155724;
        }
        
        .status-warning {
            background-color: var(--medium-risk);
            color: #856404;
        }
        
        .status-expired {
            background-color: var(--high-risk);
            color: #721c24;
        }
        
        .status-low-stock {
            background-color: var(--high-risk);
            color: #721c24;
        }
        
        .status-ok {
            background-color: var(--low-risk);
            color: #155724;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.7);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 8px;
            width: 90%;
            max-width: 850px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 5px 20px rgba(0,0,0,0.3);
        }
        
        .form-group {
            margin-bottom: 18px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            font-size: 15px;
            color: var(--primary-color);
        }
        
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            font-size: 15px;
            transition: border-color 0.3s;
            font-family: 'Calibri', 'Segoe UI', sans-serif;
        }
        
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            border-color: var(--secondary-color);
            outline: none;
            box-shadow: 0 0 8px rgba(52, 152, 219, 0.4);
        }
        
        .form-row {
            display: flex;
            gap: 18px;
            margin-bottom: 18px;
        }
        
        .form-row .form-group {
            flex: 1;
        }
        
        .form-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 20px;
            gap: 15px;
        }
        
        .required::after {
            content: " *";
            color: #e74c3c;
        }
        
        @media (max-width: 768px) {
            .tabs {
                flex-direction: column;
            }
            
            .tab {
                margin-right: 0;
                margin-bottom: 5px;
                border-radius: 5px;
            }
            
            .tab.active {
                border-bottom: 1px solid var(--border-color);
                margin-bottom: 5px;
            }
            
            .form-row {
                flex-direction: column;
                gap: 0;
            }
            
            .actions {
                flex-direction: column;
            }
            
            .btn {
                margin-right: 0;
                margin-bottom: 10px;
                width: 100%;
            }
        }
        
        .logo {
            text-align: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid #eee;
        }
        
        .logo h1 {
            background: linear-gradient(135deg, #1a3a5f 0%, #2c3e50 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            color: transparent;
            font-size: 36px;
            margin-bottom: 8px;
            font-weight: bold;
        }
        
        .logo p {
            color: #7f8c8d;
            font-size: 16px;
            font-style: italic;
        }
        
        .instructions {
            background-color: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .instructions h4 {
            margin-bottom: 8px;
            color: #856404;
            display: flex;
            align-items: center;
        }
        
        .instructions h4::before {
            content: "💡";
            margin-right: 8px;
        }
        
        .save-indicator {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--success-color);
            color: white;
            padding: 10px 15px;
            border-radius: 4px;
            font-size: 14px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
            display: none;
            z-index: 1001;
        }
    </style>
</head>
<body>
    <div class="save-indicator" id="save-indicator">Dados salvos com sucesso!</div>
    
    <div class="container">
        <div class="logo">
            <h1>Sistema de Gestão de EPI</h1>
            <p>Controle completo de Equipamentos de Proteção Individual</p>
        </div>
        
        <div class="instructions">
            <h4>Instruções de Uso</h4>
            <p>Utilize as abas para navegar entre os diferentes módulos do sistema. Preencha todos os campos obrigatórios marcados com asterisco (*). <strong>Todos os dados são salvos automaticamente!</strong></p>
        </div>
        
        <div class="dashboard">
            <div class="dashboard-card">
                <h3>Total de EPIs Cadastrados</h3>
                <div class="value" id="total-epis">0</div>
                <div class="subtext">Itens no sistema</div>
            </div>
            <div class="dashboard-card">
                <h3>EPIs Vencidos</h3>
                <div class="value" id="epis-vencidos">0</div>
                <div class="subtext">Necessitam substituição</div>
            </div>
            <div class="dashboard-card warning">
                <h3>EPIs Próximos do Vencimento</h3>
                <div class="value" id="epis-proximo-vencimento">0</div>
                <div class="subtext">Vencem em menos de 30 dias</div>
            </div>
            <div class="dashboard-card danger">
                <h3>Estoques Baixos</h3>
                <div class="value" id="estoques-baixos">0</div>
                <div class="subtext">Necessitam reposição</div>
            </div>
        </div>
        
        <div class="tabs">
            <div class="tab active" data-tab="epis">Controle de EPIs</div>
            <div class="tab" data-tab="estoque">Controle de Estoque</div>
            <div class="tab" data-tab="entregas">Controle de Entregas</div>
            <div class="tab" data-tab="relatorios">Relatórios</div>
        </div>
        
        <!-- ABA: Controle de EPIs -->
        <div class="tab-content active" id="epis-tab">
            <div class="actions">
                <button class="btn btn-primary" id="btn-adicionar-epi">
                    ➕ Adicionar EPI
                </button>
                <div class="search-box">
                    <input type="text" id="search-epi" placeholder="Buscar EPI...">
                    <button onclick="filtrarEPIs()">🔍 Buscar</button>
                </div>
            </div>
            
            <div class="table-container">
                <table id="tabela-epis">
                    <thead>
                        <tr>
                            <th>NOME DO EPI</th>
                            <th>FABRICANTE</th>
                            <th>C.A</th>
                            <th>VALIDADE DO C.A</th>
                            <th>VALIDADE DO EPI</th>
                            <th>STATUS</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Os dados serão inseridos aqui via JavaScript -->
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- ABA: Controle de Estoque -->
        <div class="tab-content" id="estoque-tab">
            <div class="actions">
                <button class="btn btn-primary" id="btn-adicionar-estoque">
                    ➕ Adicionar ao Estoque
                </button>
                <div class="search-box">
                    <input type="text" id="search-estoque" placeholder="Buscar no estoque...">
                    <button onclick="filtrarEstoque()">🔍 Buscar</button>
                </div>
            </div>
            
            <div class="table-container">
                <table id="tabela-estoque">
                    <thead>
                        <tr>
                            <th>NOME DO EPI</th>
                            <th>SAÍDAS</th>
                            <th>ENTRADAS</th>
                            <th>ESTOQUE ATUAL</th>
                            <th>QNTD. MÍNIMA</th>
                            <th>STATUS</th>
                            <th>VALOR UNITÁRIO</th>
                            <th>GASTO TOTAL</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Os dados serão inseridos aqui via JavaScript -->
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- ABA: Controle de Entregas -->
        <div class="tab-content" id="entregas-tab">
            <div class="actions">
                <button class="btn btn-primary" id="btn-nova-entrega">
                    ➕ Nova Entrega
                </button>
                <div class="search-box">
                    <input type="text" id="search-entregas" placeholder="Buscar entregas...">
                    <button onclick="filtrarEntregas()">🔍 Buscar</button>
                </div>
            </div>
            
            <div class="table-container">
                <table id="tabela-entregas">
                    <thead>
                        <tr>
                            <th>DATA</th>
                            <th>NOME DO FUNCIONÁRIO</th>
                            <th>CARGO</th>
                            <th>SETOR</th>
                            <th>EPI</th>
                            <th>QNTD.</th>
                            <th>VALOR UNITÁRIO</th>
                            <th>VALOR TOTAL</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Os dados serão inseridos aqui via JavaScript -->
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- ABA: Relatórios -->
        <div class="tab-content" id="relatorios-tab">
            <div class="actions">
                <button class="btn btn-primary" id="btn-relatorio-epis">
                    📄 Relatório de EPIs
                </button>
                <button class="btn btn-success" id="btn-relatorio-estoque">
                    📄 Relatório de Estoque
                </button>
                <button class="btn btn-warning" id="btn-relatorio-entregas">
                    📄 Relatório de Entregas
                </button>
                <button class="btn btn-danger" id="btn-backup">
                    💾 Backup Completo
                </button>
            </div>
            
            <div class="dashboard" style="grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));">
                <div class="dashboard-card">
                    <h3>EPIs por Status</h3>
                    <div id="chart-status" style="height: 200px; display: flex; align-items: center; justify-content: center;">
                        <canvas id="statusChart" width="200" height="200"></canvas>
                    </div>
                </div>
                <div class="dashboard-card">
                    <h3>Top 5 EPIs Mais Utilizados</h3>
                    <div id="chart-top-epis" style="height: 200px; display: flex; align-items: center; justify-content: center;">
                        <canvas id="topEpisChart" width="200" height="200"></canvas>
                    </div>
                </div>
                <div class="dashboard-card">
                    <h3>Gastos por Categoria</h3>
                    <div id="chart-gastos" style="height: 200px; display: flex; align-items: center; justify-content: center;">
                        <canvas id="gastosChart" width="200" height="200"></canvas>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Modal para Adicionar/Editar EPI -->
    <div class="modal" id="modal-epi">
        <div class="modal-content">
            <h2 id="modal-epi-titulo">Adicionar Novo EPI</h2>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="nome-epi" class="required">NOME DO EPI:</label>
                    <input type="text" id="nome-epi" required>
                </div>
                
                <div class="form-group">
                    <label for="fabricante-epi">FABRICANTE DO EPI:</label>
                    <input type="text" id="fabricante-epi">
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="ca-epi">C.A:</label>
                    <input type="text" id="ca-epi">
                </div>
                
                <div class="form-group">
                    <label for="validade-ca">VALIDADE DO C.A:</label>
                    <input type="date" id="validade-ca">
                </div>
                
                <div class="form-group">
                    <label for="validade-epi">VALIDADE DO EPI:</label>
                    <input type="date" id="validade-epi">
                </div>
            </div>
            
            <div class="form-actions">
                <button class="btn btn-danger" id="btn-cancelar-epi">
                    ✖ Cancelar
                </button>
                <button class="btn btn-success" id="btn-salvar-epi">
                    💾 Salvar EPI
                </button>
            </div>
        </div>
    </div>
    
    <!-- Modal para Adicionar/Editar Estoque -->
    <div class="modal" id="modal-estoque">
        <div class="modal-content">
            <h2 id="modal-estoque-titulo">Adicionar ao Estoque</h2>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="epi-estoque" class="required">EPI:</label>
                    <select id="epi-estoque" required>
                        <option value="">Selecione um EPI...</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="entradas-estoque" class="required">ENTRADAS:</label>
                    <input type="number" id="entradas-estoque" min="0" required>
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="quantidade-minima" class="required">QUANTIDADE MÍNIMA:</label>
                    <input type="number" id="quantidade-minima" min="0" required>
                </div>
                
                <div class="form-group">
                    <label for="valor-unitario">VALOR UNITÁRIO (R$):</label>
                    <input type="number" id="valor-unitario" min="0" step="0.01">
                </div>
            </div>
            
            <div class="form-actions">
                <button class="btn btn-danger" id="btn-cancelar-estoque">
                    ✖ Cancelar
                </button>
                <button class="btn btn-success" id="btn-salvar-estoque">
                    💾 Salvar Estoque
                </button>
            </div>
        </div>
    </div>
    
    <!-- Modal para Nova Entrega -->
    <div class="modal" id="modal-entrega">
        <div class="modal-content">
            <h2 id="modal-entrega-titulo">Nova Entrega de EPI</h2>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="data-entrega" class="required">DATA:</label>
                    <input type="date" id="data-entrega" required>
                </div>
                
                <div class="form-group">
                    <label for="funcionario-entrega" class="required">NOME DO FUNCIONÁRIO:</label>
                    <input type="text" id="funcionario-entrega" required>
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="cargo-entrega">CARGO:</label>
                    <input type="text" id="cargo-entrega">
                </div>
                
                <div class="form-group">
                    <label for="setor-entrega">SETOR:</label>
                    <input type="text" id="setor-entrega">
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="epi-entrega" class="required">EPI:</label>
                    <select id="epi-entrega" required>
                        <option value="">Selecione um EPI...</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="quantidade-entrega" class="required">QUANTIDADE:</label>
                    <input type="number" id="quantidade-entrega" min="1" required>
                </div>
            </div>
            
            <div class="form-actions">
                <button class="btn btn-danger" id="btn-cancelar-entrega">
                    ✖ Cancelar
                </button>
                <button class="btn btn-success" id="btn-salvar-entrega">
                    💾 Registrar Entrega
                </button>
            </div>
        </div>
    </div>

    <script>
        // Inicialização do jsPDF
        const { jsPDF } = window.jspdf;
        
        // Variáveis globais
        let epis = [];
        let estoque = [];
        let entregas = [];
        let editandoIndex = -1;
        let editandoTipo = '';
        
        // Elementos DOM
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        const saveIndicator = document.getElementById('save-indicator');
        
        // Modais
        const modalEpi = document.getElementById('modal-epi');
        const modalEstoque = document.getElementById('modal-estoque');
        const modalEntrega = document.getElementById('modal-entrega');
        
        // Carregar dados salvos ao iniciar
        document.addEventListener('DOMContentLoaded', function() {
            carregarDados();
            atualizarDashboard();
            renderizarTabelas();
            
            // Event listeners para abas
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const tabId = tab.getAttribute('data-tab');
                    abrirTab(tabId);
                });
            });
            
            // Event listeners para botões
            document.getElementById('btn-adicionar-epi').addEventListener('click', () => abrirModalEpi());
            document.getElementById('btn-adicionar-estoque').addEventListener('click', () => abrirModalEstoque());
            document.getElementById('btn-nova-entrega').addEventListener('click', () => abrirModalEntrega());
            
            document.getElementById('btn-cancelar-epi').addEventListener('click', () => fecharModalEpi());
            document.getElementById('btn-cancelar-estoque').addEventListener('click', () => fecharModalEstoque());
            document.getElementById('btn-cancelar-entrega').addEventListener('click', () => fecharModalEntrega());
            
            document.getElementById('btn-salvar-epi').addEventListener('click', salvarEpi);
            document.getElementById('btn-salvar-estoque').addEventListener('click', salvarEstoque);
            document.getElementById('btn-salvar-entrega').addEventListener('click', salvarEntrega);
            
            // Event listeners para relatórios
            document.getElementById('btn-relatorio-epis').addEventListener('click', () => gerarRelatorioEPIs());
            document.getElementById('btn-relatorio-estoque').addEventListener('click', () => gerarRelatorioEstoque());
            document.getElementById('btn-relatorio-entregas').addEventListener('click', () => gerarRelatorioEntregas());
            document.getElementById('btn-backup').addEventListener('click', () => fazerBackup());
            
            // Event listeners para busca
            document.getElementById('search-epi').addEventListener('input', filtrarEPIs);
            document.getElementById('search-estoque').addEventListener('input', filtrarEstoque);
            document.getElementById('search-entregas').addEventListener('input', filtrarEntregas);
            
            // Fechar modais clicando fora
            window.addEventListener('click', function(event) {
                if (event.target === modalEpi) fecharModalEpi();
                if (event.target === modalEstoque) fecharModalEstoque();
                if (event.target === modalEntrega) fecharModalEntrega();
            });
            
            // Mostrar mensagem de dados carregados
            mostrarMensagem('Dados carregados com sucesso!');
        });
        
        // Função para mostrar mensagem de salvamento
        function mostrarMensagem(mensagem) {
            saveIndicator.textContent = mensagem;
            saveIndicator.style.display = 'block';
            setTimeout(() => {
                saveIndicator.style.display = 'none';
            }, 3000);
        }
        
        // Função para abrir aba
        function abrirTab(tabId) {
            tabs.forEach(tab => tab.classList.remove('active'));
            tabContents.forEach(content => content.classList.remove('active'));
            
            document.querySelector(`.tab[data-tab="${tabId}"]`).classList.add('active');
            document.getElementById(`${tabId}-tab`).classList.add('active');
            
            if (tabId === 'relatorios') {
                atualizarGraficos();
            }
        }
        
        // Função para calcular status do EPI (baseado na planilha)
        function calcularStatusEPI(validadeCA, validadeEPI) {
            const hoje = new Date();
            const umMes = new Date();
            umMes.setDate(hoje.getDate() + 30);
            
            if (!validadeCA && !validadeEPI) return "NÃO INFORMADO";
            
            const dataCA = validadeCA ? new Date(validadeCA) : null;
            const dataEPI = validadeEPI ? new Date(validadeEPI) : null;
            
            // Verificar se algum está vencido
            if ((dataCA && dataCA < hoje) || (dataEPI && dataEPI < hoje)) {
                return "VENCEU";
            }
            
            // Verificar se algum vence em menos de 30 dias
            if ((dataCA && dataCA <= umMes) || (dataEPI && dataEPI <= umMes)) {
                return "MENOS DE 1 MES";
            }
            
            return "VALIDO";
        }
        
        // Função para calcular status do estoque
        function calcularStatusEstoque(estoqueAtual, quantidadeMinima) {
            if (estoqueAtual < quantidadeMinima) {
                return "ESTOQUE BAIXO";
            }
            return "ESTOQUE OK";
        }
        
        // Função para abrir modal de EPI
        function abrirModalEpi(epiIndex = -1) {
            editandoIndex = epiIndex;
            editandoTipo = 'epi';
            
            const titulo = epiIndex === -1 ? "Adicionar Novo EPI" : "Editar EPI";
            document.getElementById('modal-epi-titulo').textContent = titulo;
            
            // Limpar ou preencher formulário
            if (epiIndex === -1) {
                document.getElementById('nome-epi').value = '';
                document.getElementById('fabricante-epi').value = '';
                document.getElementById('ca-epi').value = '';
                document.getElementById('validade-ca').value = '';
                document.getElementById('validade-epi').value = '';
            } else {
                const epi = epis[epiIndex];
                document.getElementById('nome-epi').value = epi.nome;
                document.getElementById('fabricante-epi').value = epi.fabricante || '';
                document.getElementById('ca-epi').value = epi.ca || '';
                document.getElementById('validade-ca').value = epi.validadeCA || '';
                document.getElementById('validade-epi').value = epi.validadeEPI || '';
            }
            
            modalEpi.style.display = 'flex';
        }
        
        // Função para abrir modal de estoque
        function abrirModalEstoque(estoqueIndex = -1) {
            editandoIndex = estoqueIndex;
            editandoTipo = 'estoque';
            
            const titulo = estoqueIndex === -1 ? "Adicionar ao Estoque" : "Editar Estoque";
            document.getElementById('modal-estoque-titulo').textContent = titulo;
            
            // Preencher select de EPIs
            const selectEpi = document.getElementById('epi-estoque');
            selectEpi.innerHTML = '<option value="">Selecione um EPI...</option>';
            
            epis.forEach(epi => {
                const option = document.createElement('option');
                option.value = epi.id;
                option.textContent = epi.nome;
                selectEpi.appendChild(option);
            });
            
            // Limpar ou preencher formulário
            if (estoqueIndex === -1) {
                document.getElementById('epi-estoque').value = '';
                document.getElementById('entradas-estoque').value = '';
                document.getElementById('quantidade-minima').value = '';
                document.getElementById('valor-unitario').value = '';
            } else {
                const itemEstoque = estoque[estoqueIndex];
                document.getElementById('epi-estoque').value = itemEstoque.epiId;
                document.getElementById('entradas-estoque').value = itemEstoque.entradas;
                document.getElementById('quantidade-minima').value = itemEstoque.quantidadeMinima;
                document.getElementById('valor-unitario').value = itemEstoque.valorUnitario || '';
            }
            
            modalEstoque.style.display = 'flex';
        }
        
        // Função para abrir modal de entrega
        function abrirModalEntrega(entregaIndex = -1) {
            editandoIndex = entregaIndex;
            editandoTipo = 'entrega';
            
            const titulo = entregaIndex === -1 ? "Nova Entrega de EPI" : "Editar Entrega";
            document.getElementById('modal-entrega-titulo').textContent = titulo;
            
            // Preencher select de EPIs
            const selectEpi = document.getElementById('epi-entrega');
            selectEpi.innerHTML = '<option value="">Selecione um EPI...</option>';
            
            epis.forEach(epi => {
                const option = document.createElement('option');
                option.value = epi.id;
                option.textContent = epi.nome;
                selectEpi.appendChild(option);
            });
            
            // Limpar ou preencher formulário
            if (entregaIndex === -1) {
                document.getElementById('data-entrega').value = new Date().toISOString().split('T')[0];
                document.getElementById('funcionario-entrega').value = '';
                document.getElementById('cargo-entrega').value = '';
                document.getElementById('setor-entrega').value = '';
                document.getElementById('epi-entrega').value = '';
                document.getElementById('quantidade-entrega').value = '1';
            } else {
                const entrega = entregas[entregaIndex];
                document.getElementById('data-entrega').value = entrega.data;
                document.getElementById('funcionario-entrega').value = entrega.funcionario;
                document.getElementById('cargo-entrega').value = entrega.cargo || '';
                document.getElementById('setor-entrega').value = entrega.setor || '';
                document.getElementById('epi-entrega').value = entrega.epiId;
                document.getElementById('quantidade-entrega').value = entrega.quantidade;
            }
            
            modalEntrega.style.display = 'flex';
        }
        
        // Funções para fechar modais
        function fecharModalEpi() {
            modalEpi.style.display = 'none';
        }
        
        function fecharModalEstoque() {
            modalEstoque.style.display = 'none';
        }
        
        function fecharModalEntrega() {
            modalEntrega.style.display = 'none';
        }
        
        // Função para salvar EPI
        function salvarEpi() {
            const nome = document.getElementById('nome-epi').value;
            
            if (!nome) {
                alert('Por favor, preencha o nome do EPI.');
                return;
            }
            
            const epi = {
                id: editandoIndex === -1 ? Date.now().toString() : epis[editandoIndex].id,
                nome: nome,
                fabricante: document.getElementById('fabricante-epi').value,
                ca: document.getElementById('ca-epi').value,
                validadeCA: document.getElementById('validade-ca').value,
                validadeEPI: document.getElementById('validade-epi').value,
                status: calcularStatusEPI(
                    document.getElementById('validade-ca').value,
                    document.getElementById('validade-epi').value
                )
            };
            
            if (editandoIndex === -1) {
                epis.push(epi);
            } else {
                epis[editandoIndex] = epi;
            }
            
            salvarDados();
            renderizarTabelas();
            atualizarDashboard();
            fecharModalEpi();
            mostrarMensagem('EPI salvo com sucesso!');
        }
        
        // Função para salvar estoque
        function salvarEstoque() {
            const epiId = document.getElementById('epi-estoque').value;
            const entradas = parseInt(document.getElementById('entradas-estoque').value);
            const quantidadeMinima = parseInt(document.getElementById('quantidade-minima').value);
            
            if (!epiId || isNaN(entradas) || isNaN(quantidadeMinima)) {
                alert('Por favor, preencha todos os campos obrigatórios.');
                return;
            }
            
            const epi = epis.find(e => e.id === epiId);
            if (!epi) {
                alert('EPI não encontrado.');
                return;
            }
            
            // Calcular saídas (soma das quantidades entregues para este EPI)
            const saidas = entregas
                .filter(e => e.epiId === epiId)
                .reduce((total, entrega) => total + entrega.quantidade, 0);
            
            const estoqueAtual = entradas - saidas;
            const status = calcularStatusEstoque(estoqueAtual, quantidadeMinima);
            const valorUnitario = parseFloat(document.getElementById('valor-unitario').value) || 0;
            const gastoTotal = saidas * valorUnitario;
            
            const itemEstoque = {
                id: editandoIndex === -1 ? Date.now().toString() : estoque[editandoIndex].id,
                epiId: epiId,
                epiNome: epi.nome,
                saidas: saidas,
                entradas: entradas,
                estoqueAtual: estoqueAtual,
                quantidadeMinima: quantidadeMinima,
                status: status,
                valorUnitario: valorUnitario,
                gastoTotal: gastoTotal
            };
            
            if (editandoIndex === -1) {
                estoque.push(itemEstoque);
            } else {
                estoque[editandoIndex] = itemEstoque;
            }
            
            salvarDados();
            renderizarTabelas();
            atualizarDashboard();
            fecharModalEstoque();
            mostrarMensagem('Estoque atualizado com sucesso!');
        }
        
        // Função para salvar entrega
        function salvarEntrega() {
            const data = document.getElementById('data-entrega').value;
            const funcionario = document.getElementById('funcionario-entrega').value;
            const epiId = document.getElementById('epi-entrega').value;
            const quantidade = parseInt(document.getElementById('quantidade-entrega').value);
            
            if (!data || !funcionario || !epiId || isNaN(quantidade)) {
                alert('Por favor, preencha todos os campos obrigatórios.');
                return;
            }
            
            const epi = epis.find(e => e.id === epiId);
            if (!epi) {
                alert('EPI não encontrado.');
                return;
            }
            
            // Verificar se há estoque suficiente
            const itemEstoque = estoque.find(e => e.epiId === epiId);
            if (itemEstoque && itemEstoque.estoqueAtual < quantidade) {
                alert(`Estoque insuficiente. Disponível: ${itemEstoque.estoqueAtual}`);
                return;
            }
            
            const valorUnitario = itemEstoque ? itemEstoque.valorUnitario : 0;
            const valorTotal = quantidade * valorUnitario;
            
            const entrega = {
                id: editandoIndex === -1 ? Date.now().toString() : entregas[editandoIndex].id,
                data: data,
                funcionario: funcionario,
                cargo: document.getElementById('cargo-entrega').value,
                setor: document.getElementById('setor-entrega').value,
                epiId: epiId,
                epiNome: epi.nome,
                quantidade: quantidade,
                valorUnitario: valorUnitario,
                valorTotal: valorTotal
            };
            
            if (editandoIndex === -1) {
                entregas.push(entrega);
            } else {
                entregas[editandoIndex] = entrega;
            }
            
            // Atualizar estoque
            if (itemEstoque) {
                itemEstoque.saidas += quantidade;
                itemEstoque.estoqueAtual = itemEstoque.entradas - itemEstoque.saidas;
                itemEstoque.status = calcularStatusEstoque(itemEstoque.estoqueAtual, itemEstoque.quantidadeMinima);
                itemEstoque.gastoTotal = itemEstoque.saidas * itemEstoque.valorUnitario;
            }
            
            salvarDados();
            renderizarTabelas();
            atualizarDashboard();
            fecharModalEntrega();
            mostrarMensagem('Entrega registrada com sucesso!');
        }
        
        // Função para excluir item
        function excluirItem(tipo, index) {
            if (!confirm('Tem certeza que deseja excluir este item?')) return;
            
            if (tipo === 'epi') {
                const epiId = epis[index].id;
                epis.splice(index, 1);
                // Remover também do estoque e entregas
                estoque = estoque.filter(e => e.epiId !== epiId);
                entregas = entregas.filter(e => e.epiId !== epiId);
            } else if (tipo === 'estoque') {
                estoque.splice(index, 1);
            } else if (tipo === 'entrega') {
                const entrega = entregas[index];
                entregas.splice(index, 1);
                
                // Atualizar estoque
                const itemEstoque = estoque.find(e => e.epiId === entrega.epiId);
                if (itemEstoque) {
                    itemEstoque.saidas -= entrega.quantidade;
                    itemEstoque.estoqueAtual = itemEstoque.entradas - itemEstoque.saidas;
                    itemEstoque.status = calcularStatusEstoque(itemEstoque.estoqueAtual, itemEstoque.quantidadeMinima);
                    itemEstoque.gastoTotal = itemEstoque.saidas * itemEstoque.valorUnitario;
                }
            }
            
            salvarDados();
            renderizarTabelas();
            atualizarDashboard();
            mostrarMensagem('Item excluído com sucesso!');
        }
        
        // Função para renderizar todas as tabelas
        function renderizarTabelas() {
            renderizarTabelaEPIs();
            renderizarTabelaEstoque();
            renderizarTabelaEntregas();
        }
        
        // Função para renderizar tabela de EPIs
        function renderizarTabelaEPIs() {
            const tbody = document.querySelector('#tabela-epis tbody');
            tbody.innerHTML = '';
            
            if (epis.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="7" style="text-align: center; padding: 20px; font-style: italic;">Nenhum EPI cadastrado. Clique em "Adicionar EPI" para começar.</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            epis.forEach((epi, index) => {
                const tr = document.createElement('tr');
                
                // Determinar classe do status
                let statusClass = '';
                if (epi.status === 'VALIDO') statusClass = 'status-valid';
                else if (epi.status === 'MENOS DE 1 MES') statusClass = 'status-warning';
                else if (epi.status === 'VENCEU') statusClass = 'status-expired';
                
                tr.innerHTML = `
                    <td>${epi.nome}</td>
                    <td>${epi.fabricante || '-'}</td>
                    <td>${epi.ca || '-'}</td>
                    <td>${epi.validadeCA ? new Date(epi.validadeCA).toLocaleDateString('pt-BR') : '-'}</td>
                    <td>${epi.validadeEPI ? new Date(epi.validadeEPI).toLocaleDateString('pt-BR') : '-'}</td>
                    <td><span class="status-badge ${statusClass}">${epi.status}</span></td>
                    <td>
                        <button class="btn btn-primary btn-sm" onclick="abrirModalEpi(${index})">Editar</button>
                        <button class="btn btn-danger btn-sm" onclick="excluirItem('epi', ${index})">Excluir</button>
                    </td>
                `;
                
                tbody.appendChild(tr);
            });
        }
        
        // Função para renderizar tabela de estoque
        function renderizarTabelaEstoque() {
            const tbody = document.querySelector('#tabela-estoque tbody');
            tbody.innerHTML = '';
            
            if (estoque.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="9" style="text-align: center; padding: 20px; font-style: italic;">Nenhum item no estoque. Clique em "Adicionar ao Estoque" para começar.</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            estoque.forEach((item, index) => {
                const tr = document.createElement('tr');
                
                // Determinar classe do status
                const statusClass = item.status === 'ESTOQUE OK' ? 'status-ok' : 'status-low-stock';
                
                tr.innerHTML = `
                    <td>${item.epiNome}</td>
                    <td>${item.saidas}</td>
                    <td>${item.entradas}</td>
                    <td>${item.estoqueAtual}</td>
                    <td>${item.quantidadeMinima}</td>
                    <td><span class="status-badge ${statusClass}">${item.status}</span></td>
                    <td>${item.valorUnitario ? 'R$ ' + item.valorUnitario.toFixed(2) : '-'}</td>
                    <td>${item.gastoTotal ? 'R$ ' + item.gastoTotal.toFixed(2) : '-'}</td>
                    <td>
                        <button class="btn btn-primary btn-sm" onclick="abrirModalEstoque(${index})">Editar</button>
                        <button class="btn btn-danger btn-sm" onclick="excluirItem('estoque', ${index})">Excluir</button>
                    </td>
                `;
                
                tbody.appendChild(tr);
            });
        }
        
        // Função para renderizar tabela de entregas
        function renderizarTabelaEntregas() {
            const tbody = document.querySelector('#tabela-entregas tbody');
            tbody.innerHTML = '';
            
            if (entregas.length === 0) {
                const tr = document.createElement('tr');
                tr.innerHTML = `<td colspan="9" style="text-align: center; padding: 20px; font-style: italic;">Nenhuma entrega registrada. Clique em "Nova Entrega" para começar.</td>`;
                tbody.appendChild(tr);
                return;
            }
            
            entregas.forEach((entrega, index) => {
                const tr = document.createElement('tr');
                
                tr.innerHTML = `
                    <td>${new Date(entrega.data).toLocaleDateString('pt-BR')}</td>
                    <td>${entrega.funcionario}</td>
                    <td>${entrega.cargo || '-'}</td>
                    <td>${entrega.setor || '-'}</td>
                    <td>${entrega.epiNome}</td>
                    <td>${entrega.quantidade}</td>
                    <td>${entrega.valorUnitario ? 'R$ ' + entrega.valorUnitario.toFixed(2) : '-'}</td>
                    <td>${entrega.valorTotal ? 'R$ ' + entrega.valorTotal.toFixed(2) : '-'}</td>
                    <td>
                        <button class="btn btn-primary btn-sm" onclick="abrirModalEntrega(${index})">Editar</button>
                        <button class="btn btn-danger btn-sm" onclick="excluirItem('entrega', ${index})">Excluir</button>
                    </td>
                `;
                
                tbody.appendChild(tr);
            });
        }
        
        // Funções de filtro
        function filtrarEPIs() {
            const termo = document.getElementById('search-epi').value.toLowerCase();
            const linhas = document.querySelectorAll('#tabela-epis tbody tr');
            
            linhas.forEach(linha => {
                const texto = linha.textContent.toLowerCase();
                linha.style.display = texto.includes(termo) ? '' : 'none';
            });
        }
        
        function filtrarEstoque() {
            const termo = document.getElementById('search-estoque').value.toLowerCase();
            const linhas = document.querySelectorAll('#tabela-estoque tbody tr');
            
            linhas.forEach(linha => {
                const texto = linha.textContent.toLowerCase();
                linha.style.display = texto.includes(termo) ? '' : 'none';
            });
        }
        
        function filtrarEntregas() {
            const termo = document.getElementById('search-entregas').value.toLowerCase();
            const linhas = document.querySelectorAll('#tabela-entregas tbody tr');
            
            linhas.forEach(linha => {
                const texto = linha.textContent.toLowerCase();
                linha.style.display = texto.includes(termo) ? '' : 'none';
            });
        }
        
        // Função para atualizar dashboard
        function atualizarDashboard() {
            // Total de EPIs
            document.getElementById('total-epis').textContent = epis.length;
            
            // EPIs vencidos
            const episVencidos = epis.filter(epi => epi.status === 'VENCEU').length;
            document.getElementById('epis-vencidos').textContent = episVencidos;
            
            // EPIs próximos do vencimento
            const episProximoVencimento = epis.filter(epi => epi.status === 'MENOS DE 1 MES').length;
            document.getElementById('epis-proximo-vencimento').textContent = episProximoVencimento;
            
            // Estoques baixos
            const estoquesBaixos = estoque.filter(item => item.status === 'ESTOQUE BAIXO').length;
            document.getElementById('estoques-baixos').textContent = estoquesBaixos;
        }
        
        // Função para atualizar gráficos
        function atualizarGraficos() {
            // Esta função seria implementada com uma biblioteca de gráficos como Chart.js
            // Por simplicidade, vamos apenas mostrar placeholders
            document.getElementById('chart-status').innerHTML = '<p style="text-align: center;">Gráfico de Status dos EPIs</p>';
            document.getElementById('chart-top-epis').innerHTML = '<p style="text-align: center;">Gráfico dos EPIs Mais Utilizados</p>';
            document.getElementById('chart-gastos').innerHTML = '<p style="text-align: center;">Gráfico de Gastos por Categoria</p>';
        }
        
        // Funções para gerar relatórios PDF
        function gerarRelatorioEPIs() {
            const doc = new jsPDF();
            
            // Cabeçalho
            doc.setFontSize(16);
            doc.setFont(undefined, 'bold');
            doc.text("Relatório de EPIs", 105, 15, { align: 'center' });
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Gerado em: ${new Date().toLocaleDateString('pt-BR')}`, 105, 22, { align: 'center' });
            
            // Tabela
            const tableColumn = ["EPI", "Fabricante", "C.A", "Validade C.A", "Validade EPI", "Status"];
            const tableRows = [];
            
            epis.forEach(epi => {
                const epiData = [
                    epi.nome,
                    epi.fabricante || '-',
                    epi.ca || '-',
                    epi.validadeCA ? new Date(epi.validadeCA).toLocaleDateString('pt-BR') : '-',
                    epi.validadeEPI ? new Date(epi.validadeEPI).toLocaleDateString('pt-BR') : '-',
                    epi.status
                ];
                tableRows.push(epiData);
            });
            
            doc.autoTable({
                head: [tableColumn],
                body: tableRows,
                startY: 30,
                theme: 'grid',
                styles: { fontSize: 8 },
                headStyles: { fillColor: [44, 62, 80] }
            });
            
            doc.save(`Relatorio_EPIs_${new Date().toISOString().split('T')[0]}.pdf`);
            mostrarMensagem('Relatório de EPIs gerado com sucesso!');
        }
        
        function gerarRelatorioEstoque() {
            const doc = new jsPDF();
            
            // Cabeçalho
            doc.setFontSize(16);
            doc.setFont(undefined, 'bold');
            doc.text("Relatório de Estoque", 105, 15, { align: 'center' });
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Gerado em: ${new Date().toLocaleDateString('pt-BR')}`, 105, 22, { align: 'center' });
            
            // Tabela
            const tableColumn = ["EPI", "Entradas", "Saídas", "Estoque Atual", "Qtd. Mínima", "Status"];
            const tableRows = [];
            
            estoque.forEach(item => {
                const itemData = [
                    item.epiNome,
                    item.entradas.toString(),
                    item.saidas.toString(),
                    item.estoqueAtual.toString(),
                    item.quantidadeMinima.toString(),
                    item.status
                ];
                tableRows.push(itemData);
            });
            
            doc.autoTable({
                head: [tableColumn],
                body: tableRows,
                startY: 30,
                theme: 'grid',
                styles: { fontSize: 8 },
                headStyles: { fillColor: [44, 62, 80] }
            });
            
            doc.save(`Relatorio_Estoque_${new Date().toISOString().split('T')[0]}.pdf`);
            mostrarMensagem('Relatório de Estoque gerado com sucesso!');
        }
        
        function gerarRelatorioEntregas() {
            const doc = new jsPDF();
            
            // Cabeçalho
            doc.setFontSize(16);
            doc.setFont(undefined, 'bold');
            doc.text("Relatório de Entregas", 105, 15, { align: 'center' });
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Gerado em: ${new Date().toLocaleDateString('pt-BR')}`, 105, 22, { align: 'center' });
            
            // Tabela
            const tableColumn = ["Data", "Funcionário", "Cargo", "Setor", "EPI", "Qtd.", "Valor Total"];
            const tableRows = [];
            
            entregas.forEach(entrega => {
                const entregaData = [
                    new Date(entrega.data).toLocaleDateString('pt-BR'),
                    entrega.funcionario,
                    entrega.cargo || '-',
                    entrega.setor || '-',
                    entrega.epiNome,
                    entrega.quantidade.toString(),
                    entrega.valorTotal ? 'R$ ' + entrega.valorTotal.toFixed(2) : '-'
                ];
                tableRows.push(entregaData);
            });
            
            doc.autoTable({
                head: [tableColumn],
                body: tableRows,
                startY: 30,
                theme: 'grid',
                styles: { fontSize: 8 },
                headStyles: { fillColor: [44, 62, 80] }
            });
            
            doc.save(`Relatorio_Entregas_${new Date().toISOString().split('T')[0]}.pdf`);
            mostrarMensagem('Relatório de Entregas gerado com sucesso!');
        }
        
        // Função para fazer backup completo
        function fazerBackup() {
            const dados = {
                epis: epis,
                estoque: estoque,
                entregas: entregas,
                dataBackup: new Date().toISOString()
            };
            
            const blob = new Blob([JSON.stringify(dados, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `backup_epi_${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            mostrarMensagem('Backup realizado com sucesso!');
        }
        
        // Função para salvar dados no localStorage
        function salvarDados() {
            const dados = {
                epis: epis,
                estoque: estoque,
                entregas: entregas,
                dataSalvamento: new Date().toISOString()
            };
            
            localStorage.setItem('gestaoEPI', JSON.stringify(dados));
        }
        
        // Função para carregar dados do localStorage
        function carregarDados() {
            const dadosSalvos = localStorage.getItem('gestaoEPI');
            
            if (dadosSalvos) {
                try {
                    const dados = JSON.parse(dadosSalvos);
                    
                    epis = dados.epis || [];
                    estoque = dados.estoque || [];
                    entregas = dados.entregas || [];
                    
                    console.log('Dados carregados com sucesso:', {
                        epis: epis.length,
                        estoque: estoque.length,
                        entregas: entregas.length
                    });
                } catch (e) {
                    console.error('Erro ao carregar dados:', e);
                    inicializarDadosPadrao();
                }
            } else {
                inicializarDadosPadrao();
            }
        }
        
        // Função para inicializar dados padrão
        function inicializarDadosPadrao() {
            epis = [
                { id: '1', nome: 'Luvas multitato (M 8)', fabricante: '', ca: '', validadeCA: '', validadeEPI: '', status: 'NÃO INFORMADO' },
                { id: '2', nome: 'Luvas multitato (G 9)', fabricante: '', ca: '', validadeCA: '', validadeEPI: '', status: 'NÃO INFORMADO' },
                { id: '3', nome: 'Luvas PVC verde (G 9)', fabricante: '', ca: '', validadeCA: '', validadeEPI: '', status: 'NÃO INFORMADO' },
                { id: '4', nome: 'Luvas PVC azul (XG 10)', fabricante: '', ca: '', validadeCA: '', validadeEPI: '', status: 'NÃO INFORMADO' },
                { id: '5', nome: 'Macacão Tyvec (M)', fabricante: '', ca: '', validadeCA: '', validadeEPI: '', status: 'NÃO INFORMADO' }
            ];
            
            console.log('Dados padrão inicializados');
        }
    </script>
</body>
</html>
