<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Esrael Mobile Marketplace</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background-color: #f4f6f9; color: #333; padding-bottom: 60px; }
        
        .navbar { background-color: #1e272e; color: white; padding: 15px 30px; display: flex; justify-content: space-between; align-items: center; }
        .navbar-brand { font-size: 22px; font-weight: bold; color: #ff4757; text-decoration: none; }
        .secure-tag { color: #2ed573; font-size: 14px; font-weight: 600; }

        .hero { background: linear-gradient(135deg, #2f3542, #1e272e); color: white; text-align: center; padding: 50px 20px; }
        .hero h1 { font-size: 36px; margin-bottom: 10px; }
        .hero p { color: #a4b0be; font-size: 16px; }

        .main-layout { display: flex; max-width: 1200px; margin: 30px auto; padding: 0 20px; gap: 30px; }
        .catalog-section { flex: 3; }
        .cart-sidebar { flex: 1; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); height: fit-content; }

        .product-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 20px; }
        .card { background: white; border-radius: 12px; padding: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); display: flex; flex-direction: column; transition: transform 0.2s; }
        .card:hover { transform: translateY(-5px); }
        .card img { width: 100%; height: 150px; object-fit: contain; margin-bottom: 15px; }
        .brand-badge { background: #747d8c; color: white; font-size: 11px; padding: 3px 8px; border-radius: 4px; width: fit-content; margin-bottom: 10px; }
        .card h3 { font-size: 18px; margin-bottom: 8px; }
        .card p { font-size: 13px; color: #57606f; flex-grow: 1; margin-bottom: 15px; }
        
        .price { font-size: 20px; font-weight: bold; color: #2ed573; }
        .btn-buy { background: #ff4757; color: white; border: none; padding: 8px 16px; border-radius: 6px; font-weight: bold; cursor: pointer; }
        .btn-buy:hover { background: #e84118; }
        .btn-checkout { background: #1e272e; color: white; border: none; width: 100%; padding: 12px; border-radius: 6px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 15px; }

        .cart-item { display: flex; justify-content: space-between; align-items: center; background: #f1f2f6; padding: 10px; border-radius: 6px; margin-top: 10px; }
    </style>
</head>
<body>

    <div class="navbar">
        <a class="navbar-brand" href="#">📱 ESRAEL MOBILES</a>
        <div class="secure-tag">✓ SECURE DISPATCH</div>
    </div>

    <div class="hero">
        <h1>Premium Smartphone Store</h1>
        <p>Select a device to test the active shopping cart functionality.</p>
    </div>

    <div class="main-layout">
        <div class="catalog-section">
            <div class="product-grid" id="catalog-grid"></div>
        </div>

        <div class="cart-sidebar">
            <h2 style="font-size: 20px; margin-bottom: 15px;">Your Basket</h2>
            <div id="cart-container">
                <p style="color: #747d8c; text-align: center; padding: 20px 0;">Empty basket.</p>
            </div>
            <div style="display: flex; justify-content: space-between; margin-top: 20px; font-weight: bold; border-top: 2px dashed #f1f2f6; padding-top: 15px;">
                <span>Total:</span>
                <span id="cart-total" style="font-size: 22px; color: #2ed573;">$0.00</span>
            </div>
            <button class="btn-checkout" onclick="checkout()">Checkout</button>
        </div>
    </div>

    <script>
        const products = [
            { id: 1, name: "iPhone 15 Pro", brand: "Apple", price: 999.00, img: "https://images.unsplash.com/photo-1695048133142-1a20484d2569?auto=format&fit=crop&w=300&q=80", desc: "Titanium design with high performance camera systems." },
            { id: 2, name: "Galaxy S24 Ultra", brand: "Samsung", price: 1199.99, img: "https://images.unsplash.com/photo-1610945265064-0e34e5519bbf?auto=format&fit=crop&w=300&q=80", desc: "Built-in S-Pen interface with advanced AI tools." },
            { id: 3, name: "Pixel 8 Pro", brand: "Google", price: 799.00, img: "https://images.unsplash.com/photo-1598327105666-5b89351aff97?auto=format&fit=crop&w=300&q=80", desc: "Pure Android computational software build optimization." }
        ];

        let cart = [];

        function render() {
            const grid = document.getElementById('catalog-grid');
            grid.innerHTML = '';
            products.forEach(p => {
                grid.innerHTML += `
                    <div class="card">
                        <img src="${p.img}">
                        <div class="brand-badge">${p.brand}</div>
                        <h3>${p.name}</h3>
                        <p>${p.desc}</p>
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <span class="price">$${p.price}</span>
                            <button class="btn-buy" onclick="addToCart(${p.id})">Add</button>
                        </div>
                    </div>
                `;
            });
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const exists = cart.find(item => item.id === id);
            if(exists) {
                exists.qty++;
            } else {
                cart.push({...product, qty: 1});
            }
            updateCart();
        }

        function updateCart() {
            const container = document.getElementById('cart-container');
            const totalElement = document.getElementById('cart-total');
            container.innerHTML = '';
            
            if(cart.length === 0) {
                container.innerHTML = '<p style="color: #747d8c; text-align: center; padding: 20px 0;">Empty basket.</p>';
                totalElement.innerText = '$0.00';
                return;
            }

            let grandTotal = 0;
            cart.forEach(item => {
                grandTotal += item.price * item.qty;
                container.innerHTML += `
                    <div class="cart-item">
                        <div>
                            <strong>${item.name}</strong><br>
                            <small style="color: #57606f;">$${item.price} x ${item.qty}</small>
                        </div>
                        <span style="font-weight: bold;">$${(item.price * item.qty).toFixed(2)}</span>
                    </div>
                `;
            });
            totalElement.innerText = '$' + grandTotal.toFixed(2);
        }

        function checkout() {
            if(cart.length === 0) return alert("Basket is empty!");
            alert("Order completed successfully!");
            cart = [];
            updateCart();
        }

        render();
    </script>
</body>
</html>
