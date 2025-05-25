<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>CüzdanSende</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap');

        body {
            font-family: 'Montserrat', sans-serif;
            background: linear-gradient(135deg, #74ebd5 0%, #ACB6E5 100%);
            margin: 0;
            padding: 30px 20px;
            display: flex;
            justify-content: center;
        }
        .container {
            background-color: white;
            max-width: 500px;
            width: 100%;
            border-radius: 16px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.15);
            padding: 30px;
        }
        h1 {
            text-align: center;
            color: #34495e;
            margin-bottom: 25px;
            font-weight: 600;
            font-size: 2.5rem;
            letter-spacing: 1.5px;
        }
        input[type="text"], input[type="number"] {
            width: 100%;
            padding: 14px 18px;
            margin-bottom: 18px;
            border-radius: 10px;
            border: 1.8px solid #ddd;
            font-size: 1.1rem;
            transition: border-color 0.3s ease;
        }
        input[type="text"]:focus, input[type="number"]:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 8px #3498dbaa;
        }
        button {
            background-color: #3498db;
            color: white;
            width: 100%;
            padding: 15px;
            font-size: 1.2rem;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #2980b9;
        }
        h2 {
            margin-top: 30px;
            color: #2c3e50;
            font-weight: 600;
            text-align: center;
            font-size: 1.6rem;
        }
        #history {
            margin-top: 20px;
            max-height: 320px;
            overflow-y: auto;
        }
        .entry {
            background-color: #ecf0f1;
            border-radius: 12px;
            padding: 14px 18px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 1.1rem;
            font-weight: 500;
            color: #2c3e50;
            box-shadow: 0 1px 5px rgba(0,0,0,0.07);
        }
        .delete-btn {
            background-color: #e74c3c;
            border: none;
            color: white;
            padding: 6px 14px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s ease;
            font-size: 1rem;
        }
        .delete-btn:hover {
            background-color: #c0392b;
        }
        @media (max-width: 600px) {
            body {
                padding: 20px 10px;
            }
            .container {
                padding: 25px 20px;
            }
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>CüzdanSende</h1>
        <input type="text" id="description" placeholder="Açıklama (örn: Oyuncak)" />
        <input type="number" id="amount" placeholder="Ne kadar harcadın? (TL)" />
        <button onclick="addExpense()"💸 Harcama Ekle </button>
        <h2>Toplam Harcama: <span id="total">12.233.15</span> TL</h2>
        <div id="history"></div>
    </div>

    <script>
        let expenses = [];
        let total = 0;

        function renderExpenses() {
            const history = document.getElementById('history');
            history.innerHTML = '';
            total = 0;

            expenses.forEach((exp, index) => {
                total += exp.amount;

                const entry = document.createElement('div');
                entry.className = 'entry';

                const text = document.createElement('span');
                text.innerText = `${exp.desc}: ${exp.amount.toFixed(2)} TL`;

                const delBtn = document.createElement('button');
                delBtn.className = 'delete-btn';
                delBtn.innerText = 'Sil';
                delBtn.onclick = () => {
                    expenses.splice(index, 1);
                    renderExpenses();
                };

                entry.appendChild(text);
                entry.appendChild(delBtn);
                history.appendChild(entry);
            });

            document.getElementById('total').innerText = total.toFixed(2);
        }

        function addExpense() {
            const desc = document.getElementById('description').value.trim();
            const amount = parseFloat(document.getElementById('amount').value);

            if (desc && !isNaN(amount) && amount > 0) {
                expenses.push({ desc: desc, amount: amount });
                renderExpenses();

                document.getElementById('description').value = '';
                document.getElementById('amount').value = '';
            } else {
                alert("Lütfen geçerli bir açıklama ve pozitif miktar girin.");
            }
        }
    </script>
</body>
</html>
