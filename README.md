# bsa-calculator
ROI calculator for BSA activities
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AML Automation Savings Calculator</title>
<style>
body{
    font-family: Arial, sans-serif;
    background: #f4f6f8;
    margin: 0;
    padding: 40px;
}

.container{
    max-width: 800px;
    margin: auto;
    background: white;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 2px 12px rgba(0,0,0,.12);
}

h1{
    color: #003366;
    text-align: center;
}

.assumptions{
    background: #eef6ff;
    padding: 15px;
    border-radius: 8px;
    margin-bottom: 25px;
}

label{
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

input{
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
}

button{
    width: 100%;
    margin-top: 20px;
    background: #0078d4;
    color: white;
    border: none;
    padding: 15px;
    font-size: 16px;
    border-radius: 6px;
    cursor: pointer;
}

button:hover{
    background: #005ea6;
}

.results{
    margin-top: 25px;
    padding: 20px;
    border-radius: 8px;
    background: #f8f9fa;
}

.result-line{
    margin-bottom: 12px;
    font-size: 18px;
}

.savings{
    font-size: 42px;
    font-weight: bold;
    color: #0a8f2b;
    text-align: center;
}

.hours{
    font-size: 28px;
    font-weight: bold;
    color: #003366;
    text-align: center;
}
</style>
</head>

<body>

<div class="container">

<h1>AML Automation Savings Calculator</h1>

<div class="assumptions">
    <strong>Industry Assumptions</strong>
    <ul>
        <li>CTR Filing Cost = $19</li>
        <li>SAR Filing Cost = $238</li>
        <li>CTR Preparation Time = 15 minutes</li>
        <li>SAR Preparation Time = 2.5 hours</li>
        <li>Automation Efficiency Gain = 60%</li>
    </ul>
</div>

<label>Monthly CTR Filings</label>
<input type="number" id="ctrs" value="50">

<label>Monthly SAR Filings</label>
<input type="number" id="sars" value="10">

<button onclick="calculateSavings()">
Calculate Savings
</button>

<div class="results">

<div class="result-line">
Annual CTR Cost:
<strong id="annualCtrCost">$0</strong>
</div>

<div class="result-line">
Annual SAR Cost:
<strong id="annualSarCost">$0</strong>
</div>

<div class="result-line">
Total Annual Manual Cost:
<strong id="annualManualCost">$0</strong>
</div>

<hr>

<div class="hours" id="hoursSaved">
0 Hours Saved Annually
</div>

<br>

<div class="savings" id="annualSavings">
$0
</div>

<p style="text-align:center;">
Estimated Annual Savings Opportunity
</p>

</div>

</div>

<script>
function money(value) {
    return value.toLocaleString('en-US', {
        style: 'currency',
        currency: 'USD',
        maximumFractionDigits: 0
    });
}

function calculateSavings() {

    const ctrs = Number(document.getElementById("ctrs").value);
    const sars = Number(document.getElementById("sars").value);

    const CTR_COST = 19;
    const SAR_COST = 238;

    const CTR_HOURS = 0.25;
    const SAR_HOURS = 2.5;

    const SAVINGS_FACTOR = 0.60;

    const annualCtrCost = ctrs * 12 * CTR_COST;
    const annualSarCost = sars * 12 * SAR_COST;

    const annualManualCost =
        annualCtrCost + annualSarCost;

    const annualHours =
        (ctrs * 12 * CTR_HOURS) +
        (sars * 12 * SAR_HOURS);

    const hoursSaved =
        annualHours * SAVINGS_FACTOR;

    const annualSavings =
        annualManualCost * SAVINGS_FACTOR;

    document.getElementById("annualCtrCost").innerText =
        money(annualCtrCost);

    document.getElementById("annualSarCost").innerText =
        money(annualSarCost);

    document.getElementById("annualManualCost").innerText =
        money(annualManualCost);

    document.getElementById("hoursSaved").innerText =
        Math.round(hoursSaved).toLocaleString() +
        " Hours Saved Annually";

    document.getElementById("annualSavings").innerText =
        money(Math.round(annualSavings));
}

calculateSavings();
</script>

</body>
</html>
