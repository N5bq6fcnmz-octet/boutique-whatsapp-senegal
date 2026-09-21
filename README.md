 <!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ma Boutique Sénégal 🇸🇳</title>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: Arial, sans-serif; background: #f5f5f5; color: #222; }
header { background: #111; color: white; padding: 18px 15px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 100; }
header h1 { font-size: 20px; }
#cartButton { background: white; color: #111; border: none; padding: 10px 14px; border-radius: 8px; font-weight: bold; cursor: pointer; }
.hero { background: linear-gradient(135deg, #00853f, #fdef42, #e31b23); padding: 55px 20px; text-align: center; color: white; }
.hero h2 { font-size: 32px; margin-bottom: 15px; }
.hero p { font-size: 17px; margin-bottom: 25px; }
.hero a { display: inline-block; background: #111; color: white; text-decoration: none; padding: 13px 20px; border-radius: 8px; font-weight: bold; }
.container { max-width: 1100px; margin: auto; padding: 35px 15px; }
.section-title { text-align: center; margin-bottom: 25px; font-size: 27px; }
.products { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
.product { background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 3px 12px rgba(0,0,0,0.08); }
.product-image { height: 190px; background: #ddd; display: flex; align-items: center; justify-content: center; font-size: 65px; }
.product-content { padding: 18px; }
.product h3 { margin-bottom: 10px; font-size: 20px; }
.product p { color: #666; margin-bottom: 12px; line-height: 1.5; }
.price { font-size: 20px; font-weight: bold; margin-bottom: 15px; }
.add { width: 100%; border: none; background: #00853f; color: white; padding: 12px; border-radius: 7px; cursor: pointer; font-weight: bold; }
.add:hover { opacity: 0.9; }
#cart { display: none; background: white; margin: 25px auto; max-width: 600px; padding: 20px; border-radius: 12px; box-shadow: 0 3px 15px rgba(0,0,0,0.12); }
#cart h2 { margin-bottom: 15px; }
.cart-item { display: flex; justify-content: space-between; gap: 10px; padding: 12px 0; border-bottom: 1px solid #ddd; }
.remove { background: #e31b23; color: white; border: none; padding: 5px 9px; border-radius: 5px; cursor: pointer; }
.total { font-size: 20px; font-weight: bold; margin: 20px 0; }
.whatsapp { display: block; width: 100%; background: #25D366; color: white; text-align: center; text-decoration: none; padding: 14px; border-radius: 8px; font-weight: bold; border: none; cursor: pointer; font-size: 16px; }
footer { background: #111; color: white; text-align: center; padding: 25px 15px; margin-top: 40px; }
</style>
</head>
<body>

<header>
<h1>🇸🇳 Ma Boutique</h1>
<button id="cartButton" onclick="toggleCart()">🛒 Panier (<span id="cartCount">0</span>)</button>
</header>

<div class="hero">
<h2>Bienvenue dans ma boutique</h2>
<p>Découvrez nos produits et commandez facilement au Sénégal.</p>
<a href="#produits">Voir les produits</a>
</div>

<div class="container" id="produits">
<h2 class="section-title">Nos produits</h2>
<div class="products">
<div class="product"><div class="product-image">👕</div><div class="product-content"><h3>T-shirt tendance</h3><p>Un t-shirt moderne et confortable.</p><div class="price">7 500 FCFA</div><button class="add" onclick="addToCart('T-shirt tendance', 7500)">Ajouter au panier</button></div></div>
<div class="product"><div class="product-image">👟</div><div class="product-content"><h3>Baskets modernes</h3><p>Baskets stylées pour tous les jours.</p><div class="price">20 000 FCFA</div><button class="add" onclick="addToCart('Baskets modernes', 20000)">Ajouter au panier</button></div></div>
<div class="product"><div class="product-image">🎧</div><div class="product-content"><h3>Écouteurs Bluetooth</h3><p>Écouteurs sans fil avec boîtier de recharge.</p><div class="price">12 500 FCFA</div><button class="add" onclick="addToCart('Écouteurs Bluetooth', 12500)">Ajouter au panier</button></div></div>
<div class="product"><div class="product-image">⌚</div><div class="product-content"><h3>Montre connectée</h3><p>Une montre pratique et élégante.</p><div class="price">25 000 FCFA</div><button class="add" onclick="addToCart('Montre connectée', 25000)">Ajouter au panier</button></div></div>
</div>

<div id="cart">
<h2>🛒 Votre panier</h2>
<div id="cartItems"><p>Votre panier est vide.</p></div>
<div class="total">Total : <span id="cartTotal">0</span> FCFA</div>
<button class="whatsapp" onclick="orderWhatsApp()">📱 Commander sur WhatsApp</button>
</div>
</div>

<footer>© 2026 Ma Boutique Sénégal 🇸🇳<br>Commande rapide et simple sur WhatsApp.</footer>

<script>
let cart = [];
function addToCart(name, price) {
  cart.push({ name, price });
  updateCart();
  alert(name + " a été ajouté au panier !");
}
function removeFromCart(index) {
  cart.splice(index, 1);
  updateCart();
}
function updateCart() {
  document.getElementById("cartCount").textContent = cart.length;
  const cartItems = document.getElementById("cartItems");
  cartItems.innerHTML = "";
  let total = 0;
  if(cart.length === 0){
    cartItems.innerHTML = "<p>Votre panier est vide.</p>";
  } else {
    cart.forEach((item, index) => {
      total += item.price;
      const div = document.createElement("div");
      div.className = "cart-item";
      div.innerHTML = `<span>${item.name} - ${item.price.toLocaleString("fr-FR")} FCFA</span> <button class="remove" onclick="removeFromCart(${index})">Supprimer</button>`;
      cartItems.appendChild(div);
    });
  }
  document.getElementById("cartTotal").textContent = total.toLocaleString("fr-FR");
}
function toggleCart() {
  const cartBox = document.getElementById("cart");
  cartBox.style.display = cartBox.style.display === "block" ? "none" : "block";
  if(cartBox.style.display === "block") cartBox.scrollIntoView({ behavior: "smooth" });
}
function orderWhatsApp() {
  if (cart.length === 0) { alert("Votre panier est vide."); return; }
  const numeroWhatsApp = "221764962025";
  let message = "Bonjour Ma Boutique Sénégal 🇸🇳,%0A%0AJe souhaite commander :%0A%0A";
  let total = 0;
  cart.forEach(item => {
    message += "• " + item.name + " - " + item.price.toLocaleString("fr-FR") + " FCFA%0A";
    total += item.price;
  });
  message += "%0ATotal : " + total.toLocaleString("fr-FR") + " FCFA%0A%0AMerci de me confirmer la disponibilité.";
  const url = "https://wa.me/" + numeroWhatsApp + "?text=" + message;
  window.open(url, "_blank");
}
</script>
</body>
</html>
