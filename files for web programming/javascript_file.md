// --- Navigation Logic ---
document.addEventListener('DOMContentLoaded', () => {
    const navItems = document.querySelectorAll('#main-nav li');
    const viewSections = document.querySelectorAll('.view-section');
    const pageTitle = document.getElementById('page-title');

    navItems.forEach(item => {
        item.addEventListener('click', () => {
            // Remove active from all nav
            navItems.forEach(nav => nav.classList.remove('active'));
            // Add active to clicked nav
            item.classList.add('active');

            // Set Page Title
            pageTitle.innerText = item.getAttribute('data-title');

            // Switch Views
            const targetViewId = item.getAttribute('data-view');
            viewSections.forEach(section => {
                if (section.id === targetViewId) {
                    section.classList.add('active');
                } else {
                    section.classList.remove('active');
                }
            });
        });
    });
    
    // Initial UI Setup
    updateUI();
});

// --- Reusable Toast Notification ---
function showToast(message) {
    const toast = document.getElementById('toast');
    toast.innerText = message;
    toast.classList.add('show');
    setTimeout(() => {
        toast.classList.remove('show');
    }, 3000);
}

// --- Login Logic ---
function handleLogin(e) {
    e.preventDefault();
    const password = document.getElementById('login-password').value;
    
    if (password === '1234') {
        const loginScreen = document.getElementById('login-screen');
        const dashScreen = document.getElementById('dashboard-screen');
        
        // Add exit animation to login
        loginScreen.classList.add('animate-out');
        
        // Wait for animation to finish
        setTimeout(() => {
            loginScreen.style.display = 'none';
            loginScreen.classList.remove('animate-out'); // Reset
            
            // Show dashboard with entry animation
            dashScreen.style.display = 'flex';
            dashScreen.classList.add('animate-in');
            
            // Cleanup animation class after it finishes
            setTimeout(() => dashScreen.classList.remove('animate-in'), 500);
            
            showToast('Login Successful!');
            e.target.reset(); // clear the form
        }, 500); // 500ms matches the CSS animation duration
    } else {
        showToast('Invalid Password! Try 1234');
    }
}

// --- Profile Update Logic ---
function handleProfileUpdate(e) {
    e.preventDefault();
    
    // Get Name
    const newName = document.getElementById('prof-fullname').value;
    
    // Update Sidebar Name
    document.getElementById('sidebar-user-name').innerText = newName;
    
    // Show Toast
    showToast('Profile Updated Successfully!');
}

// --- State Management ---
let appState = {
    budget: 0,
    expenses: [] // Array of { id, name, amount, category, date }
};

let expenseChartInstance = null; // To hold the Chart.js instance

// --- Core Functions (Input, Process) ---

// 1. Set Budget
function handleSetBudget(e) {
    e.preventDefault();
    const input = document.getElementById('budget-input');
    const amount = parseFloat(input.value);
    
    if (amount > 0) {
        appState.budget = amount;
        input.value = ''; // clear input
        updateUI();
    }
}

// 2. Add Expense
function handleAddExpense(e) {
    e.preventDefault();
    const nameInput = document.getElementById('exp-name');
    const amountInput = document.getElementById('exp-amount');
    const catInput = document.getElementById('exp-category');

    const expense = {
        id: Date.now().toString(),
        name: nameInput.value,
        amount: parseFloat(amountInput.value),
        category: catInput.value,
        date: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', hour: '2-digit', minute:'2-digit' })
    };

    if (expense.amount > 0) {
        appState.expenses.push(expense);
        // Clear inputs
        nameInput.value = '';
        amountInput.value = '';
        catInput.value = '';
        
        updateUI();
    }
}

// 4. Calculate Total Expenses
function calculateTotalExpenses() {
    return appState.expenses.reduce((total, exp) => total + exp.amount, 0);
}

// 5. Calculate Remaining Budget
function calculateRemainingBudget(totalExpenses) {
    return appState.budget - totalExpenses;
}

// 6. Identify Largest Expense
function getLargestExpense() {
    if (appState.expenses.length === 0) return null;
    return appState.expenses.reduce((max, exp) => (exp.amount > max.amount ? exp : max), appState.expenses[0]);
}

// 7. Log out / Exit (Reset State)
function logoutAndReset() {
    // Clear State
    appState = {
        budget: 0,
        expenses: []
    };
    updateUI();
    
    // Clear all input forms so the next session starts fresh
    document.getElementById('budget-form').reset();
    document.getElementById('expense-form').reset();
    
    const loginScreen = document.getElementById('login-screen');
    const dashScreen = document.getElementById('dashboard-screen');
    
    // Animate dashboard out
    dashScreen.classList.add('animate-out');
    
    setTimeout(() => {
        dashScreen.style.display = 'none';
        dashScreen.classList.remove('animate-out');
        
        // Animate login screen in
        loginScreen.style.display = 'flex';
        loginScreen.classList.add('animate-in');
        
        // Ensure login password field is cleared out
        document.getElementById('login-form').reset();
        
        setTimeout(() => loginScreen.classList.remove('animate-in'), 500);
        
        showToast("Logged out successfully.");
    }, 500);
}

// --- Export Functions ---

function exportToCSV() {
    if (appState.expenses.length === 0) {
        showToast("No expenses to export!");
        return;
    }

    // Define headers and map data
    const headers = ['Date', 'Expense Name', 'Category', 'Amount'];
    const rows = appState.expenses.map(exp => [
        `"${exp.date}"`, 
        `"${exp.name}"`, 
        `"${exp.category}"`, 
        exp.amount
    ]);

    // Construct CSV string
    const csvContent = [
        headers.join(','),
        ...rows.map(e => e.join(','))
    ].join('\n');

    // Trigger Download
    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");
    link.setAttribute("href", url);
    link.setAttribute("download", "Expense_Report.csv");
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    
    showToast("CSV Exported Successfully!");
}

function exportToPDF() {
    if (appState.expenses.length === 0) {
        showToast("No expenses to export!");
        return;
    }

    // Initialize jsPDF
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    // Add Report Title
    doc.setFontSize(18);
    doc.text("Personal Expense Report", 14, 22);
    
    // Add Budget Summary
    doc.setFontSize(11);
    doc.setTextColor(100);
    const totalExp = calculateTotalExpenses();
    doc.text(`Total Budget: $${appState.budget.toFixed(2)}`, 14, 32);
    doc.text(`Total Expenses: $${totalExp.toFixed(2)}`, 14, 38);
    doc.text(`Remaining Budget: $${calculateRemainingBudget(totalExp).toFixed(2)}`, 14, 44);

    // Generate Table Data
    const tableColumn = ["Date", "Expense Name", "Category", "Amount ($)"];
    const tableRows = appState.expenses.map(exp => [
        exp.date,
        exp.name,
        exp.category,
        exp.amount.toFixed(2)
    ]);

    // AutoTable Plugin
    doc.autoTable({
        head: [tableColumn],
        body: tableRows,
        startY: 50,
        theme: 'striped',
        headStyles: { fillColor: [55, 66, 250] }, // Matches neon-blue theme
        styles: { font: 'helvetica' }
    });

    // Save the PDF
    doc.save('Expense_Report.pdf');
    showToast("PDF Exported Successfully!");
}

// --- UI Rendering (Output) ---

function updateUI() {
    // Calculate metrics
    const totalExp = calculateTotalExpenses();
    const remaining = calculateRemainingBudget(totalExp);
    const largestExp = getLargestExpense();

    // Format Currency
    const formatMoney = (num) => '$' + num.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });

    // Update Metrics Cards
    document.getElementById('ui-budget').innerText = formatMoney(appState.budget);
    document.getElementById('ui-total-expense').innerText = formatMoney(totalExp);
    
    const remainingEl = document.getElementById('ui-remaining');
    remainingEl.innerText = formatMoney(remaining);
    // Change color to red if remaining is negative (over budget)
    if (remaining < 0) {
        remainingEl.classList.remove('neon-green');
        remainingEl.classList.add('neon-red');
    } else {
        remainingEl.classList.add('neon-green');
        remainingEl.classList.remove('neon-red');
    }

    if (largestExp) {
        document.getElementById('ui-largest').innerText = `${formatMoney(largestExp.amount)} (${largestExp.name})`;
    } else {
        document.getElementById('ui-largest').innerText = "$0.00";
    }

    // 3. Render Recorded Expenses List
    renderExpenseList();

    // Update Chart
    renderChart();
}

function renderExpenseList() {
    const container = document.getElementById('expense-list-container');
    container.innerHTML = ''; // Clear current

    if (appState.expenses.length === 0) {
        container.innerHTML = '<div class="empty-state">No expenses recorded yet.</div>';
        return;
    }

    // Sort newest first
    const sortedExpenses = [...appState.expenses].reverse();

    sortedExpenses.forEach(exp => {
        // Determine icon based on category
        let icon = '📦';
        if (exp.category === 'Housing') icon = '🏠';
        else if (exp.category === 'Food') icon = '🍔';
        else if (exp.category === 'Transport') icon = '🚗';
        else if (exp.category === 'Utilities') icon = '⚡';
        else if (exp.category === 'Entertainment') icon = '🎮';

        const itemHtml = `
            <div class="transaction-item">
                <div class="tx-left">
                    <div class="tx-icon">${icon}</div>
                    <div class="tx-info">
                        <span class="tx-name">${exp.name}</span>
                        <span class="tx-category">${exp.category} • ${exp.date}</span>
                    </div>
                </div>
                <span class="tx-amount neon-red">-$${exp.amount.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
            </div>
        `;
        container.insertAdjacentHTML('beforeend', itemHtml);
    });
}

function renderChart() {
    const ctx = document.getElementById('expenseChart').getContext('2d');
    
    // Aggregate data by category
    const categoryTotals = {};
    appState.expenses.forEach(exp => {
        const cat = exp.category.split(' ')[0]; // Remove emoji if it was passed
        categoryTotals[cat] = (categoryTotals[cat] || 0) + exp.amount;
    });

    const labels = Object.keys(categoryTotals);
    const data = Object.values(categoryTotals);

    // Destroy existing chart to prevent overlap bugs
    if (expenseChartInstance) {
        expenseChartInstance.destroy();
    }

    if (data.length === 0) {
        // Show empty doughnut if no data
        expenseChartInstance = new Chart(ctx, {
            type: 'doughnut',
            data: {
                labels: ['No Data'],
                datasets: [{ data: [1], backgroundColor: ['rgba(255,255,255,0.1)'], borderWidth: 0 }]
            },
            options: { cutout: '80%', plugins: { tooltip: { enabled: false }, legend: {display: false} } }
        });
        return;
    }

    Chart.defaults.color = '#a4b0be';
    Chart.defaults.font.family = "'Inter', sans-serif";

    expenseChartInstance = new Chart(ctx, {
        type: 'doughnut',
        data: {
            labels: labels,
            datasets: [{
                data: data,
                backgroundColor: [
                    '#ff4757', // Red
                    '#3742fa', // Blue
                    '#ff9f43', // Orange
                    '#2ed573', // Green
                    '#a55eea', // Purple
                    '#48dbfb'  // Light Blue
                ],
                borderWidth: 0,
                hoverOffset: 5
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            cutout: '75%',
            plugins: {
                legend: {
                    position: 'bottom',
                    labels: { usePointStyle: true, padding: 15, font: { size: 11 } }
                },
                tooltip: {
                    backgroundColor: 'rgba(30, 27, 46, 0.9)',
                    callbacks: {
                        label: function(context) {
                            return ' $' + context.parsed.toLocaleString('en-US', {minimumFractionDigits: 2});
                        }
                    }
                }
            }
        }
    });
}

// Initialize empty state on load
document.addEventListener('DOMContentLoaded', updateUI);