<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>جلد وورق | Handmade Leather & Paper</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cairo', sans-serif; }
        body { background-color: #fdfaf6; color: #3e2c1c; }
        
        /* Header */
        header {
            background: #fff; padding: 20px 8%; display: flex; justify-content: space-between;
            align-items: center; box-shadow: 0 2px 10px rgba(0,0,0,0.05); position: sticky; top: 0; z-index: 100;
        }
        .logo { font-size: 1.8rem; font-weight: 900; color: #8b5e3c; }
        nav a { margin: 0 15px; text-decoration: none; color: #3e2c1c; font-weight: 700; transition: 0.3s; }
        nav a:hover { color: #c49a6c; }
        .cart-icon { cursor: pointer; font-weight: 700; background: #8b5e3c; color: #fff; padding: 8px 15px; border-radius: 20px; }

        /* Hero */
        .hero {
            height: 70vh; display: flex; align-items: center; justify-content: center; text-align: center;
            background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), url('https://images.unsplash.com/photo-1544816155-12df9643f363?q=80&w=1600&auto=format&fit=crop') center/cover;
            color: #fff;
        }
        .hero h1 { font-size: 3.5rem; margin-bottom: 15px; }
        .hero p { font-size: 1.2rem; margin-bottom: 25px; }
        .btn { background: #c49a6c; color: #fff; padding: 12px 30px; border: none; border-radius: 5px; font-size: 1rem; cursor: pointer; transition: 0.3s; text-decoration: none; display: inline-block; }
        .btn:hover { background: #8b5e3c; }

        /* Sections */
        .section-title { text-align: center; font-size: 2.5rem; margin: 50px 0 30px; color: #8b5e3c; }
        .products-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; padding: 0 8% 60px; }
        
        .product-card {
            background: #fff; border-radius: 10px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            transition: 0.3s; text-align: center;
        }
        .product-card:hover { transform: translateY(-5px); box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .product-img { width: 100%; height: 250px; object-fit: cover; }
        .product-info { padding: 20px; }
        .product-info h3 { font-size: 1.3rem; margin-bottom: 10px; }
        .price { color: #c49a6c; font-weight: 900; font-size: 1.2rem; margin-bottom: 15px; display: block; }
        .add-to-cart { background: #3e2c1c; color: #fff; padding: 10px 20px; border: none; border-radius: 5px; cursor: pointer; font-weight: 700; width: 100%; transition: 0.3s; }
        .add-to-cart:hover { background: #8b5e3c; }

        /* Cart Modal */
        .cart-modal {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5); justify-content: center; align-items: center; z-index: 200;
        }
        .cart-content { background: #fff; padding: 30px; border-radius: 10px; width: 90%; max-width: 500px; max-height: 80vh; overflow-y: auto; }
        .cart-content h2 { margin-bottom: 20px; color: #8b5e3c; }
        .cart-item { display: flex; justify-content: space-between; margin-bottom: 15px; border-bottom: 1px solid #eee; padding-bottom: 10px; }
        .cart-total { margin-top: 20px; font-weight: 900; font-size: 1.2rem; text-align: left; }
        .close-cart { background: #e74c3c; color: #fff; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer; margin-top: 15px; width: 100%; }

        /* Footer */
        footer { background: #3e2c1c; color: #fff; text-align: center; padding: 30px; }
        
        @media (max-width: 768px) {
            .hero h1 { font-size: 2.5rem; }
            nav { display: none; }
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="logo">جلد وورق</div>
        <nav>
            <a href="#notebooks">الدفاتر</a>
            <a href="#leather">الإكسسوارات الجلدية</a>
            <a href="#paper">الورق</a>
        </nav>
        <div class="cart-icon" onclick="toggleCart()">🛒 السلة (<span id="cart-count">0</span>)</div>
    </header>

    <!-- Hero -->
    <section class="hero">
        <div>
            <h1>فن الجلد الطبيعي</h1>
            <p>دفاتر وإكسسوارات مصنوعة يدوياً بحب</p>
            <a href="#notebooks" class="btn">تسوق الآن</a>
        </div>
    </section>

    <!-- Section 1: Notebooks -->
    <h2 class="section-title" id="notebooks">الدفاتر</h2>
    <div class="products-grid" id="notebooks-grid">
        <!-- Products will be injected here via JS -->
    </div>

    <!-- Section 2: Leather Accessories -->
    <h2 class="section-title" id="leather">الإكسسوارات الجلدية</h2>
    <div class="products-grid" id="leather-grid"></div>

    <!-- Section 3: Paper -->
    <h2 class="section-title" id="paper">الورق</h2>
    <div class="products-grid" id="paper-grid"></div>

    <!-- Cart Modal -->
    <div class="cart-modal" id="cartModal">
        <div class="cart-content">
            <h2>سلة المشتريات</h2>
            <div id="cart-items"></div>
            <div class="cart-total" id="cart-total">الإجمالي: 0 ج.م</div>
            <button class="close-cart" onclick="toggleCart()">إغلاق</button>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <p>© 2024 جلد وورق - جميع الحقوق محفوظة. صنع يدوياً بحب.</p>
    </footer>

    <script>
        // بيانات المنتجات (يمكنك تعديلها بسهولة)
        const products = {
            notebooks: [
                { id: 1, name: "دفتر جلدي بنجمة البحر", price: 250, img: "https://images.unsplash.com/photo-1531346878377-a5be20888e57?q=80&w=600&auto=format&fit=crop" },
                { id: 2, name: "دفتر جلدي كلاسيك", price: 200, img: "https://images.unsplash.com/photo-1544816155-12df9643f363?q=80&w=600&auto=format&fit=crop" },
                { id: 3, name: "دفتر مرصع باليد", price: 300, img: "https://images.unsplash.com/photo-1517842645767-c639042777db?q=80&w=600&auto=format&fit=crop" }
            ],
            leather: [
                { id: 4, name: "محفظة جلد طبيعي", price: 150, img: "https://images.unsplash.com/photo-1627123424574-724758594e93?q=80&w=600&auto=format&fit=crop" },
                { id: 5, name: "حزام جلد كلاسيك", price: 180, img: "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?q=80&w=600&auto=format&fit=crop" }
            ],
            paper: [
                { id: 6, name: "ورق مقوى مزخرف", price: 50, img: "https://images.unsplash.com/photo-1586075010923-2dd4570fb338?q=80&w=600&auto=format&fit=crop" },
                { id: 7, name: "كروت معايدة يدوية", price: 30, img: "https://images.unsplash.com/photo-1607344645866-009c320b63e0?q=80&w=600&auto=format&fit=crop" }
            ]
        };

        let cart = [];

        // دالة عرض المنتجات
        function renderProducts(category, containerId) {
            const container = document.getElementById(containerId);
            container.innerHTML = products[category].map(p => `
                <div class="product-card">
                    <img src="${p.img}" alt="${p.name}" class="product-img">
                    <div class="product-info">
                        <h3>${p.name}</h3>
                        <span class="price">${p.price} ج.م</span>
                        <button class="add-to-cart" onclick="addToCart(${p.id}, '${p.name}', ${p.price})">أضف للسلة</button>
                    </div>
                </div>
            `).join('');
        }

        // دالة إضافة للسلة
        function addToCart(id, name, price) {
            const existing = cart.find(item => item.id === id);
            if (existing) {
                existing.qty += 1;
            } else {
                cart.push({ id, name, price, qty: 1 });
            }
            updateCart();
        }

        // تحديث السلة
        function updateCart() {
            document.getElementById('cart-count').innerText = cart.reduce((sum, item) => sum + item.qty, 0);
            
            const cartItemsDiv = document.getElementById('cart-items');
            const totalDiv = document.getElementById('cart-total');
            
            if (cart.length === 0) {
                cartItemsDiv.innerHTML = '<p style="text-align:center; color:#888;">السلة فاضية</p>';
                totalDiv.innerText = 'الإجمالي: 0 ج.م';
                return;
            }

            let total = 0;
            cartItemsDiv.innerHTML = cart.map(item => {
                total += item.price * item.qty;
                return `
                    <div class="cart-item">
                        <span>${item.name} (x${item.qty})</span>
                        <span>${item.price * item.qty} ج.م</span>
                    </div>
                `;
            }).join('');
            totalDiv.innerText = `الإجمالي: ${total} ج.م`;
        }

        // فتح/إغلاق السلة
        function toggleCart() {
            const modal = document.getElementById('cartModal');
            modal.style.display = modal.style.display === 'flex' ? 'none' : 'flex';
        }

        // تشغيل عند تحميل الصفحة
        window.onload = () => {
            renderProducts('notebooks', 'notebooks-grid');
            renderProducts('leather', 'leather-grid');
            renderProducts('paper', 'paper-grid');
        };
    </script>
</body>
</html>
