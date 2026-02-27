<!DOCTYPE html>
<html>
<head>
  <title>FO/CO Grade Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f4f4f4;
      padding: 20px;
    }

    img {
      max-width: 220px;
      margin-bottom: 15px;
    }

    h1 {
      margin-bottom: 20px;
    }

    #foList {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 5px;
      margin-bottom: 20px;
      max-width: 400px;
      margin-left: auto;
      margin-right: auto;
    }

    input[type="range"],
    input[type="number"] {
      width: 60%;
      margin: 10px 0;
    }

    button {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 15px;
    }

    #result {
      font-size: 22px;
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>

<body>

  <!-- Replace this with Loyola logo link -->
<img src="https://www.luc.edu/media/lucedu/universitymarketingcommunication/umcsiteimages/interiorimages-1000x560/standards-1000x560/download-logos-1000x560.jpg"
     alt="Loyola University Chicago Logo"
     style="max-width: 300px; display: block; margin: 0 auto;">

  <h1>FO / CO Grade Calculator</h1>

  <h3>FO Mastery (25 total)</h3>
  <div id="foList"></div>

  <h3>CO Points (0–15): <span id="coVal">0</span></h3>
  <input type="range" id="co" min="0" max="15" step="0.1" value="0"
         oninput="coVal.innerText = this.value">

  <h3>Course Activities %</h3>
  <input type="number" id="courseAct" min="0" max="100" placeholder="Enter %">

  <br>
  <button onclick="calculateGrade()">Calculate Grade</button>

  <div id="result"></div>

<script>
  const totalFOs = 25;
  const foContainer = document.getElementById("foList");

  // Generate FO checkboxes
  for (let i = 1; i <= totalFOs; i++) {
    const label = document.createElement("label");
    label.innerHTML = `
      <input type="checkbox" id="fo${i}">
      FO${i}
    `;
    foContainer.appendChild(label);
  }

  function calculateGrade() {

    // Count FOs
    let foCount = 0;
    for (let i = 1; i <= totalFOs; i++) {
      if (document.getElementById(`fo${i}`).checked) {
        foCount++;
      }
    }

    let coScore = parseFloat(document.getElementById("co").value) || 0;
    let actScore = parseFloat(document.getElementById("courseAct").value) || 0;

    // Convert to percentages
    let foPercent = (foCount / 25) * 100;
    let coPercent = (coScore / 15) * 100;

    // Weighted average
    let finalPercent =
      0.5 * foPercent +
      0.4 * coPercent +
      0.1 * actScore;

    finalPercent = finalPercent.toFixed(2);

    // Letter grade cutoffs
    let letter;

    if (finalPercent >= 90) letter = "A";
    else if (finalPercent >= 86) letter = "A-";
    else if (finalPercent >= 82) letter = "B+";
    else if (finalPercent >= 78) letter = "B";
    else if (finalPercent >= 74) letter = "B-";
    else if (finalPercent >= 70) letter = "C+";
    else if (finalPercent >= 66) letter = "C";
    else if (finalPercent >= 62) letter = "C-";
    else if (finalPercent >= 58) letter = "D";
    else letter = "F";

    document.getElementById("result").innerHTML =
      `Final %: ${finalPercent}% <br> Letter Grade: ${letter}`;
  }
</script>

</body>
</html>
