<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Aravind Traders</title>

<style>
body {
    font-family: Arial;
    background-color: #d6ecff;
    margin: 0;
}

header {
    background: #2196f3;
    color: white;
    padding: 15px;
    display: flex;
    justify-content: space-between;
}

.categories {
    margin: 20px;
}

.categories button {
    padding: 10px;
    margin: 5px;
    cursor: pointer;
    border: none;
    background: #2196f3;
    color: white;
    border-radius: 5px;
}

#products {
    display: flex;
    flex-wrap: wrap;
    padding: 20px;
}

.product {
    background: white;
    padding: 15px;
    margin: 10px;
    border-radius: 10px;
    width: 200px;
    text-align: center;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.product button {
    background: green;
    color: white;
    padding: 8px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
}

.modal {
    display: none;
    position: fixed;
    background: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
}

.modal-content {
    background: white;
    margin: 10% auto;
    padding: 20px;
    width: 300px;
    border-radius: 10px;
}
</style>

</head>

<body>

<header>
    <h1>Aravind Traders</h1>
    <button onclick="viewCart()">🛒 Cart (<span id="cartCount">0</span>)</button>
</header>

<h2 style="padding-left:20px;">Select Category</h2>

<div class="categories">
    <button onclick="showCategory('mccb')">MCCB</button>
    <button onclick="showCategory('mcb')">MCB</button>
    <button onclick="showCategory('isolator')">Isolator</button>
    <button onclick="showCategory('bolts')">Bolts</button>
    <button onclick="showCategory('others')">Others</button>
</div>

<div id="products"></div>

<!-- CART -->
<div id="cartModal" class="modal">
    <div class="modal-content">
        <h2>Your Cart</h2>
        <ul id="cartItems"></ul>
        <h3>Total: ₹<span id="totalAmount">0</span></h3>
        <button onclick="checkout()">Buy via WhatsApp</button>
        <button onclick="closeCart()">Close</button>
    </div>
</div>

<script>
let cart = [];
let total = 0;

const data = {
    mccb: [
        { name: "MCCB 2-6A", price: 500 },
        { name: "MCCB 4-6A", price: 700 },
        { name: "MCCB 6-10A", price: 900 }
    ],
    mcb: [
        { name: "MCB 2A", price: 150 },
        { name: "MCB 6A", price: 200 },
        { name: "MCB 10A", price: 250 }
    ],
    isolator: [
        { name: "Isolator 16A", price: 300 },
        { name: "Isolator 32A", price: 450 }
    ],
    bolts: [
        { name: "Bolt Small", price: 50 },
        { name: "Bolt Medium", price: 80 },
        { name: "Bolt Large", price: 120 }
    ],
    others: [
        { name: "Wire Roll", price: 800 },
        { name: "Switch", price: 120 }
    ]
};

function showCategory(category) {
    let productsDiv = document.getElementById("products");
    productsDiv.innerHTML = "";

    data[category].forEach(item => {
        productsDiv.innerHTML += `
            <div class="product">
                <h3>${item.name}</h3>
                <p>₹${item.price}</p>
                <button onclick="addToCart('${item.name}', ${item.price})">Add</button>
            </div>
        `;
    });
}

function addToCart(name, price) {
    cart.push({ name, price });
    total += price;
    document.getElementById("cartCount").innerText = cart.length;
    alert(name + " added to cart");
}

function viewCart() {
    let list = document.getElementById("cartItems");
    list.innerHTML = "";

    cart.forEach(item => {
        list.innerHTML += `<li>${item.name} - ₹${item.price}</li>`;
    });

    document.getElementById("totalAmount").innerText = total;
    document.getElementById("cartModal").style.display = "block";
}

function closeCart() {
    document.getElementById("cartModal").style.display = "none";
}

function checkout() {
    let message = "Order Details:%0A";

    cart.forEach(item => {
        message += item.name + " - ₹" + item.price + "%0A";
    });

    message += "Total: ₹" + total;

    window.open("https://wa.me/919949083739?text=" + message, "_blank");
}
</script>

</body>
</html>
