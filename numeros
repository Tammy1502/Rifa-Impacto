<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rifa do Impacto Infantil - Online</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-main: #e0f7fa;
            --bg-container: #ffffff;
            --bg-available: #f8f9fa;
            --bg-available-hover: #e2e6ea;
            --bg-reserved: #d32f2f;
            --text-dark: #004d40;
            --text-light: #ffffff;
            --border-color: #b2dfdb;
            --shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            --loading-spinner: #00796b;
        }

        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            background-color: var(--bg-main);
            color: var(--text-dark);
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
        }

        .raffle-container {
            width: 100%;
            max-width: 1200px;
            background-color: var(--bg-container);
            padding: 25px 30px;
            border-radius: 16px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
            position: relative;
        }

        .title {
            text-align: center;
            font-size: clamp(2rem, 5vw, 2.8rem);
            color: var(--text-dark);
            margin-bottom: 25px;
            font-weight: 700;
        }

        .raffle-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
            gap: 12px;
            margin-bottom: 30px;
        }

        .number-cell {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 60px;
            font-size: 1.2em;
            font-weight: 600;
            border-radius: 8px;
            border: 1px solid var(--border-color);
            transition: all 0.2s ease-in-out;
            user-select: none;
        }

        .available { background-color: var(--bg-available); color: var(--text-dark); cursor: pointer; }
        .available:hover { background-color: var(--bg-available-hover); transform: translateY(-3px) scale(1.05); box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1); }
        .reserved { 
            background-color: var(--bg-reserved); 
            color: var(--text-light); 
            cursor: not-allowed; 
            text-decoration: none; /* Alterado de line-through para none para um visual mais limpo */
            opacity: 0.9; 
        }

        .stats-panel { padding: 20px; background-color: #f1f8f7; border-radius: 10px; border: 1px solid var(--border-color); }
        .stats-panel h2 { text-align: center; margin-top: 0; margin-bottom: 15px; color: var(--text-dark); }
        #stats-content { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px 20px; font-size: 1.1em; font-weight: 600; }
        .stat-item { background-color: white; padding: 5px 15px; border-radius: 20px; border: 1px solid var(--border-color); }

        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0, 0, 0, 0.6); display: none; justify-content: center; align-items: center; z-index: 1000; backdrop-filter: blur(5px); }
        .modal-content { background-color: white; padding: 30px; border-radius: 12px; box-shadow: 0 5px 20px rgba(0,0,0,0.25); text-align: center; width: 90%; max-width: 400px; animation: fadeIn 0.3s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.9); } to { opacity: 1; transform: scale(1); } }
        .modal-content h2 { margin-top: 0; }
        #name-selector { width: 100%; padding: 12px; margin: 20px 0; font-size: 1.1em; border-radius: 8px; border: 1px solid #ccc; background-color: #f8f8f8; }
        .modal-actions button { padding: 12px 24px; font-size: 1em; font-weight: 600; border-radius: 8px; border: none; cursor: pointer; transition: all 0.2s; margin: 0 8px; }
        #confirm-btn { background-color: #2e7d32; color: white; } #confirm-btn:hover { background-color: #1b5e20; transform: translateY(-2px); }
        #cancel-btn { background-color: #6c757d; color: white; } #cancel-btn:hover { background-color: #5a6268; }

        /* --- Loading Spinner --- */
        #loading-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 999;
            border-radius: 16px;
        }
        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #f3f3f3;
            border-top: 5px solid var(--loading-spinner);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

    </style>
</head>
<body>

    <div class="raffle-container">
        <div id="loading-overlay"><div class="spinner"></div></div>
        <h1 class="title">Rifa do Impacto Infantil</h1>
        <div class="raffle-grid" id="raffle-grid"></div>
        <div class="stats-panel">
            <h2>Contagem de Reservas</h2>
            <div id="stats-content"></div>
        </div>
    </div>

    <div class="modal-overlay" id="modal-overlay">
        <div class="modal-content">
            <h2 id="modal-title">Reservar Número</h2>
            <p>Selecione quem está fazendo a reserva:</p>
            <select id="name-selector"></select>
            <div class="modal-actions">
                <button id="confirm-btn">Confirmar Reserva</button>
                <button id="cancel-btn">Cancelar</button>
            </div>
        </div>
    </div>
    
    <script type="module">
        // Importa as funções necessárias do SDK do Firebase
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
        import { getFirestore, collection, doc, onSnapshot, setDoc } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-firestore.js";

        // *******************************************************************
        // PASSO 2: COLE A SUA CONFIGURAÇÃO DO FIREBASE AQUI
        // (Obtenha isto no seu projeto Firebase em "Configurações do Projeto")
        const firebaseConfig = {
            // SUBSTITUA ESTAS CREDENCIAIS PELA SUA CONFIGURAÇÃO PESSOAL
            apiKey: "AIzaSyDIMqmx1Xlcl4_qK9C6k0liMc0ybEQ6ye4",
            authDomain: "rifa-do-impacto.firebaseapp.com",
            projectId: "rifa-do-impacto",
            storageBucket: "rifa-do-impacto.firebasestorage.app",
            messagingSenderId: "499086169777",
            appId: "1:499086169777:web:e7ac2847a1046f411ab490"
        };
        // *******************************************************************

        // --- VERIFICAÇÃO DE CONFIGURAÇÃO DO FIREBASE ---
        if (firebaseConfig.apiKey.startsWith("AIzaSy") && firebaseConfig.projectId.includes("rifa-do-impacto")) {
            // Este é o check para o seu caso específico, onde a config inicial está presente.
            // Para um uso genérico, a verificação original é boa.
            console.error("ERRO: Configuração de demonstração do Firebase ainda está no código. Substitua-a pela sua.");
            document.body.innerHTML = `<div style="padding: 30px; margin: 20px; border-radius: 10px; background-color: #fff3cd; border: 1px solid #ffeeba; color: #856404; font-family: 'Poppins', sans-serif; text-align: center;"><h1><strong style="color: #d32f2f;">[ERRO]</strong> Configuração do Firebase Incompleta</h1><p style="font-size: 1.1em;">As credenciais do Firebase não foram adicionadas ao código-fonte ou estão incorretas.</p><p>Para que a rifa funcione, precisa de seguir as instruções e colar o seu objeto <code>firebaseConfig</code> pessoal no local indicado no ficheiro HTML.</p><p>O site não funcionará corretamente até que esta configuração seja feita.</p></div>`;
            throw new Error("Configuração do Firebase não foi preenchida. O script foi interrompido.");
        }

        // --- INICIALIZAÇÃO E CONFIGURAÇÃO DA APLICAÇÃO ---
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        const totalNumbers = 500;
        const names = ['Lorena', 'Cauana', 'Poliana', 'Arthur', 'Tamara'];

        const grid = document.getElementById('raffle-grid');
        const statsContent = document.getElementById('stats-content');
        const modalOverlay = document.getElementById('modal-overlay');
        const modalTitle = document.getElementById('modal-title');
        const nameSelector = document.getElementById('name-selector');
        const confirmBtn = document.getElementById('confirm-btn');
        const cancelBtn = document.getElementById('cancel-btn');
        const loadingOverlay = document.getElementById('loading-overlay');

        let selectedNumber = null;
        let currentReservations = {};

        // --- FUNÇÕES ---

        /**
         * Gera a grade inicial com todos os números.
         */
        function createGrid() {
            for (let i = 1; i <= totalNumbers; i++) {
                const numberCell = document.createElement('div');
                numberCell.classList.add('number-cell');
                numberCell.textContent = i;
                numberCell.dataset.number = i;
                grid.appendChild(numberCell);
            }
        }

        /**
         * Ouve as alterações na base de dados em tempo real.
         */
        function listenToReservations() {
            const reservationsCol = collection(db, 'reservations');
            onSnapshot(reservationsCol, (snapshot) => {
                currentReservations = {};
                snapshot.forEach(doc => {
                    currentReservations[doc.id] = doc.data().reservedBy;
                });
                
                updateUI(currentReservations);
                loadingOverlay.style.display = 'none'; // Esconde o spinner após carregar os dados
            }, (error) => {
                // Tratamento de erro para a conexão
                console.error("Erro ao conectar ao Firestore: ", error);
                loadingOverlay.innerHTML = `<p style="text-align:center; color: #d32f2f; padding: 20px;">Falha ao conectar à base de dados.<br>Verifique a sua conexão com a internet e a configuração do Firebase.</p>`;
            });
        }
        
        /**
         * Atualiza toda a interface (grelha e estatísticas) com base nos dados.
         * @param {object} reservations - O objeto com os números reservados.
         */
        function updateUI(reservations) {
            // Atualiza a grelha de números
            for (let i = 1; i <= totalNumbers; i++) {
                const cell = grid.querySelector(`[data-number="${i}"]`);
                if (!cell) continue;

                // Limpa classes antigas para evitar duplicação
                cell.classList.remove('available', 'reserved');
                cell.removeEventListener('click', handleNumberClick);

                if (reservations[String(i)]) { // Garante que a chave é uma string para a busca
                    // Número reservado
                    cell.classList.add('reserved');
                    cell.title = `Reservado por: ${reservations[String(i)]}`;
                } else {
                    // Número disponível
                    cell.classList.add('available');
                    cell.title = '';
                    cell.addEventListener('click', handleNumberClick);
                }
            }
            
            // Atualiza as estatísticas
            updateStats(reservations);
        }

        /**
         * Calcula e exibe a contagem de reservas por pessoa.
         */
        function updateStats(reservations) {
            const counts = names.reduce((acc, name) => ({ ...acc, [name]: 0 }), {});
            for (const number in reservations) {
                const name = reservations[number];
                if (counts[name] !== undefined) {
                    counts[name]++;
                }
            }

            statsContent.innerHTML = '';
            names.forEach(name => {
                const statElement = document.createElement('div');
                statElement.classList.add('stat-item');
                statElement.textContent = `${name}: ${counts[name]}`;
                statsContent.appendChild(statElement);
            });
        }

        function handleNumberClick(event) {
            selectedNumber = event.target.dataset.number;
            // Verifica novamente se o número não foi reservado enquanto o utilizador hesitava
            if(currentReservations[selectedNumber]){
                alert("Oops! Alguém acabou de reservar este número. Tente outro.");
                return;
            }
            modalTitle.textContent = `Reservar o Número ${selectedNumber}`;
            modalOverlay.style.display = 'flex';
        }

        function closeModal() {
            modalOverlay.style.display = 'none';
            selectedNumber = null;
        }

        /**
         * Confirma a reserva e guarda na base de dados.
         */
        async function confirmReservation() {
            if (!selectedNumber) return;

            const selectedName = nameSelector.value;
            confirmBtn.disabled = true;
            confirmBtn.textContent = 'A guardar...';

            try {
                // Cria um documento na coleção 'reservations' com o ID igual ao número
                const reservationRef = doc(db, 'reservations', String(selectedNumber));
                await setDoc(reservationRef, { reservedBy: selectedName });
                // A atualização da UI acontece automaticamente pelo 'onSnapshot'
            } catch (error) {
                console.error("Erro ao guardar a reserva: ", error);
                alert("Ocorreu um erro ao tentar reservar. Por favor, tente novamente.");
            } finally {
                confirmBtn.disabled = false;
                confirmBtn.textContent = 'Confirmar Reserva';
                closeModal();
            }
        }

        // --- INICIALIZAÇÃO DA APLICAÇÃO ---
        
        // Popula o seletor de nomes
        names.forEach(name => {
            const option = document.createElement('option');
            option.value = name;
            option.textContent = name;
            nameSelector.appendChild(option);
        });

        // Adiciona os event listeners dos botões do modal
        confirmBtn.addEventListener('click', confirmReservation);
        cancelBtn.addEventListener('click', closeModal);
        modalOverlay.addEventListener('click', (event) => {
            if (event.target === modalOverlay) closeModal();
        });

        // Cria a grelha e começa a ouvir as atualizações da base de dados
        createGrid();
        listenToReservations();

    </script>
</body>
</html>
