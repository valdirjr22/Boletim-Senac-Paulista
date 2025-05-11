<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciador de Notas de Boletim</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #fff;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        h1, h2, h3 {
            color: #1a73e8; /* Azul */
        }
        h2, h3 {
            border-bottom: 2px solid #ff6600; /* Laranja */
            padding-bottom: 5px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #1a73e8; /* Azul */
            color: white;
        }
        .button {
            background-color: #ff6600; /* Laranja */
            color: white;
            padding: 10px 15px;
            border: none;
            cursor: pointer;
            margin: 5px;
            border-radius: 5px;
            display: block; 
            width: calc(100% - 10px); 
        }
        .button:hover {
            background-color: #ff4500; /* Laranja escuro */
        }
        .hidden {
            display: none !important;
        }
        .error {
            color: red;
            font-size: 14px;
        }
        #loginContainer {
            text-align: center;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background-color: #f9f9f9;
        }
        input[type="text"], input[type="password"], select {
            padding: 8px;
            margin: 5px 0;
            width: 200px;
            border-radius: 5px;
            border: 1px solid #ddd;
            box-sizing: border-box;
        }

        #appContainer {
            display: flex;
            width: 100%;
            height: 100vh;
            overflow: hidden;
        }

        #sidebar {
            width: 230px;
            background-color: #f0f0f0;
            padding: 15px;
            display: flex;
            flex-direction: column;
            border-right: 1px solid #ccc;
            height: 100%;
            box-sizing: border-box;
        }
        #sidebar h2, #sidebar h3 {
            margin-top: 10px;
            margin-bottom: 10px;
            font-size: 1.2em;
        }
        #sidebar .button {
            margin-bottom: 10px;
        }
        #sidebar .button.logout-button {
            margin-top: auto;
        }

        #mainContentArea {
            flex-grow: 1;
            padding: 20px;
            overflow-y: auto;
            height: 100%;
            box-sizing: border-box;
        }
        #mainContentArea h1 {
            margin-top: 0;
        }

        /* Modal styles */
        .modal {
            position: fixed;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            width: 500px; /* Ajustado para melhor visualização */
            max-width: 90%; /* Responsividade */
            max-height: 80vh;
            overflow-y: auto;
            position: relative;
        }
        .modal-content h2 {
            margin-top: 0;
        }
        .modal-content label{
            display: block;
            margin-top: 10px;
            font-weight: bold;
        }
        .modal-content input[type="text"]{
            width: 100%; /* Ocupa toda a largura do modal content */
        }


        .close-button {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 24px;
            font-weight: bold;
            cursor: pointer;
        }

        #professorDisciplinesCheckboxes div,
        #professorClassesCheckboxes div {
            margin-bottom: 5px;
        }
        #professorDisciplinesCheckboxes label, /* Label do checkbox */
        #professorClassesCheckboxes label { /* Label do checkbox */
            margin-left: 5px;
            font-weight: normal; /* Reset para label de checkbox */
            display: inline; /* Para ficar ao lado do checkbox */
        }


        @media print {
            body {
                margin: 0;
                display: block;
            }
            #sidebar, #loginContainer, .modal, .button, input[type="text"], input[type="password"], select.unitCheckbox, input[name="reportType"], #searchName, .close-button {
                display: none !important;
            }
            #appContainer{
                display: block;
                height: auto;
                width: auto;
            }
            #mainContentArea {
                width: 100%;
                padding: 0;
                overflow-y: visible;
                height: auto;
            }
            table {
                page-break-inside: auto;
            }
            tr {
                page-break-inside: avoid;
                page-break-after: auto;
            }
        }
    </style>
</head>
<body>

<div id="loginContainer">
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Usuário">
    <input type="password" id="password" placeholder="Senha">
    <button type="button" class="button" id="loginButton" style="width: auto; display: inline-block;">Entrar</button>
    <p id="loginError" class="error"></p>
</div>

<div id="appContainer" class="hidden">
    <div id="sidebar">
        <h2>Menu</h2>
        <div id="userManagementSection" class="hidden">
            <h3>Gerenciar Usuários</h3>
            <button type="button" class="button" onclick="showAddProfessorForm()">Adicionar Professor</button>
            <button type="button" class="button" onclick="showAddCoordenadorForm()">Adicionar Coordenador</button>
        </div>
        <hr>
        <button type="button" class="button logout-button" onclick="logout()">Sair</button>
    </div>

    <div id="mainContentArea">
        <h1>Gerenciador de Notas de Boletim</h1>

        <h2>Adicionar Aluno</h2>
        <input type="text" id="studentName" placeholder="Nome do Aluno">
        <select id="course">
            <option value="">Selecione o Curso</option>
            <option value="Médio Técnico DS">Médio Técnico DS</option>
            <option value="Formação Profissional">Formação Profissional</option>
            <option value="Médio Técnico D JOGOS">Médio Técnico D JOGOS</option>
            <option value="Médio Tecnico Informática">Médio Tecnico Informática</option>
        </select>
        <select id="class">
            <option value="">Selecione a Turma</option>
            <option value="1A">1A</option>
            <option value="1B">1B</option>
            <option value="1C">1C</option>
            <option value="1D">1D</option>
            <option value="2A">2A</option>
            <option value="2B">2B</option>
            <option value="3A">3A</option>
        </select>
        <select id="unit">
            <option value="">Selecione o Turno</option>
            <option value="Manhã">Manhã</option>
            <option value="Tarde">Tarde</option>
       </select>
        <button type="button" class="button" onclick="addStudent()" style="width: auto; display: inline-block;">Adicionar Aluno</button>

        <h3>Adicionar Disciplina ao Aluno</h3>
        <select id="studentSelect"></select>
        <select id="disciplineSelect">
            <option value="">Selecione a Disciplina</option>
            <option value="Redação">Redação</option>
            <option value="Gramática">Gramática</option>
            <option value="Educação Física">Educação Física</option>
            <option value="Literatura">Literatura</option>
            <option value="Geografia">Geografia</option>
            <option value="Inglês">Inglês</option>
            <option value="História">História</option>
            <option value="Projeto de Vida">Projeto de Vida</option>
            <option value="Artes">Artes</option>
            <option value="Matemática">Matemática</option>
            <option value="Filosofia">Filosofia</option>
            <option value="Física">Física</option>
            <option value="Química">Química</option>
            <option value="Biologia">Biologia</option>
            <option value="Formação Profissional">Formação Profissional</option>
            <option value="Inovaê">Inovaê</option>
        </select>
        <select id="unitSelect"> <option value="">Selecione a Unidade</option>
            <option value="1">1° Unidade</option>
            <option value="2">2° Unidade</option>
            <option value="3">3° Unidade</option>
        </select>
        <select id="evaluation1">
            <option value="">Avaliação 1</option>
            <option value="A">A</option>
            <option value="PA">PA</option>
            <option value="ND">ND</option>
        </select>
        <select id="evaluation2">
            <option value="">Avaliação 2</option>
            <option value="A">A</option>
            <option value="PA">PA</option>
            <option value="ND">ND</option>
        </select>
        <select id="finalGrade">
            <option value="">Menção Final</option>
            <option value="D">Desenvolveu (D)</option>
            <option value="ND">Não Desenvolveu (ND)</option>
        </select>
        <button type="button" class="button" onclick="addDiscipline()" style="width: auto; display: inline-block;">Adicionar Disciplina</button>

        <h2>Consultar Alunos</h2>
        <input type="text" id="searchName" placeholder="Pesquisar Aluno">
        <button type="button" class="button" onclick="searchStudent()" style="width: auto; display: inline-block;">Pesquisar</button>

        <h3>Imprimir Boletim</h3>
          <div>
              <label>Selecione o Aluno:</label>
              <select id="studentSelectPrint"></select>
          </div>
          <div>
              <label>Selecione as Unidades:</label>
              <div>
                  <label><input type="checkbox" class="unitCheckbox" value="1"> Unidade 1</label>
                  <label><input type="checkbox" class="unitCheckbox" value="2"> Unidade 2</label>
                  <label><input type="checkbox" class="unitCheckbox" value="3"> Unidade 3</label>
                  <label><input type="checkbox" class="unitCheckbox" value="4"> Unidade 4</label>
              </div>
          </div>
          <div>
              <label><input type="radio" name="reportType" value="full" checked> Incluir Avaliações</label>
              <label><input type="radio" name="reportType" value="summary"> Somente Menção e Situação</label>
          </div>
        <button type="button" class="button" onclick="printAllReports()" style="width: auto; display: inline-block;">Imprimir Todos os Boletins</button>
        <button type="button" class="button" onclick="printStudentReport()" style="width: auto; display: inline-block;">Imprimir Boletim do Aluno</button>

        <table id="studentTable">
            <thead>
                <tr>
                    <th>Nome</th>
                    <th>Curso</th>
                    <th>Turma</th>
                    <th>Turno</th>
                    <th>Disciplina</th>
                    <th>Unidade</th>
                    <th>Avaliação 1</th>
                    <th>Avaliação 2</th>
                    <th>Menção Final</th>
                    <th>Situação</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
            </tbody>
        </table>
    </div>
</div>

<div id="addProfessorModal" class="modal hidden">
    <div class="modal-content">
        <span class="close-button" onclick="closeAddProfessorModal()">&times;</span>
        <h2>Adicionar Novo Professor</h2>
        <div>
            <label for="professorNameInput">Nome do Professor:</label>
            <input type="text" id="professorNameInput" placeholder="Nome completo">
        </div>
        
        <h3>Disciplinas Lecionadas:</h3>
        <div id="professorDisciplinesCheckboxes">
            </div>

        <h3>Turmas Lecionadas:</h3>
        <div id="professorClassesCheckboxes">
            </div>
        <button type="button" class="button" onclick="saveProfessor()" style="width: auto; display: inline-block; margin-top:15px;">Salvar Professor</button>
    </div>
</div>


<script>
    const students = JSON.parse(localStorage.getItem('students')) || [];
    let teachersData = JSON.parse(localStorage.getItem('teachersData')) || [];
    let userRole = '';

    document.getElementById('loginButton').addEventListener('click', login);

    function setRolePermissions(isProfessorView) {
        const formElementsToToggle = [
            'studentName', 'course', 'class', 'unit', 
            'studentSelect', 'disciplineSelect', 'unitSelect', 
            'evaluation1', 'evaluation2', 'finalGrade'
        ];

        formElementsToToggle.forEach(id => {
            const element = document.getElementById(id);
            if (element) {
                element.disabled = isProfessorView;
            }
        });

        const addStudentButton = document.querySelector('button[onclick="addStudent()"]');
        const addDisciplineButton = document.querySelector('button[onclick="addDiscipline()"]');

        if (addStudentButton) addStudentButton.disabled = isProfessorView;
        if (addDisciplineButton) addDisciplineButton.disabled = isProfessorView;

        const userManagementSection = document.getElementById('userManagementSection');
        if (isProfessorView) {
            userManagementSection.classList.add('hidden');
        } else { 
            userManagementSection.classList.remove('hidden');
        }
    }

    function login() {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;
        const loginError = document.getElementById('loginError');

        loginError.textContent = ''; 

        if (username === 'professor' && password === 'professor') {
            userRole = 'professor';
            document.getElementById('loginContainer').classList.add('hidden');
            document.body.style.display = 'block'; 
            document.getElementById('appContainer').classList.remove('hidden');
            alert('Bem-vindo, Professor!');
            setRolePermissions(true); 
            renderAll();
        } else if (username === 'administrador' && password === 'admsenac2024') {
            userRole = 'admin';
            document.getElementById('loginContainer').classList.add('hidden');
            document.body.style.display = 'block'; 
            document.getElementById('appContainer').classList.remove('hidden');
            alert('Bem-vindo, Administrador!');
            setRolePermissions(false);
            renderAll();
        } else {
            loginError.textContent = 'Usuário ou senha incorretos.';
        }
    }

    function logout() {
        userRole = '';
        document.getElementById('appContainer').classList.add('hidden');
        document.getElementById('loginContainer').classList.remove('hidden');
        document.body.style.display = 'flex'; 
        document.getElementById('userManagementSection').classList.add('hidden'); 
        document.getElementById('username').value = ''; 
        document.getElementById('password').value = ''; 
        document.getElementById('loginError').textContent = ''; 
        alert('Você deslogou com sucesso.');
    }

    function addStudent() {
        const studentName = document.getElementById('studentName').value;
        const course = document.getElementById('course').value;
        const className = document.getElementById('class').value;
        const unit = document.getElementById('unit').value; 

        if (!studentName || !course || !className || !unit) {
            alert('Por favor, preencha todos os campos do aluno.');
            return;
        }

        const student = { name: studentName, course, class: className, unit, disciplines: [] };
        students.push(student);
        localStorage.setItem('students', JSON.stringify(students));
        alert('Aluno adicionado com sucesso!');
        renderAll();

        document.getElementById('studentName').value = '';
        document.getElementById('course').value = '';
        document.getElementById('class').value = '';
        document.getElementById('unit').value = '';
    }

    function addDiscipline() {
        const studentName = document.getElementById('studentSelect').value;
        const disciplineName = document.getElementById('disciplineSelect').value;
        const unitValue = document.getElementById('unitSelect').value; 
        const evaluation1 = document.getElementById('evaluation1').value;
        const evaluation2 = document.getElementById('evaluation2').value;
        const finalGrade = document.getElementById('finalGrade').value;

        if (!studentName || !disciplineName || !unitValue || !evaluation1 || !evaluation2 || !finalGrade) {
            alert('Por favor, preencha todos os campos da disciplina.');
            return;
        }

        const student = students.find(s => s.name === studentName);
        if (student) {
            const existingDiscipline = student.disciplines.find(d => d.discipline === disciplineName && d.unit === unitValue);
            if (existingDiscipline) {
                alert(`A disciplina "${disciplineName}" para a unidade "${unitValue}" já foi adicionada para este aluno.`);
                return;
            }

            student.disciplines.push({ discipline: disciplineName, unit: unitValue, evaluation1, evaluation2, finalGrade });
            localStorage.setItem('students', JSON.stringify(students));
            alert('Disciplina adicionada com sucesso!');
            renderAll();
        }
        document.getElementById('studentSelect').value = '';
        document.getElementById('disciplineSelect').value = '';
        document.getElementById('unitSelect').value = '';
        document.getElementById('evaluation1').value = '';
        document.getElementById('evaluation2').value = '';
        document.getElementById('finalGrade').value = '';
    }

    function renderStudentTable() {
        const studentTableBody = document.getElementById('studentTable').querySelector('tbody');
        studentTableBody.innerHTML = '';
        const isAdminView = userRole === 'admin';

        students.forEach(student => {
            const hasDisciplines = student.disciplines.length > 0;

            if (!hasDisciplines) {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${student.name}</td>
                    <td>${student.course}</td>
                    <td>${student.class}</td>
                    <td>${student.unit}</td>
                    <td colspan="6">Sem disciplinas cadastradas</td>
                    <td>${isAdminView ? `<button type="button" class="button" style="width:auto; display:inline-block; margin-bottom:3px;" onclick="deleteStudent('${student.name}')">Excluir Aluno</button>` : 'N/A'}</td>
                `;
                studentTableBody.appendChild(row);
            } else {
                student.disciplines.forEach((discipline, index) => {
                    const row = document.createElement('tr');
                    let actionsHtml = '';
                     if(isAdminView){
                        actionsHtml = `<button type="button" class="button" style="width:auto; display:inline-block; margin-bottom:3px;" onclick="deleteDiscipline('${student.name}', '${discipline.discipline}', '${discipline.unit}')">Excluir Disciplina</button>`;
                        if(index === 0){ 
                            actionsHtml = `<button type="button" class="button" style="width:auto; display:inline-block; margin-bottom:3px;" onclick="deleteStudent('${student.name}')">Excluir Aluno</button><br>` + actionsHtml;
                        }
                     } else {
                        actionsHtml = 'N/A';
                     }

                     if (index === 0) {
                         row.innerHTML = `
                            <td rowspan="${student.disciplines.length}">${student.name}</td>
                            <td rowspan="${student.disciplines.length}">${student.course}</td>
                            <td rowspan="${student.disciplines.length}">${student.class}</td>
                            <td rowspan="${student.disciplines.length}">${student.unit}</td>
                            <td>${discipline.discipline}</td>
                            <td>${discipline.unit}</td>
                            <td>${discipline.evaluation1}</td>
                            <td>${discipline.evaluation2}</td>
                            <td>${discipline.finalGrade}</td>
                            <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                            <td rowspan="${student.disciplines.length}">${actionsHtml}</td>`; // Ações com rowspan
                     } else {
                         row.innerHTML = `
                            <td>${discipline.discipline}</td>
                            <td>${discipline.unit}</td>
                            <td>${discipline.evaluation1}</td>
                            <td>${discipline.evaluation2}</td>
                            <td>${discipline.finalGrade}</td>
                            <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                            `; // Demais linhas de disciplina não repetem a célula de ações devido ao rowspan
                     }
                    studentTableBody.appendChild(row);
                });
            }
        });
    }

    function renderStudentSelect() {
        const studentSelect = document.getElementById('studentSelect');
        studentSelect.innerHTML = '<option value="">Selecione o Aluno</option>';
        students.forEach(student => {
            const option = document.createElement('option');
            option.value = student.name;
            option.textContent = student.name;
            studentSelect.appendChild(option);
        });
    }

    function renderStudentSelectPrint() {
        const studentSelectPrint = document.getElementById('studentSelectPrint');
        studentSelectPrint.innerHTML = '<option value="">Selecione o Aluno</option>';
        students.forEach(student => {
            const option = document.createElement('option');
            option.value = student.name;
            option.textContent = student.name;
            studentSelectPrint.appendChild(option);
        });
    }

    function deleteStudent(name) {
        if (!confirm(`Tem certeza que deseja excluir o aluno ${name} e todas as suas disciplinas?`)) return;
        const index = students.findIndex(student => student.name === name);
        if (index !== -1) {
            students.splice(index, 1);
            localStorage.setItem('students', JSON.stringify(students));
            renderAll();
        }
    }

    function deleteDiscipline(studentName, disciplineNameToDelete, disciplineUnitToDelete) {
        if (!confirm(`Tem certeza que deseja excluir a disciplina ${disciplineNameToDelete} (Unidade: ${disciplineUnitToDelete}) do aluno ${studentName}?`)) return;
        const student = students.find(s => s.name === studentName);
        if (student) {
            const disciplineIndex = student.disciplines.findIndex(d => d.discipline === disciplineNameToDelete && d.unit === disciplineUnitToDelete);
            if (disciplineIndex !== -1) {
                student.disciplines.splice(disciplineIndex, 1);
                localStorage.setItem('students', JSON.stringify(students));
                renderAll();
            }
        }
    }

    function printAllReports() {
        const selectedUnits = [...document.querySelectorAll('.unitCheckbox:checked')].map(checkbox => checkbox.value);
        const reportType = document.querySelector('input[name="reportType"]:checked').value;

        if(selectedUnits.length === 0){
            alert("Por favor, selecione pelo menos uma unidade para imprimir.");
            return;
        }

        const printWindow = window.open('', '', 'height=600,width=800');
        let reportContent = '<html><head><title>Relatório de Notas</title>';
        reportContent += `<style>
            body{font-family:Arial, sans-serif; margin: 20px;}
            table{width:100%;border-collapse:collapse; margin-bottom: 20px;}
            td,th{border:1px solid #ddd;padding:8px;text-align:center;}
            th{background-color:#1a73e8;color:white;}
            h1, h2, h3 { color: #1a73e8; text-align: center; }
            .student-report { page-break-after: always; } 
            .student-report:last-child { page-break-after: avoid; } 
            </style></head><body>`;
        reportContent += '<h1>SENAC PAULISTA-PE</h1>';
        reportContent += '<h2>Boletim Escolar 2025</h2>';

        students.forEach((student) => {
            const disciplinesToPrint = student.disciplines.filter(discipline => selectedUnits.includes(discipline.unit));
            if (disciplinesToPrint.length === 0 && !selectedUnits.includes("all")) return; 

            reportContent += `<div class="student-report">`;
            reportContent += `<h3>Aluno: ${student.name}</h3>`;
            reportContent += `<p style="text-align:center;">Curso: ${student.course} | Turma: ${student.class} | Turno: ${student.unit}</p>`;
            reportContent += '<table><thead><tr><th>Disciplina</th><th>Unidade</th>';
            if (reportType === 'full') {
                reportContent += '<th>Avaliação 1</th><th>Avaliação 2</th>';
            }
            reportContent += '<th>Menção Final</th><th>Situação</th></tr></thead><tbody>';

            if (disciplinesToPrint.length > 0) {
                disciplinesToPrint.forEach(discipline => {
                    reportContent += `<tr>
                        <td>${discipline.discipline}</td>
                        <td>${discipline.unit}</td>
                        ${reportType === 'full' ? `<td>${discipline.evaluation1}</td><td>${discipline.evaluation2}</td>` : ''}
                        <td>${discipline.finalGrade}</td>
                        <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                    </tr>`;
                });
            } else {
                 reportContent += `<tr><td colspan="${reportType === 'full' ? 6 : 4}">Nenhuma disciplina encontrada para as unidades selecionadas.</td></tr>`;
            }
            reportContent += '</tbody></table></div>';
        });

        reportContent += '</body></html>';
        printWindow.document.write(reportContent);
        printWindow.document.close();
        printWindow.print();
    }

    function printStudentReport() {
        const selectedStudentName = document.getElementById('studentSelectPrint').value;
        const selectedUnits = [...document.querySelectorAll('.unitCheckbox:checked')].map(checkbox => checkbox.value);
        const reportType = document.querySelector('input[name="reportType"]:checked').value;

        if (!selectedStudentName) {
            alert('Por favor, selecione um aluno.');
            return;
        }
        if (selectedUnits.length === 0) {
            alert("Por favor, selecione pelo menos uma unidade para imprimir.");
            return;
        }

        const student = students.find(s => s.name === selectedStudentName);
        if (!student) {
            alert('Aluno não encontrado.');
            return;
        }

        const disciplinesToPrint = student.disciplines.filter(discipline => selectedUnits.includes(discipline.unit));

        const printWindow = window.open('', '', 'height=600,width=800');
        let reportContent = '<html><head><title>Boletim do Aluno</title>';
        reportContent += `<style>
            body{font-family:Arial, sans-serif; margin: 20px;}
            table{width:100%;border-collapse:collapse;}
            td,th{border:1px solid #ddd;padding:8px;text-align:center;}
            th{background-color:#1a73e8;color:white;}
            h1, h2, h3 { color: #1a73e8; text-align: center;}
            </style></head><body>`;
        reportContent += '<h1>SENAC PAULISTA-PE</h1>';
        reportContent += '<h2>Boletim Escolar 2025</h2>';
        reportContent += `<h3>Aluno: ${student.name}</h3>`;
        reportContent += `<p style="text-align:center;">Curso: ${student.course} | Turma: ${student.class} | Turno: ${student.unit}</p>`;
        reportContent += '<table><thead><tr><th>Disciplina</th><th>Unidade</th>';
        if (reportType === 'full') {
            reportContent += '<th>Avaliação 1</th><th>Avaliação 2</th>';
        }
        reportContent += '<th>Menção Final</th><th>Situação</th></tr></thead><tbody>';

        if (disciplinesToPrint.length > 0) {
            disciplinesToPrint.forEach(discipline => {
                reportContent += `<tr>
                    <td>${discipline.discipline}</td>
                    <td>${discipline.unit}</td>
                    ${reportType === 'full' ? `<td>${discipline.evaluation1}</td><td>${discipline.evaluation2}</td>` : ''}
                    <td>${discipline.finalGrade}</td>
                    <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                </tr>`;
            });
        } else {
            reportContent += `<tr><td colspan="${reportType === 'full' ? 6 : 4}">Nenhuma disciplina encontrada para as unidades selecionadas.</td></tr>`;
        }

        reportContent += '</tbody></table></body></html>';
        printWindow.document.write(reportContent);
        printWindow.document.close();
        printWindow.print();
    }

    function showAddProfessorForm() {
        const modal = document.getElementById('addProfessorModal');
        document.getElementById('professorNameInput').value = ''; // Limpa o campo nome
        populateCheckboxes('professorDisciplinesCheckboxes', 'disciplineSelect', 'prof_disc_');
        populateCheckboxes('professorClassesCheckboxes', 'class', 'prof_class_');
        modal.classList.remove('hidden');
    }

    function closeAddProfessorModal() {
        document.getElementById('addProfessorModal').classList.add('hidden');
    }

    function populateCheckboxes(containerId, selectElementId, idPrefix) {
        const container = document.getElementById(containerId);
        const selectElement = document.getElementById(selectElementId);
        container.innerHTML = ''; // Limpa checkboxes anteriores

        Array.from(selectElement.options).forEach(option => {
            if (option.value) { 
                const div = document.createElement('div');
                const checkbox = document.createElement('input');
                checkbox.type = 'checkbox';
                checkbox.id = `${idPrefix}${option.value.replace(/\s+/g, '_').toLowerCase()}`;
                checkbox.value = option.value;
                checkbox.name = containerId; // Usar o ID do container como nome do grupo

                const label = document.createElement('label');
                label.htmlFor = checkbox.id;
                label.textContent = option.textContent;

                div.appendChild(checkbox);
                div.appendChild(label);
                container.appendChild(div);
            }
        });
    }
    
    function saveProfessor() {
        const professorName = document.getElementById('professorNameInput').value.trim();
        if (!professorName) {
            alert('Por favor, insira o nome do professor.');
            return;
        }

        const selectedDisciplines = Array.from(document.querySelectorAll('#professorDisciplinesCheckboxes input[type="checkbox"]:checked'))
                                       .map(cb => cb.value);

        const selectedClasses = Array.from(document.querySelectorAll('#professorClassesCheckboxes input[type="checkbox"]:checked'))
                                   .map(cb => cb.value);

        if (selectedDisciplines.length === 0) {
            alert('Por favor, selecione pelo menos uma disciplina para o professor.');
            return;
        }

        if (selectedClasses.length === 0) {
            alert('Por favor, selecione pelo menos uma turma para o professor.');
            return;
        }
        
        const newProfessor = {
            id: `prof_${Date.now()}`,
            name: professorName,
            disciplines: selectedDisciplines,
            classes: selectedClasses
        };

        teachersData.push(newProfessor);
        localStorage.setItem('teachersData', JSON.stringify(teachersData));

        alert(`Professor ${professorName} adicionado com sucesso!`);
        console.log("Professores cadastrados:", teachersData); 
        closeAddProfessorModal();
    }


    function showAddCoordenadorForm() {
        alert('Funcionalidade "Adicionar Coordenador" ainda não implementada.');
    }

    function renderAll(){
        renderStudentTable();
        renderStudentSelect();
        renderStudentSelectPrint();
    }

    document.addEventListener('DOMContentLoaded', () => {
        document.getElementById('appContainer').classList.add('hidden');
        document.getElementById('loginContainer').classList.remove('hidden');
        document.body.style.display = 'flex'; 
    });

</script>
</body>
</html>
