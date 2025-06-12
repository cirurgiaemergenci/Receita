<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Prescrição Médica</title>
    <style>
        @media print {
            body { margin: 0; }
            .no-print { display: none; }
            .prescription-container { 
                width: 100%;
                height: 100vh;
                page-break-after: avoid;
            }
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Times New Roman', serif;
            background-color: #f5f5f5;
            padding: 20px;
        }

        .form-container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #333;
        }

        input, select, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }

        .form-row {
            display: flex;
            gap: 15px;
        }

        .form-row .form-group {
            flex: 1;
        }

        button {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            margin-right: 10px;
        }

        button:hover {
            background-color: #0056b3;
        }

        .add-medication {
            background-color: #28a745;
        }

        .add-medication:hover {
            background-color: #1e7e34;
        }

        .prescription-container {
            width: 297mm;
            height: 210mm;
            background: white;
            margin: 20px auto;
            display: flex;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }

        .prescription-copy {
            width: 50%;
            height: 100%;
            border: 2px solid #000;
            padding: 15px;
            position: relative;
            font-size: 12px;
        }

        .prescription-copy:first-child {
            border-right: 1px solid #000;
        }

        .header {
            text-align: center;
            border-bottom: 2px solid #000;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }

        .logo {
            font-size: 18px;
            font-weight: bold;
            color: #0066cc;
        }

        .via-info {
            font-size: 14px;
            font-weight: bold;
            margin: 5px 0;
        }

        .doctor-info {
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ccc;
        }

        .doctor-field {
            margin-bottom: 8px;
        }

        .doctor-field strong {
            display: inline-block;
            width: 120px;
        }

        .patient-info {
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ccc;
        }

        .patient-field {
            margin-bottom: 5px;
        }

        .patient-field strong {
            display: inline-block;
            width: 80px;
        }

        .prescription-box {
            border: 1px solid #000;
            min-height: 300px;
            padding: 10px;
            position: relative;
            margin-bottom: 15px;
        }

        .medication {
            margin-bottom: 15px;
        }

        .usage {
            font-weight: bold;
            margin-bottom: 3px;
        }

        .active-ingredient {
            margin-left: 20px;
            margin-bottom: 3px;
        }

        .dosage {
            margin-left: 40px;
            margin-bottom: 3px;
        }

        .duration {
            margin-left: 60px;
        }

        .prescription-footer {
            position: absolute;
            bottom: 10px;
            width: calc(100% - 20px);
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
        }

        .date {
            font-size: 11px;
        }

        .signature-area {
            text-align: center;
        }

        .signature-line {
            border-top: 1px solid #000;
            width: 200px;
            margin-top: 20px;
            margin-bottom: 5px;
        }

        .doctor-name {
            font-size: 11px;
            font-weight: bold;
        }

        .medication-form {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .remove-btn {
            background-color: #dc3545;
            font-size: 12px;
            padding: 5px 10px;
        }

        .remove-btn:hover {
            background-color: #c82333;
        }

        .medication-item {
            border: 1px solid #ddd;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 4px;
        }

        .hidden {
            display: none;
        }

        .database-view {
            margin-top: 20px;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        th {
            background-color: #f8f9fa;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="form-container no-print">
        <h2>Sistema de Prescrição Médica</h2>
        
        <div class="form-row">
            <div class="form-group">
                <label for="crm">CRM:</label>
                <input type="text" id="crm" placeholder="Digite o CRM">
            </div>
            <div class="form-group">
                <label for="doctorName">Nome do Médico:</label>
                <input type="text" id="doctorName" placeholder="Nome será preenchido automaticamente">
            </div>
            <div class="form-group">
                <label for="specialty">Especialidade:</label>
                <input type="text" id="specialty" placeholder="Especialidade será preenchida automaticamente">
            </div>
        </div>

        <div class="form-row">
            <div class="form-group">
                <label for="patientName">Nome do Paciente:</label>
                <input type="text" id="patientName" placeholder="Digite o nome do paciente">
            </div>
            <div class="form-group">
                <label for="patientAge">Idade:</label>
                <input type="text" id="patientAge" placeholder="Digite a idade">
            </div>
        </div>

        <div class="form-row">
            <div class="form-group">
                <label for="patientAddress">Endereço:</label>
                <input type="text" id="patientAddress" placeholder="Digite o endereço">
            </div>
            <div class="form-group">
                <label for="patientPhone">Telefone:</label>
                <input type="text" id="patientPhone" placeholder="Digite o telefone">
            </div>
        </div>

        <h3>Medicamentos</h3>
        <div id="medicationsContainer">
            <div class="medication-form">
                <div class="form-row">
                    <div class="form-group">
                        <label>Uso:</label>
                        <select class="usage-select">
                            <option value="Uso Interno">Uso Interno</option>
                            <option value="Uso Externo">Uso Externo</option>
                            <option value="Uso Tópico">Uso Tópico</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Princípio Ativo:</label>
                        <input type="text" class="active-ingredient-input" placeholder="Digite o princípio ativo">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label>Dose por Unidade:</label>
                        <input type="text" class="dose-input" placeholder="ex: 500mg">
                    </div>
                    <div class="form-group">
                        <label>Posologia:</label>
                        <input type="text" class="posology-input" placeholder="ex: 1 comprimido de 8/8h">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label>Número de Dias:</label>
                        <input type="number" class="days-input" placeholder="Digite o número de dias" min="1">
                    </div>
                    <div class="form-group">
                        <label>Total de Comprimidos/Frascos:</label>
                        <input type="text" class="total-units" readonly>
                    </div>
                </div>
                
                <button type="button" class="remove-btn" onclick="removeMedication(this)">Remover Medicamento</button>
            </div>
        </div>

        <button type="button" class="add-medication" onclick="addMedication()">Adicionar Medicamento</button>
        <button type="button" onclick="generatePrescription()">Gerar Prescrição</button>
        <button type="button" onclick="printPrescription()">Imprimir</button>
        <button type="button" onclick="toggleDatabase()">Ver Banco de Dados</button>
    </div>

    <div class="prescription-container hidden" id="prescriptionContainer">
        <div class="prescription-copy">
            <div class="header">
                <div class="logo">🏥 HOSPITAL NOSSA SENHORA DA CONCEIÇÃO</div>
                <div class="via-info">RECEITA MÉDICA - 1ª VIA</div>
            </div>
            
            <div class="doctor-info">
                <div class="doctor-field"><strong>Médico:</strong> <span id="displayDoctorName1"></span></div>
                <div class="doctor-field"><strong>CRM:</strong> <span id="displayCRM1"></span></div>
                <div class="doctor-field"><strong>Especialidade:</strong> <span id="displaySpecialty1"></span></div>
            </div>
            
            <div class="patient-info">
                <div class="patient-field"><strong>Paciente:</strong> <span id="displayPatientName1"></span></div>
                <div class="patient-field"><strong>Idade:</strong> <span id="displayPatientAge1"></span></div>
                <div class="patient-field"><strong>Endereço:</strong> <span id="displayPatientAddress1"></span></div>
                <div class="patient-field"><strong>Telefone:</strong> <span id="displayPatientPhone1"></span></div>
            </div>
            
            <div class="prescription-box">
                <div id="medicationsList1"></div>
                
                <div class="prescription-footer">
                    <div class="date" id="prescriptionDate1"></div>
                    <div class="signature-area">
                        <div class="signature-line"></div>
                        <div class="doctor-name" id="signatureName1"></div>
                        <div class="doctor-name" id="signatureCRM1"></div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="prescription-copy">
            <div class="header">
                <div class="logo">🏥 HOSPITAL NOSSA SENHORA DA CONCEIÇÃO</div>
                <div class="via-info">RECEITA MÉDICA - 2ª VIA</div>
            </div>
            
            <div class="doctor-info">
                <div class="doctor-field"><strong>Médico:</strong> <span id="displayDoctorName2"></span></div>
                <div class="doctor-field"><strong>CRM:</strong> <span id="displayCRM2"></span></div>
                <div class="doctor-field"><strong>Especialidade:</strong> <span id="displaySpecialty2"></span></div>
            </div>
            
            <div class="patient-info">
                <div class="patient-field"><strong>Paciente:</strong> <span id="displayPatientName2"></span></div>
                <div class="patient-field"><strong>Idade:</strong> <span id="displayPatientAge2"></span></div>
                <div class="patient-field"><strong>Endereço:</strong> <span id="displayPatientAddress2"></span></div>
                <div class="patient-field"><strong>Telefone:</strong> <span id="displayPatientPhone2"></span></div>
            </div>
            
            <div class="prescription-box">
                <div id="medicationsList2"></div>
                
                <div class="prescription-footer">
                    <div class="date" id="prescriptionDate2"></div>
                    <div class="signature-area">
                        <div class="signature-line"></div>
                        <div class="doctor-name" id="signatureName2"></div>
                        <div class="doctor-name" id="signatureCRM2"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="database-view hidden no-print" id="databaseView">
        <h3>Banco de Dados do Sistema</h3>
        
        <h4>Médicos Cadastrados</h4>
        <table id="doctorsTable">
            <thead>
                <tr>
                    <th>CRM</th>
                    <th>Nome</th>
                    <th>Especialidade</th>
                    <th>Data Cadastro</th>
                </tr>
            </thead>
            <tbody id="doctorsTableBody"></tbody>
        </table>

        <h4>Prescrições Realizadas</h4>
        <table id="prescriptionsTable">
            <thead>
                <tr>
                    <th>Data</th>
                    <th>Médico</th>
                    <th>Paciente</th>
                    <th>Medicamento</th>
                    <th>Dias</th>
                </tr>
            </thead>
            <tbody id="prescriptionsTableBody"></tbody>
        </table>
    </div>

    <script>
        // Banco de dados em memória
        let doctors = {
            '12345': { name: 'Dr. João Silva', specialty: 'Cardiologia' },
            '67890': { name: 'Dra. Maria Santos', specialty: 'Pediatria' },
            '11111': { name: 'Dr. Pedro Oliveira', specialty: 'Clínica Geral' }
        };

        let prescriptions = [];

        // Event listeners
        document.getElementById('crm').addEventListener('input', function(e) {
            const crm = e.target.value;
            if (doctors[crm]) {
                document.getElementById('doctorName').value = doctors[crm].name;
                document.getElementById('specialty').value = doctors[crm].specialty;
            } else {
                document.getElementById('doctorName').value = '';
                document.getElementById('specialty').value = '';
            }
        });

        // Salvar médico quando CRM, nome e especialidade estiverem preenchidos
        document.getElementById('specialty').addEventListener('blur', function() {
            const crm = document.getElementById('crm').value;
            const name = document.getElementById('doctorName').value;
            const specialty = document.getElementById('specialty').value;
            
            if (crm && name && specialty) {
                doctors[crm] = { name: name, specialty: specialty };
            }
        });

        // Calcular total de comprimidos automaticamente
        function setupMedicationCalculation(container) {
            const posologyInput = container.querySelector('.posology-input');
            const daysInput = container.querySelector('.days-input');
            const totalUnits = container.querySelector('.total-units');

            function calculateTotal() {
                const posology = posologyInput.value.toLowerCase();
                const days = parseInt(daysInput.value) || 0;
                
                if (posology && days > 0) {
                    // Extrair número de comprimidos por dia da posologia
                    let dailyDose = 1;
                    
                    // Padrões comuns de posologia
                    if (posology.includes('de 8/8') || posology.includes('8 em 8')) {
                        dailyDose = 3;
                    } else if (posology.includes('de 12/12') || posology.includes('12 em 12')) {
                        dailyDose = 2;
                    } else if (posology.includes('de 6/6') || posology.includes('6 em 6')) {
                        dailyDose = 4;
                    } else if (posology.includes('2x') || posology.includes('duas vezes')) {
                        dailyDose = 2;
                    } else if (posology.includes('3x') || posology.includes('três vezes')) {
                        dailyDose = 3;
                    } else if (posology.includes('4x') || posology.includes('quatro vezes')) {
                        dailyDose = 4;
                    }

                    const total = dailyDose * days;
                    totalUnits.value = total + ' comprimidos';
                }
            }

            posologyInput.addEventListener('input', calculateTotal);
            daysInput.addEventListener('input', calculateTotal);
        }

        // Configurar cálculo para o primeiro medicamento
        setupMedicationCalculation(document.querySelector('.medication-form'));

        function addMedication() {
            const container = document.getElementById('medicationsContainer');
            const newMedication = document.querySelector('.medication-form').cloneNode(true);
            
            // Limpar valores dos inputs
            newMedication.querySelectorAll('input, select').forEach(input => {
                if (input.type !== 'button') {
                    input.value = '';
                }
            });

            container.appendChild(newMedication);
            setupMedicationCalculation(newMedication);
        }

        function removeMedication(button) {
            const medicationForms = document.querySelectorAll('.medication-form');
            if (medicationForms.length > 1) {
                button.closest('.medication-form').remove();
            } else {
                alert('Deve haver pelo menos um medicamento na prescrição.');
            }
        }

        function generatePrescription() {
            // Validar campos obrigatórios
            const crm = document.getElementById('crm').value;
            const doctorName = document.getElementById('doctorName').value;
            const patientName = document.getElementById('patientName').value;

            if (!crm || !doctorName || !patientName) {
                alert('Por favor, preencha todos os campos obrigatórios (CRM, Médico e Paciente).');
                return;
            }

            // Preencher dados do médico e paciente nas duas vias
            fillPrescriptionData();

            // Gerar lista de medicamentos
            generateMedicationsList();

            // Definir data atual
            const currentDate = new Date().toLocaleDateString('pt-BR');
            document.getElementById('prescriptionDate1').textContent = currentDate;
            document.getElementById('prescriptionDate2').textContent = currentDate;

            // Preencher área de assinatura
            document.getElementById('signatureName1').textContent = doctorName;
            document.getElementById('signatureName2').textContent = doctorName;
            document.getElementById('signatureCRM1').textContent = 'CRM: ' + crm;
            document.getElementById('signatureCRM2').textContent = 'CRM: ' + crm;

            // Salvar prescrições no banco de dados
            savePrescriptions();

            // Mostrar prescrição
            document.getElementById('prescriptionContainer').classList.remove('hidden');
        }

        function fillPrescriptionData() {
            const doctorName = document.getElementById('doctorName').value;
            const crm = document.getElementById('crm').value;
            const specialty = document.getElementById('specialty').value;
            const patientName = document.getElementById('patientName').value;
            const patientAge = document.getElementById('patientAge').value;
            const patientAddress = document.getElementById('patientAddress').value;
            const patientPhone = document.getElementById('patientPhone').value;

            // Preencher primeira via
            document.getElementById('displayDoctorName1').textContent = doctorName;
            document.getElementById('displayCRM1').textContent = crm;
            document.getElementById('displaySpecialty1').textContent = specialty;
            document.getElementById('displayPatientName1').textContent = patientName;
            document.getElementById('displayPatientAge1').textContent = patientAge;
            document.getElementById('displayPatientAddress1').textContent = patientAddress;
            document.getElementById('displayPatientPhone1').textContent = patientPhone;

            // Preencher segunda via
            document.getElementById('displayDoctorName2').textContent = doctorName;
            document.getElementById('displayCRM2').textContent = crm;
            document.getElementById('displaySpecialty2').textContent = specialty;
            document.getElementById('displayPatientName2').textContent = patientName;
            document.getElementById('displayPatientAge2').textContent = patientAge;
            document.getElementById('displayPatientAddress2').textContent = patientAddress;
            document.getElementById('displayPatientPhone2').textContent = patientPhone;
        }

        function generateMedicationsList() {
            const medicationForms = document.querySelectorAll('.medication-form');
            let medicationsHTML = '';

            medicationForms.forEach((form, index) => {
                const usage = form.querySelector('.usage-select').value;
                const activeIngredient = form.querySelector('.active-ingredient-input').value;
                const dose = form.querySelector('.dose-input').value;
                const posology = form.querySelector('.posology-input').value;
                const days = form.querySelector('.days-input').value;
                const totalUnits = form.querySelector('.total-units').value;

                if (activeIngredient) {
                    medicationsHTML += `
                        <div class="medication">
                            <div class="usage">${usage}</div>
                            <div class="active-ingredient">${activeIngredient} ${dose} ----------------------- ${totalUnits}</div>
                            <div class="dosage">${posology}</div>
                            <div class="duration">${days} dias</div>
                        </div>
                    `;
                }
            });

            document.getElementById('medicationsList1').innerHTML = medicationsHTML;
            document.getElementById('medicationsList2').innerHTML = medicationsHTML;
        }

        function savePrescriptions() {
            const doctorName = document.getElementById('doctorName').value;
            const patientName = document.getElementById('patientName').value;
            const currentDate = new Date().toLocaleDateString('pt-BR');

            const medicationForms = document.querySelectorAll('.medication-form');
            
            medicationForms.forEach(form => {
                const activeIngredient = form.querySelector('.active-ingredient-input').value;
                const days = form.querySelector('.days-input').value;

                if (activeIngredient) {
                    prescriptions.push({
                        date: currentDate,
                        doctor: doctorName,
                        patient: patientName,
                        medication: activeIngredient,
                        days: days
                    });
                }
            });
        }

        function printPrescription() {
            if (document.getElementById('prescriptionContainer').classList.contains('hidden')) {
                alert('Gere a prescrição antes de imprimir.');
                return;
            }
            window.print();
        }

        function toggleDatabase() {
            const databaseView = document.getElementById('databaseView');
            if (databaseView.classList.contains('hidden')) {
                databaseView.classList.remove('hidden');
                updateDatabaseTables();
            } else {
                databaseView.classList.add('hidden');
            }
        }

        function updateDatabaseTables() {
            // Atualizar tabela de médicos
            const doctorsTableBody = document.getElementById('doctorsTableBody');
            doctorsTableBody.innerHTML = '';
            
            for (const [crm, doctor] of Object.entries(doctors)) {
                const row = doctorsTableBody.insertRow();
                row.insertCell(0).textContent = crm;
                row.insertCell(1).textContent = doctor.name;
                row.insertCell(2).textContent = doctor.specialty;
                row.insertCell(3).textContent = new Date().toLocaleDateString('pt-BR');
            }

            // Atualizar tabela de prescrições
            const prescriptionsTableBody = document.getElementById('prescriptionsTableBody');
            prescriptionsTableBody.innerHTML = '';
            
            prescriptions.forEach(prescription => {
                const row = prescriptionsTableBody.insertRow();
                row.insertCell(0).textContent = prescription.date;
                row.insertCell(1).textContent = prescription.doctor;
                row.insertCell(2).textContent = prescription.patient;
                row.insertCell(3).textContent = prescription.medication;
                row.insertCell(4).textContent = prescription.days;
            });
        }

        // Carregar dados de teste iniciais
        window.addEventListener('load', function() {
            // Preencher alguns dados de teste
            document.getElementById('crm').value = '12345';
            document.getElementById('crm').dispatchEvent(new Event('input'));
            document.getElementById('patientName').value = 'João da Silva';
            document.getElementById('patientAge').value = '45 anos';
            document.getElementById('patientAddress').value = 'Rua das Flores, 123';
            document.getElementById('patientPhone').value = '(51) 99999-9999';
            
            // Preencher primeiro medicamento de teste
            const firstForm = document.querySelector('.medication-form');
            firstForm.querySelector('.active-ingredient-input').value = 'Paracetamol';
            firstForm.querySelector('.dose-input').value = '500mg';
            firstForm.querySelector('.posology-input').value = '1 comprimido de 8/8h';
            firstForm.querySelector('.days-input').value = '7';
            firstForm.querySelector('.days-input').dispatchEvent(new Event('input'));
        });
    </script>
</body>
</html>
