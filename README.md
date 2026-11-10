# Cell-potential-
To find the cell potential of the electrodes 

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Electrode Cell Potential Calculator</title>

<style>
* {
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #dbeafe, #e0e7ff);
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: 30px auto;
    background: white;
    padding: 25px;
    border-radius: 15px;
    box-shadow: 0 5px 20px #888;
}

h1 {
    text-align: center;
    color: #1e3a8a;
}

h3 {
    color: #2563eb;
}

label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

input {
    width: 100%;
    padding: 12px;
    margin-top: 6px;
    border: 1px solid #aaa;
    border-radius: 7px;
    font-size: 16px;
}

button {
    width: 100%;
    padding: 14px;
    margin-top: 20px;
    background: #2563eb;
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 17px;
    cursor: pointer;
}

button:hover {
    background: #1e40af;
}

.result {
    margin-top: 20px;
    padding: 18px;
    background: #eff6ff;
    border-radius: 10px;
    display: none;
    line-height: 1.8;
}

.formula {
    background: #f1f5f9;
    padding: 12px;
    border-radius: 8px;
    margin-top: 20px;
    text-align: center;
}
</style>
</head>

<body>

<div class="container">

<h1>⚡ Cell Potential Calculator</h1>

<p style="text-align:center">
Calculate the EMF and electrode cell potential easily.
</p>

<h3>1. Electrode Potentials</h3>

<label>Cathode Reduction Potential (V)</label>
<input type="number" id="cathode" step="any"
placeholder="Example: 0.34">

<label>Anode Reduction Potential (V)</label>
<input type="number" id="anode" step="any"
placeholder="Example: -0.76">

<h3>2. Nernst Equation Parameters</h3>

<label>Number of electrons transferred (n)</label>
<input type="number" id="electrons" value="2" min="1">

<label>Temperature (Kelvin)</label>
<input type="number" id="temperature" value="298.15" min="0.01">

<label>Reaction Quotient (Q)</label>
<input type="number" id="quotient" value="1" min="0.000000001">

<button onclick="calculate()">Calculate Cell Potential</button>

<div class="result" id="result"></div>

<div class="formula">
<h3>Formula Used</h3>

<p><b>Standard Cell Potential:</b></p>
E°cell = E°cathode - E°anode

<p><b>Nernst Equation:</b></p>
Ecell = E°cell - (RT/nF) ln Q

<p>R = 8.314 J mol⁻¹ K⁻¹</p>
<p>F = 96485 C mol⁻¹</p>
</div>

</div>

<script>

function calculate() {

    let cathode = parseFloat(
        document.getElementById("cathode").value
    );

    let anode = parseFloat(
        document.getElementById("anode").value
    );

    let n = parseFloat(
        document.getElementById("electrons").value
    );

    let T = parseFloat(
        document.getElementById("temperature").value
    );

    let Q = parseFloat(
        document.getElementById("quotient").value
    );

    let result = document.getElementById("result");

    if (
        !Number.isFinite(cathode) ||
        !Number.isFinite(anode) ||
        !Number.isFinite(n) ||
        !Number.isFinite(T) ||
        !Number.isFinite(Q) ||
        n <= 0 || T <= 0 || Q <= 0
    ) {
        alert("Please enter valid values in all fields.");
        return;
    }

    // Standard cell potential
    let E0 = cathode - anode;

    // Constants
    let R = 8.314;
    let F = 96485;

    // Nernst equation
    let E = E0 - ((R * T) / (n * F)) * Math.log(Q);

    let status = "";

    if (E > 0) {
        status = "Spontaneous reaction (Galvanic cell)";
    }
    else if (E < 0) {
        status = "Non-spontaneous reaction";
    }
    else {
        status = "Equilibrium condition";
    }

    result.style.display = "block";

    result.innerHTML = `
        <h3>Calculation Results</h3>

        <b>Standard Cell Potential:</b>
        ${E0.toFixed(4)} V
        <br>

        <b>Cell Potential (E):</b>
        ${E.toFixed(4)} V
        <br>

        <b>Reaction Quotient (Q):</b>
        ${Q}
        <br>

        <b>Temperature:</b>
        ${T} K
        <br>

        <b>Reaction Nature:</b>
        ${status}
    `;
}

</script>

</body>
</html>
