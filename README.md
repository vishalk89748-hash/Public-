
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#8b2500">
  <title>Daya Kulcha & Dhaba</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #fff8ed;
      color: #342017;
    }
    header {
      background: #8b2500;
      color: white;
      text-align: center;
      padding: 24px 12px;
    }
    header h1 { margin: 0 0 8px; }
    main {
      max-width: 650px;
      margin: auto;
      padding: 20px;
    }
    .item {
      background: white;
      padding: 16px;
      margin: 12px 0;
      border-radius: 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      box-shadow: 0 2px 8px #0000000d;
    }
    button {
      background: #8b2500;
      color: white;
      border: 0;
      border-radius: 8px;
      padding: 12px 16px;
      cursor: pointer;
    }
    #cart {
      background: white;
      padding: 16px;
      border-radius: 12px;
      margin-top: 22px;
    }
  </style>
</head>
<body>
  <header>
    <h1>Daya Kulcha & Dhaba</h1>
    <p>स्वाद ऐसा, जो याद रहे!</p>
  </header>

  <main>
    <h2>हमारा मेन्यू / Our Menu</h2>
    <div id="menu"></div>

    <section id="cart">
      <h2>आपका ऑर्डर</h2>
      <div id="cartItems">अभी कार्ट खाली है।</div>
      <h3>कुल: ₹<span id="total">0</span></h3>
      <button onclick="sendOrder()">WhatsApp पर ऑर्डर करें</button>
      <p id="notice" role="status"></p>
    </section>
  </main>

  <script>
    const products = [
      { name: "आलू कुलचा", price: 40 },
      { name: "पनीर कुलचा", price: 60 },
      { name: "मिक्स कुलचा", price: 50 },
      { name: "प्लेन कुलचा", price: 30 }
    ];

    const cart = {};

    document.getElementById("menu").innerHTML =
      products.map((p, i) => `
        <div class="item">
          <div>
            <strong>${p.name}</strong>
            <p>₹${p.price}</p>
          </div>
          <button onclick="addItem(${i})">जोड़ें +</button>
        </div>
      `).join("");

    function addItem(i) {
      cart[i] = (cart[i] || 0) + 1;
      renderCart();
    }

    function renderCart() {
      const items = Object.keys(cart);
      document.getElementById("cartItems").innerHTML =
        items.length
          ? items.map(i =>
              `${products[i].name} × ${cart[i]} = ₹${products[i].price * cart[i]}`
            ).join("<br>")
          : "अभी कार्ट खाली है।";

      const total = items.reduce(
        (sum, i) => sum + products[i].price * cart[i], 0
      );
      document.getElementById("total").textContent = total;
    }

    function sendOrder() {
      if (!Object.keys(cart).length) {
        document.getElementById("notice").textContent =
          "कृपया पहले मेन्यू से कुछ चुनें।";
        return;
      }

      document.getElementById("notice").textContent =
        "अगले चरण में धाबे का सही WhatsApp नंबर जोड़ना होगा।";
    }
  </script>
</body>
</html>
