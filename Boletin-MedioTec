<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciador de Notas de Boletim</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #fff;
            color: #333;
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
        }
        .button:hover {
            background-color: #ff4500; /* Laranja escuro */
        }
        .hidden {
            display: none;
        }
        .error {
            color: red;
            font-size: 14px;
        }
        #loginContainer {
            text-align: center;
        }
        input[type="text"], input[type="password"], select {
            padding: 8px;
            margin: 5px;
            width: 200px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        @media print {
            body {
                margin: 0;
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
    <button type="button" class="button" id="loginButton">Entrar</button>
    <p id="loginError" class="error"></p>
</div>

<div id="appContainer" class="hidden">
    <h1>Gerenciador de Notas de Boletim</h1>

    <button type="button" class="button" onclick="logout()">Sair</button>

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
    <button type="button" class="button" onclick="addStudent()">Adicionar Aluno</button>

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
    <select id="unitSelect">
        <option value="">Selecione a Unidade</option>
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
    <button type="button" class="button" onclick="addDiscipline()">Adicionar Disciplina</button>

    <h2>Consultar Alunos</h2>
    <input type="text" id="searchName" placeholder="Pesquisar Aluno">
    <button type="button" class="button" onclick="searchStudent()">Pesquisar</button>

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
    <button type="button" class="button" onclick="printAllReports()">Imprimir Todos os Boletins</button>
    <button type="button" class="button" onclick="printStudentReport()">Imprimir Boletim do Aluno</button>

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

<script>
    const students = JSON.parse(localStorage.getItem('students')) || [];
    let userRole = '';

    document.getElementById('loginButton').addEventListener('click', login);

    function login() {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;

        if (username === 'professor' && password === 'professor') {
            userRole = 'professor';
            document.getElementById('loginContainer').classList.add('hidden');
            document.getElementById('appContainer').classList.remove('hidden');
            alert('Bem-vindo, Professor!');
            hideAdminFeatures();
        } else if (username === 'administrador' && password === 'admsenac2024') {
            userRole = 'admin';
            document.getElementById('loginContainer').classList.add('hidden');
            document.getElementById('appContainer').classList.remove('hidden');
            alert('Bem-vindo, Administrador!');
        } else {
            document.getElementById('loginError').textContent = 'Usuário ou senha incorretos.';
        }
    }

    function hideAdminFeatures() {
        document.getElementById('studentName').disabled = true;
        document.getElementById('course').disabled = true;
        document.getElementById('class').disabled = true;
        document.getElementById('studentSelect').disabled = true;
        document.getElementById('disciplineSelect').disabled = true;
        document.getElementById('unitSelect').disabled = true;
        document.getElementById('evaluation1').disabled = true;
        document.getElementById('evaluation2').disabled = true;
        document.getElementById('finalGrade').disabled = true;
    }

    function logout() {
        userRole = '';
        document.getElementById('loginContainer').classList.remove('hidden');
        document.getElementById('appContainer').classList.add('hidden');
        alert('Você deslogou com sucesso.');
    }

    function addStudent() {
        const studentName = document.getElementById('studentName').value;
        const course = document.getElementById('course').value;
        const className = document.getElementById('class').value;
        const unit = document.getElementById('unit').value;

        if (!studentName || !course || !className || !unit) {
            alert('Por favor, preencha todos os campos.');
            return;
        }

        const student = { name: studentName, course, class: className, unit, disciplines: [] };
        students.push(student);
        localStorage.setItem('students', JSON.stringify(students));
        alert('Aluno adicionado com sucesso!');
        renderStudentTable();
        renderStudentSelect();
        renderStudentSelectPrint();
        

        // Limpa os campos do formulário
        document.getElementById('studentName').value = '';
        document.getElementById('course').value = '';
        document.getElementById('class').value = '';
        document.getElementById('unit').value = '';

        console.log('Dados do aluno adicionado:', student);
        console.log('Lista de alunos atualizada:', students);
        console.log('Dados salvos no localStorage:', localStorage.getItem('students'));  // Verificando o localStorage

        renderStudentTable();
    }


    function addDiscipline() {
        const studentName = document.getElementById('studentSelect').value;
        const discipline = document.getElementById('disciplineSelect').value;
        const unit = document.getElementById('unitSelect').value;
        const evaluation1 = document.getElementById('evaluation1').value;
        const evaluation2 = document.getElementById('evaluation2').value;
        const finalGrade = document.getElementById('finalGrade').value;

        if (!studentName || !discipline || !unit || !evaluation1 || !evaluation2 || !finalGrade) {
            alert('Por favor, preencha todos os campos.');
            return;
        }

        const student = students.find(s => s.name === studentName);
        if (student) {
            student.disciplines.push({ discipline, unit, evaluation1, evaluation2, finalGrade });
            localStorage.setItem('students', JSON.stringify(students));
            alert('Disciplina adicionada com sucesso!');
            renderStudentTable();
        }
        // Limpa os campos do formulário de disciplina
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

        students.forEach(student => {
            const hasDisciplines = student.disciplines.length > 0;
            const rowSpan = hasDisciplines ? student.disciplines.length : 1;
            const firstRow = document.createElement('tr');

            firstRow.innerHTML = `
                <td rowspan="${rowSpan}">${student.name}</td>
                <td rowspan="${rowSpan}">${student.course}</td>
                <td rowspan="${rowSpan}">${student.class}</td>
                <td rowspan="${rowSpan}">${student.unit}</td>
                ${hasDisciplines ? `<td>${student.disciplines[0].discipline}</td>
                                   <td>${student.disciplines[0].unit}</td>
                                   <td>${student.disciplines[0].evaluation1}</td>
                                   <td>${student.disciplines[0].evaluation2}</td>
                                   <td>${student.disciplines[0].finalGrade}</td>
                                   <td>${student.disciplines[0].finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                                   <td>
                                       <button type="button" class="button" onclick="deleteStudent('${student.name}')">Excluir Aluno</button>
                                       <button type="button" class="button" onclick="deleteDiscipline('${student.name}', '${student.disciplines[0].discipline}')">Excluir Disciplina</button>
                                   </td>` :
                                   `<td colspan="6"></td>
                                    <td><button type="button" class="button" onclick="deleteStudent('${student.name}')">Excluir Aluno</button></td>`}
            `;
            studentTableBody.appendChild(firstRow);

            if (hasDisciplines) {
                for (let i = 1; i < student.disciplines.length; i++) {
                    const discipline = student.disciplines[i];
                    const newRow = document.createElement('tr');
                    newRow.innerHTML = `
                        <td>${discipline.discipline}</td>
                        <td>${discipline.unit}</td>
                        <td>${discipline.evaluation1}</td>
                        <td>${discipline.evaluation2}</td>
                        <td>${discipline.finalGrade}</td>
                        <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                        <td><button type="button" class="button" onclick="deleteDiscipline('${student.name}', '${discipline.discipline}')">Excluir Disciplina</button></td>
                    `;
                    studentTableBody.appendChild(newRow);
                }
            } else {
                const emptyRow = document.createElement('tr');
                emptyRow.innerHTML = `<td colspan="10"></td>`;
                studentTableBody.appendChild(emptyRow);
            }
        });
    }


    function renderStudentSelect() {
        const studentSelect = document.getElementById('studentSelect');
        studentSelect.innerHTML = '';
        const defaultOption = document.createElement('option');
        defaultOption.value = '';
        defaultOption.textContent = 'Selecione o Aluno';
        studentSelect.appendChild(defaultOption);
        students.forEach(student => {
            const option = document.createElement('option');
            option.value = student.name;
            option.textContent = student.name;
            studentSelect.appendChild(option);
        });
    }

    function renderStudentSelectPrint() {
        const studentSelect = document.getElementById('studentSelectPrint');
        studentSelect.innerHTML = '';
        const defaultOption = document.createElement('option');
        defaultOption.value = '';
        defaultOption.textContent = 'Selecione o Aluno';
        studentSelect.appendChild(defaultOption);
        students.forEach(student => {
            const option = document.createElement('option');
            option.value = student.name;
            option.textContent = student.name;
            studentSelect.appendChild(option);
        });
    }

    function deleteStudent(name) {
        const index = students.findIndex(student => student.name === name);
        if (index !== -1) {
            students.splice(index, 1);
            localStorage.setItem('students', JSON.stringify(students));
            renderStudentTable();
            renderStudentSelect();
            renderStudentSelectPrint();
        }
    }

    function deleteDiscipline(studentName, disciplineName) {
        const student = students.find(s => s.name === studentName);
        if (student) {
            const disciplineIndex = student.disciplines.findIndex(d => d.discipline === disciplineName);
            if (disciplineIndex !== -1) {
                student.disciplines.splice(disciplineIndex, 1);
                localStorage.setItem('students', JSON.stringify(students));
                renderStudentTable();
            }
        }
    }


    function printAllReports() {
        const selectedUnits = [...document.querySelectorAll('.unitCheckbox:checked')].map(checkbox => checkbox.value);
        const reportType = document.querySelector('input[name="reportType"]:checked').value;

        const printWindow = window.open('', '', 'height=600,width=800');
        let reportContent = '<html><head><title>Relatório de Notas</title></head><body>';
        reportContent += '<h1>SENAC PAULISTA-PE</h1>';
        reportContent += '<h2>Boletin 2025</h2>';
        reportContent += '<style>body{font-family:Arial, sans-serif;}table{width:100%;border-collapse:collapse;}td,th{border:1px solid #ddd;padding:8px;text-align:center;}th{background-color:#1a73e8;color:white;}</style>';
        reportContent += '<h1>Relatório de Boletins</h1>';
        reportContent += '<table><thead><tr><th>Nome</th><th>Curso</th><th>Turma</th><th>Turno</th><th>Disciplina</th><th>Unidade</th>';
        if (reportType === 'full') {
            reportContent += '<th>Avaliação 1</th><th>Avaliação 2</th>';
        }
        reportContent += '<th>Menção Final</th><th>Situação</th></tr></thead><tbody>';

        students.forEach(student => {
            const hasDisciplines = student.disciplines.length > 0;
            if (!hasDisciplines){
                 reportContent += `<tr>
                        <td>${student.name}</td>
                        <td>${student.course}</td>
                        <td>${student.class}</td>
                        <td>${student.unit}</td>
                        <td colspan="6">Sem Disciplinas</td>
                        </tr>`;
            }
            student.disciplines.forEach(discipline => {
                if (selectedUnits.includes(discipline.unit)) {
                    reportContent += `<tr>
                        <td>${student.name}</td>
                        <td>${student.course}</td>
                        <td>${student.class}</td>
                        <td>${student.unit}</td>
                        <td>${discipline.discipline}</td>
                        <td>${discipline.unit}</td>
                        ${reportType === 'full' ? `<td>${discipline.evaluation1}</td><td>${discipline.evaluation2}</td>` : ''}
                        <td>${discipline.finalGrade}</td>
                        <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                    </tr>`;
                }
            });
        });

        reportContent += '</tbody></table>';
        reportContent += '</body></html>';
        printWindow.document.write(reportContent);
        printWindow.document.close();
        printWindow.print();
    }

    function printStudentReport() {
        const selectedStudentName = document.getElementById('studentSelectPrint').value;
        const selectedUnits = [...document.querySelectorAll('.unitCheckbox:checked')].map(checkbox => checkbox.value);
        const reportType = document.querySelector('input[name="reportType"]:checked').value;

        const student = students.find(s => s.name === selectedStudentName);

        if (!student) {
            alert('Aluno não encontrado.');
            return;
        }

        const printWindow = window.open('', '', 'height=600,width=800');
        let reportContent = '<html><head><title>Boletim do Aluno</title></head><body>';
        reportContent += '<h1>SENAC PAULISTA-PE</h1>';
        reportContent += '<h2>Boletin 2025</h2>';
        reportContent += '<style>body{font-family:Arial, sans-serif;}table{width:100%;border-collapse:collapse;}td,th{border:1px solid #ddd;padding:8px;text-align:center;}th{background-color:#1a73e8;color:white;}</style>';
        reportContent += `<h1>Boletim do Aluno: ${student.name}</h1>`;
        reportContent += '<table><thead><tr><th>Curso</th><th>Turma</th><th>Turno</th><th>Disciplina</th><th>Unidade</th>';
        if (reportType === 'full') {
            reportContent += '<th>Avaliação 1</th><th>Avaliação 2</th>';
        }
        reportContent += '<th>Menção Final</th><th>Situação</th></tr></thead><tbody>';

        const hasDisciplines = student.disciplines.length > 0;
            if (!hasDisciplines){
                 reportContent += `<tr>
                        <td>${student.course}</td>
                        <td>${student.class}</td>
                        <td>${student.unit}</td>
                        <td colspan="6">Sem Disciplinas</td>
                        </tr>`;
            }
        student.disciplines.forEach(discipline => {
            if (selectedUnits.includes(discipline.unit)) {
                reportContent += `<tr>
                    <td>${student.course}</td>
                    <td>${student.class}</td>
                    <td>${student.unit}</td>
                    <td>${discipline.discipline}</td>
                    <td>${discipline.unit}</td>
                    ${reportType === 'full' ? `<td>${discipline.evaluation1}</td><td>${discipline.evaluation2}</td>` : ''}
                    <td>${discipline.finalGrade}</td>
                    <td>${discipline.finalGrade === 'D' ? 'Aprovado' : 'Reprovado'}</td>
                </tr>`;
            }
        });

        reportContent += '</tbody></table>';
        reportContent += '</body></html>';
        printWindow.document.write(reportContent);
        printWindow.document.close();
        printWindow.print();
    }

    renderStudentTable();
    renderStudentSelect();
    renderStudentSelectPrint();
</script>
</body>
</html>
