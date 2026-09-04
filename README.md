<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sahu's Shopping Collection</title>

<!-- EmailJS SDK -->
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>

<style>
  :root{
    --primary:#ff6b35;
    --primary-dark:#e55a2b;
    --dark:#1f2937;
    --light-bg:#f9fafb;
    --white:#ffffff;
    --gray:#6b7280;
    --radius:14px;
    --shadow:0 6px 20px rgba(0,0,0,0.08);
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  body{
    font-family:'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    background:var(--light-bg);
    color:var(--dark);
    line-height:1.5;
    overflow-x:hidden;
  }
  a{text-decoration:none;color:inherit;}
  img{max-width:100%;display:block;}

  /* ---------- HEADER ---------- */
  header{
    position:sticky;
    top:0;
    z-index:100;
    background:var(--white);
    box-shadow:0 2px 10px rgba(0,0,0,0.06);
    padding:14px 20px;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }
  .logo{
    font-size:1.25rem;
    font-weight:800;
    color:var(--primary);
  }
  .logo span{color:var(--dark);}

  /* ---------- HERO ---------- */
  .hero{
    position:relative;
    width:100%;
    min-height:78vh;
    background:url('https://i.ibb.co/bR8R0BvV/IMG-0895.jpg') center/cover no-repeat;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    color:#fff;
  }
  .hero::before{
    content:"";
    position:absolute;
    inset:0;
    background:linear-gradient(180deg, rgba(0,0,0,0.45), rgba(0,0,0,0.6));
  }
  .hero-content{
    position:relative;
    z-index:2;
    padding:20px;
    max-width:700px;
  }
  .hero-content h1{
    font-size:clamp(2rem, 6vw, 3.2rem);
    font-weight:800;
    margin-bottom:12px;
    text-shadow:0 3px 12px rgba(0,0,0,0.4);
  }
  .hero-content p{
    font-size:clamp(1rem, 2.5vw, 1.3rem);
    margin-bottom:26px;
    opacity:0.95;
  }
  .btn-primary{
    display:inline-block;
    background:var(--primary);
    color:#fff;
    border:none;
    padding:14px 32px;
    font-size:1rem;
    font-weight:700;
    border-radius:50px;
    cursor:pointer;
    box-shadow:0 8px 20px rgba(255,107,53,0.4);
    transition:transform .2s, background .2s;
  }
  .btn-primary:hover{
    background:var(--primary-dark);
    transform:translateY(-2px);
  }

  /* ---------- SECTION TITLES ---------- */
  .section{
    padding:50px 20px;
    max-width:1100px;
    margin:0 auto;
  }
  .section h2{
    font-size:1.8rem;
    font-weight:800;
    margin-bottom:6px;
    text-align:center;
  }
  .section .subtitle{
    text-align:center;
    color:var(--gray);
    margin-bottom:30px;
  }

  /* ---------- PRODUCT CAROUSEL ---------- */
  .carousel-wrap{
    position:relative;
  }
  .carousel{
    display:flex;
    gap:20px;
    overflow-x:auto;
    scroll-behavior:smooth;
    padding:10px 6px 20px;
    scrollbar-width:thin;
    scrollbar-color:var(--primary) #eee;
  }
  .carousel::-webkit-scrollbar{height:8px;}
  .carousel::-webkit-scrollbar-thumb{background:var(--primary);border-radius:10px;}

  .product-card{
    flex:0 0 240px;
    background:var(--white);
    border-radius:var(--radius);
    box-shadow:var(--shadow);
    overflow:hidden;
    display:flex;
    flex-direction:column;
    transition:transform .2s;
  }
  .product-card:hover{transform:translateY(-4px);}
  .product-card img{
    width:100%;
    height:180px;
    object-fit:cover;
    background:#eee;
  }
  .product-info{
    padding:16px;
    display:flex;
    flex-direction:column;
    flex:1;
  }
  .product-info h3{
    font-size:1.05rem;
    margin-bottom:6px;
  }
  .price{
    color:var(--primary);
    font-weight:800;
    font-size:1.1rem;
    margin-bottom:14px;
  }
  .add-cart-btn{
    margin-top:auto;
    background:var(--dark);
    color:#fff;
    border:none;
    padding:10px;
    border-radius:8px;
    font-weight:600;
    cursor:pointer;
    transition:background .2s;
  }
  .add-cart-btn:hover{background:var(--primary);}

  /* ---------- FLOATING CART ICON ---------- */
  .cart-fab{
    position:fixed;
    bottom:90px;
    right:22px;
    background:var(--primary);
    color:#fff;
    width:60px;
    height:60px;
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:1.6rem;
    box-shadow:0 8px 20px rgba(255,107,53,0.5);
    cursor:pointer;
    z-index:200;
    border:none;
  }
  .cart-count{
    position:absolute;
    top:-4px;
    right:-4px;
    background:var(--dark);
    color:#fff;
    font-size:0.75rem;
    font-weight:700;
    width:22px;
    height:22px;
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
  }

  /* ---------- WHATSAPP FLOATING BUTTON ---------- */
  .whatsapp-fab{
    position:fixed;
    bottom:20px;
    right:22px;
    background:#25D366;
    color:#fff;
    width:56px;
    height:56px;
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:1.7rem;
    box-shadow:0 8px 20px rgba(37,211,102,0.5);
    z-index:200;
  }

  /* ---------- CART DRAWER ---------- */
  .overlay{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.5);
    z-index:300;
    display:none;
  }
  .overlay.active{display:block;}

  .cart-drawer{
    position:fixed;
    top:0;
    right:-100%;
    width:100%;
    max-width:400px;
    height:100%;
    background:#fff;
    z-index:301;
    transition:right .3s ease;
    display:flex;
    flex-direction:column;
    box-shadow:-4px 0 20px rgba(0,0,0,0.2);
  }
  .cart-drawer.active{right:0;}

  .cart-header{
    padding:18px 20px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    border-bottom:1px solid #eee;
  }
  .cart-header h2{font-size:1.2rem;}
  .close-btn{
    background:none;
    border:none;
    font-size:1.5rem;
    cursor:pointer;
    color:var(--gray);
  }

  .cart-items{
    flex:1;
    overflow-y:auto;
    padding:10px 20px;
  }
  .cart-item{
    display:flex;
    gap:12px;
    align-items:center;
    padding:12px 0;
    border-bottom:1px solid #f0f0f0;
  }
  .cart-item img{
    width:56px;
    height:56px;
    object-fit:cover;
    border-radius:8px;
    background:#eee;
  }
  .cart-item-info{flex:1;}
  .cart-item-info h4{font-size:0.95rem;margin-bottom:2px;}
  .cart-item-info .price{font-size:0.9rem;margin-bottom:0;}
  .qty-controls{
    display:flex;
    align-items:center;
    gap:8px;
  }
  .qty-controls button{
    width:26px;
    height:26px;
    border-radius:6px;
    border:1px solid #ddd;
    background:#fff;
    cursor:pointer;
    font-weight:700;
  }
  .remove-btn{
    background:none;
    border:none;
    color:#e11d48;
    cursor:pointer;
    font-size:1.1rem;
    margin-left:6px;
  }
  .empty-cart{
    text-align:center;
    color:var(--gray);
    padding:40px 10px;
  }

  .cart-footer{
    padding:16px 20px 22px;
    border-top:1px solid #eee;
  }
  .cart-total{
    display:flex;
    justify-content:space-between;
    font-weight:700;
    font-size:1.1rem;
    margin-bottom:16px;
  }

  .order-form{
    display:flex;
    flex-direction:column;
    gap:10px;
    margin-bottom:14px;
  }
  .order-form input, .order-form textarea{
    padding:10px 12px;
    border:1px solid #ddd;
    border-radius:8px;
    font-size:0.95rem;
    font-family:inherit;
  }
  .order-form textarea{resize:vertical;min-height:60px;}

  .send-order-btn{
    width:100%;
    background:var(--primary);
    color:#fff;
    border:none;
    padding:14px;
    border-radius:10px;
    font-weight:700;
    font-size:1rem;
    cursor:pointer;
  }
  .send-order-btn:disabled{
    background:#ccc;
    cursor:not-allowed;
  }

  .status-msg{
    margin-top:10px;
    text-align:center;
    font-size:0.9rem;
    font-weight:600;
  }
  .status-msg.success{color:#16a34a;}
  .status-msg.error{color:#dc2626;}

  footer{
    text-align:center;
    padding:24px;
    color:var(--gray);
    font-size:0.85rem;
  }

  @media(max-width:480px){
    .product-card{flex:0 0 200px;}
  }
</style>
</head>
<body>

<!-- ---------- HEADER ---------- -->
<header>
  <div class="logo">Sahu's <span>Shopping Collection</span></div>
</header>

<!-- ---------- HERO ---------- -->
<section class="hero">
  <div class="hero-content">
    <h1>Sahu's Shopping Collection</h1>
    <p>Fresh Finds, Best Prices</p>
    <button class="btn-primary" onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">Shop Now</button>
  </div>
</section>

<!-- ---------- PRODUCTS ---------- -->
<section class="section" id="products">
  <h2>Our Products</h2>
  <p class="subtitle">Swipe to explore our best picks</p>

  <div class="carousel-wrap">
    <div class="carousel" id="carousel">
      <!-- product cards injected by JS -->
    </div>
  </div>
</section>

<footer>
  &copy; 2026 Sahu's Shopping Collection. All rights reserved.
</footer>

<!-- ---------- FLOATING CART BUTTON ---------- -->
<button class="cart-fab" onclick="openCart()">
  🛒
  <span class="cart-count" id="cartCount">0</span>
</button>

<!-- ---------- WHATSAPP FLOATING BUTTON ---------- -->
<a class="whatsapp-fab" href="https://wa.me/918302088881" target="_blank" rel="noopener">💬</a>

<!-- ---------- CART DRAWER ---------- -->
<div class="overlay" id="overlay" onclick="closeCart()"></div>
<div class="cart-drawer" id="cartDrawer">
  <div class="cart-header">
    <h2>Your Cart</h2>
    <button class="close-btn" onclick="closeCart()">&times;</button>
  </div>

  <div class="cart-items" id="cartItems">
    <p class="empty-cart">Your cart is empty</p>
  </div>

  <div class="cart-footer">
    <div class="cart-total">
      <span>Total</span>
      <span id="cartTotal">₹0</span>
    </div>

    <form class="order-form" id="orderForm">
      <input type="text" id="custName" placeholder="Your Name" required>
      <input type="tel" id="custPhone" placeholder="Your Phone Number" required pattern="[0-9]{10}" title="Enter a 10-digit phone number">
      <textarea id="custNote" placeholder="Delivery address / notes (optional)"></textarea>
      <button type="submit" class="send-order-btn" id="sendOrderBtn">Send Order</button>
    </form>
    <div id="statusMsg"></div>
  </div>
</div>

<script>
/* ===========================================================
   EmailJS CONFIGURATION
   -----------------------------------------------------------
   1. Create a free account at https://www.emailjs.com
   2. Add an Email Service (e.g. Gmail) and note the SERVICE_ID
   3. Create an Email Template with variables:
      {{customer_name}}, {{customer_phone}}, {{customer_note}},
      {{order_items}}, {{order_total}}, {{to_email}}
   4. Note the TEMPLATE_ID and your PUBLIC_KEY (Account > API Keys)
   5. Replace the placeholders below.
   =========================================================== */
const EMAILJS_PUBLIC_KEY  = "YOUR_PUBLIC_KEY";
const EMAILJS_SERVICE_ID  = "YOUR_SERVICE_ID";
const EMAILJS_TEMPLATE_ID = "YOUR_TEMPLATE_ID";
const OWNER_EMAIL = "sahugirja751@gmail.com";

emailjs.init(EMAILJS_PUBLIC_KEY);

/* ---------- PRODUCT DATA ---------- */
const products = [
  {
    id: 1,
    name: "Wireless Mouse",
    price: 499,
    image: "https://i.ibb.co/GfDTVCDM/mouse.jpg"
  },
  {
    id: 2,
    name: "Over-Ear Headphones",
    price: 1299,
    image: "https://i.ibb.co/PvVFKRX1/headphone.jpg"
  },
  {
    id: 3,
    name: "Wireless Earbuds",
    price: 999,
    image: "https://i.ibb.co/RG2DL4sh/air-buds.jpg"
  }
];

let cart = [];

/* ---------- RENDER PRODUCTS ---------- */
const carousel = document.getElementById('carousel');
products.forEach(p => {
  const card = document.createElement('div');
  card.className = 'product-card';
  card.innerHTML = `
    <img src="${p.image}" alt="${p.name}">
    <div class="product-info">
      <h3>${p.name}</h3>
      <div class="price">₹${p.price}</div>
      <button class="add-cart-btn" onclick="addToCart(${p.id})">Add to Cart</button>
    </div>
  `;
  carousel.appendChild(card);
});

/* ---------- CART LOGIC ---------- */
function addToCart(id){
  const product = products.find(p => p.id === id);
  const existing = cart.find(item => item.id === id);
  if(existing){
    existing.qty += 1;
  } else {
    cart.push({...product, qty: 1});
  }
  renderCart();
  openCart();
}

function changeQty(id, delta){
  const item = cart.find(i => i.id === id);
  if(!item) return;
  item.qty += delta;
  if(item.qty <= 0){
    cart = cart.filter(i => i.id !== id);
  }
  renderCart();
}

function removeItem(id){
  cart = cart.filter(i => i.id !== id);
  renderCart();
}

function renderCart(){
  const cartItemsEl = document.getElementById('cartItems');
  const cartCountEl = document.getElementById('cartCount');
  const cartTotalEl = document.getElementById('cartTotal');

  const totalQty = cart.reduce((sum, i) => sum + i.qty, 0);
  cartCountEl.textContent = totalQty;

  if(cart.length === 0){
    cartItemsEl.innerHTML = '<p class="empty-cart">Your cart is empty</p>';
    cartTotalEl.textContent = '₹0';
    return;
  }

  let total = 0;
  cartItemsEl.innerHTML = cart.map(item => {
    total += item.price * item.qty;
    return `
      <div class="cart-item">
        <img src="${item.image}" alt="${item.name}">
        <div class="cart-item-info">
          <h4>${item.name}</h4>
          <div class="price">₹${item.price}</div>
          <div class="qty-controls">
            <button onclick="changeQty(${item.id}, -1)">−</button>
            <span>${item.qty}</span>
            <button onclick="changeQty(${item.id}, 1)">+</button>
            <button class="remove-btn" onclick="removeItem(${item.id})">🗑</button>
          </div>
        </div>
      </div>
    `;
  }).join('');

  cartTotalEl.textContent = `₹${total}`;
}

/* ---------- DRAWER OPEN/CLOSE ---------- */
function openCart(){
  document.getElementById('cartDrawer').classList.add('active');
  document.getElementById('overlay').classList.add('active');
}
function closeCart(){
  document.getElementById('cartDrawer').classList.remove('active');
  document.getElementById('overlay').classList.remove('active');
}

/* ---------- SEND ORDER VIA EMAILJS ---------- */
document.getElementById('orderForm').addEventListener('submit', function(e){
  e.preventDefault();

  const statusEl = document.getElementById('statusMsg');
  const btn = document.getElementById('sendOrderBtn');

  if(cart.length === 0){
    statusEl.textContent = "Your cart is empty. Add items before sending your order.";
    statusEl.className = "status-msg error";
    return;
  }

  const name = document.getElementById('custName').value.trim();
  const phone = document.getElementById('custPhone').value.trim();
  const note = document.getElementById('custNote').value.trim();

  if(!name || !phone){
    statusEl.textContent = "Please enter your name and phone number.";
    statusEl.className = "status-msg error";
    return;
  }

  let total = 0;
  const itemsList = cart.map(item => {
    total += item.price * item.qty;
    return `${item.name} x${item.qty} - ₹${item.price * item.qty}`;
  }).join('\n');

  const templateParams = {
    customer_name: name,
    customer_phone: phone,
    customer_note: note || "N/A",
    order_items: itemsList,
    order_total: `₹${total}`,
    to_email: OWNER_EMAIL
  };

  btn.disabled = true;
  btn.textContent = "Sending...";

  emailjs.send(EMAILJS_SERVICE_ID, EMAILJS_TEMPLATE_ID, templateParams)
    .then(function(){
      statusEl.textContent = "Order sent successfully! We'll contact you shortly.";
      statusEl.className = "status-msg success";
      cart = [];
      renderCart();
      document.getElementById('orderForm').reset();
      btn.disabled = false;
      btn.textContent = "Send Order";
    })
    .catch(function(err){
      console.error("EmailJS error:", err);
      statusEl.textContent = "Failed to send order. Please try again or contact us on WhatsApp.";
      statusEl.className = "status-msg error";
      btn.disabled = false;
      btn.textContent = "Send Order";
    });
});
</script>

</body>
</html>
