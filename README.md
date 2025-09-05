<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ADTEMPCO MANABO COOPMART</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="integrity="sha512-9usAa10IRO0HhonpyAIVpjrylPvoDwiPUiKdWk5t3PyolY1cOd4DSE0Ga+ri4AuTroPR5aQvXU9xC6qOPnzFeg==" crossorigin="anonymous" referrerpolicy="no-referrer" rel="stylesheet">
    <style>
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        .section-header {
            background: linear-gradient(45deg, #1e3a8a, #3b82f6);
            color: white;
            border-radius: 8px 8px 0 0;
        }
        .btn-primary {
            background: linear-gradient(45deg, #10b981, #059669);
        }
        .btn-secondary {
            background: linear-gradient(45deg, #f59e0b, #d97706);
        }
        .btn-add-line {
            background: linear-gradient(45deg, #8b5cf6, #7c3aed);
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            padding: 12px;
            text-align: center;
            border-bottom: 1px solid #ddd;
        }
        th {
            background-color: #f9fafb;
            font-weight: 600;
        }
        .toggle-btn.active {
            background-color: #3b82f6;
            color: white;
        }
        .journal-line {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }
        .journal-line select, .journal-line input {
            flex: 1;
        }
        .remove-line {
            color: #dc2626;
            cursor: pointer;
        }
        .report-header {
            text-align: center;
            margin-bottom: 20px;
            font-weight: bold;
        }
        .signatories {
            display: flex;
            justify-content: space-around;
            margin-top: 40px;
        }
        .sub-ledger {
            margin-top: 20px;
            border-top: 2px solid #e5e7eb;
            padding-top: 10px;
        }
        .client-ledger {
            margin-bottom: 20px;
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 8px;
            background-color: #f9fafb;
        }
        .ledger-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .view-ledger-btn {
            background-color: #3b82f6;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .client-ledger-table {
            width: 100%;
            border-collapse: collapse;
        }
        .client-ledger-table th,
        .client-ledger-table td {
            padding: 8px;
            text-align: left;
        }
        .sub-ledger-hidden {
            display: none;
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        .modal.active {
            display: flex;
        }
        .modal-content {
            background: white;
            border-radius: 8px;
            max-width: 800px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            padding: 20px;
            position: relative;
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .modal-close {
            cursor: pointer;
            font-size: 1.5rem;
            font-weight: bold;
            border: none;
            background: none;
        }
        .client-link {
            cursor: pointer;
            color: #3b82f6;
            text-decoration: underline;
        }
        @media print {
            body * {
                visibility: hidden;
            }
            .printable, .printable * {
                visibility: visible;
            }
            .printable {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
            }
        }
    </style>
</head>
<body class="min-h-screen py-8">
    <div class="container mx-auto p-6 max-w-6xl">
        <header class="section-header p-4 mb-6">
            <h1 class="text-3xl font-bold flex items-center">
                <i class="fas fa-calculator mr-3"></i>
                ADTEMPCO MANABO COOPMART
            </h1>
            <p class="mt-2 opacity-90">Manage your finances with precision, style, and functionality.</p>
        </header>

        <!-- Navigation Tabs -->
        <div class="flex flex-wrap justify-center mb-6">
            <button id="accounts-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn active font-semibold" data-section="accounts">Manage Accounts</button>
            <button id="clients-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn font-semibold" data-section="clients">Clients Portal</button>
            <button id="journal-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn font-semibold" data-section="journal">General Journal</button>
            <button id="balance-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn font-semibold" data-section="balance">Balance Sheet</button>
            <button id="reports-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn font-semibold" data-section="reports">Monitoring & Reports</button>
            <button id="backup-btn" class="toggle-btn px-6 py-3 mx-2 bg-gray-200 rounded-full shadow-md toggle-btn font-semibold" data-section="backup">Backup & Restore</button>
        </div>

        <!-- Manage Accounts Section -->
        <div id="accounts-section" class="section bg-white p-6 rounded-lg shadow-lg">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800">Manage Accounts</h2>
            <form id="add-account-form" class="flex flex-wrap gap-4 mb-6">
                <input type="text" id="account-name" placeholder="Account Name" class="flex-1 p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                <select id="account-type" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="Asset">Asset</option>
                    <option value="Liability">Liability</option>
                    <option value="Equity">Equity</option>
                    <option value="Revenue">Revenue</option>
                    <option value="Expense">Expense</option>
                </select>
                <button type="submit" class="btn-primary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-plus mr-2"></i>Add Account
                </button>
            </form>
            <div id="accounts-list" class="overflow-x-auto">
                <table>
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Type</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="accounts-table-body"></tbody>
                </table>
            </div>
            <div id="no-accounts" class="text-center text-gray-500 mt-4 hidden">No accounts added yet.</div>
        </div>

        <!-- Clients Portal Section -->
        <div id="clients-section" class="section bg-white p-6 rounded-lg shadow-lg hidden">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800">Clients Portal</h2>
            <form id="add-client-form" class="flex flex-wrap gap-4 mb-6">
                <input type="text" id="client-name" placeholder="Client Name" class="flex-1 p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                <input type="text" id="client-contact" placeholder="Contact Info" class="flex-1 p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                <button type="submit" class="btn-primary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-plus mr-2"></i>Add Client
                </button>
            </form>
            <div id="clients-list" class="overflow-x-auto">
                <table>
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Contact</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="clients-table-body"></tbody>
                </table>
            </div>
            <div id="no-clients" class="text-center text-gray-500 mt-4 hidden">No clients added yet.</div>
        </div>

        <!-- Client Ledger Modal -->
        <div id="client-ledger-modal" class="modal" role="dialog" aria-modal="true" aria-labelledby="client-ledger-title">
            <div class="modal-content printable">
                <div class="modal-header">
                    <h2 id="client-ledger-title" class="text-xl font-bold">Subsidiary Ledger</h2>
                    <button class="modal-close" aria-label="Close">&times;</button>
                </div>
                <table class="client-ledger-table">
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Memo</th>
                            <th>Account Title</th>
                            <th>Debit</th>
                            <th>Credit</th>
                        </tr>
                    </thead>
                    <tbody id="client-ledger-body"></tbody>
                </table>
                <div class="mt-4 text-right">
                    <button id="print-client-ledger" class="btn-secondary px-4 py-2 rounded shadow hover:shadow-lg transition">
                        <i class="fas fa-print mr-2"></i>Print Ledger
                    </button>
                </div>
            </div>
        </div>

        <!-- General Journal Section -->
        <div id="journal-section" class="section bg-white p-6 rounded-lg shadow-lg hidden">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800">General Journal</h2>
            <form id="add-journal-form" class="mb-6">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-4">
                    <input type="date" id="entry-date" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    <input type="text" id="entry-memo" placeholder="Memo/Description" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                    <select id="debit-client" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="">Select Debit Client</option>
                        <!-- Populated by JS -->
                    </select>
                    <select id="credit-client" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="">Select Credit Client</option>
                        <!-- Populated by JS -->
                    </select>
                    <input type="text" id="posted-by" placeholder="Posted By (User)" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                </div>
                <div id="journal-lines" class="mb-4">
                    <div class="journal-line flex flex-col md:flex-row">
                        <select id="entry-account-1" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Select Account Title & No.</option>
                            <!-- Populated by JS -->
                        </select>
                        <select id="entry-debit-credit-1" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="debit">Debit</option>
                            <option value="credit">Credit</option>
                        </select>
                        <input type="number" step="0.01" id="entry-amount-1" placeholder="Amount" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                <div class="flex justify-between">
                    <button type="button" id="add-line-btn" class="btn-add-line text-white px-4 py-2 rounded-lg shadow hover:shadow-lg transition">
                        <i class="fas fa-plus mr-2"></i>Add Line
                    </button>
                    <button type="submit" class="btn-primary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                        <i class="fas fa-save mr-2"></i>Post Entry
                    </button>
                </div>
            </form>
            <div id="journal-list" class="overflow-x-auto">
                <table id="journal-table">
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Memo</th>
                            <th>Account Title</th>
                            <th>Debit/Credit</th>
                            <th>Amount</th>
                            <th>Client</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="journal-table-body"></tbody>
                </table>
            </div>
            <div id="no-journal" class="text-center text-gray-500 mt-4 hidden">No journal entries yet.</div>
        </div>

        <!-- Balance Sheet Section -->
        <div id="balance-section" class="section bg-white p-6 rounded-lg shadow-lg hidden">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800 text-center">Balance Sheet</h2>
            <div id="balance-list" class="overflow-x-auto">
                <table class="text-center">
                    <thead>
                        <tr>
                            <th>Account No.</th>
                            <th>Account Title</th>
                            <th>Type</th>
                            <th>Amount</th>
                        </tr>
                    </thead>
                    <tbody id="balance-table-body"></tbody>
                </table>
                <div id="no-balance" class="text-center text-gray-500 mt-4 hidden">No accounts to display balance.</div>
            </div>
            <div class="mt-6 text-center bg-gray-100 p-4 rounded">
                <p class="font-semibold text-blue-600">Total Assets: $<span id="total-assets">0.00</span></p>
                <p class="font-semibold text-red-600">Total Liabilities & Equity: $<span id="total-liabilities-equity">0.00</span></p>
                <p class="font-semibold text-purple-600">Net Income: $<span id="net-income">0.00</span></p>
            </div>
        </div>

        <!-- Monitoring & Reports Section -->
        <div id="reports-section" class="section bg-white p-6 rounded-lg shadow-lg hidden">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800">Monitoring & Reports</h2>
            <div class="report-section printable">
                <div class="report-header">
                    <h1 class="text-2xl font-bold">ADTEMPCO MANABO COOPMART</h1>
                    <p class="text-sm">SAN JUAN NORTE, MANABO, ABRA 2810</p>
                    <hr class="my-4">
                </div>
                <div class="mb-6">
                    <h3 class="text-xl font-semibold text-center mb-4">Balance Sheet Report</h3>
                    <table class="text-center">
                        <thead>
                            <tr>
                                <th>Account No.</th>
                                <th>Account Title</th>
                                <th>Type</th>
                                <th>Amount</th>
                            </tr>
                        </thead>
                        <tbody id="report-balance-body"></tbody>
                    </table>
                    <div class="text-center mt-4 bg-gray-100 p-4 rounded">
                        <p class="font-semibold text-blue-600">Total Assets: $<span id="report-total-assets">0.00</span></p>
                        <p class="font-semibold text-red-600">Total Liabilities & Equity: $<span id="report-total-liabilities-equity">0.00</span></p>
                        <p class="font-semibold text-purple-600">Net Income: $<span id="report-net-income">0.00</span></p>
                    </div>
                </div>
                <div class="mb-6">
                    <h3 class="text-xl font-semibold text-center mb-4">General Journal Report</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>Date</th>
                                <th>Memo</th>
                                <th>Account Title</th>
                                <th>Debit/Credit</th>
                                <th>Amount</th>
                                <th>Client</th>
                            </tr>
                        </thead>
                        <tbody id="report-journal-body"></tbody>
                    </table>
                </div>
                <div class="signatories">
                    <div class="text-center">
                        <p>Prepared By:</p>
                        <br><br>
                        ____________________<br>
                        Accountant
                    </div>
                    <div class="text-center">
                        <p>Approved By:</p>
                        <br><br>
                        ____________________<br>
                        Treasurer
                    </div>
                    <div class="text-center">
                        <p>Certified Correct:</p>
                        <br><br>
                        ____________________<br>
                        Chairman
                    </div>
                </div>
            </div>
            <div class="flex justify-center gap-4 mt-6">
                <button id="print-report-btn" class="btn-secondary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-print mr-2"></i>Print Report
                </button>
                <button id="export-report-btn" class="btn-primary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-download mr-2"></i>Export to PDF (Print)
                </button>
            </div>
        </div>

        <!-- Backup & Restore Section -->
        <div id="backup-section" class="section bg-white p-6 rounded-lg shadow-lg hidden">
            <h2 class="text-2xl font-semibold mb-4 text-gray-800">Backup & Restore Data</h2>
            <div class="flex flex-col sm:flex-row gap-4 mb-6">
                <button id="backup-download" class="btn-secondary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-download mr-2"></i>Backup Data
                </button>
                <input type="file" id="restore-file" accept=".json" class="hidden">
                <label for="restore-file" class="btn-secondary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition cursor-pointer">
                    <i class="fas fa-upload mr-2"></i>Choose Restore File
                </label>
                <button id="restore-data" class="btn-primary text-white px-6 py-3 rounded-lg shadow hover:shadow-lg transition">
                    <i class="fas fa-refresh mr-2"></i>Restore Data
                </button>
            </div>
            <p class="text-sm text-gray-600">Backup downloads all your data as a JSON file. Restore uploads a JSON file to replace current data. Be cautious with restores!</p>
        </div>

        <!-- Footer -->
        <footer class="mt-8 text-center text-white">
            <p class="text-sm opacity-75">Powered by Pure HTML, CSS & JavaScript | Data stored locally & professionally managed</p>
        </footer>
    </div>

    <script>
        // Data storage in localStorage
        let accounts = JSON.parse(localStorage.getItem('accounts')) || [];
        let clients = JSON.parse(localStorage.getItem('clients')) || [];
        let journalEntries = JSON.parse(localStorage.getItem('journalEntries')) || [];
        let lineCount = 1;

        // DOM elements
        const sections = document.querySelectorAll('.section');
        const toggleBtns = document.querySelectorAll('.toggle-btn');
        const accountsTableBody = document.getElementById('accounts-table-body');
        const noAccountsDiv = document.getElementById('no-accounts');
        const clientsTableBody = document.getElementById('clients-table-body');
        const noClientsDiv = document.getElementById('no-clients');
        const journalTableBody = document.getElementById('journal-table-body');
        const noJournalDiv = document.getElementById('no-journal');
        const balanceTableBody = document.getElementById('balance-table-body');
        const noBalanceDiv = document.getElementById('no-balance');
        const reportBalanceBody = document.getElementById('report-balance-body');
        const reportJournalBody = document.getElementById('report-journal-body');
        const addAccountForm = document.getElementById('add-account-form');
        const addClientForm = document.getElementById('add-client-form');
        const addJournalForm = document.getElementById('add-journal-form');
        const journalLines = document.getElementById('journal-lines');
        const addLineBtn = document.getElementById('add-line-btn');
        const backupDownloadBtn = document.getElementById('backup-download');
        const restoreFileInput = document.getElementById('restore-file');
        const restoreDataBtn = document.getElementById('restore-data');
        const printReportBtn = document.getElementById('print-report-btn');
        const exportReportBtn = document.getElementById('export-report-btn');
        const clientLedgerModal = document.getElementById('client-ledger-modal');
        const clientLedgerTitle = document.getElementById('client-ledger-title');
        const clientLedgerBody = document.getElementById('client-ledger-body');
        const printClientLedgerBtn = document.getElementById('print-client-ledger');

        // Initialize
        loadAccounts();
        loadClients();
        loadJournalEntries();
        updateBalanceSheet();
        updateAccountOptions();
        updateClientOptions();

        // Toggle sections
        toggleBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const targetSection = btn.dataset.section;
                sections.forEach(section => section.classList.add('hidden'));
                document.getElementById(targetSection + '-section').classList.remove('hidden');
                toggleBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
            });
        });

        // Add account
        addAccountForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const name = document.getElementById('account-name').value.trim();
            const type = document.getElementById('account-type').value;
            if (accounts.some(acc => acc.name.toLowerCase() === name.toLowerCase())) {
                alert('Account name already exists!');
                return;
            }
            const newAccount = { id: accounts.length + 1, name, type };
            accounts.push(newAccount);
            saveData();
            loadAccounts();
            updateAccountOptions();
            addAccountForm.reset();
        });

        // Add client
        addClientForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const name = document.getElementById('client-name').value.trim();
            const contact = document.getElementById('client-contact').value.trim();
            if (clients.some(client => client.name.toLowerCase() === name.toLowerCase())) {
                alert('Client name already exists!');
                return;
            }
            const newClient = { id: clients.length + 1, name, contact };
            clients.push(newClient);
            saveData();
            loadClients();
            updateClientOptions();
            addClientForm.reset();
        });

        // Add journal entry with lines
        addJournalForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const date = document.getElementById('entry-date').value;
            const memo = document.getElementById('entry-memo').value;
            const debitClientId = parseInt(document.getElementById('debit-client').value) || null;
            const creditClientId = parseInt(document.getElementById('credit-client').value) || null;
            const postedBy = document.getElementById('posted-by').value;
            const lines = [];
            for (let i = 1; i <= lineCount; i++) {
                const accountSelect = document.getElementById(`entry-account-${i}`);
                const typeSelect = document.getElementById(`entry-debit-credit-${i}`);
                const amountInput = document.getElementById(`entry-amount-${i}`);
                if (accountSelect && accountSelect.value && typeSelect && amountInput.value) {
                    const accountId = parseInt(accountSelect.value);
                    const debit = typeSelect.value === 'debit' ? parseFloat(amountInput.value) : 0;
                    const credit = typeSelect.value === 'credit' ? parseFloat(amountInput.value) : 0;
                    lines.push({ accountId, debit, credit });
                }
            }
            if (lines.length === 0) {
                alert('Add at least one line to the journal entry.');
                return;
            }
            const newEntry = {
                id: journalEntries.length + 1,
                date,
                memo,
                debitClientId,
                creditClientId,
                postedBy,
                lines
            };
            journalEntries.push(newEntry);
            saveData();
            loadClients();
            loadJournalEntries();
            updateBalanceSheet();
            addJournalForm.reset();
            resetJournalForm();
        });

        // Add line button
        addLineBtn.addEventListener('click', () => {
            lineCount++;
            const div = document.createElement('div');
            div.className = 'journal-line flex flex-col md:flex-row';
            div.innerHTML = `
                <select id="entry-account-${lineCount}" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="">Select Account Title & No.</option>
                    ${accounts.map(acc => `<option value="${acc.id}">${acc.name} (${acc.type}) #${acc.id}</option>`).join('')}
                </select>
                <select id="entry-debit-credit-${lineCount}" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="debit">Debit</option>
                    <option value="credit">Credit</option>
                </select>
                <input type="number" step="0.01" id="entry-amount-${lineCount}" placeholder="Amount" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                <i class="fas fa-times remove-line ml-2 mt-3 md:mt-0" onclick="removeLine(${lineCount})"></i>
            `;
            journalLines.appendChild(div);
        });

        // Remove line
        window.removeLine = function(num) {
            const div = document.getElementById(`entry-account-${num}`).parentElement;
            div.remove();
            lineCount--;
        };

        // Backup data
        backupDownloadBtn.addEventListener('click', () => {
            const data = JSON.stringify({ accounts, clients, journalEntries }, null, 2);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'accounting-backup.json';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            alert('Backup downloaded!');
        });

        // Restore data
        restoreDataBtn.addEventListener('click', () => {
            const file = restoreFileInput.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = () => {
                    try {
                        const data = JSON.parse(reader.result);
                        accounts = data.accounts || [];
                        clients = data.clients || [];
                        journalEntries = data.journalEntries || [];
                        saveData();
                        loadAccounts();
                        loadClients();
                        loadJournalEntries();
                        updateBalanceSheet();
                        updateAccountOptions();
                        updateClientOptions();
                        alert('Data restored!');
                    } catch (error) {
                        alert('Invalid file format!');
                    }
                };
                reader.readAsText(file);
            } else {
                alert('Please select a file.');
            }
        });

        // Print report
        printReportBtn.addEventListener('click', () => {
            window.print();
        });

        // Export report (use browser print for PDF export)
        exportReportBtn.addEventListener('click', () => {
            window.print();
        });

        // Modal close
        document.querySelector('.modal-close').addEventListener('click', () => {
            clientLedgerModal.classList.remove('active');
        });

        // Print client ledger
        printClientLedgerBtn.addEventListener('click', () => {
            window.print();
        });

        // Functions
        function saveData() {
            localStorage.setItem('accounts', JSON.stringify(accounts));
            localStorage.setItem('clients', JSON.stringify(clients));
            localStorage.setItem('journalEntries', JSON.stringify(journalEntries));
        }

        function loadAccounts() {
            accountsTableBody.innerHTML = '';
            if (accounts.length === 0) {
                noAccountsDiv.classList.remove('hidden');
            } else {
                noAccountsDiv.classList.add('hidden');
                accounts.forEach(account => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${account.id}</td>
                        <td>${account.name}</td>
                        <td>${account.type}</td>
                        <td><button class="text-red-500 hover:text-red-700" onclick="deleteAccount(${account.id})"><i class="fas fa-trash"></i> Delete</button></td>
                    `;
                    accountsTableBody.appendChild(row);
                });
            }
        }

        function loadClients() {
            clientsTableBody.innerHTML = '';
            if (clients.length === 0) {
                noClientsDiv.classList.remove('hidden');
            } else {
                noClientsDiv.classList.add('hidden');
                clients.forEach(client => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${client.id}</td>
                        <td class="client-link" onclick="showClientLedger(${client.id})">${client.name}</td>
                        <td>${client.contact}</td>
                        <td><button class="text-red-500 hover:text-red-700" onclick="deleteClient(${client.id})"><i class="fas fa-trash"></i> Delete</button></td>
                    `;
                    clientsTableBody.appendChild(row);
                });
            }
        }

        function loadJournalEntries() {
            journalTableBody.innerHTML = '';
            if (journalEntries.length === 0) {
                noJournalDiv.classList.remove('hidden');
            } else {
                noJournalDiv.classList.add('hidden');
                journalEntries.forEach(entry => {
                    entry.lines.forEach((line, index) => {
                        const account = accounts.find(acc => acc.id === line.accountId);
                        const accountTitle = account ? `${account.name} (#${account.id})` : 'Unknown';
                        const dc = line.debit > 0 ? 'Debit' : 'Credit';
                        const amount = (line.debit > 0 ? line.debit : line.credit).toFixed(2);
                        const client = line.debit > 0 ? (clients.find(c => c.id === entry.debitClientId) ? clients.find(c => c.id === entry.debitClientId).name : 'N/A') : (clients.find(c => c.id === entry.creditClientId) ? clients.find(c => c.id === entry.creditClientId).name : 'N/A');
                        const row = document.createElement('tr');
                        if (index === 0) {
                            row.innerHTML = `
                                <td>${entry.date}</td>
                                <td>${entry.memo}</td>
                                <td>${accountTitle}</td>
                                <td>${dc}</td>
                                <td>$${amount}</td>
                                <td>${client}</td>
                                <td rowspan="${entry.lines.length}"><button class="text-red-500 hover:text-red-700" onclick="deleteJournalEntry(${entry.id})"><i class="fas fa-trash"></i> Delete</button></td>
                            `;
                        } else {
                            row.innerHTML = `
                                <td></td>
                                <td></td>
                                <td>${accountTitle}</td>
                                <td>${dc}</td>
                                <td>$${amount}</td>
                                <td>${client}</td>
                                <td></td>
                            `;
                        }
                        journalTableBody.appendChild(row);
                    });
                });
            }
        }

        function updateAccountOptions() {
            for (let i = 1; i <= lineCount; i++) {
                const select = document.getElementById(`entry-account-${i}`);
                if (select) {
                    select.innerHTML = '<option value="">Select Account Title & No.</option>';
                    accounts.forEach(acc => {
                        const option = document.createElement('option');
                        option.value = acc.id;
                        option.textContent = `${acc.name} (${acc.type}) #${acc.id}`;
                        select.appendChild(option);
                    });
                }
            }
        }

        function updateClientOptions() {
            const debitSelect = document.getElementById('debit-client');
            const creditSelect = document.getElementById('credit-client');
            const clientOptions = '<option value="">Select Client</option>' + clients.map(c => `<option value="${c.id}">${c.name}</option>`).join('');
            debitSelect.innerHTML = clientOptions;
            creditSelect.innerHTML = clientOptions;
        }

        function resetJournalForm() {
            journalLines.innerHTML = `
                <div class="journal-line flex flex-col md:flex-row">
                    <select id="entry-account-1" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="">Select Account Title & No.</option>
                        ${accounts.map(acc => `<option value="${acc.id}">${acc.name} (${acc.type}) #${acc.id}</option>`).join('')}
                    </select>
                    <select id="entry-debit-credit-1" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="debit">Debit</option>
                        <option value="credit">Credit</option>
                    </select>
                    <input type="number" step="0.01" id="entry-amount-1" placeholder="Amount" class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
            `;
            lineCount = 1;
            document.getElementById('entry-date').value = '';
            document.getElementById('entry-memo').value = '';
            updateClientOptions();
            document.getElementById('debit-client').selectedIndex = 0;
            document.getElementById('credit-client').selectedIndex = 0;
            document.getElementById('posted-by').value = '';
        }

        function updateBalanceSheet() {
            balanceTableBody.innerHTML = '';
            reportBalanceBody.innerHTML = '';
            if (accounts.length === 0) {
                noBalanceDiv.classList.remove('hidden');
            } else {
                noBalanceDiv.classList.add('hidden');
                let totalAssets = 0;
                let totalLiabilitiesEquity = 0;
                let totalRevenue = 0;
                let totalExpense = 0;
                accounts.forEach(account => {
                    const balance = journalEntries.reduce((sum, entry) => {
                        return entry.lines.reduce((subSum, line) => {
                            if (line.accountId === account.id) {
                                if (account.type === 'Asset' || account.type === 'Expense') return subSum + line.debit - line.credit;
                                else return subSum + line.credit - line.debit;
                            }
                            return subSum;
                        }, sum);
                    }, 0);
                    const row = document.createElement('tr');
                    row.innerHTML = `<td>${account.id}</td><td>${account.name}</td><td>${account.type}</td><td>$${balance.toFixed(2)}</td>`;
                    balanceTableBody.appendChild(row);
                    reportBalanceBody.appendChild(row.cloneNode(true));
                    if (account.type === 'Asset') totalAssets += balance;
                    else if (account.type === 'Liability' || account.type === 'Equity') totalLiabilitiesEquity += balance;
                    else if (account.type === 'Revenue') totalRevenue += balance;
                    else if (account.type === 'Expense') totalExpense += balance;
                });
                document.getElementById('total-assets').textContent = totalAssets.toFixed(2);
                document.getElementById('total-liabilities-equity').textContent = totalLiabilitiesEquity.toFixed(2);
                document.getElementById('net-income').textContent = (totalRevenue - totalExpense).toFixed(2);
                document.getElementById('report-total-assets').textContent = totalAssets.toFixed(2);
                document.getElementById('report-total-liabilities-equity').textContent = totalLiabilitiesEquity.toFixed(2);
                document.getElementById('report-net-income').textContent = (totalRevenue - totalExpense).toFixed(2);
            }
        }

        // Show client ledger modal
        window.showClientLedger = function(clientId) {
            const client = clients.find(c => c.id === clientId);
            if (!client) return;
            clientLedgerTitle.textContent = `Subsidiary Ledger for ${client.name}`;
            clientLedgerBody.innerHTML = '';
            journalEntries.forEach(entry => {
                if (entry.debitClientId === clientId || entry.creditClientId === clientId) {
                    entry.lines.forEach((line, index) => {
                        if ((line.debit > 0 && entry.debitClientId === clientId) || (line.credit > 0 && entry.creditClientId === clientId)) {
                            const account = accounts.find(acc => acc.id === line.accountId);
                            const accountTitle = account ? `${account.name} (#${account.id})` : 'Unknown';
                            const debit = line.debit > 0 ? `$${line.debit.toFixed(2)}` : '';
                            const credit = line.credit > 0 ? `$${line.credit.toFixed(2)}` : '';
                            const row = document.createElement('tr');
                            if (index === 0) {
                                row.innerHTML = `
                                    <td>${entry.date}</td>
                                    <td>${entry.memo}</td>
                                    <td>${accountTitle}</td>
                                    <td>${debit}</td>
                                    <td>${credit}</td>
                                `;
                            } else {
                                row.innerHTML = `
                                    <td></td>
                                    <td></td>
                                    <td>${accountTitle}</td>
                                    <td>${debit}</td>
                                    <td>${credit}</td>
                                `;
                            }
                            clientLedgerBody.appendChild(row);
                        }
                    });
                }
            });
            clientLedgerModal.classList.add('active');
        };

        // Delete functions
        window.deleteAccount = function(id) {
            if (confirm('Are you sure you want to delete this account? This may affect journal entries.')) {
                accounts = accounts.filter(acc => acc.id !== id);
                journalEntries.forEach(entry => entry.lines = entry.lines.filter(line => line.accountId !== id));
                saveData();
                loadAccounts();
                loadClients();
                loadJournalEntries();
                updateBalanceSheet();
                updateAccountOptions();
            }
        };

        window.deleteClient = function(id) {
            if (confirm('Are you sure you want to delete this client? This may affect journal entries.')) {
                clients = clients.filter(client => client.id !== id);
                journalEntries.forEach(entry => {
                    if (entry.debitClientId === id) entry.debitClientId = null;
                    if (entry.creditClientId === id) entry.creditClientId = null;
                });
                saveData();
                loadClients();
                loadJournalEntries();
                updateClientOptions();
            }
        };

        window.deleteJournalEntry = function(id) {
            journalEntries = journalEntries.filter(entry => entry.id !== id);
            saveData();
            loadClients();
            loadJournalEntries();
            updateBalanceSheet();
        };
    </script>
</body>
</html>
</content>
</create_file>
</think>
</content>
</create_file>
