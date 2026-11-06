
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>HudHud MART | Online Grocery Shop</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f2f3f8;color:#222;padding-bottom:75px}
header{background:white;padding:14px;position:sticky;top:0;z-index:5;box-shadow:0 2px 6px #ddd}
.brand{font-size:25px;font-weight:bold;color:#e94b24}
.brand span{color:#248d45}
.search{display:flex;margin-top:12px;gap:7px}
.search input{flex:1;padding:13px;border:1px solid #ddd;border-radius:25px;font-size:15px;min-width:0}
.search button{background:#f45b18;color:white;border:0;border-radius:25px;padding:0 18px;font-weight:bold}
h3{margin:18px 14px 10px}
.categories{display:flex;overflow-x:auto;gap:10px;padding:8px 12px}
.cat{min-width:90px;background:white;border-radius:12px;padding:12px 6px;text-align:center;font-size:12px;border:1px solid #eee}
.cat .emoji{font-size:27px;display:block;margin-bottom:7px}
.cat button{border:0;background:none;color:#333;font-weight:bold}
.banner{margin:12px;background:linear-gradient(110deg,#e94b24,#ff9b39);color:white;padding:22px;border-radius:14px}
.banner h2{margin:0 0 7px}
.banner p{margin:0}
.products{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;padding:10px}
.product{background:white;border-radius:12px;overflow:hidden;padding-bottom:12px}
.photo{height:135px;background:#f7f7f7;display:flex;align-items:center;justify-content:center;font-size:65px}
.photo img{width:100%;height:100%;object-fit:cover}
.info{padding:9px}
.name{font-size:14px;min-height:35px}
.price{color:#ef4056;font-size:19px;margin:8px 0}
.add{width:100%;padding:10px;border:0;border-radius:7px;background:#248d45;color:white;font-weight:bold}
.bottom{position:fixed;bottom:0;left:0;right:0;background:white;display:flex;justify-content:space-around;padding:10px 2px;box-shadow:0 -2px 8px #ddd;z-index:8}
.bottom a{color:#555;text-decoration:none;text-align:center;font-size:12px}
.bottom span{display:block;font-size:22px;margin-bottom:3px}
.cartbox{background:white;margin:12px;padding:14px;border-radius:12px}
.cartline{display:flex;justify-content:space-between;gap:8px;margin:12px 0;font-size:14px}
.checkout{width:100%;padding:13px;background:#20a052;color:white;border:0;border-radius:8px;font-size:16px;font-weight:bold}
input,textarea{font-family:Arial}
.hidden{display:none}
footer{text-align:center;padding:20px;color:#666;font-size:12px}
</style>
</head>
<body>

<header>
  <div class="brand">🐦 HudHud <span>MART</span></div>
  <div class="search">
    <input id="search" placeholder="Search groceries..." oninput="showProducts()">
    <button onclick="showProducts()">Search</button>
  </div>
</header>

<h3>Shop by Category</h3>
<div class="categories">
  <div class="cat"><span class="emoji">🍚</span><button onclick="filter('Rice & Dry Foods')">Rice & Dry Foods</button></div>
  <div class="cat"><span class="emoji">🥬</span><button onclick="filter('Vegetables & Fruits')">Vegetables & Fruits</button></div>
  <div class="cat"><span class="emoji">🍪</span><button onclick="filter('Snacks & Biscuits')">Snacks & Biscuits</button></div>
  <div class="cat"><span class="emoji">🥤</span><button onclick="filter('Drinks')">Drinks</button></div>
  <div class="cat"><span class="emoji">🥛</span><button onclick="filter('Milk & Dairy')">Milk & Dairy</button></div>
  <div class="cat"><span class="emoji">🧹</span><button onclick="filter('Household Cleaning')">Cleaning</button></div>
  <div class="cat"><span class="emoji">🧴</span><button onclick="filter('Personal Care')">Personal Care</button></div>
  <div class="cat"><span class="emoji">🛒</span><button onclick="filter('Other Grocery')">Other Grocery</button></div>
</div>

<div class="banner">
  <h2>Welcome to HudHud MART!</h2>
  <p>Your daily groceries, delivered to your home.</p>
  <p>🛍️ Easy shopping | 📲 WhatsApp orders | 💵 Cash on Delivery</p>
</div>

<h3 id="productHeading">Popular Products</h3>
<div class="products" id="products"></div>

<section id="cart">
  <h3>🛒 Your Shopping Cart</h3>
  <div class="cartbox">
    <div id="cartItems">Your cart is empty.</div>
    <h3 id="total">Total: Rs. 0</h3>
    <input id="customer" placeholder="Your name" style="width:100%;padding:12px;margin:5px 0">
    <input id="phone" placeholder="Phone number" style="width:100%;padding:12px;margin:5px 0">
    <textarea id="address" placeholder="Delivery address and town" style="width:100%;padding:12px;margin:5px 0"></textarea>
    <button class="checkout" onclick="checkout()">Order through WhatsApp</button>
    <p style="font-size:12px;color:#666">Payment: Cash on Delivery (COD). Confirm your order and delivery details through WhatsApp.</p>
  </div>
</section>

<footer>
  <b>HudHud MART</b><br>
  Online Grocery Shopping – Sri Lanka<br>
  © 2026 HudHud MART
</footer>

<nav class="bottom">
  <a href="#"><span>🏠</span>Home</a>
  <a href="#products"><span>☷</span>Products</a>
  <a href="#cart"><span>🛒</span>Cart</a>
  <a href="#cart"><span>👤</span>Account</a>
</nav>

<script>
const items=[
 {name:"Rice",cat:"Rice & Dry Foods",price:220,emoji:"🍚"},
 {name:"Red Lentils (Dhal)",cat:"Rice & Dry Foods",price:180,emoji:"🫘"},
 {name:"Fresh Vegetables",cat:"Vegetables & Fruits",price:150,emoji:"🥬"},
 {name:"Fresh Fruits",cat:"Vegetables & Fruits",price:250,emoji:"🍎"},
 {name:"Biscuits",cat:"Snacks & Biscuits",price:120,emoji:"🍪"},
 {name:"Potato Chips",cat:"Snacks & Biscuits",price:100,emoji:"🍟"},
 {name:"Soft Drink",cat:"Drinks",price:180,emoji:"🥤"},
 {name:"Milk Packet",cat:"Milk & Dairy",price:220,emoji:"🥛"},
 {name:"Dishwashing Liquid",cat:"Household Cleaning",price:350,emoji:"🧴"},
 {name:"Laundry Soap",cat:"Household Cleaning",price:180,emoji:"🧼"},
 {name:"Shampoo",cat:"Personal Care",price:450,emoji:"🧴"},
 {name:"Toothpaste",cat:"Personal Care",price:300,emoji:"🪥"},
 {name:"Grocery Item",cat:"Other Grocery",price:100,emoji:"🛒"}
];
let selected="All",cart=[];

function showProducts(){
 const q=document.getElementById("search").value.toLowerCase();
 const list=items.filter(p=>(selected==="All"||p.cat===selected)&&p.name.toLowerCase().includes(q));
 document.getElementById("products").innerHTML=list.map((p)=>`
 <div class="product">
 <div class="photo">${p.emoji}</div>
 <div class="info">
 <div class="name">${p.name}</div>
 <div class="price">Rs. ${p.price}</div>
 <button class="add" onclick="addCart('${p.name}')">Add to Cart</button>
 </div></div>`).join("")||"No products found.";
}
function filter(cat){
 selected=cat;
 document.getElementById("productHeading").innerText=cat;
 showProducts();
 document.getElementById("products").scrollIntoView({behavior:"smooth"});
}
function addCart(name){
 const p=items.find(x=>x.name===name);
 const found=cart.find(x=>x.name===name);
 if(found)found.qty++;else cart.push({...p,qty:1});
 updateCart();
 alert(name+" added to cart!");
}
function updateCart(){
 let total=0;
 document.getElementById("cartItems").innerHTML=cart.length?cart.map((p,i)=>{
 total+=p.price*p.qty;
 return `<div class="cartline"><span>${p.name} × ${p.qty}</span><span>Rs. ${p.price*p.qty} <button onclick="removeItem(${i})">✖</button></span></div>`;
 }).join(""):"Your cart is empty.";
 document.getElementById("total").innerText="Total: Rs. "+total;
}
function removeItem(i){cart.splice(i,1);updateCart();}
function checkout(){
 if(!cart.length){alert("Please add products to your cart.");return;}
 const name=document.getElementById("customer").value.trim();
 const phone=document.getElementById("phone").value.trim();
 const address=document.getElementById("address").value.trim();
 if(!name||!phone||!address){alert("Please enter your name, phone number and delivery address.");return;}
 let total=cart.reduce((s,p)=>s+p.price*p.qty,0);
 let message="HudHud MART Order%0A";
 message+="Name: "+encodeURIComponent(name)+"%0APhone: "+encodeURIComponent(phone)+"%0AAddress: "+encodeURIComponent(address)+"%0A%0A";
 cart.forEach(p=>message+=encodeURIComponent(p.name+" x "+p.qty+" = Rs. "+(p.price*p.qty))+"%0A");
 message+="%0ATotal: Rs. "+total+"%0APayment: Cash on Delivery";
 window.open("https://wa.me/94767366548?text="+message,"_blank");
}
showProducts();
</script>
</body>
</html>
