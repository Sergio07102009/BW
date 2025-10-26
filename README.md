<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>B & W - Money is made, not born.</title>
  <style>
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;background:#121212;color:#fff}
    header{display:flex;justify-content:space-between;align-items:center;padding:18px 34px;background:#1f1f1f;border-bottom:1px solid #333}
    .logo{font-weight:700;font-size:24px;color:#fff}
    nav a{margin-left:18px;text-decoration:none;color:#fff;font-weight:600}
    nav a:hover{color:#f0a500}
    .hero{padding:48px 34px;display:flex;gap:40px;align-items:center;background:#1a1a1a;border-radius:12px;margin:12px}
    .hero-left{flex:1}
    .hero-right{flex:1}
    .hero h1{font-size:44px;margin-bottom:12px;color:#fff}
    .hero p{color:#ccc;margin-bottom:16px}
    .btn{background:#f0a500;color:#121212;padding:12px 18px;border-radius:8px;text-decoration:none;display:inline-block;font-weight:600}
    .btn:hover{opacity:0.9}
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:18px;padding:24px}
    .card{border:1px solid #333;border-radius:12px;padding:12px;background:#1f1f1f}
    .card img{width:100%;height:240px;object-fit:cover;border-radius:8px}
    .price{font-weight:700;margin-top:8px;color:#f0a500}
    footer{padding:24px;text-align:center;border-top:1px solid #333;margin-top:24px;color:#ccc}
    .modal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(0,0,0,0.7)}
    .modal .box{background:#1f1f1f;padding:18px;border-radius:12px;max-width:420px;width:100%;color:#fff}
    input,select,textarea{width:100%;padding:8px;margin:8px 0;border:1px solid #333;border-radius:8px;background:#121212;color:#fff}
  </style>
</head>
<body>
  <header>
    <div class="logo">B & W</div>
    <nav>
      <a href="#home">Home</a>
      <a href="#shop">Shop</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
      <a href="#cart" id="cartBtn">Cart (0)</a>
    </nav>
  </header>  <section class="hero" id="home">
    <div class="hero-left">
      <h1>Money is made, not born.</h1>
      <p>Executive premium tees designed for people who hustle. Simple. Bold. Timeless.</p>
      <a class="btn" href="#shop">Shop Collection</a>
    </div>
    <div class="hero-right">
      <img src="https://images.unsplash.com/photo-1541099649105-f69ad21f3246?q=80&w=1000&auto=format&fit=crop&ixlib=rb-4.0.3&s=abc" style="width:100%;border-radius:12px;object-fit:cover;height:320px">
    </div>
  </section>  <section id="shop">
    <h2 style="padding:0 34px 10px 34px">Shop</h2>
    <div class="grid" id="productGrid">
      <!-- products inserted by JS -->
    </div>
  </section>  <section id="about" style="padding:0 34px 24px 34px">
    <h2>About B & W</h2>
    <p style="max-width:720px;margin-top:12px">B & W is a premium t-shirt brand for creators and hustlers. Founded by Priyanshu Raj, our mission is to provide minimal, executive apparel that speaks volume without shouting.</p>
  </section>  <section id="contact" style="padding:12px 34px 60px 34px">
    <h2>Contact</h2>
    <form id="contactForm" style="max-width:600px;margin-top:12px">
      <input placeholder="Name" id="cname">
      <input placeholder="Email" id="cemail" value="hraj07029@gmail.com">
      <textarea placeholder="Message" id="cmessage"></textarea>
      <button class="btn" type="button" onclick="submitContact()">Send Message</button>
    </form>
  </section>  <footer>
    © B & W — Money is made, not born.
  </footer>  <div class="modal" id="cartModal">
    <div class="box">
      <h3>Your Cart</h3>
      <div id="cartItems"></div>
      <div style="margin-top:12px">
        <strong>Total: ₹<span id="cartTotal">0</span></strong>
      </div>
      <div style="margin-top:12px">
        <button class="btn" onclick="checkout()">Checkout</button>
        <button style="margin-left:8px;padding:10px 14px;border-radius:8px" onclick="closeCart()">Close</button>
      </div>
    </div>
  </div>  <script>
    const products = [
      {id: 1, title: 'T-shirt', price: 10, img: 'https://via.placeholder.com/300x300?text=T-shirt'}
    ];

    const productGrid = document.getElementById('productGrid');
    const cartBtn = document.getElementById('cartBtn');
    const cartModal = document.getElementById('cartModal');
    let cart = [];

    function renderProducts(){
      products.forEach(p=>{
        const card = document.createElement('div');
        card.className='card';
        card.innerHTML=`<img src="${p.img}"><h3>${p.title}</h3><div class="price">₹${p.price}</div><div style=\"margin-top:10px\"><button class='btn' onclick='addToCart(${p.id})'>Add to Cart</button></div>`;
        productGrid.appendChild(card);
      });
    }
    renderProducts();

    function addToCart(id){
      const product = products.find(x=>x.id===id);
      cart.push(product);
      updateCartBadge();
      alert('Added to cart');
    }

    function updateCartBadge(){
      cartBtn.innerText=`Cart (${cart.length})`;
    }

    cartBtn.addEventListener('click', (e)=>{e.preventDefault();openCart();});

    function openCart(){
      cartModal.style.display='flex';
      const cartItemsDiv = document.getElementById('cartItems');
      cartItemsDiv.innerHTML='';
      let total=0;
      cart.forEach((it,idx)=>{
        total+=it.price;
        const div = document.createElement('div');
        div.style.padding='8px 0';
        div.innerHTML=`${it.title} - ₹${it.price} <button onclick='removeFromCart(${idx})' style='margin-left:8px;padding:6px;border-radius:6px'>Remove</button>`;
        cartItemsDiv.appendChild(div);
      });
      document.getElementById('cartTotal').innerText=total;
    }

    function closeCart(){cartModal.style.display='none'}
    function removeFromCart(i){cart.splice(i,1);openCart();updateCartBadge()}

    function checkout(){
      const total = cart.reduce((s,it)=>s+it.price,0);
      if(total===0){alert('Cart is empty');return}
      const paymentLink = 'YOUR_REAL_RAZORPAY_LINK';
      window.open(paymentLink, '_blank');
    }

    function submitContact(){
      const name=document.getElementById('cname').value;
      const email=document.getElementById('cemail
