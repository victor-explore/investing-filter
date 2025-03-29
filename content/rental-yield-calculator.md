---
title: Rental Yield Calculator
date:
draft: false
description:
showToc: false
math: true
---

<div class="calculator-section">
  <div class="calculator-intro">
  </div>

  <div id="calculator" class="calculator-container">
    <div class="calculator-row">
      <label for="monthlyRent">Monthly Rent (₹):</label>
      <input type="number" id="monthlyRent" value="2000" min="0"> <!-- Input field for monthly rent with minimum value of 0 -->
    </div>
    <div class="calculator-row">
      <label for="propertyValue">Property Value (₹):</label>
      <input type="number" id="propertyValue" value="400000" min="1"> <!-- Input field for property value with minimum value of 1 -->
    </div>
    <div class="calculator-row">
      <button onclick="calculateYield()">Calculate Yield</button> <!-- Button to trigger calculation -->
    </div>
    <div class="calculator-result">
      <div class="result-card">
        <h3>Annual Rental Income</h3>
        <p class="result-value">₹<span id="annualIncome">24000.00</span></p>
      </div>
      <div class="result-card">
        <h3>Gross Rental Yield</h3>
        <p class="result-value"><span id="rentalYield">6.00</span>%</p>
      </div>
    </div>
  </div>

</div>

<style>
.calculator-section {
  max-width: 800px;
  margin: 0 auto;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Modern, readable font */
}

.calculator-intro {
  margin-bottom: 25px;
  text-align: center;
  color: #333;
  line-height: 1.6;
}

.calculator-container {
  background-color: #f8f9fa;
  border-radius: 12px;
  padding: 30px;
  margin: 20px auto;
  max-width: 600px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
  text-align: center;
}

.calculator-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  align-items: center;
}

.calculator-row label {
  flex-basis: 40%;
  font-weight: 600;
  text-align: left;
  color: #444;
}

.calculator-row input {
  flex-basis: 55%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 16px;
  transition: border-color 0.3s ease; /* Smooth transition for focus effect */
}

.calculator-row input:focus {
  border-color: #0066cc;
  outline: none;
  box-shadow: 0 0 0 2px rgba(0, 102, 204, 0.2); /* Subtle focus indicator */
}

.calculator-row button {
  width: 100%;
  padding: 14px;
  background-color: #0066cc;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  transition: background-color 0.3s ease; /* Smooth hover transition */
}

.calculator-row button:hover {
  background-color: #0052a3;
}

.calculator-result {
  margin-top: 30px;
  padding-top: 20px;
  border-top: 1px solid #ddd;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.result-card {
  background-color: white;
  border-radius: 8px;
  padding: 15px;
  margin: 10px;
  min-width: 200px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05); /* Very subtle shadow */
}

.result-card h3 {
  margin-top: 0;
  color: #555;
  font-size: 16px;
  font-weight: 600;
}

.result-value {
  font-size: 24px;
  font-weight: 700;
  color: #0066cc;
  margin: 10px 0 0 0;
}

.calculator-explanation {
  margin-top: 40px;
  padding: 25px;
  background-color: #f0f7ff;
  border-radius: 12px;
  color: #333;
  line-height: 1.6;
}

.calculator-explanation h3 {
  color: #0066cc;
  margin-top: 0;
}

.formula {
  background-color: white;
  padding: 15px;
  border-radius: 8px;
  margin: 20px 0;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .calculator-row {
    flex-direction: column;
    align-items: stretch;
  }
  
  .calculator-row label {
    margin-bottom: 8px;
    text-align: left;
  }
  
  .calculator-row input {
    width: 100%;
  }
  
  .result-card {
    width: 100%;
    margin: 10px 0;
  }
}
</style>

<script>
/**
 * Calculates the rental yield based on user inputs
 * This function is called when the Calculate button is clicked
 */
function calculateYield() {
  // Get input values
  const monthlyRent = parseFloat(document.getElementById('monthlyRent').value) || 0; // Get monthly rent value
  const propertyValue = parseFloat(document.getElementById('propertyValue').value) || 1; // Get property value, default to 1 to avoid division by zero
  
  // Calculate annual income
  const annualIncome = monthlyRent * 12; // Calculate annual rental income by multiplying monthly rent by 12
  
  // Calculate yield
  const yield = (annualIncome / propertyValue) * 100; // Calculate rental yield percentage
  
  // Format the results with thousands separators
  const formattedAnnualIncome = annualIncome.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
  
  // Update results in the DOM
  document.getElementById('annualIncome').textContent = formattedAnnualIncome; // Display formatted annual income
  document.getElementById('rentalYield').textContent = yield.toFixed(2); // Display rental yield with 2 decimal places
  
  // Add animation effect to results
  animateResults();
}

/**
 * Adds a subtle animation to the result values when updated
 */
function animateResults() {
  const resultElements = document.querySelectorAll('.result-value');
  
  resultElements.forEach(element => {
    // Add and remove a class to trigger CSS animation
    element.classList.add('updated');
    setTimeout(() => {
      element.classList.remove('updated');
    }, 500);
  });
}

// Calculate on page load to initialize the calculator
document.addEventListener('DOMContentLoaded', function() {
  calculateYield();
  
  // Add input event listeners for real-time calculation
  document.getElementById('monthlyRent').addEventListener('input', calculateYield);
  document.getElementById('propertyValue').addEventListener('input', calculateYield);
});
</script>
