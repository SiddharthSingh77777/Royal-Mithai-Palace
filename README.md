<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Royal Mithai Palace</title>

<style>
/* ---------- PROFESSIONAL IMAGE BACKGROUND ---------- */
body {
    margin: 0;
    font-family: 'Segoe UI', Arial, sans-serif;
    min-height: 100vh;
    color: white;
    background: 
        linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
        url("https://images.unsplash.com/photo-1600628422019-54f94b6f8f5f");
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
}

/* ---------- HEADER ---------- */
header {
    background: rgba(0,0,0,0.5);
    backdrop-filter: blur(10px);
    padding: 18px 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.cart {
    font-size: 18px;
}

/* ---------- HERO ---------- */
.banner {
    text-align: center;
    padding: 60px 20px;
}

/* ---------- CUSTOMER ---------- */
.customer-box {
    text-align: center;
    margin-bottom: 20px;
}

.customer-box input {
    padding: 12px 18px;
    border-radius: 25px;
    border: none;
    outline: none;
    width: 280px;
    font-size: 16px;
}

/* ---------- PRODUCTS ---------- */
.products {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 25px;
    padding: 30px;
}

.product {
    background: rgba(255,255,255,0.18);
    backdrop-filter: blur(12px);
    border-radius: 15px;
    padding: 20px;
    text-align: center;
    box-shadow: 0 10px 25px rgba(0,0,0,0.3);
}

.product button {
    margin-top: 10px;
    background: linear-gradient(135deg, #ff9a9e, #fad0c4);
    border: none;
    padding: 10px 18px;
    border-radius: 20px;
    cursor: pointer;
    font-weight: bold;
}

/* ---------- CART ---------- */
.cart-box {
    background: rgba(255,255,255,0.18);
    backdrop-filter: blur(12px);
    margin: 30px;
    padding: 25px;
    border-radius: 15px;
}

.cart-box ul {
    list-style: none;
    padding: 0;
}

.cart-box li {
    display: flex;
    justify-content: space-between;
    margin: 8px 0;
}

.cart-box button {
    background: linear-gradient(135deg, #ff512f, #dd2476);
    border: none;
    padding: 12px 22px;
    border-radius: 25px;
    color: white;
    cursor: pointer;
}
</style>
</head>

<body>

<header>
    <h1>👑 Royal Mithai Palace</h1>
    <div class="cart">🛒 Items: <span id="cartCount">0</span></div>
</header>

<section class="banner">
    <h2>Premium Indian Sweets</h2>
    <p>Professional • Elegant • Multi-Customer Ordering</p>
</section>

<div class="customer-box">
    <input type="text" id="customerName" placeholder="Enter Customer Name">
</div>

<section class="products" id="products"></section>

<section class="cart-box">
    <h2>Current Order</h2>
    <p><strong>Customer:</strong> <span id="currentCustomer">None</span></p>
    <ul id="cartItems"></ul>
    <h3>Total: ₹<span id="total">0</span></h3>
    <button onclick="checkout()">Place Order</button>
</section>

<script>
const sweets = [
    {name:"Gulab Jamun", price:200, unit:"kg"},
    {name:"Rasgulla", price:180, unit:"kg"},
    {name:"Kaju Katli", price:600, unit:"kg"},
    {name:"Jalebi", price:150, unit:"kg"},
    {name:"Ladoo", price:250, unit:"kg"},
    {name:"Barfi", price:300, unit:"kg"},
    {name:"Peda", price:280, unit:"kg"},
    {name:"Mysore Pak", price:350, unit:"kg"}
];

let orders = {};
let currentCart = [];

const productsDiv = document.getElementById("products");
const cartItems = document.getElementById("cartItems");
const total = document.getElementById("total");
const cartCount = document.getElementById("cartCount");
const customerNameInput = document.getElementById("customerName");
const currentCustomer = document.getElementById("currentCustomer");

sweets.forEach((item, index) => {
    productsDiv.innerHTML += `
        <div class="product">
            <h3>${item.name}</h3>
            <p>₹${item.price} / ${item.unit}</p>
            <button onclick="addToCart(${index})">Add</button>
        </div>
    `;
});

function addToCart(index) {
    const name = customerNameInput.value.trim();
    if (!name) {
        alert("Customer name likh pehle bro!");
        return;
    }

    if (!orders[name]) orders[name] = [];
    orders[name].push(sweets[index]);
    currentCart = orders[name];
    updateCart(name);
}

function updateCart(name) {
    cartItems.innerHTML = "";
    let sum = 0;

    currentCart.forEach(item => {
        sum += item.price;
        cartItems.innerHTML += `
            <li>${item.name} - ₹${item.price} / ${item.unit}</li>
        `;
    });

    total.innerText = sum;
    cartCount.innerText = currentCart.length;
    currentCustomer.innerText = name;
}

function checkout() {
    const name = customerNameInput.value.trim();
    if (!name || !orders[name] || orders[name].length === 0) {
        alert("Order empty hai bro!");
        return;
    }

    alert(`Order placed successfully for ${name} 👑`);
    orders[name] = [];
    currentCart = [];
    updateCart(name);
}
</script>

</body>
</html>
