<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<title>สปาร์คปลาบอลลูน</title>
<style>
body { font-family: Arial; margin:0; background:#eaf6ff; }
header { background:#0099ff; color:white; padding:15px; display:flex; justify-content:space-between; }
.container { padding:20px; }
.grid { display:grid; grid-template-columns: repeat(auto-fill,minmax(200px,1fr)); gap:15px; }
.card { background:white; padding:15px; border-radius:10px; box-shadow:0 2px 5px rgba(0,0,0,0.1); text-align:center; }
img { width:100%; border-radius:10px; }
button { padding:8px 12px; border:none; border-radius:5px; cursor:pointer; }
.btn { background:#0099ff; color:white; }
.cart { cursor:pointer; font-size:20px; }
.modal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.5); justify-content:center; align-items:center; }
.modal-content { background:white; padding:20px; border-radius:10px; width:300px; }
input { width:100%; padding:5px; margin:5px 0; }
</style>
</head>
<body>

<header>
<h2>สปาร์คปลาบอลลูน</h2>
<div class="cart" onclick="openCart()">🛒</div>
</header>

<div class="container">
<h3>สินค้า</h3>
<div class="grid" id="products"></div>
</div>

<div class="modal" id="cartModal">
<div class="modal-content">
<h3>ตะกร้า</h3>
<div id="cartItems"></div>
<p id="total"></p>
<button class="btn" onclick="checkout()">ยืนยัน</button>
</div>
</div>

<script>
let products = [
 {name:"ปลาบอลลูน เรดเฮด", price:100, img:"https://upload.wikimedia.org/wikipedia/commons/6/6e/Goldfish3.jpg"},
 {name:"ปลาบอลลูน สีฟ้า", price:120, img:"https://upload.wikimedia.org/wikipedia/commons/2/25/Fish_tank.jpg"}
];
let cart = [];

function renderProducts(){
let el = document.getElementById('products');
el.innerHTML='';
products.forEach((p,i)=>{
el.innerHTML += `
<div class="card">
<img src="${p.img}">
<h4>${p.name}</h4>
<p>${p.price} บาท</p>
<input type="number" id="qty${i}" value="1">
<button class="btn" onclick="addToCart(${i})">เลือก</button>
</div>`;
});
}

function addToCart(i){
let qty = parseInt(document.getElementById('qty'+i).value);
cart.push({...products[i], qty});
alert('เพิ่มแล้ว');
}

function openCart(){
document.getElementById('cartModal').style.display='flex';
let el = document.getElementById('cartItems');
let total = 0;
el.innerHTML='';
cart.forEach(c=>{
total += c.price * c.qty;
el.innerHTML += `<p>${c.name} x${c.qty}</p>`;
});
document.getElementById('total').innerText = 'รวม: '+total+' บาท';
}

function checkout(){
alert('สั่งซื้อสำเร็จ!');
cart=[];
location.reload();
}

renderProducts();
</script>

</body>
</html>
