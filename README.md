# Kupfer-shop
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kupfer-Shop | 99% Rein</title>

<style>
body {
    margin:0;
    font-family: Arial, sans-serif;
    background: linear-gradient(to bottom, #1c1c1c, #111);
    color:white;
}

header {
    text-align:center;
    padding:30px 20px;
    background: #000;
    border-bottom: 3px solid #b87333;
}

header img {
    width:180px;
}

h1 {
    margin-top:15px;
    color:#b87333;
}

.container {
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:30px;
    padding:40px 20px;
}

.product {
    background:#1e1e1e;
    border-radius:15px;
    padding:20px;
    width:300px;
    box-shadow: 0 0 20px rgba(184,115,51,0.3);
}

.product img {
    width:100%;
    border-radius:10px;
}

.product h2 {
    color:#b87333;
}

.product select,
.product input {
    width:100%;
    padding:8px;
    margin:10px 0;
    border-radius:5px;
    border:none;
}

button {
    width:100%;
    padding:10px;
    background:#b87333;
    border:none;
    border-radius:8px;
    color:white;
    font-weight:bold;
    cursor:pointer;
}

button:hover {
    background:#d18b47;
}

.cart {
    background:#000;
    padding:25px;
    margin:40px auto;
    max-width:600px;
    border-radius:15px;
    border:2px solid #b87333;
}

.cart h2 {
    color:#b87333;
}

footer {
    text-align:center;
    padding:20px;
    background:#000;
    margin-top:40px;
    font-size:14px;
    color:#aaa;
}
</style>
</head>
<body>

<header>
    <img src="logo.png" alt="Kupfer Shop Logo">
    <h1>Kupfer 99% Rein</h1>
</header>

<div class="container">

    <!-- Kupferbarren -->
    <div class="product">
        <img src="barren.png" alt="Kupferbarren">
        <h2>Kupferbarren</h2>

        <label>Gewicht:</label>
        <select id="barren-weight">
            <option value="100">100g – 25 CHF</option>
            <option value="250">250g – 55 CHF</option>
            <option value="500">500g – 95 CHF</option>
            <option value="1000">1kg – 180 CHF</option>
        </select>

        <label>Gravur / Muster (optional):</label>
        <input type="text" id="gravur" placeholder="z.B. Name, Logo">

        <button onclick="addBarren()">In den Warenkorb</button>
    </div>

    <!-- Granulat -->
    <div class="product">
        <img src="granulat.png" alt="Kupfergranulat">
        <h2>Kupfergranulat</h2>

        <label>Menge (Gramm):</label>
        <input type="number" id="granulat-menge" placeholder="z.B. 500">

        <button onclick="addGranulat()">In den Warenkorb</button>
    </div>

</div>

<div class="cart">
    <h2>Warenkorb</h2>
    <ul id="cart-items"></ul>
    <p>Zwischensumme: <span id="subtotal">0</span> CHF</p>
    <p>Versand: 9 CHF</p>
    <h3>Gesamt: <span id="total">0</span> CHF</h3>
</div>

<footer>
    © 2026 Kupfer-Shop | 99% Rein | Individuelle Gravuren möglich
</footer>

<script>
let cart = [];
let barrenPrices = {100:25, 250:55, 500:95, 1000:180};
let granulatPreisProGramm = 0.25;
let versand = 9;

function addBarren() {
    let weight = document.getElementById("barren-weight").value;
    let gravur = document.getElementById("gravur").value;
    let price = barrenPrices[weight];

    cart.push({
        name: "Kupferbarren " + weight + "g",
        gravur: gravur,
        price: price
    });

    updateCart();
}

function addGranulat() {
    let menge = document.getElementById("granulat-menge").value;

    if(menge <= 0) {
        alert("Bitte gültige Menge eingeben");
        return;
    }

    let price = menge * granulatPreisProGramm;

    cart.push({
        name: "Kupfergranulat " + menge + "g",
        gravur: "-",
        price: price
    });

    updateCart();
}

function updateCart() {
    let list = document.getElementById("cart-items");
    list.innerHTML = "";
    let subtotal = 0;

    cart.forEach(item => {
        subtotal += item.price;
        let li = document.createElement("li");
        li.textContent = item.name + " | Gravur: " + item.gravur + " | " + item.price.toFixed(2) + " CHF";
        list.appendChild(li);
    });

    document.getElementById("subtotal").textContent = subtotal.toFixed(2);
    document.getElementById("total").textContent = (subtotal + versand).toFixed(2);
}
</script>

</body>
</html>
