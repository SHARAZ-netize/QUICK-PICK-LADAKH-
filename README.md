# QUICK-PICK-LADAKH-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Quick Pick Ladakh</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #fff;
      color: #333;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }
    header {
      background: #ff6600; /* bright orange */
      color: white;
      padding: 1rem;
      text-align: center;
      font-size: 1.8rem;
      font-weight: bold;
    }
    nav {
      display: flex;
      justify-content: center;
      background: #fff3e0; /* light orange tint */
      border-bottom: 2px solid #ff6600;
      gap: 1rem;
      flex-wrap: wrap;
      padding: 0.5rem 0;
    }
    nav button {
      background: #ff6600;
      color: white;
      border: none;
      padding: 0.6rem 1.2rem;
      cursor: pointer;
      font-weight: bold;
      border-radius: 5px;
      transition: background 0.3s ease;
      font-size: 1rem;
    }
    nav button:hover, nav button.active {
      background: #e65c00;
    }
    main {
      flex-grow: 1;
      padding: 1rem;
      background: #fff;
    }
    .hidden {
      display: none;
    }
    .products {
      display: grid;
      grid-template-columns: repeat(auto-fill,minmax(180px,1fr));
      gap: 1rem;
    }
    .product {
      border: 1px solid #ddd;
      border-radius: 6px;
      padding: 1rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      background: #fff8f0;
    }
    .product img {
      max-width: 100%;
      height: 120px;
      object-fit: contain;
      margin-bottom: 0.8rem;
    }
    .product h3 {
      margin: 0.2rem 0;
      font-size: 1.1rem;
      color: #ff6600;
      text-align: center;
    }
    .product p {
      margin: 0.2rem 0 0.8rem;
      font-weight: bold;
      color: #555;
    }
    .product button {
      background: #ff6600;
      border: none;
      color: white;
      padding: 0.5rem 1rem;
      cursor: pointer;
      border-radius: 4px;
      font-weight: bold;
      transition: background 0.3s ease;
    }
    .product button:hover {
      background: #e65c00;
    }
    .cart-items, .orders-list {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    .cart-item, .order-item {
      border-bottom: 1px solid #ddd;
      padding: 0.5rem 0;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .cart-item span, .order-item span {
      flex-grow: 1;
    }
    .action-btn {
      background: #ff6600;
      border: none;
      color: white;
      padding: 0.3rem 0.7rem;
      cursor: pointer;
      border-radius: 4px;
      font-weight: bold;
      margin-left: 0.5rem;
      transition: background 0.3s ease;
      font-size: 0.9rem;
    }
    .action-btn:hover {
      background: #e65c00;
    }
    form {
      max-width: 400px;
      margin: auto;
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
    }
    form input, form select {
      padding: 0.5rem;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    form button {
      background: #ff6600;
      color: white;
      border: none;
      padding: 0.7rem;
      font-size: 1.1rem;
      cursor: pointer;
      border-radius: 5px;
      font-weight: bold;
      transition: background 0.3s ease;
    }
    form button:hover {
      background: #e65c00;
    }
    footer {
      background: #ff6600;
      color: white;
      text-align: center;
      padding: 0.7rem;
      font-size: 0.9rem;
    }

    /* Mobile Responsive */
    @media (max-width: 600px) {
      nav {
        flex-direction: column;
        gap: 0.5rem;
        padding: 0.5rem;
      }
      nav button {
        width: 100%;
        font-size: 1.2rem;
      }
      .products {
        grid-template-columns: 1fr;
      }
      .product {
        padding: 1rem;
      }
      input, select, button.action-btn, form button {
        font-size: 1.1rem;
      }
    }
  </style>
</head>
<body>

<header>QUICK PICK LADAKH</header>

<nav>
  <button class="tab-btn active" data-tab="login">Login</button>
  <button class="tab-btn" data-tab="home">Home</button>
  <button class="tab-btn" data-tab="cart">Cart</button>
  <button class="tab-btn" data-tab="checkout">Checkout</button>
  <button class="tab-btn" data-tab="orders">My Orders</button>
  <button class="tab-btn" data-tab="admin">Admin Panel</button>
</nav>

<main>
  <!-- Login -->
  <section id="login" class="tab-content">
    <form id="login-form">
      <input type="text" id="username" placeholder="Enter your name" required />
      <button type="submit">Login</button>
    </form>
  </section>

  <!-- Home -->
  <section id="home" class="tab-content hidden">
    <div class="products" id="product-list">
      <!-- Products injected by JS -->
    </div>
  </section>

  <!-- Cart -->
  <section id="cart" class="tab-content hidden">
    <ul class="cart-items" id="cart-items"></ul>
    <p id="cart-empty-msg">Your cart is empty.</p>
  </section>

  <!-- Checkout -->
  <section id="checkout" class="tab-content hidden">
    <form id="checkout-form">
      <input type="text" id="address" placeholder="Delivery Address" required />
      <input type="tel" id="phone" placeholder="Phone Number" required />
      <button type="submit">Place Order</button>
    </form>
  </section>

  <!-- My Orders -->
  <section id="orders" class="tab-content hidden">
    <ul class="orders-list" id="orders-list"></ul>
    <p id="orders-empty-msg">You have no orders yet.</p>
  </section>

  <!-- Admin Panel -->
  <section id="admin" class="tab-content hidden">
    <h2>All Orders</h2>
    <ul class="orders-list" id="admin-orders-list"></ul>
    <p id="admin-orders-empty-msg">No orders yet.</p>
  </section>
</main>

<footer>© 2025 Quick Pick Ladakh</footer>

<script>
  // Sample product data
  const products = [
    {id: 1, name: "Apples", price: 50, img: "https://via.placeholder.com/150?text=Apples"},
    {id: 2, name: "Bananas", price: 30, img: "https://via.placeholder.com/150?text=Bananas"},
    {id: 3, name: "Carrots", price: 40, img: "https://via.placeholder.com/150?text=Carrots"},
    {id: 4, name: "Tomatoes", price: 35, img: "https://via.placeholder.com/150?text=Tomatoes"},
    {id: 5, name: "Potatoes", price: 25, img: "https://via.placeholder.com/150?text=Potatoes"}
  ];

  let currentUser = null;

  // Utility functions for localStorage
  function saveData(key, data) {
    localStorage.setItem(key, JSON.stringify(data));
  }
  function loadData(key) {
    const data = localStorage.getItem(key);
    return data ? JSON.parse(data) : null;
  }

  // Manage tabs
  const tabButtons = document.querySelectorAll('nav .tab-btn');
  const tabContents = document.querySelectorAll('main .tab-content');
  function switchTab(tabName) {
    tabButtons.forEach(btn => {
      btn.classList.toggle('active', btn.dataset.tab === tabName);
    });
    tabContents.forEach(section => {
      section.classList.toggle('hidden', section.id !== tabName);
    });
  }
  tabButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      switchTab(btn.dataset.tab);
      if (btn.dataset.tab === 'home') renderProducts();
      if (btn.dataset.tab === 'cart') renderCart();
      if (btn.dataset.tab === 'orders') renderOrders();
      if (btn.dataset.tab === 'admin') renderAdminOrders();
    });
  });

  // Login form
  document.getElementById('login-form').addEventListener('submit', e => {
    e.preventDefault();
    const usernameInput = document.getElementById('username');
    currentUser = usernameInput.value.trim();
    if (currentUser) {
      alert(`Welcome, ${currentUser}!`);
      saveData('currentUser', currentUser);
      usernameInput.value = '';
      switchTab('home');
    }
  });

  // Load current user from localStorage on page load
  window.addEventListener('load', () => {
    currentUser = loadData('currentUser');
    if (currentUser) {
      switchTab('home');
    }
  });

  // Render products
  function renderProducts() {
    const productList = document.getElementById('product-list');
    productList.innerHTML = '';
    products.forEach(p => {
      const div = document.createElement('div');
      div.className = 'product';
      div.innerHTML = `
        <img src="${p.img}" alt="${p.name}" />
        <h3>${p.name}</h3>
        <p>₹${p.price}</p>
        <button data-id="${p.id}">Add to Cart</button>
      `;
      div.querySelector('button').addEventListener('click', () => {
        addToCart(p.id);
      });
      productList.appendChild(div);
    });
  }

  // Cart functions
  function getCart() {
    const cart = loadData(`cart_${currentUser}`);
    return cart ? cart : [];
  }
  function saveCart(cart) {
    saveData(`cart_${currentUser}`, cart);
  }
  function addToCart(productId) {
    let cart = getCart();
    const existing = cart.find(item => item.productId === productId);
    if (existing) {
      existing.quantity++;
    } else {
      cart.push({productId, quantity: 1});
    }
    saveCart(cart);
    alert("Added to cart!");
  }
  function renderCart() {
    const cartItems = document.getElementById('cart-items');
    const cartEmptyMsg = document.getElementById('cart-empty-msg');
    const cart = getCart();
    cartItems.innerHTML = '';

    if (cart.length === 0) {
      cartEmptyMsg.style.display = 'block';
      return;
    } else {
      cartEmptyMsg.style.display = 'none';
    }

    cart.forEach(item => {
      const product = products.find(p => p.id === item.productId);
      const li = document.createElement('li');
      li.className = 'cart-item';
      li.innerHTML = `
        <span>${product.name} x ${item.quantity}</span>
        <button class="action-btn" data-id="${item.productId}">Remove</button>
      `;
      li.querySelector('button').addEventListener('click', () => {
        removeFromCart(item.productId);
      });
      cartItems.appendChild(li);
    });
  }
  function removeFromCart(productId) {
    let cart = getCart();
    cart = cart.filter(item => item.productId !== productId);
    saveCart(cart);
    renderCart();
  }

  // Checkout
  document.getElementById('checkout-form').addEventListener('submit', e => {
    e.preventDefault();
    const address = document.getElementById('address').value.trim();
    const phone = document.getElementById('phone').value.trim();
    const cart = getCart();

    if (!address || !phone || cart.length === 0) {
      alert("Please fill all fields and add items to your cart.");
      return;
    }

    // Save order
    const orders = loadData('orders') || [];
    const newOrder = {
      id: Date.now(),
      user: currentUser,
      items: cart,
      address,
      phone,
      status: "Pending",
      timestamp: new Date().toISOString()
    };
    orders.push(newOrder);
    saveData('orders', orders);

    // Clear user cart
    saveCart([]);

    alert("Order placed successfully!");
    document.getElementById('checkout-form').reset();
    switchTab('orders');
    renderOrders();
  });

  // Render user orders
  function renderOrders() {
    const ordersList = document.getElementById('orders-list');
    const ordersEmptyMsg = document.getElementById('orders-empty-msg');
    const orders = loadData('orders') || [];
    const userOrders = orders.filter(o => o.user === currentUser);

    ordersList.innerHTML = '';

    if (userOrders.length === 0) {
      ordersEmptyMsg.style.display = 'block';
      return;
    } else {
      ordersEmptyMsg.style.display = 'none';
    }

    userOrders.forEach(order => {
      const li = document.createElement('li');
      li.className = 'order-item';
      li.innerHTML = `
        <span>Order #${order.id} - ${order.status}</span>
        <button class="action-btn" data-id="${order.id}">Details</button>
      `;
      li.querySelector('button').addEventListener('click', () => {
        alert(
          `Order Details:\n\n` +
          `Items:\n` + order.items.map(i => {
            const prod = products.find(p => p.id === i.productId);
            return `${prod.name} x ${i.quantity}`;
          }).join('\n') + `\n\n` +
          `Address: ${order.address}\n` +
          `Phone: ${order.phone}\n` +
          `Status: ${order.status}`
        );
      });
      ordersList.appendChild(li);
    });
  }

  // Admin panel
  function renderAdminOrders() {
    const adminOrdersList = document.getElementById('admin-orders-list');
    const adminOrdersEmptyMsg = document.getElementById('admin-orders-empty-msg');
    const orders = loadData('orders') || [];

    adminOrdersList.innerHTML = '';

    if (orders.length === 0) {
      adminOrdersEmptyMsg.style.display = 'block';
      return;
    } else {
      adminOrdersEmptyMsg.style.display = 'none';
    }

    orders.forEach(order => {
      const li = document.createElement('li');
      li.className = 'order-item';
      li.innerHTML = `
        <span>Order #${order.id} by ${order.user} - Status: ${order.status}</span>
        <select data-id="${order.id}">
          <option value="Pending" ${order.status === "Pending" ? "selected" : ""}>Pending</option>
          <option value="Packed" ${order.status === "Packed" ? "selected" : ""}>Packed</option>
          <option value="Out for Delivery" ${order.status === "Out for Delivery" ? "selected" : ""}>Out for Delivery</option>
          <option value="Delivered" ${order.status === "Delivered" ? "selected" : ""}>Delivered</option>
        </select>
      `;
      li.querySelector('select').addEventListener('change', (e) => {
        updateOrderStatus(order.id, e.target.value);
      });
      adminOrdersList.appendChild(li);
    });
  }

  function updateOrderStatus(orderId, newStatus) {
    const orders = loadData('orders') || [];
    const orderIndex = orders.findIndex(o => o.id === orderId);
    if (orderIndex > -1) {
      orders[orderIndex].status = newStatus;
      saveData('orders', orders);
      alert(`Order #${orderId} status updated to ${newStatus}`);
      renderOrders();
      renderAdminOrders();
    }
  }
</script>

</body>
</html>
