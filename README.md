<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Use our free online EMI calculator to calculate your multiple loan EMIs with detailed breakdown and user feedback options." />
  <meta name="keywords" content="EMI Calculator, Loan Calculator, Multiple EMI, Finance Tools, Loan Management" />
  <meta name="author" content="Your Name" />
  <title>EMI Calculator - Free Online Loan EMI Tool</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f9f9f9;
    }
    header, footer {
      background-color: #004080;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    main {
      padding: 1rem;
      max-width: 900px;
      margin: auto;
    }
    .emi-section {
      background: #fff;
      padding: 1rem;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      margin-bottom: 2rem;
    }
    .emi-inputs, .feedback-form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    label {
      font-weight: bold;
    }
    input, textarea {
      padding: 0.5rem;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      background: #004080;
      color: white;
      border: none;
      padding: 0.75rem;
      border-radius: 5px;
      cursor: pointer;
    }
    .results {
      margin-top: 1rem;
      font-weight: bold;
    }
    .adsense {
      margin: 2rem 0;
      text-align: center;
    }
    .adsense-block {
      margin: 1rem 0;
      padding: 1rem;
      background-color: #eef0f1;
      border: 1px dashed #ccc;
      text-align: center;
    }
    @media (max-width: 600px) {
      .emi-inputs, .feedback-form {
        flex-direction: column;
      }
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 1rem;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 8px;
      text-align: center;
    }
    th {
      background-color: #f0f0f0;
    }
  </style>
</head>
<body>
  <header>
    <h1>EMI Calculator</h1>
    <p>Calculate EMIs for multiple loans easily and accurately.</p>
  </header>

  <main>
    <section class="adsense-block">
      <!-- Google AdSense Ad Unit Placeholder (Top) -->
      <ins class="adsbygoogle"
           style="display:block"
           data-ad-client="ca-pub-XXXXXXXXXXXXXX"
           data-ad-slot="1234567890"
           data-ad-format="auto"
           data-full-width-responsive="true"></ins>
      <script>
        (adsbygoogle = window.adsbygoogle || []).push({});
      </script>
    </section>

    <section class="emi-section">
      <h2>Loan EMI Calculator</h2>
      <form id="emiForm" class="emi-inputs">
        <label for="amount">Loan Amount (₹):</label>
        <input type="number" id="amount" min="0" required />

        <label for="interest">Annual Interest Rate (%):</label>
        <input type="number" id="interest" min="0" required />

        <label for="tenure">Tenure (months):</label>
        <input type="number" id="tenure" min="1" required />

        <button type="submit">Calculate EMI</button>
      </form>
      <div id="result" class="results"></div>
    </section>

    <section class="adsense-block">
      <!-- Google AdSense Ad Unit Placeholder (Middle) -->
      <ins class="adsbygoogle"
           style="display:block"
           data-ad-client="ca-pub-XXXXXXXXXXXXXX"
           data-ad-slot="2345678901"
           data-ad-format="auto"
           data-full-width-responsive="true"></ins>
      <script>
        (adsbygoogle = window.adsbygoogle || []).push({});
      </script>
    </section>

    <section class="emi-section">
      <h2>Share Your Feedback</h2>
      <form class="feedback-form">
        <label for="feedback">Your Opinion:</label>
        <textarea id="feedback" rows="5" placeholder="Let us know your thoughts..."></textarea>
        <button type="button" onclick="submitFeedback()">Submit Feedback</button>
        <div id="feedback-message"></div>
      </form>
    </section>

    <section class="adsense-block">
      <!-- Google AdSense Ad Unit Placeholder (Bottom) -->
      <ins class="adsbygoogle"
           style="display:block"
           data-ad-client="ca-pub-XXXXXXXXXXXXXX"
           data-ad-slot="3456789012"
           data-ad-format="auto"
           data-full-width-responsive="true"></ins>
      <script>
        (adsbygoogle = window.adsbygoogle || []).push({});
      </script>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 EMI Calculator. All rights reserved.</p>
  </footer>

  <script>
    document.getElementById('emiForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const amount = parseFloat(document.getElementById('amount').value);
      const interest = parseFloat(document.getElementById('interest').value);
      const tenure = parseInt(document.getElementById('tenure').value);

      if (amount <= 0 || interest < 0 || tenure <= 0) {
        document.getElementById('result').innerHTML = "<p style='color:red;'>Please enter valid positive values for all fields.</p>";
        return;
      }

      const monthlyInterest = interest / (12 * 100);
      const emi = (amount * monthlyInterest * Math.pow(1 + monthlyInterest, tenure)) /
                  (Math.pow(1 + monthlyInterest, tenure) - 1);

      let remainingPrincipal = amount;
      let totalInterest = 0;
      let amortization = `
        <h3>EMI Breakdown</h3>
        <p><strong>Monthly EMI:</strong> ₹${emi.toFixed(2)}</p>
        <table>
          <thead>
            <tr>
              <th>Month</th>
              <th>Principal Paid (₹)</th>
              <th>Interest Paid (₹)</th>
              <th>Remaining Balance (₹)</th>
            </tr>
          </thead>
          <tbody>
      `;

      for (let month = 1; month <= tenure; month++) {
        const interestPaid = remainingPrincipal * monthlyInterest;
        const principalPaid = emi - interestPaid;
        remainingPrincipal -= principalPaid;
        totalInterest += interestPaid;

        amortization += `
          <tr>
            <td>${month}</td>
            <td>${principalPaid.toFixed(2)}</td>
            <td>${interestPaid.toFixed(2)}</td>
            <td>${remainingPrincipal > 0 ? remainingPrincipal.toFixed(2) : '0.00'}</td>
          </tr>
        `;
      }

      amortization += `
          </tbody>
        </table>
        <p><strong>Total Interest Paid:</strong> ₹${totalInterest.toFixed(2)}</p>
        <p><strong>Total Amount Paid:</strong> ₹${(emi * tenure).toFixed(2)}</p>
      `;

      document.getElementById('result').innerHTML = amortization;
    });

    function submitFeedback() {
      const feedback = document.getElementById('feedback').value;
      if (feedback.trim()) {
        document.getElementById('feedback-message').innerText = "Thank you for your feedback!";
        document.getElementById('feedback').value = '';
      } else {
        document.getElementById('feedback-message').innerText = "Please enter your feedback before submitting.";
      }
    }
  </script>
  <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
</body>
</html>
