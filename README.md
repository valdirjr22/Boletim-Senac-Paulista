<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciador de Notas de Boletim - MÉDIOTEC</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Modern font */
            margin: 0;
            background-color: #f0f2f5; /* Slightly gray background */
            color: #333;
            min-height: 100vh;
            padding-bottom: 40px; /* Add bottom padding for fixed footer */
            box-sizing: border-box; /* Include padding in total height */
        }
        /* Center login container when visible */
        body:has(#loginContainer:not(.hidden)) {
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(to bottom right, #005aaa, #00397a); /* Gradient background for login */
            padding-bottom: 0; /* Remove body padding on login screen */
        }

        h1, h2, h3 {
            color: #1a73e8; /* Blue */
        }
        h2, h3 {
            border-bottom: 2px solid #ff6600; /* Orange */
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
            background-color: #1a73e8; /* Blue */
            color: white;
        }
        .button {
            background-color: #ff6600; /* Orange */
            color: white;
            padding: 10px 15px;
            border: none;
            cursor: pointer;
            margin: 5px;
            border-radius: 5px;
            display: block;
            width: calc(100% - 10px);
            transition: background-color 0.3s ease; /* Smooth transition */
        }
        .button:hover {
            background-color: #ff4500; /* Darker orange */
        }
         .button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
         .button.delete-button {
             background-color: #dc3545; /* Red for delete */
         }
         .button.delete-button:hover {
             background-color: #c82333; /* Darker red */
          }
        .hidden {
            display: none !important;
        }
        .error {
            color: #dc3545; /* Bootstrap red */
            font-size: 14px;
            margin-top: 10px; /* Space above */
        }

        /* --- Improved Login Screen Styles --- */
        #loginContainer {
            text-align: center;
            padding: 40px 35px; /* More padding */
            border: none; /* Remove border */
            border-radius: 10px; /* More rounded corners */
            background-color: #ffffff; /* White background */
            position: relative;
            overflow: hidden;
            width: 400px; /* Slightly larger container */
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15); /* More pronounced shadow */
        }
        /* Highlighted SENAC name */
        #loginContainer .senac-title {
            font-size: 3em; /* Larger size */
            font-weight: bold;
            color: #ff6600; /* SENAC Orange */
            margin-bottom: 30px; /* More space below */
            line-height: 1.1;
        }

        /* Login Watermark Logo (Adjusted) */
        .login-watermark {
            position: absolute;
            bottom: 10px; /* Bottom position */
            left: 50%;
            transform: translateX(-50%);
            opacity: 0.05; /* More subtle */
            z-index: 0;
            pointer-events: none;
            width: 60%; /* Relative width */
        }
        .login-watermark img {
             max-width: 100%;
             height: auto;
        }

        /* Improved Input Fields */
        #loginContainer input[type="text"],
        #loginContainer input[type="password"] {
            padding: 15px; /* More internal padding */
            margin: 15px 0; /* More vertical space */
            width: 100%;
            border-radius: 5px;
            border: 1px solid #ccc; /* Subtle border */
            box-sizing: border-box;
            font-size: 16px;
            transition: border-color 0.3s ease, box-shadow 0.3s ease; /* Transitions */
        }
        #loginContainer input[type="text"]:focus,
        #loginContainer input[type="password"]:focus {
            border-color: #ff6600; /* Orange on focus */
            box-shadow: 0 0 0 3px rgba(255, 102, 0, 0.2); /* Outer shadow on focus */
            outline: none; /* Remove default outline */
        }

         /* Improved Login Button */
         #loginContainer #loginButton {
             width: 100% !important; /* Full width */
             display: block !important;
             padding: 15px 30px; /* Generous padding */
             margin-top: 25px; /* Space above */
             font-size: 18px; /* Font size */
             font-weight: bold;
             background-color: #ff6600; /* Orange */
             border: none;
             border-radius: 5px;
             color: white;
             cursor: pointer;
             transition: background-color 0.3s ease, box-shadow 0.3s ease;
         }
         #loginContainer #loginButton:hover {
             background-color: #ff4500; /* Darker orange */
             box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
         }
         /* --- End Login Styles --- */


        #appContainer {
            display: flex;
            width: 100%;
            height: 100vh;
            overflow: hidden;
            background-color: #fff; /* White background for app */
        }

        #sidebar {
            width: 230px;
            background-color: #f8f9fa; /* Bootstrap sidebar color */
            padding: 15px;
            display: flex;
            flex-direction: column;
            border-right: 1px solid #dee2e6; /* Bootstrap border */
            height: 100%;
            box-sizing: border-box;
            flex-shrink: 0;
        }
        #sidebar h2, #sidebar h3 {
            margin-top: 10px;
            margin-bottom: 10px;
            font-size: 1.1em; /* Adjusted size */
            color: #495057; /* Darker color */
        }
        #sidebar .button {
            margin-bottom: 10px;
             text-align: left; /* Align button text */
             padding: 10px 12px;
             width: 100%; /* Full width */
             box-sizing: border-box;
        }
        #sidebar .button.logout-button {
            margin-top: auto;
            background-color: #6c757d; /* Dark gray logout */
        }
         #sidebar .button.logout-button:hover {
             background-color: #5a6268;
         }

        #mainContentArea {
            flex-grow: 1;
            padding: 25px; /* General padding */
            padding-top: 80px; /* Space for fixed logo/text */
            overflow-y: auto;
            height: calc(100vh - 80px - 40px); /* Adjusted height for fixed header and footer */
            box-sizing: border-box;
            position: relative;
        }
        /* App Text - Top Right Corner */
        #appHeaderText {
            position: fixed;
            top: 15px;
            right: 25px;
            font-size: 2em; /* Large size */
            font-weight: bold;
            color: #00397a; /* Dark blue */
            z-index: 1001;
        }


        #mainContentArea h1 {
            margin-top: 0;
            margin-bottom: 25px; /* More space below main title */
        }

        /* General adjustments for inputs/selects within the App */
        input[type="text"], input[type="password"], select {
            padding: 10px; /* Increase padding */
            margin: 5px 3px; /* Adjust margin */
            width: auto; /* Allow initial auto adjustment */
            min-width: 180px; /* Minimum width */
            border-radius: 5px;
            border: 1px solid #ced4da; /* Bootstrap border */
            box-sizing: border-box;
            font-size: 15px;
        }
         input[type="text"]:disabled, select:disabled {
             background-color: #e9ecef;
             cursor: not-allowed;
         }
        /* Inline buttons with inputs */
        #addStudentSection button, #addDisciplineSection button, #mainContentArea h2 + button, #mainContentArea h3 + button {
             width: auto !important;
             display: inline-block !important;
             vertical-align: middle; /* Align with selects/inputs */
             margin-left: 10px;
        }
        /* Adjustment for observation input, can be wider */
        #addDisciplineSection input[type="text"]#observationInput {
            min-width: 250px; /* Allow a bit more space for observation */
        }


        /* Modal styles */
        .modal { position: fixed; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.5); z-index: 1000; display: flex; justify-content: center; align-items: center; }
        .modal-content { background-color: white; padding: 20px; border-radius: 8px; width: 500px; max-width: 90%; max-height: 80vh; overflow-y: auto; position: relative; z-index: 1002; }
        .modal-content h2 { margin-top: 0; }
        .modal-content label{ display: block; margin-top: 10px; font-weight: bold; }
        .modal-content input[type="text"], .modal-content input[type="password"] { width: 100%; } /* Inputs in modal 100% */
        .close-button { position: absolute; top: 10px; right: 15px; font-size: 24px; font-weight: bold; cursor: pointer; }
        #professorDisciplinesCheckboxes div, #professorClassesCheckboxes div, #editProfessorDisciplinesCheckboxes div, #editProfessorClassesCheckboxes div { margin-bottom: 5px; } /* Added edit IDs */
        #professorDisciplinesCheckboxes label, #professorClassesCheckboxes label, #editProfessorDisciplinesCheckboxes label, #editProfessorClassesCheckboxes label { margin-left: 5px; font-weight: normal; display: inline-block; margin-right: 10px; } /* Added edit IDs */
        #professorDisciplinesCheckboxes input[type="checkbox"], #professorClassesCheckboxes input[type="checkbox"], #editProfessorDisciplinesCheckboxes input[type="checkbox"], #editProfessorClassesCheckboxes input[type="checkbox"] { vertical-align: middle;} /* Added edit IDs */

        /* Style for editable cells */
        .editable-cell {
            cursor: pointer;
            border: 1px dashed #ccc; /* Dashed border to indicate editable */
        }
         .editable-cell:hover {
             background-color: #e9e9e9;
         }
         .editable-cell input[type="text"], .editable-cell select {
             width: 100%;
             padding: 0;
             margin: 0;
             border: none;
             background: none;
             text-align: center;
             font-size: inherit;
             font-family: inherit;
             box-sizing: border-box;
             outline: none; /* Remove outline when editing */
         }
         .editable-cell.editing {
             background-color: #fff; /* White background when editing */
         }

        /* Styles for User Management Table */
        #manageUsersSection table {
             margin-top: 15px;
             width: 95%; /* Slightly wider table to fit password */
             margin-left: auto;
             margin-right: auto;
        }
         #manageUsersSection table th, #manageUsersSection table td {
             text-align: left;
              padding: 10px; /* More padding */
         }
          #manageUsersSection table td:nth-last-child(2) { /* Password Column (second to last before Actions) */
             font-family: 'Courier New', Courier, monospace; /* Monospaced font for passwords */
             font-size: 0.9em;
             overflow-wrap: break-word; /* Break password if too long */
          }
          #manageUsersSection table th:nth-last-child(2), #manageUsersSection table td:nth-last-child(2) { /* Center Password title */
             text-align: center;
          }
           #manageUsersSection table td:last-child { /* Actions Column */
                text-align: center;
                width: 120px; /* Space for buttons */
           }
           #manageUsersSection table .button {
                width: auto;
                display: inline-block;
                margin: 2px;
           }
            #manageUsersSection p { /* Message when no users */
                 text-align: center;
                 font-style: italic;
                 color: #666;
            }
            #manageUsersSection .security-warning {
                color: #dc3545; /* Red */
                text-align: center;
                margin-top: 20px;
                font-weight: bold;
            }

            /* Styles for Professor Section */
             #professorSection h1 {
                 margin-bottom: 15px;
             }
             #professorSection p {
                 margin-bottom: 15px;
             }
              #professorSection label {
                  font-weight: bold;
                  margin-right: 5px;
              }
              #professorSection select {
                 margin-right: 15px;
              }
              #professorSection table.professor-table th, #professorSection table.professor-table td {
                   text-align: center; /* Center cells in professor table */
               }
               #professorSection table.professor-table td:first-child {
                  text-align: left; /* Student name aligned left */
               }
                /* Adjustment for observation cell in professor table */
               #professorSection table.professor-table td:last-child {
                   text-align: left; /* Align observations left */
               }

            /* Fixed footer in the application */
            #appFooter {
                width: 100%;
                height: 40px; /* Footer height */
                background-color: #00397a; /* SENAC Blue */
                color: white;
                text-align: center;
                line-height: 40px; /* Vertically center text */
                font-size: 0.9em;
                position: fixed; /* Fix to bottom */
                bottom: 0;
                left: 0;
                z-index: 1000;
            }


        /* Print Styles (UPDATED) */
        @media print {
            body { margin: 0; display: block; background-color: #fff !important; color: #000; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; font-size: 10pt; }
            body:has(#loginContainer:not(.hidden)) { display: none !important; } /* Hide everything if on login screen */
             body { padding-bottom: 0 !important; } /* Remove body bottom padding on print */


            /* Hide UI elements */
            #sidebar, #loginContainer, .modal, .button, input, select, .unitCheckbox, label[for="studentSelectPrint"], label[for="reportType"],
             #searchName, .close-button, th button, td button, #appHeaderText, .login-watermark,
             #loginContainer .senac-title, #manageUsersSection, #manageUsersSection table .button, #manageUsersSection .security-warning,
             #professorSection select, #professorSection label, #appFooter /* Hide footer on print */
             { display: none !important; }

             #appContainer{ display: block; height: auto; width: 100%; overflow: visible; background-color: #fff !important;}
             #mainContentArea { width: 100%; padding: 0; overflow-y: visible; height: auto; flex-grow: 0; }

             /* Table Styles for Print */
             table { width: 100%; border-collapse: collapse; margin-top: 10px; }
             th, td { border: 1px solid #000; padding: 6px; text-align: center; font-size: 9pt; }
             th { background-color: #ddd !important; color: #000 !important; font-weight: bold; }
             td { text-align: center; } /* Ensure data cells are centered */
             td:first-child { text-align: left; } /* Align student name left in table */
             /* Adjustments for the new Observations column in print */
             #studentTable td:nth-last-child(2), #professorStudentTable td:nth-last-child(1) {
                 text-align: left; /* Align observation text left */
                 font-size: 8pt; /* Slightly smaller font if observation is long */
             }


             /* Control page breaks */
             tr { page-break-inside: avoid; page-break-after: auto; }
             table, tr, td, th { page-break-inside: avoid !important; } /* Prevent breaks inside table elements */
              .student-report { page-break-inside: avoid; page-break-after: always; margin-bottom: 0; padding: 10px 0;} /* Ensure report block stays together and force break after */
              .student-report:last-child { page-break-after: avoid; margin-bottom: 0; } /* Don't force break after the last report */

             /* Styles for each report header */
              .student-report div:first-child { text-align: center; margin-bottom: 10px; padding-bottom: 5px; border-bottom: 1px solid #ccc;}
              .student-report h2 { color: #000 !important; border-bottom: none; margin: 0; padding: 0; font-size: 14pt;}
              .student-report p { margin: 2px 0; font-size: 10pt;}
              .student-report strong { font-weight: bold; }

             /* Styles for the generated bulletin table */
             .bulletin-table {
                 width: 100%;
                 border-collapse: collapse;
                 margin-top: 15px;
             }
             .bulletin-table th, .bulletin-table td {
                 border: 1px solid #000;
                 padding: 8px;
                 text-align: center;
                 font-size: 9pt;
             }
             .bulletin-table th {
                 background-color: #eee !important; /* Light gray background for bulletin header */
                 color: #000 !important;
                 font-weight: bold;
             }
             .bulletin-table td {
                  text-align: center;
             }
             .bulletin-table td:first-child {
                 text-align: left; /* Discipline name aligned left */
             }
              .bulletin-table td:last-child {
                  text-align: left; /* Observation aligned left */
              }

             /* New styles for the bulletin header layout */
              .bulletin-header {
                  text-align: center;
                  margin-bottom: 20px; /* More space below the header block */
                  padding-bottom: 15px; /* More padding below the header content */
                  border-bottom: 2px solid #000; /* Thicker border */
              }
              .bulletin-header h2 {
                  margin-top: 0;
                  margin-bottom: 5px; /* Space below the main title */
                  font-size: 16pt; /* Slightly larger font */
                  color: #000; /* Ensure black color for printing */
              }
               .bulletin-header p {
                   margin: 5px 0; /* More space between paragraphs */
                   font-size: 11pt; /* Slightly larger font for student info */
                   color: #333; /* Ensure dark color */
               }
               .bulletin-header p strong {
                   font-weight: bold;
               }
                /* Specific styles for the consolidated header lines */
                .bulletin-header .line1 {
                    font-size: 18pt; /* Larger font for the main title line */
                    font-weight: bold;
                    margin-bottom: 8px; /* Space below line 1 */
                }
                 .bulletin-header .line2 {
                     font-size: 14pt; /* Slightly smaller for the secondary title */
                     margin-bottom: 8px; /* Space below line 2 */
                 }
                  .bulletin-header .line3 {
                      font-size: 11pt; /* Standard font for student info line */
                      margin-top: 8px; /* Add space above line 3 */
                      margin-bottom: 0; /* No margin below the last line of the header block */
                  }


             /* Page Margins */
              @page { size: A4; margin: 1.5cm; } /* Define page margins */
              body { padding: 0; } /* Remove body padding if margin is defined in @page */

              /* Ensure editable cell content is printed */
             .editable-cell span { display: inline !important; }

        }
    </style>
</head>
<body>

<div id="loginContainer">
    <div class="login-watermark">
        <img src="senac_logo.png" alt="Logo SENAC">
    </div>

    <h1 class="senac-title">SENAC</h1>

    <input type="text" id="username" placeholder="Usuário">
    <input type="password" id="password" placeholder="Senha">
    <button type="button" class="button" id="loginButton">Entrar</button>
    <p id="loginError" class="error"></p>
</div>

<div id="appContainer" class="hidden">
    <div id="sidebar">
        <button type="button" class="button" onclick="goHome()">Voltar ao Início</button>
        <div id="userManagementSection" class="hidden">
            <h3>Gerenciar Usuários</h3>
            <button type="button" class="button" onclick="showAddProfessorForm()">Adicionar Professor</button>
             <button type="button" class="button" onclick="showAddCoordenadorForm()">Adicionar Coordenador</button>
            <button type="button" class="button" onclick="showManageUsersSection()">Gerenciar Professores/Coordenadores</button>
        </div>
        <hr id="sidebarHr" class="hidden">
        <button type="button" class="button logout-button" onclick="logout()">Sair</button>
    </div>

    <div id="mainContentArea">
        <div id="appHeaderText">MÉDIOTEC</div>

        <div id="studentManagementSection" class="hidden"> <h1>Gerenciador de Notas de Boletim</h1>

            <div id="addStudentSection" class="hidden"> <h2>Adicionar Aluno</h2>
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
                     <option value="1A">1A</option> <option value="1B">1B</option>
                     <option value="1C">1C</option>
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
            </div>

            <div id="addDisciplineSection" class="hidden"> <h3>Adicionar Disciplina ao Aluno</h3>
                <select id="studentSelect">
                    <option value="">Selecione o Aluno</option>
                    </select>
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
                    <option value="Sociologia">Sociologia</option>
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
                 <input type="text" id="observationInput" placeholder="Observações (Opcional)">
                <button type="button" class="button" onclick="addDiscipline()">Adicionar Disciplina</button>
            </div>

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
                 </div>
             </div>
             <div>
                 <label><input type="radio" name="reportType" value="full" checked> Incluir Avaliações</label>
                 <label><input type="radio" name="reportType" value="summary"> Somente Menção e Situação</label>
             </div>
            <button type="button" class="button" onclick="printAllReports()">Imprimir Todos os Boletins</button>
            <button type="button" class="button" onclick="printStudentReport()">Imprimir Boletim do Aluno</button>

             <h3>Backup/Restaurar Dados (Manual)</h3>
            <button type="button" class="button" onclick="exportData()">Exportar Dados (Backup)</button>
            <div style="margin-top: 10px; border: 1px solid #ccc; padding: 10px; border-radius: 5px;">
                <p style="margin-top: 0; font-weight: bold;">Importar Dados:</p>
                <input type="file" id="importFile" accept=".json" style="display:none;">
                <button type="button" class="button" onclick="document.getElementById('importFile').click()" style="width: auto; display: inline-block; margin: 5px 0;">Selecionar Arquivo</button>
                <span id="importFileName" style="margin-left: 10px; font-style: italic;">Nenhum arquivo selecionado.</span>
                <button type="button" class="button delete-button" onclick="importData()" disabled id="performImportButton" style="width: auto; display: inline-block; margin: 5px;">Confirmar Importação (Irá substituir dados atuais!)</button>
                <p id="importStatus" class="error" style="margin-top: 5px;"></p>
            </div>
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
                         <th>Observações</th> <th>Ações</th>
                     </tr>
                 </thead>
                 <tbody>
                     </tbody>
             </table>
        </div>

        <div id="manageUsersSection" class="hidden"> <h1>Gerenciar Professores e Coordenadores</h1>
             <button type="button" class="button" style="width:auto; margin-bottom: 20px;" onclick="showStudentManagementSection()">Voltar para Gerenciar Alunos</button>

             <p class="security-warning">AVISO DE SEGURANÇA: As senhas estão visíveis nesta tela apenas para demonstração. Em um sistema real, senhas nunca devem ser exibidas ou armazenadas em texto plano.</p>
             <p id="noUsersMessage">Nenhum usuário (Professor ou Coordenador) cadastrado além do administrador principal.</p>
             <table id="usersTable">
                 <thead>
                     <tr>
                          <th>Nome</th>
                          <th>Usuário</th>
                          <th>Papel</th>
                          <th>Disciplinas Atribuídas</th>
                          <th>Turmas Atribuídas</th>
                          <th>Senha</th>
                          <th>Ações</th>
                     </tr>
                 </thead>
                 <tbody>
                     </tbody>
             </table>
        </div>

         <div id="professorSection" class="hidden"> <h1 id="professorWelcome">Olá, Professor(a)!</h1> <p>Selecione a disciplina, turma e unidade para lançar ou editar as notas dos alunos.</p>

             <div>
                 <label for="professorDisciplineSelect">Disciplina:</label>
                 <select id="professorDisciplineSelect">
                     <option value="">Selecione a Disciplina</option>
                     </select>

                 <label for="professorClassSelect" style="margin-left: 20px;">Turma:</label>
                 <select id="professorClassSelect">
                      <option value="">Selecione a Turma</option>
                      </select>

                 <label for="professorUnitSelect" style="margin-left: 20px;">Unidade:</label>
                 <select id="professorUnitSelect">
                      <option value="">Selecione a Unidade</option>
                      <option value="1">1° Unidade</option>
                      <option value="2">2° Unidade</option>
                      <option value="3">3° Unidade</option>
                 </select>
             </div>

             <table id="professorStudentTable" class="professor-table" style="margin-top: 20px;">
                  <thead>
                      <tr>
                           <th>Nome do Aluno</th>
                           <th>Curso</th>
                           <th>Turno</th>
                           <th>Avaliação 1</th>
                           <th>Avaliação 2</th>
                           <th>Menção Final</th>
                           <th>Situação</th>
                           <th>Observações</th> </tr>
                  </thead>
                  <tbody>
                      </tbody>
             </table>
             <p id="professorNoStudentsMessage" style="text-align: center; font-style: italic; margin-top: 20px;">Selecione a disciplina, turma e unidade acima para ver os alunos.</p>

         </div>


    </div>
    <footer id="appFooter">SENAC</footer>
</div>

<div id="addProfessorModal" class="modal hidden">
    <div class="modal-content">
        <span class="close-button" onclick="closeAddProfessorModal()">&times;</span>
        <h2>Adicionar Novo Professor</h2>
        <div>
            <label for="newProfessorNameInput">Nome Completo:</label>
            <input type="text" id="newProfessorNameInput" placeholder="Nome completo do professor">
        </div>
         <div>
             <label for="newProfessorUsernameInput">Usuário (Login):</label>
             <input type="text" id="newProfessorUsernameInput" placeholder="Nome de usuário para login">
         </div>
         <div>
             <label for="newProfessorPasswordInput">Senha:</label>
             <input type="password" id="newProfessorPasswordInput" placeholder="Senha para login">
         </div>

        <h3>Atribuições:</h3>
        <label>Disciplinas:</label>
        <div id="professorDisciplinesCheckboxes">
             </div>

         <label style="margin-top: 15px;">Turmas:</label>
         <div id="professorClassesCheckboxes">
             </div>
        <button type="button" class="button" onclick="saveProfessor()" style="width: auto; display: inline-block; margin-top:20px;">Salvar Professor</button>
    </div>
</div>

<div id="addCoordinatorModal" class="modal hidden">
    <div class="modal-content">
        <span class="close-button" onclick="closeAddCoordenadorModal()">&times;</span>
        <h2>Adicionar Novo Coordenador</h2>
        <div>
            <label for="newCoordinatorNameInput">Nome Completo:</label>
            <input type="text" id="newCoordinatorNameInput" placeholder="Nome completo do coordenador">
        </div>
         <div>
             <label for="newCoordinatorUsernameInput">Usuário (Login):</label>
             <input type="text" id="newCoordinatorUsernameInput" placeholder="Nome de usuário para login">
         </div>
         <div>
             <label for="newCoordinatorPasswordInput">Senha:</label>
             <input type="password" id="newCoordinatorPasswordInput" placeholder="Senha para login">
         </div>
         <p style="margin-top: 15px; color: #555;">Coordenadores têm acesso total ao sistema, exceto a criação/edição de usuários.</p>
        <button type="button" class="button" onclick="saveCoordinator()" style="width: auto; display: inline-block; margin-top:20px;">Salvar Coordenador</button>
    </div>
</div>


<div id="editUserModal" class="modal hidden">
    <div class="modal-content">
        <span class="close-button" onclick="closeEditUserModal()">&times;</span>
        <h2 id="editUserModalTitle">Editar Usuário</h2>
        <input type="hidden" id="editUserOriginalUsername">
        <input type="hidden" id="editUserRole">
        <div>
            <label for="editUserNameInput">Nome Completo:</label>
            <input type="text" id="editUserNameInput" placeholder="Nome completo">
        </div>
         <div>
             <label for="editUserUsernameInput">Usuário (Login):</label>
             <input type="text" id="editUserUsernameInput" placeholder="Nome de usuário para login">
             <small style="display: block; margin-top: 5px; color: #555;">Alterar o usuário pode exigir um novo login.</small>
         </div>
         <div>
             <label for="editUserPasswordInput">Senha:</label>
             <input type="password" id="editUserPasswordInput" placeholder="Deixe em branco para manter a senha atual">
             <small style="display: block; margin-top: 5px; color: #555;">Deixe este campo em branco para não alterar a senha.</small>
         </div>

        <div id="editProfessorAssignments">
             <h3>Atribuições:</h3>
             <label>Disciplinas:</label>
             <div id="editProfessorDisciplinesCheckboxes">
                  </div>

              <label style="margin-top: 15px;">Turmas:</label>
              <div id="editProfessorClassesCheckboxes">
                  </div>
        </div>
        <button type="button" class="button" onclick="updateUser()" style="width: auto; display: inline-block; margin-top:20px;">Atualizar Usuário</button>
    </div>
</div>

<script>
    // --- DATA SIMULATION IN MEMORY (Replace with Local Storage or Backend) ---
    // This is a basic structure for demonstration.
    // In a real system, you'd load this data from a persistent source.
    let students = [
        // Example data structure for a student with disciplines and grades/observations
        {
            id: 's1', // Unique student ID
            name: 'Aluno Exemplo Um',
            course: 'Médio Técnico DS',
            class: '1A', // Updated class
            unit: 'Manhã', // Turno
            disciplines: [
                { discipline: 'Matemática', unit: 1, eval1: 'A', eval2: 'PA', finalGrade: 'D', situation: 'Aprovado', observation: 'Ótimo desempenho na primeira unidade.' },
                { discipline: 'Português', unit: 1, eval1: 'PA', eval2: 'ND', finalGrade: 'ND', situation: 'Reprovado', observation: 'Precisa melhorar na interpretação de texto.' },
                 { discipline: 'Matemática', unit: 2, eval1: 'A', eval2: 'A', finalGrade: 'D', situation: 'Aprovado', observation: '' },
            ]
        },
         {
            id: 's2',
            name: 'Aluno Exemplo Dois',
            course: 'Médio Técnico DS',
            class: '2B', // Updated class
            unit: 'Tarde',
            disciplines: [
                { discipline: 'Matemática', unit: 1, eval1: 'ND', eval2: 'ND', finalGrade: 'ND', situation: 'Reprovado', observation: 'Muita dificuldade com a matéria.' },
                 { discipline: 'Física', unit: 1, eval1: 'A', eval2: 'A', finalGrade: 'D', situation: 'Aprovado', observation: 'Excelente participação em aula.' },
            ]
        }
        // ... add more students here
    ];

    // Basic user example (replace with Local Storage or Backend)
    let users = [
        { username: 'administrador', password: 'admsenac2024', role: 'admin', name: 'Administrador' }, // Admin credentials updated
        { username: 'profmath', password: 'passprof', role: 'professor', name: 'Prof. Matemática', disciplines: ['Matemática', 'Física'], classes: ['1A', '2B'] }, // Example professor assignments updated
         { username: 'coord', password: 'passcoord', role: 'coordenador', name: 'Coordenador Geral' }, // Plaintext password: INSECURE!
    ];

    let currentUser = null; // Currently logged in user

    // --- Basic Section Display Functions ---
    const loginContainer = document.getElementById('loginContainer');
    const appContainer = document.getElementById('appContainer');
    const studentManagementSection = document.getElementById('studentManagementSection');
    const manageUsersSection = document.getElementById('manageUsersSection');
    const professorSection = document.getElementById('professorSection');
    const userManagementSection = document.getElementById('userManagementSection');
    const sidebarHr = document.getElementById('sidebarHr');
    const professorWelcome = document.getElementById('professorWelcome');

    function showSection(sectionToShow) {
        studentManagementSection.classList.add('hidden');
        manageUsersSection.classList.add('hidden');
        professorSection.classList.add('hidden');
        // Add other sections here if any
        sectionToShow.classList.remove('hidden');
    }

    function showStudentManagementSection() {
        showSection(studentManagementSection);
        // Logic to populate the full student table for admin/coordinator
        renderStudentTable(students);
         // Logic to populate the student select for printing
         populateStudentPrintSelect();
         // Show/hide Add Student/Discipline based on role (already handled in login, but good to be explicit)
         if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'coordenador')) {
              document.getElementById('addStudentSection').classList.remove('hidden');
              document.getElementById('addDisciplineSection').classList.remove('hidden');
              // Populate student select for adding discipline
              populateStudentSelectForDiscipline();
         } else {
             document.getElementById('addStudentSection').classList.add('hidden');
             document.getElementById('addDisciplineSection').classList.add('hidden');
         }
    }

    function showManageUsersSection() {
        showSection(manageUsersSection);
        // Logic to populate the user management table
        renderUsersTable(users);
    }

    function showProfessorSection(user) {
        showSection(professorSection);
        professorWelcome.textContent = 'Olá, ' + user.name + '!';
         populateProfessorSelects(user); // Populate professor's dropdowns
         // Professor's student table will be loaded when discipline/class/unit are selected
         document.querySelector('#professorStudentTable tbody').innerHTML = ''; // Clear table initially
         document.getElementById('professorNoStudentsMessage').classList.remove('hidden'); // Show initial message
    }

    // Function to navigate back to the appropriate main section
    function goHome() {
        if (currentUser) {
            if (currentUser.role === 'admin' || currentUser.role === 'coordenador') {
                showStudentManagementSection(); // Go to student management for admin/coord
            } else if (currentUser.role === 'professor') {
                showProfessorSection(currentUser); // Go to professor section for professor
            }
        } else {
             // If somehow not logged in, go back to login (shouldn't happen if appContainer is visible)
             logout();
        }
    }


    function logout() {
        currentUser = null; // Clear logged in user in memory
        localStorage.removeItem('currentUser'); // Optional: clear from Local Storage as well
        appContainer.classList.add('hidden');
        loginContainer.classList.remove('hidden');
        document.getElementById('username').value = '';
        document.getElementById('password').value = '';
        document.getElementById('loginError').textContent = '';
        userManagementSection.classList.add('hidden'); // Hide user management menu
        sidebarHr.classList.add('hidden'); // Hide divider
        // Clear tables or interface states if necessary
        document.querySelector('#studentTable tbody').innerHTML = '';
        document.querySelector('#usersTable tbody').innerHTML = '';
        document.querySelector('#professorStudentTable tbody').innerHTML = '';
         document.getElementById('addStudentSection').classList.add('hidden');
         document.getElementById('addDisciplineSection').classList.add('hidden');
    }

    // --- Login Logic ---
    document.getElementById('loginButton').addEventListener('click', function() {
        const usernameInput = document.getElementById('username');
        const passwordInput = document.getElementById('password');
        const loginError = document.getElementById('loginError');

        const username = usernameInput.value;
        const password = passwordInput.value;

        loginError.textContent = ''; // Clear previous errors

        // Attempt to find the user
        let foundUser = users.find(user => user.username === username && user.password === password);

        if (foundUser) {
            currentUser = foundUser; // Set the logged in user
             // Optional: Save user to Local Storage (with security caveats)
             // localStorage.setItem('currentUser', JSON.stringify(currentUser));

            console.log('Login successful for:', currentUser.username);

            loginContainer.classList.add('hidden');
            appContainer.classList.remove('hidden');

            // Redireciona ou mostra a seção correta com base no papel
            if (currentUser.role === 'admin' || currentUser.role === 'coordenador') {
                showStudentManagementSection(); // Mostra a seção principal para admin/coord
                userManagementSection.classList.remove('hidden'); // Mostra o link de gerenciar usuários
                sidebarHr.classList.remove('hidden'); // Mostra o divisor

            } else if (currentUser.role === 'professor') {
                showProfessorSection(currentUser); // Mostra a seção do professor
                userManagementSection.classList.add('hidden'); // Esconde link de gerenciar usuários
                sidebarHr.classList.add('hidden'); // Esconde divisor
            }

        } else {
            // Login failed
            loginError.textContent = 'Usuário ou senha inválidos.';
            console.log('Login failed for:', username);
        }
    });

    // Check if already logged in on page load
     window.addEventListener('load', function() {
         // In a real application, you would check for a valid session token here
         // Using Local Storage for a simple example (INSEGURO for sensitive data)
         const savedUser = JSON.parse(localStorage.getItem('currentUser'));
         if (savedUser) {
              // Find the full user from saved data (ensures 'users' is populated)
              currentUser = users.find(user => user.username === savedUser.username && user.role === savedUser.role);
              if (currentUser) {
                 appContainer.classList.remove('hidden');
                 loginContainer.classList.add('hidden');

                 if (currentUser.role === 'admin' || currentUser.role === 'coordenador') {
                      showStudentManagementSection();
                      userManagementSection.classList.remove('hidden');
                      sidebarHr.classList.remove('hidden');

                 } else if (currentUser.role === 'professor') {
                     showProfessorSection(currentUser);
                      userManagementSection.classList.add('hidden');
                      sidebarHr.classList.add('hidden');
                 }
              } else {
                   // User saved in storage but not found in current data (e.g., data cleared)
                  logout(); // Force logout
              }
         } else {
              // Not logged in, show login screen
             loginContainer.classList.remove('hidden');
             appContainer.classList.add('hidden');
         }
     });


    // --- Table Rendering Functions (Basic) ---

    // Renders the full student table for Admin/Coordinator
    function renderStudentTable(studentsToRender) {
        const tableBody = document.querySelector('#studentTable tbody');
        tableBody.innerHTML = ''; // Clear the table body

        if (!studentsToRender || studentsToRender.length === 0) {
             // Optional: Show "Nenhum aluno encontrado" message
             return;
         }

        studentsToRender.forEach(student => {
            student.disciplines.forEach(discipline => {
                const row = tableBody.insertRow();

                row.insertCell().textContent = student.name;
                row.insertCell().textContent = student.course;
                row.insertCell().textContent = student.class;
                row.insertCell().textContent = student.unit; // Turno
                row.insertCell().textContent = discipline.discipline;
                row.insertCell().textContent = discipline.unit;

                // Editable cells for Evaluations and Final Grade
                const eval1Cell = row.insertCell();
                eval1Cell.classList.add('editable-cell');
                eval1Cell.dataset.studentId = student.id;
                eval1Cell.dataset.disciplineName = discipline.discipline;
                eval1Cell.dataset.unitNumber = discipline.unit;
                eval1Cell.dataset.field = 'eval1';
                eval1Cell.dataset.type = 'select'; // Indicate it should use a select
                eval1Cell.dataset.options = ',"A","PA","ND"'; // Options for select
                eval1Cell.innerHTML = `<span>${discipline.eval1 || ''}</span>`;

                const eval2Cell = row.insertCell();
                eval2Cell.classList.add('editable-cell');
                 eval2Cell.dataset.studentId = student.id;
                 eval2Cell.dataset.disciplineName = discipline.discipline;
                 eval2Cell.dataset.unitNumber = discipline.unit;
                 eval2Cell.dataset.field = 'eval2';
                 eval2Cell.dataset.type = 'select';
                 eval2Cell.dataset.options = ',"A","PA","ND"';
                eval2Cell.innerHTML = `<span>${discipline.eval2 || ''}</span>`;

                // Editable cell for Final Grade
                const finalGradeCell = row.insertCell();
                finalGradeCell.classList.add('editable-cell');
                 finalGradeCell.dataset.studentId = student.id;
                 finalGradeCell.dataset.disciplineName = discipline.discipline;
                 finalGradeCell.dataset.unitNumber = discipline.unit;
                 finalGradeCell.dataset.field = 'finalGrade';
                 finalGradeCell.dataset.type = 'select';
                 finalGradeCell.dataset.options = ',"D","ND"'; // Options for select
                finalGradeCell.innerHTML = `<span>${discipline.finalGrade || ''}</span>`;

                // Editable cell for Situation
                const situationCell = row.insertCell();
                situationCell.classList.add('editable-cell');
                 situationCell.dataset.studentId = student.id;
                 situationCell.dataset.disciplineName = discipline.discipline;
                 situationCell.dataset.unitNumber = discipline.unit;
                 situationCell.dataset.field = 'situation';
                 situationCell.dataset.type = 'select';
                 situationCell.dataset.options = ',"Aprovado","Reprovado","Pendente"'; // Options for select
                situationCell.innerHTML = `<span>${discipline.situation || ''}</span>`; // Use empty if null/undefined


                // Editable cell for Observations
                const observationCell = row.insertCell();
                observationCell.classList.add('editable-cell');
                 observationCell.dataset.studentId = student.id;
                 observationCell.dataset.disciplineName = discipline.discipline;
                 observationCell.dataset.unitNumber = discipline.unit;
                 observationCell.dataset.field = 'observation';
                 observationCell.dataset.type = 'text'; // Indicate it should use a text input
                observationCell.innerHTML = `<span>${discipline.observation || ''}</span>`; // Use empty if no observation

                const actionsCell = row.insertCell();
                // Add action buttons (Edit, Delete - logic needs to be implemented)
                 actionsCell.innerHTML = `
                     <button type="button" class="button" onclick="editStudentDiscipline('${student.id}', '${discipline.discipline}', ${discipline.unit})">Editar</button>
                     <button type="button" class="button delete-button" onclick="deleteStudentDiscipline('${student.id}', '${discipline.discipline}', ${discipline.unit})">Excluir</button>
                 `;
            });
        });
         attachEditableCellListeners('#studentTable'); // Add edit listeners
    }

     // Renders the table for the Professor section
    function renderProfessorTable(studentsToRender) {
        const tableBody = document.querySelector('#professorStudentTable tbody');
        tableBody.innerHTML = ''; // Clear the table body

        if (!studentsToRender || studentsToRender.length === 0) {
             document.getElementById('professorNoStudentsMessage').classList.remove('hidden');
             return;
         } else {
             document.getElementById('professorNoStudentsMessage').classList.add('hidden');
         }

         const selectedDiscipline = document.getElementById('professorDisciplineSelect').value;
         const selectedClass = document.getElementById('professorClassSelect').value;
         const selectedUnit = parseInt(document.getElementById('professorUnitSelect').value); // Convert to number

        studentsToRender.forEach(student => {
             // Find the specific discipline/unit data for this student
             const disciplineData = student.disciplines.find(d =>
                 d.discipline === selectedDiscipline && d.unit === selectedUnit
             );

            // Render the row only if there is data for the selected discipline/unit
             if (disciplineData) {
                 const row = tableBody.insertRow();

                 row.insertCell().textContent = student.name;
                 row.insertCell().textContent = student.course;
                 row.insertCell().textContent = student.unit; // Student's Turno

                 // Editable cells for Evaluations and Final Grade
                 const eval1Cell = row.insertCell();
                 eval1Cell.classList.add('editable-cell');
                 eval1Cell.dataset.studentId = student.id;
                 eval1Cell.dataset.disciplineName = disciplineData.discipline;
                 eval1Cell.dataset.unitNumber = disciplineData.unit;
                 eval1Cell.dataset.field = 'eval1';
                 eval1Cell.dataset.type = 'select';
                 eval1Cell.dataset.options = ',"A","PA","ND"';
                 eval1Cell.innerHTML = `<span>${disciplineData.eval1 || ''}</span>`; // Use empty if null/undefined

                 const eval2Cell = row.insertCell();
                 eval2Cell.classList.add('editable-cell');
                  eval2Cell.dataset.studentId = student.id;
                  eval2Cell.dataset.disciplineName = disciplineData.discipline;
                  eval2Cell.dataset.unitNumber = disciplineData.unit;
                  eval2Cell.dataset.field = 'eval2';
                  eval2Cell.dataset.type = 'select';
                  eval2Cell.dataset.options = ',"A","PA","ND"';
                 eval2Cell.innerHTML = `<span>${disciplineData.eval2 || ''}</span>`;

                 const finalGradeCell = row.insertCell();
                 finalGradeCell.classList.add('editable-cell');
                  finalGradeCell.dataset.studentId = student.id;
                  finalGradeCell.dataset.disciplineName = disciplineData.discipline;
                  finalGradeCell.dataset.unitNumber = disciplineData.unit;
                  finalGradeCell.dataset.field = 'finalGrade';
                  finalGradeCell.dataset.type = 'select';
                  finalGradeCell.dataset.options = ',"D","ND"';
                  finalGradeCell.innerHTML = `<span>${disciplineData.finalGrade || ''}</span>`;


                 // Editable cell for Situation (Professor view)
                 const situationCell = row.insertCell();
                 situationCell.classList.add('editable-cell');
                  situationCell.dataset.studentId = student.id;
                  situationCell.dataset.disciplineName = disciplineData.discipline;
                  situationCell.dataset.unitNumber = disciplineData.unit;
                  situationCell.dataset.field = 'situation';
                  situationCell.dataset.type = 'select';
                  situationCell.dataset.options = ',"Aprovado","Reprovado","Pendente"'; // Options for select
                 situationCell.innerHTML = `<span>${disciplineData.situation || ''}</span>`; // Use empty if null/undefined


                 // Editable cell for Observations
                 const observationCell = row.insertCell();
                 observationCell.classList.add('editable-cell');
                  observationCell.dataset.studentId = student.id;
                  observationCell.dataset.disciplineName = disciplineData.discipline;
                  observationCell.dataset.unitNumber = disciplineData.unit;
                  observationCell.dataset.field = 'observation';
                  observationCell.dataset.type = 'text';
                 observationCell.innerHTML = `<span>${disciplineData.observation || ''}</span>`; // Use empty if no observation

             }
        });
        attachEditableCellListeners('#professorStudentTable'); // Add edit listeners for professor table
    }


     // Renders the user table for Admin
     function renderUsersTable(usersToRender) {
         const tableBody = document.querySelector('#usersTable tbody');
         tableBody.innerHTML = ''; // Clear the table body
         const noUsersMessage = document.getElementById('noUsersMessage');

         // Filter out the main admin from the list
         const displayUsers = usersToRender.filter(user => user.username !== 'administrador'); // Updated admin username check

         if (!displayUsers || displayUsers.length === 0) {
             noUsersMessage.classList.remove('hidden');
              // Optional: Hide the table if no users
              document.getElementById('usersTable').classList.add('hidden');

         } else {
             noUsersMessage.classList.add('hidden');
              document.getElementById('usersTable').classList.remove('hidden');

             displayUsers.forEach(user => {
                 const row = tableBody.insertRow();

                 row.insertCell().textContent = user.name;
                 row.insertCell().textContent = user.username;
                 row.insertCell().textContent = user.role.charAt(0).toUpperCase() + user.role.slice(1); // Capitalize role

                 // Assigned Disciplines
                 const disciplinesCell = row.insertCell();
                 disciplinesCell.textContent = user.disciplines ? user.disciplines.join(', ') : '-';

                 // Assigned Classes
                 const classesCell = row.insertCell();
                 classesCell.textContent = user.classes ? user.classes.join(', ') : '-';

                 // Password (ATTENTION: INSECURE)
                 row.insertCell().textContent = user.password; // Insecure demonstration

                 const actionsCell = row.insertCell();
                  actionsCell.innerHTML = `
                      <button type="button" class="button" onclick="editUser('${user.username}')">Editar</button>
                      <button type="button" class="button delete-button" onclick="deleteUser('${user.username}')">Excluir</button>
                  `;
             });
         }
     }


     // --- Editable Cell Logic (Basic) ---
    function attachEditableCellListeners(tableSelector) {
        const table = document.querySelector(tableSelector);
        // Remove existing listeners to prevent duplicates
        table.querySelectorAll('.editable-cell').forEach(cell => {
             const newCell = cell.cloneNode(true); // Clone to remove all listeners
             cell.parentNode.replaceChild(newCell, cell);
        });

        // Add new listeners to the cloned cells
        table.querySelectorAll('.editable-cell').forEach(cell => {
            cell.addEventListener('click', activateEditableCell);
        });
    }

    function activateEditableCell(event) {
        const cell = event.target.closest('.editable-cell');
        if (!cell || cell.classList.contains('editing')) return; // Don't edit if already editing

        cell.classList.add('editing');
        const currentValue = cell.textContent.trim(); // Get current text value
        const studentId = cell.dataset.studentId;
        const disciplineName = cell.dataset.disciplineName;
        const unitNumber = parseInt(cell.dataset.unitNumber);
        const field = cell.dataset.field; // 'eval1', 'eval2', 'finalGrade', 'situation', 'observation'
        const inputType = cell.dataset.type; // 'text' or 'select'
        const options = cell.dataset.options ? cell.dataset.options.split(',') : []; // Options for select

        let inputElement;

        // Create the appropriate input element
        if (inputType === 'select') {
             inputElement = document.createElement('select');
             options.forEach(optionValue => {
                 const option = document.createElement('option');
                 option.value = optionValue;
                 // Display text for options
                 if (field === 'finalGrade') {
                     option.textContent = optionValue === 'D' ? 'Desenvolveu (D)' : (optionValue === 'ND' ? 'Não Desenvolveu (ND)' : (optionValue === '' ? ' - ' : optionValue));
                 } else if (field === 'situation') {
                      option.textContent = optionValue || (optionValue === '' ? ' - ' : optionValue);
                 }
                 else {
                     option.textContent = optionValue || (optionValue === '' ? ' - ' : optionValue);
                 }

                 // Select the current value
                 if (currentValue === optionValue || (currentValue === '-' && optionValue === '') || (field === 'finalGrade' && currentValue.includes(optionValue)) || (field === 'situation' && currentValue.includes(optionValue))) {
                     option.selected = true;
                 }
                 inputElement.appendChild(option);
             });
         } else if (inputType === 'text') {
            inputElement = document.createElement('input');
            inputElement.type = 'text';
            inputElement.value = currentValue;
        } else {
             // Unknown field type, not editable
             cell.classList.remove('editing');
             return;
         }


        // Replace cell content with the input element
        cell.innerHTML = '';
        cell.appendChild(inputElement);

        // Focus on the input element
        inputElement.focus();

        // Add listeners to save on blur or Enter key press
        inputElement.addEventListener('blur', saveEditableCell);
        inputElement.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                saveEditableCell(e);
            }
        });
    }

    function saveEditableCell(event) {
        const inputElement = event.target;
        const cell = inputElement.closest('.editable-cell');
        if (!cell || !cell.classList.contains('editing')) return; // Exit if not editing

        const newValue = inputElement.value;
        const studentId = cell.dataset.studentId;
        const disciplineName = cell.dataset.disciplineName;
        const unitNumber = parseInt(cell.dataset.unitNumber);
        const field = cell.dataset.field;

        // Find the student and discipline in the simulated data
        const student = students.find(s => s.id === studentId);
        if (student) {
            const discipline = student.disciplines.find(d =>
                d.discipline === disciplineName && d.unit === unitNumber
            );
            if (discipline) {
                // Update the value in the simulated data array
                discipline[field] = newValue;
                 // ATTENTION: In a real system, you would save this to Local Storage or backend here!
                 console.log(`Data updated: Student ${student.name}, ${discipline.discipline} U${discipline.unit}, Field ${field}, New Value: ${newValue}`);

                 // Optional: Recalculate situation after saving grades (requires logic)
                 // discipline.situation = calculateSituation(discipline.eval1, discipline.eval2, discipline.finalGrade);

                 // Update the cell display with the new value (using span again)
                 let displayValue = newValue || '';
                 if (field === 'finalGrade') {
                      displayValue = newValue === 'D' ? 'Desenvolveu (D)' : (newValue === 'ND' ? 'Não Desenvolveu (ND)' : ' - ');
                 } else if ((field === 'eval1' || field === 'eval2' || field === 'situation') && newValue === '') {
                     displayValue = ' - ';
                 } else {
                     displayValue = newValue;
                 }

                 cell.innerHTML = `<span>${displayValue}</span>`;


                 // If in the professor table, you might want to re-render just this row or the whole table
                 // to reflect the updated situation (if situation logic is complex)
                 // This basic implementation assumes situation is static or calculated elsewhere for now.
            }
        }

        cell.classList.remove('editing'); // Remove the editing class
    }


    // --- Professor Section Select Population and Table Loading ---
    function populateProfessorSelects(user) {
        const disciplineSelect = document.getElementById('professorDisciplineSelect');
        const classSelect = document.getElementById('professorClassSelect');
        // Unit is a fixed select (1, 2, 3)

        // Clear current selects
        disciplineSelect.innerHTML = '<option value="">Selecione a Disciplina</option>';
        classSelect.innerHTML = '<option value="">Selecione a Turma</option>';

        // Populate disciplines based on professor's assignments
        if (user && user.disciplines) {
            user.disciplines.forEach(discipline => {
                const option = document.createElement('option');
                option.value = discipline;
                option.textContent = discipline;
                disciplineSelect.appendChild(option);
            });
        }

        // Populate classes based on professor's assignments
        if (user && user.classes) {
            user.classes.forEach(className => {
                const option = document.createElement('option');
                option.value = className;
                option.textContent = className;
                classSelect.appendChild(option);
            });
        }

         // Add listeners to load the professor table when selects change
         disciplineSelect.addEventListener('change', loadProfessorTable);
         classSelect.addEventListener('change', loadProfessorTable);
         document.getElementById('professorUnitSelect').addEventListener('change', loadProfessorTable);
    }

     // Function to load the professor table based on selections
     function loadProfessorTable() {
         const selectedDiscipline = document.getElementById('professorDisciplineSelect').value;
         const selectedClass = document.getElementById('professorClassSelect').value;
         const selectedUnit = document.getElementById('professorUnitSelect').value;

         // Verifica se todos os selects estão selecionados
         if (selectedDiscipline && selectedClass && selectedUnit) {
             // Filtra os alunos que correspondem à turma selecionada
              const studentsInSelectedClass = students.filter(student =>
                  student.class === selectedClass
              );

             // Renderiza a tabela com os alunos da turma selecionada
             // A função renderProfessorTable já filtra as disciplinas/unidades dentro de cada aluno
             renderProfessorTable(studentsInSelectedClass);

         } else {
             // Limpa a tabela se a seleção não estiver completa
             document.querySelector('#professorStudentTable tbody').innerHTML = '';
             document.getElementById('professorNoStudentsMessage').classList.remove('hidden');
         }
     }

    // --- Basic Add Student/Discipline Logic ---
    function addStudent() {
        const studentNameInput = document.getElementById('studentName');
        const courseSelect = document.getElementById('course');
        const classSelect = document.getElementById('class');
        const unitSelect = document.getElementById('unit');

        const name = studentNameInput.value.trim();
        const course = courseSelect.value;
        const className = classSelect.value;
        const unit = unitSelect.value; // Turno

        if (!name || !course || !className || !unit) {
            alert('Por favor, preencha todos os campos do aluno.'); // Use um modal de mensagem em vez de alert em produção
            return;
        }

        // Gera um ID simples (para demonstração)
        const newStudentId = 's' + (students.length + 1);

        const newStudent = {
            id: newStudentId,
            name: name,
            course: course,
            class: className,
            unit: unit, // Turno
            disciplines: [] // Começa sem disciplinas
        };

        students.push(newStudent);
        console.log('Aluno adicionado:', newStudent);

        // ATENÇÃO: Em um sistema real, você salvaria 'students' no Local Storage ou backend aqui!

        // Limpa o formulário
        studentNameInput.value = '';
        courseSelect.value = '';
        classSelect.value = '';
        unitSelect.value = '';

        // Atualiza as tabelas e selects que mostram alunos
        renderStudentTable(students);
        populateStudentSelectForDiscipline();
        populateStudentPrintSelect();
         // Se o professor estiver na seção dele, re-renderizar se a nova turma/turno for a selecionada
         if (currentUser && currentUser.role === 'professor') {
             loadProfessorTable(); // Recarrega a tabela do professor
         }

        alert('Aluno adicionado com sucesso!'); // Use um modal de mensagem em produção
    }

    function addDiscipline() {
        const studentSelect = document.getElementById('studentSelect');
        const disciplineSelect = document.getElementById('disciplineSelect');
        const unitSelectDiscipline = document.getElementById('unitSelect'); // Unidade da Disciplina
        const evaluation1Select = document.getElementById('evaluation1');
        const evaluation2Select = document.getElementById('evaluation2');
        const finalGradeSelect = document.getElementById('finalGrade');
        const observationInput = document.getElementById('observationInput');

        const studentId = studentSelect.value;
        const disciplineName = disciplineSelect.value;
        const unitNumber = parseInt(unitSelectDiscipline.value); // Converte para número
        const eval1 = evaluation1Select.value;
        const eval2 = evaluation2Select.value;
        const finalGrade = finalGradeSelect.value;
        const observation = observationInput.value.trim();

        if (!studentId || !disciplineName || !unitNumber || !eval1 || !eval2 || !finalGrade) {
            alert('Por favor, preencha todos os campos da disciplina (exceto Observações).'); // Use um modal de mensagem em vez de alert em produção
            return;
        }

        const student = students.find(s => s.id === studentId);

        if (student) {
            // Verifica se a disciplina/unidade já existe para este aluno
            const existingDiscipline = student.disciplines.find(d =>
                d.discipline === disciplineName && d.unit === unitNumber
            );

            if (existingDiscipline) {
                alert(`A disciplina "${disciplineName}" para a Unidade ${unitNumber} já existe para este aluno.`); // Use um modal de mensagem
                return;
            }

            // Calcula a situação (exemplo básico)
             let situation = 'Pendente'; // Situação inicial
             if (finalGrade === 'D') {
                 situation = 'Aprovado';
             } else if (finalGrade === 'ND') {
                 situation = 'Reprovado';
             }
             // Lógica mais complexa pode envolver as avaliações também

            const newDiscipline = {
                discipline: disciplineName,
                unit: unitNumber,
                eval1: eval1,
                eval2: eval2,
                finalGrade: finalGrade,
                situation: situation, // Situação calculada
                observation: observation
            };

            student.disciplines.push(newDiscipline);
            console.log('Disciplina adicionada:', newDiscipline, 'para o aluno:', student.name);

            // ATENÇÃO: Em um sistema real, você salvaria 'students' no Local Storage ou backend aqui!

            // Limpa o formulário
            studentSelect.value = '';
            disciplineSelect.value = '';
            unitSelectDiscipline.value = '';
            evaluation1Select.value = '';
            evaluation2Select.value = '';
            finalGradeSelect.value = '';
            observationInput.value = '';

            // Atualiza as tabelas que mostram dados de alunos
            renderStudentTable(students);
             // Se o professor estiver na seção dele e a disciplina/turma/unidade corresponder, re-renderizar
             if (currentUser && currentUser.role === 'professor') {
                 loadProfessorTable(); // Recarrega a tabela do professor
             }


            alert('Disciplina adicionada com sucesso!'); // Use um modal de mensagem em produção

        } else {
            alert('Aluno não encontrado.'); // Use um modal de mensagem
        }
    }

    // Popula o select de alunos para adicionar disciplina
    function populateStudentSelectForDiscipline() {
        const studentSelect = document.getElementById('studentSelect');
        studentSelect.innerHTML = '<option value="">Selecione o Aluno</option>'; // Limpa e adiciona opção padrão

        students.forEach(student => {
            const option = document.createElement('option');
            option.value = student.id;
            option.textContent = student.name + ' (' + student.class + ' - ' + student.unit + ')'; // Nome (Turma - Turno)
            studentSelect.appendChild(option);
        });
    }

    // Popula o select de alunos para impressão
    function populateStudentPrintSelect() {
         const studentSelect = document.getElementById('studentSelectPrint');
         studentSelect.innerHTML = '<option value="">Selecione o Aluno</option>'; // Limpa e adiciona opção padrão

         students.forEach(student => {
             const option = document.createElement('option');
             option.value = student.id;
             option.textContent = student.name + ' (' + student.class + ' - ' + student.unit + ')'; // Nome (Turma - Turno)
             studentSelect.appendChild(option);
         });
     }


    // --- Basic Print Logic ---
    function printAllReports() {
        // This function simply triggers the browser's print dialog for the current page.
        // The @media print CSS controls what is visible and how it's formatted.
        alert('Preparando para imprimir o conteúdo visível na tela (conforme as configurações de impressão do seu navegador). Para boletins formatados, é necessária uma implementação mais complexa.'); // Use modal
        window.print();
    }

    function printStudentReport() {
         const studentId = document.getElementById('studentSelectPrint').value;
         const selectedUnits = Array.from(document.querySelectorAll('.unitCheckbox:checked')).map(cb => parseInt(cb.value));
         const reportType = document.querySelector('input[name="reportType"]:checked').value;

         if (!studentId) {
             alert('Por favor, selecione um aluno para imprimir.'); // Use modal
             return;
         }

         const student = students.find(s => s.id === studentId);

         if (!student) {
             alert('Aluno não encontrado para impressão.'); // Use modal
             return;
         }

         // --- Generate Bulletin HTML ---
         let bulletinHTML = `
             <div class="student-report">
                 <div class="bulletin-header">
                     <p class="line1"><strong>SENAC-PAULISTA</strong> - 2025</p>
                     <p class="line2">Boletim Escolar - MÉDIOTEC</p>
                     <p class="line3"><strong>Aluno:</strong> ${student.name} - <strong>Turma:</strong> ${student.class} - <strong>Turno:</strong> ${student.unit}</p>
                 </div>
                 <table class="bulletin-table">
                     <thead>
                         <tr>
                             <th>Disciplina</th>
                             <th>Unidade</th>
                             ${reportType === 'full' ? '<th>Avaliação 1</th><th>Avaliação 2</th>' : ''}
                             <th>Menção Final</th>
                             <th>Situação</th>
                             <th>Observações</th>
                         </tr>
                     </thead>
                     <tbody>
         `;

         // Filter disciplines based on selected units
         const disciplinesToPrint = student.disciplines.filter(d => selectedUnits.includes(d.unit));

         if (disciplinesToPrint.length === 0) {
             bulletinHTML += `<tr><td colspan="${reportType === 'full' ? 7 : 5}">Nenhuma disciplina encontrada para as unidades selecionadas.</td></tr>`;
         } else {
             disciplinesToPrint.forEach(discipline => {
                 bulletinHTML += `
                     <tr>
                         <td>${discipline.discipline}</td>
                         <td>${discipline.unit}</td>
                         ${reportType === 'full' ? `<td>${discipline.eval1 || ''}</td><td>${discipline.eval2 || ''}</td>` : ''}
                         <td>${discipline.finalGrade || ''}</td>
                         <td>${discipline.situation || ''}</td>
                         <td>${discipline.observation || ''}</td>
                     </tr>
                 `;
             });
         }


         bulletinHTML += `
                     </tbody>
                 </table>
             </div>
         `;
         // --- End Generate Bulletin HTML ---

         // --- Print the Generated HTML ---
         const printWindow = window.open('', '_blank');
         printWindow.document.open();
         printWindow.document.write(`
             <!DOCTYPE html>
             <html>
             <head>
                 <title>Boletim de ${student.name}</title>
                 <style>
                     /* Include relevant print styles here */
                     body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 1.5cm; font-size: 10pt; }
                     .student-report { page-break-inside: avoid; page-break-after: always; margin-bottom: 0; padding: 10px 0;}
                     .student-report:last-child { page-break-after: avoid; margin-bottom: 0; }
                     .bulletin-header { /* Moved styles here */
                         text-align: center;
                         margin-bottom: 20px; /* More space below the header block */
                         padding-bottom: 15px; /* More padding below the header content */
                         border-bottom: 2px solid #000; /* Thicker border */
                     }
                     .bulletin-header h2 { /* Removed this specific h2 style as we are using p with classes */
                         display: none; /* Hide the old h2 */
                     }
                      .bulletin-header p { /* Base style for paragraphs in header */
                          margin: 5px 0; /* More space between paragraphs */
                          font-size: 11pt; /* Slightly larger font for student info */
                          color: #333; /* Ensure dark color */
                      }
                      .bulletin-header p strong {
                          font-weight: bold;
                      }
                /* Specific styles for the consolidated header lines */
                .bulletin-header .line1 {
                    font-size: 18pt; /* Larger font for the main title line */
                    font-weight: bold;
                    margin-bottom: 8px; /* Space below line 1 */
                }
                 .bulletin-header .line2 {
                     font-size: 14pt; /* Slightly smaller for the secondary title */
                     margin-bottom: 8px; /* Space below line 2 */
                 }
                  .bulletin-header .line3 {
                      font-size: 11pt; /* Standard font for student info line */
                      margin-top: 8px; /* Add space above line 3 */
                      margin-bottom: 0; /* No margin below the last line of the header block */
                  }


                     .bulletin-table { width: 100%; border-collapse: collapse; margin-top: 15px; }
                     .bulletin-table th, .bulletin-table td { border: 1px solid #000; padding: 8px; text-align: center; font-size: 9pt; }
                     .bulletin-table th { background-color: #eee !important; color: #000 !important; font-weight: bold; }
                     .bulletin-table td:first-child { text-align: left; }
                     .bulletin-table td:last-child { text-align: left; } /* Align observations left */
                     @page { size: A4; margin: 1.5cm; }
                 </style>
             </head>
             <body>
                 ${bulletinHTML}
             </body>
             </html>
         `);
         printWindow.document.close();
         printWindow.print();
         // printWindow.close(); // Close after printing (might need a delay)
         // --- End Print Generated HTML ---
     }


    // --- Placeholder Functions (To be implemented) ---
    function showAddProfessorForm() { console.log('Mostrar formulário Adicionar Professor'); /* Implementar modal e lógica */
         // Exemplo básico de popular checkboxes (precisa de lista mestra de disciplinas/turmas)
         populateProfessorDisciplineCheckboxes(); // Populate discipline checkboxes
         populateProfessorClassCheckboxes(); // Populate class checkboxes
         document.getElementById('addProfessorModal').classList.remove('hidden');
     }
     function closeAddProfessorModal() { console.log('Fechar modal Adicionar Professor'); document.getElementById('addProfessorModal').classList.add('hidden'); }
     function saveProfessor() {
         console.log('Attempting to save Professor');
         const nameInput = document.getElementById('newProfessorNameInput');
         const usernameInput = document.getElementById('newProfessorUsernameInput');
         const passwordInput = document.getElementById('newProfessorPasswordInput');
         const disciplineCheckboxes = document.querySelectorAll('#professorDisciplinesCheckboxes input[type="checkbox"]:checked');
         const classCheckboxes = document.querySelectorAll('#professorClassesCheckboxes input[type="checkbox"]:checked');

         const name = nameInput.value.trim();
         const username = usernameInput.value.trim();
         const password = passwordInput.value; // Keep password as is for demo (INSECURE)
         const disciplines = Array.from(disciplineCheckboxes).map(cb => cb.value);
         const classes = Array.from(classCheckboxes).map(cb => cb.value);

         if (!name || !username || !password) {
             alert('Por favor, preencha Nome, Usuário e Senha para o professor.');
             return;
         }

         // Check if username already exists
         if (users.some(user => user.username === username)) {
             alert('Nome de usuário já existe. Por favor, escolha outro.');
             return;
         }

         const newProfessor = {
             username: username,
             password: password, // INSECURE: Storing plaintext password
             role: 'professor',
             name: name,
             disciplines: disciplines,
             classes: classes
         };

         users.push(newProfessor);
         console.log('Professor adicionado:', newProfessor);

         // ATENÇÃO: Em um sistema real, você salvaria 'users' no Local Storage ou backend aqui!

         // Clear the form
         nameInput.value = '';
         usernameInput.value = '';
         passwordInput.value = '';
         disciplineCheckboxes.forEach(cb => cb.checked = false);
         classCheckboxes.forEach(cb => cb.checked = false);


         closeAddProfessorModal(); // Close the modal
         renderUsersTable(users); // Update the user management table

         alert('Professor adicionado com sucesso!');
     }


     function showAddCoordenadorForm() { console.log('Mostrar formulário Adicionar Coordenador'); /* Implementar modal e lógica */ document.getElementById('addCoordinatorModal').classList.remove('hidden'); }
     function closeAddCoordenadorModal() { console.log('Fechar modal Adicionar Coordenador'); document.getElementById('addCoordinatorModal').classList.add('hidden'); }
     function saveCoordinator() {
         console.log('Attempting to save Coordinator');
         const nameInput = document.getElementById('newCoordinatorNameInput');
         const usernameInput = document.getElementById('newCoordinatorUsernameInput');
         const passwordInput = document.getElementById('newCoordinatorPasswordInput');

         const name = nameInput.value.trim();
         const username = usernameInput.value.trim();
         const password = passwordInput.value; // Keep password as is for demo (INSECURE)

         if (!name || !username || !password) {
             alert('Por favor, preencha Nome, Usuário e Senha para o coordenador.');
             return;
         }

         // Check if username already exists
         if (users.some(user => user.username === username)) {
             alert('Nome de usuário já existe. Por favor, escolha outro.');
             return;
         }

         const newCoordinator = {
             username: username,
             password: password, // INSECURE: Storing plaintext password
             role: 'coordenador',
             name: name,
             // Coordinators don't have specific discipline/class assignments in this model
             disciplines: [],
             classes: []
         };

         users.push(newCoordinator);
         console.log('Coordenador adicionado:', newCoordinator);

         // ATENÇÃO: Em um sistema real, você salvaria 'users' no Local Storage ou backend aqui!

         // Clear the form
         nameInput.value = '';
         usernameInput.value = '';
         passwordInput.value = '';

         closeAddCoordenadorModal(); // Close the modal
         renderUsersTable(users); // Update the user management table

         alert('Coordenador adicionado com sucesso!');
     }


     function showManageUsersSection() {
         showSection(manageUsersSection);
         renderUsersTable(users); // Renderiza a tabela de usuários
     }


     function editUser(username) { console.log('Editar Usuário:', username); /* Implementar modal e lógica de edição */ alert('Função Editar Usuário a ser implementada.'); }
     function deleteUser(username) { console.log('Excluir Usuário:', username); /* Implementar lógica de exclusão */ alert('Função Excluir Usuário a ser implementada.'); }
     function updateUser() { console.log('Atualizar Usuário'); /* Implementar salvar edições de usuário */ alert('Função Atualizar Usuário a ser implementada.'); closeEditUserModal(); renderUsersTable(users); /* Atualiza tabela de usuários */ }
     function closeEditUserModal() { console.log('Fechar modal Editar Usuário'); document.getElementById('editUserModal').classList.add('hidden'); }


     // Function to search students
     function searchStudent() {
         const searchTerm = document.getElementById('searchName').value.toLowerCase();
         console.log('Pesquisando por:', searchTerm);

         if (searchTerm.trim() === '') {
             // If search term is empty, show all students
             renderStudentTable(students);
         } else {
             // Filter students whose name includes the search term
             const filteredStudents = students.filter(student =>
                 student.name.toLowerCase().includes(searchTerm)
             );
             renderStudentTable(filteredStudents);
         }
     }


     function exportData() { console.log('Exportar dados'); /* Implementar lógica de exportação (JSON) */ alert('Função Exportar Dados a ser implementada.'); }
     function importData() { console.log('Importar dados'); /* Implementar lógica de importação (JSON) */ alert('Função Importar Dados a ser implementada.'); }

     function editStudentDiscipline(studentId, disciplineName, unitNumber) { console.log('Editar disciplina de aluno:', studentId, disciplineName, unitNumber); /* Opcional: se precisar de um modal de edição mais complexo */
         alert(`Função Editar Disciplina (para ${studentId}, ${disciplineName} U${unitNumber}) a ser implementada.`);
         // A edição básica já funciona clicando na célula, esta função seria para um modal mais completo.
     }
     function deleteStudentDiscipline(studentId, disciplineName, unitNumber) { console.log('Excluir disciplina de aluno:', studentId, disciplineName, unitNumber); /* Implementar lógica de exclusão */ alert('Função Excluir Disciplina a ser implementada.'); }
     // function calculateSituation(eval1, eval2, finalGrade) { /* Implementar lógica de cálculo de situação (Aprovado/Reprovado) */ return "Situação Calculada"; }


      // Lógica básica para o botão de importar arquivo (apenas exibe o nome do arquivo e habilita o botão)
      document.getElementById('importFile').addEventListener('change', function(event) {
          const fileNameSpan = document.getElementById('importFileName');
          const performImportButton = document.getElementById('performImportButton');
          const file = event.target.files[0];

          if (file) {
              fileNameSpan.textContent = file.name;
              performImportButton.disabled = false; // Habilita o botão de importar se um arquivo foi selecionado
          } else {
              fileNameSpan.textContent = 'Nenhum arquivo selecionado.';
              performImportButton.disabled = true; // Desabilita o botão se nenhum arquivo foi selecionado
          }
          document.getElementById('importStatus').textContent = ''; // Limpa status anterior
      });

      // Example list of all possible classes
      const allClasses = ["1A", "1B", "1C", "2A", "2B", "3A"]; // Updated list of classes

      // Basic example to populate discipline and class checkboxes in user modals
      function populateProfessorDisciplineCheckboxes() {
          const disciplines = ["Redação", "Gramática", "Educação Física", "Literatura", "Geografia", "Inglês", "História", "Projeto de Vida", "Artes", "Matemática", "Filosofia", "Física", "Química", "Biologia", "Formação Profissional", "Inovaê", "Sociologia"]; // Your master list
          const container = document.getElementById('professorDisciplinesCheckboxes');
          container.innerHTML = ''; // Clear the container
          disciplines.forEach(discipline => {
              const div = document.createElement('div');
              const checkbox = document.createElement('input');
              checkbox.type = 'checkbox';
              checkbox.value = discipline;
              checkbox.id = 'add-discipline-' + discipline.replace(/\s+/g, '-').toLowerCase(); // Generate a unique ID
              const label = document.createElement('label');
              label.htmlFor = checkbox.id;
              label.textContent = discipline;
              div.appendChild(checkbox);
              div.appendChild(label);
              container.appendChild(div);
          });
      }

      function populateProfessorClassCheckboxes() {
           const classes = allClasses; // Use the updated list of classes
           const container = document.getElementById('professorClassesCheckboxes');
           container.innerHTML = ''; // Clear the container
           classes.forEach(className => {
               const div = document.createElement('div');
               const checkbox = document.createElement('input');
               checkbox.type = 'checkbox';
               checkbox.value = className;
               checkbox.id = 'add-class-' + className.replace(/\s+/g, '-').toLowerCase(); // Generate a unique ID
               const label = document.createElement('label');
               label.htmlFor = checkbox.id;
               label.textContent = className;
               div.appendChild(checkbox);
               div.appendChild(label);
               container.appendChild(div);
           });
      }
       // Call these functions when opening the add professor modal
       // Example: showAddProfessorForm() { populateProfessorDisciplineCheckboxes(); populateProfessorClassCheckboxes(); document.getElementById('addProfessorModal').classList.remove('hidden'); }


       // Basic example to populate discipline and class checkboxes in EDIT user modals
       function populateEditProfessorDisciplineCheckboxes(assignedDisciplines = []) {
           const disciplines = ["Redação", "Gramática", "Educação Física", "Literatura", "Geografia", "Inglês", "História", "Projeto de Vida", "Artes", "Matemática", "Filosofia", "Física", "Química", "Biologia", "Formação Profissional", "Inovaê", "Sociologia"]; // Your master list
           const container = document.getElementById('editProfessorDisciplinesCheckboxes');
           container.innerHTML = ''; // Clear the container
           disciplines.forEach(discipline => {
               const div = document.createElement('div');
               const checkbox = document.createElement('input');
               checkbox.type = 'checkbox';
               checkbox.value = discipline;
               checkbox.id = 'edit-discipline-' + discipline.replace(/\s+/g, '-').toLowerCase(); // Generate a unique ID
               if (assignedDisciplines.includes(discipline)) {
                   checkbox.checked = true;
               }
               const label = document.createElement('label');
               label.htmlFor = checkbox.id;
               label.textContent = discipline;
               div.appendChild(checkbox);
               div.appendChild(label);
               container.appendChild(div);
           });
       }

       function populateEditProfessorClassCheckboxes(assignedClasses = []) {
            const classes = allClasses; // Use the updated list of classes
            const container = document.getElementById('editProfessorClassesCheckboxes');
            container.innerHTML = ''; // Clear the container
            classes.forEach(className => {
                const div = document.createElement('div');
                const checkbox = document.createElement('input');
                checkbox.type = 'checkbox';
                checkbox.value = className;
                checkbox.id = 'edit-class-' + className.replace(/\s+/g, '-').toLowerCase(); // Generate a unique ID
                 if (assignedClasses.includes(className)) {
                    checkbox.checked = true;
                }
                const label = document.createElement('label');
                label.htmlFor = checkbox.id;
                label.textContent = className;
                div.appendChild(checkbox);
                div.appendChild(label);
                container.appendChild(div);
            });
       }
        // Call these functions when opening the edit user modal, passing the user's current assignments
        // Example: editUser(username) { ... populateEditProfessorDisciplineCheckboxes(user.disciplines); populateEditProfessorClassCheckboxes(user.classes); ... }


</script>
</body>
</html>
