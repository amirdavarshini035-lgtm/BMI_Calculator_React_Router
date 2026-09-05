# Ex06 BMI Calculator
## Date: 01.09.2026

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
## javascripts:
```
import { useState } from "react";
import "./App.css";

function App() {
  const [height, setHeight] = useState("");
  const [weight, setWeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    const heightInMeters = Number(height) / 100;
    const weightInKg = Number(weight);

    if (
      heightInMeters <= 0 ||
      weightInKg <= 0 ||
      height === "" ||
      weight === ""
    ) {
      setBmi(null);
      setCategory("");
      alert("Please enter a valid height and weight.");
      return;
    }

    const calculatedBMI = weightInKg / (heightInMeters * heightInMeters);

    setBmi(calculatedBMI.toFixed(2));

    if (calculatedBMI < 18.5) {
      setCategory("Underweight");
    } else if (calculatedBMI < 25) {
      setCategory("Normal Weight");
    } else if (calculatedBMI < 30) {
      setCategory("Overweight");
    } else {
      setCategory("Obese");
    }
  };

  const resetCalculator = () => {
    setHeight("");
    setWeight("");
    setBmi(null);
    setCategory("");
  };

  return (
    <div className="page">
      <header className="header">
        <h1>BMI Calculator</h1>
        <p>Check your Body Mass Index quickly and easily</p>
      </header>

      <main className="container">
        <section className="calculator-card">
          <div className="card-title">
            <h2>Calculate Your BMI</h2>
            <p>Enter your height and weight below</p>
          </div>

          <div className="input-group">
            <label htmlFor="height">Height</label>

            <div className="input-wrapper">
              <input
                id="height"
                type="number"
                placeholder="Enter height"
                value={height}
                onChange={(e) => setHeight(e.target.value)}
              />
              <span>cm</span>
            </div>
          </div>

          <div className="input-group">
            <label htmlFor="weight">Weight</label>

            <div className="input-wrapper">
              <input
                id="weight"
                type="number"
                placeholder="Enter weight"
                value={weight}
                onChange={(e) => setWeight(e.target.value)}
              />
              <span>kg</span>
            </div>
          </div>

          <div className="button-group">
            <button className="calculate-btn" onClick={calculateBMI}>
              Calculate BMI
            </button>

            <button className="reset-btn" onClick={resetCalculator}>
              Reset
            </button>
          </div>

          {bmi && (
            <div className="result">
              <h3>Your BMI</h3>

              <div className="bmi-value">{bmi}</div>

              <div className="category">
                {category}
              </div>

              <p className="result-message">
                Your BMI category is <strong>{category}</strong>.
              </p>
            </div>
          )}
        </section>

        <section className="info-card">
          <h2>BMI Categories</h2>

          <div className="category-list">
            <div className="category-row">
              <span>Below 18.5</span>
              <strong>Underweight</strong>
            </div>

            <div className="category-row">
              <span>18.5 – 24.9</span>
              <strong>Normal Weight</strong>
            </div>

            <div className="category-row">
              <span>25 – 29.9</span>
              <strong>Overweight</strong>
            </div>

            <div className="category-row">
              <span>30 and above</span>
              <strong>Obese</strong>
            </div>
          </div>

          <div className="formula">
            <h3>BMI Formula</h3>
            <p>
              BMI = Weight (kg) ÷ Height² (m)
            </p>
          </div>
        </section>
      </main>

      <footer className="footer">
        <p>
          Designed by <strong>SHARMILA</strong>
        </p>
        <p>
          Register Number: <strong>212225040404</strong>
        </p>
        <p className="copyright">
          © 2026 BMI Calculator | React Application
        </p>
      </footer>
    </div>
  );
}

export default App;
```
## css:
```
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  background: #f4f7fb;
  color: #1f2937;
}

.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Header */

.header {
  background: #2563eb;
  color: white;
  text-align: center;
  padding: 45px 20px;
}

.header h1 {
  font-size: 42px;
  margin-bottom: 10px;
}

.header p {
  font-size: 17px;
  opacity: 0.9;
}

/* Main */

.container {
  width: 90%;
  max-width: 1000px;
  margin: 45px auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
}

/* Cards */

.calculator-card,
.info-card {
  background: white;
  border-radius: 18px;
  padding: 32px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
}

.card-title {
  text-align: center;
  margin-bottom: 30px;
}

.card-title h2,
.info-card h2 {
  font-size: 26px;
  margin-bottom: 8px;
}

.card-title p {
  color: #6b7280;
}

/* Input */

.input-group {
  margin-bottom: 22px;
}

.input-group label {
  display: block;
  font-weight: bold;
  margin-bottom: 8px;
}

.input-wrapper {
  display: flex;
  border: 2px solid #dbe3ef;
  border-radius: 10px;
  overflow: hidden;
  transition: 0.3s;
}

.input-wrapper:focus-within {
  border-color: #2563eb;
}

.input-wrapper input {
  width: 100%;
  border: none;
  outline: none;
  padding: 14px;
  font-size: 16px;
}

.input-wrapper span {
  background: #eef4ff;
  color: #2563eb;
  padding: 14px;
  font-weight: bold;
}

/* Buttons */

.button-group {
  display: flex;
  gap: 12px;
  margin-top: 25px;
}

button {
  border: none;
  padding: 14px;
  border-radius: 10px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

.calculate-btn {
  flex: 1;
  background: #2563eb;
  color: white;
}

.calculate-btn:hover {
  background: #1d4ed8;
}

.reset-btn {
  padding-left: 25px;
  padding-right: 25px;
  background: #e5e7eb;
  color: #374151;
}

.reset-btn:hover {
  background: #d1d5db;
}

/* Result */

.result {
  margin-top: 30px;
  padding: 25px;
  text-align: center;
  border-radius: 15px;
  background: #eff6ff;
  border: 2px solid #bfdbfe;
}

.result h3 {
  font-size: 18px;
  margin-bottom: 8px;
}

.bmi-value {
  font-size: 48px;
  font-weight: bold;
  color: #2563eb;
  margin: 5px 0;
}

.category {
  display: inline-block;
  background: #2563eb;
  color: white;
  padding: 8px 18px;
  border-radius: 20px;
  font-weight: bold;
  margin: 8px 0;
}

.result-message {
  margin-top: 10px;
  color: #4b5563;
}

/* BMI Information */

.info-card h2 {
  margin-bottom: 25px;
}

.category-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.category-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  background: #f8fafc;
  border-radius: 10px;
  border-left: 4px solid #2563eb;
}

.category-row span {
  color: #4b5563;
}

.category-row strong {
  color: #1f2937;
}

.formula {
  margin-top: 30px;
  padding: 20px;
  background: #f8fafc;
  border-radius: 12px;
  text-align: center;
}

.formula h3 {
  margin-bottom: 10px;
}

.formula p {
  color: #2563eb;
  font-weight: bold;
}

/* Footer */

.footer {
  margin-top: auto;
  background: #111827;
  color: white;
  text-align: center;
  padding: 25px 15px;
  line-height: 1.8;
}

.footer strong {
  color: #60a5fa;
}

.copyright {
  margin-top: 5px;
  font-size: 14px;
  color: #9ca3af;
}

/* Responsive Design */

@media (max-width: 768px) {
  .header h1 {
    font-size: 32px;
  }

  .container {
    grid-template-columns: 1fr;
    width: 92%;
    margin: 30px auto;
  }

  .calculator-card,
  .info-card {
    padding: 25px;
  }
}

@media (max-width: 480px) {
  .header {
    padding: 35px 15px;
  }

  .header h1 {
    font-size: 28px;
  }

  .header p {
    font-size: 14px;
  }

  .container {
    width: 94%;
  }

  .button-group {
    flex-direction: column;
  }

  .reset-btn {
    width: 100%;
  }

  .category-row {
    flex-direction: column;
    gap: 5px;
    text-align: center;
  }
}
```
 ## html:
 ```
html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
}
```

## OUTPUT
<img width="1916" height="896" alt="Screenshot 2026-09-05 135025" src="https://github.com/user-attachments/assets/f3c21314-b8f8-4a92-9c2d-124d0dce69e4" />
<img width="1916" height="885" alt="Screenshot 2026-09-05 135041" src="https://github.com/user-attachments/assets/3cc94bf3-7df9-4b5a-9d85-a0b2939e6169" />


## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
