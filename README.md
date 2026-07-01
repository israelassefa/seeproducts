<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Esrael Mobile Marketplace</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { background-color: #f8f9fa; }
        .navbar-brand { font-weight: bold; color: #ff4757 !important; }
        .card { border: none; box-shadow: 0 4px 10px rgba(0,0,0,0.05); transition: 0.3s; }
        .card:hover { transform: translateY(-5px); box-shadow: 0 6px 15px rgba(0,0,0,0.1); }
        .btn-buy { background-color: #ff4757; color: white; border: none; }
        .btn-buy:hover { background-color: #e84118; color: white; }
    </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="#">📱 ESRAEL MOBILES</a>
            <span class="navbar-text text-white-50">Static GitHub Shop Demonstration</span>
        </div>
    </nav>

    <div class="container my-5">
        <h2 class="text-center mb-4">Latest Smartphones Available</h2>
        <div class="row g-4" id="product-container">
            </div>
    </div>

    <script>
        // Simulating the Python database directly inside the browser storage environment
        const mobiles = [
            {
                name: "iPhone 15 Pro",
                brand: "Apple",
                price: 999.00,
                image_url: "https://images.unsplash.com/photo-1695048133142-1a20484d2569?auto=format&fit=crop&w=300&q=80",
                description: "Titanium design, A17 Pro chip, customizable Action button, and a powerful camera system."
            },
            {
                name: "Galaxy S24 Ultra",
                brand: "Samsung",
                price: 1199.99,
                image_url: "https://images.unsplash.com/photo-1610945265064-0e34e5519bbf?auto=format&fit=crop&w=300&q=80",
                description: "Built-in S Pen, advanced Galaxy AI integration, 200MP camera lens, and ultra-durable frame."
            },
            {
                name: "Pixel 8 Pro",
                brand: "Google",
                price: 799.00,
                image_url: "https://images.unsplash.com/photo-1598327105666-5b89351aff97?auto=format&fit=crop&w=300&q=80",
                description: "Pure Android experience, Tensor G3 chip, advanced computational AI photography tools."
            }
        ];

        const container = document.getElementById('product-container');
        
        mobiles.forEach(mobile => {
            container.innerHTML += `
                <div class="col-md-4">
                    <div class="card h-100">
                        <img src="${mobile.image_url}" class="card-img-top p-3" alt="${mobile.name}" style="max-height: 250px; object-fit: contain;">
                        <div class="card-body d-flex flex-column">
                            <h5 class="card-title">${mobile.name}</h5>
                            <p class="text-muted small mb-1">Brand: ${mobile.brand}</p>
                            <p class="card-text text-secondary flex-grow-1">${mobile.description}</p>
                            <div class="d-flex justify-content-between align-items-center mt-3">
                                <span class="fs-4 fw-bold text-dark">$${mobile.price.toFixed(2)}</span>
                                <button class="btn btn-buy px-4" onclick="alert('Order request simulation completed for ${mobile.name}!')">Buy Now</button>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        });
    </script>
</body>
</html>
