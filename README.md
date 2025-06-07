# QUICK-PICK-LADAKH-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Quick Pick Ladakh - Admin Panel</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #fffaf5;
      color: #333;
      margin: 0;
      padding: 1rem;
    }
    header {
      background-color: #ff6600;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 1rem;
    }
    th, td {
      border: 1px solid #ffb366;
      padding: 0.5rem;
      text-align: left;
    }
    th {
      background-color: #ff6600;
      color: white;
    }
    select {
      padding: 0.3rem;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <header>
    <h1>Quick Pick Ladakh - Admin Panel</h1>
  </header>
  <main>
    <h2>Orders</h2>
    <table id="ordersTable">
      <thead>
        <tr>
          <th>User</th>
          <th>Date</th>
          <th>Address</th>
          <th>Phone</th>
          <th>Items</th>
          <th>Status</th>
          <th>Update Status</th>
        </tr>
      </thead>
      <tbody>
        <!-- Orders will load here -->
      </tbody>
    </table>
  </main>

  <script>
    const statusOptions = ["Pending", "Packed", "Out for Delivery", "Delivered"];

    function loadOrders() {
      const orders = JSON.parse(localStorage.getItem('qp_orders')) || [];
      const tbody = document.querySelector('#ordersTable tbody');
      tbody.innerHTML = '';

      if (orders.length === 0) {
        tbody.innerHTML = '<tr><td colspan="7" style="text-align:center;">No orders found.</td></tr>';
        return;
      }

      orders.forEach((order, index) => {
        const tr = document.createElement('tr');

        const itemsList = order.cart.map(item => `${item.name} (${item.price})`).join(', ');

        // Current status or default to Pending
        const currentStatus = order.status || "Pending";

        tr.innerHTML = `
          <td>${order.user}</td>
          <td>${order.date}</td>
          <td>${order.address}</td>
          <td>${order.phone}</td>
          <td>${itemsList}</td>
          <td id="status-${index}">${currentStatus}</td>
          <td>
            <select onchange="updateStatus(${index}, this.value)">
              ${statusOptions.map(s => `<option value="${s}" ${s === currentStatus ? "selected" : ""}>${s}</option>`).join('')}
            </select>
          </td>
        `;

        tbody.appendChild(tr);
      });
    }

    function updateStatus(index, newStatus) {
      const orders = JSON.parse(localStorage.getItem('qp_orders')) || [];
      if (orders[index]) {
        orders[index].status = newStatus;
        localStorage.setItem('qp_orders', JSON.stringify(orders));
        document.getElementById(`status-${index}`).innerText = newStatus;
        alert(`Order status updated to "${newStatus}"`);
      }
    }

    loadOrders();
  </script>
</body>
</html>
