<img width="980" height="980" alt="image" src="https://github.com/user-attachments/assets/0ba561fc-d3b4-43e6-a02f-6e74b7bd5793" /><img width="225" height="225" alt="image" src="https://github.com/user-attachments/assets/6a60ea1e-b673-47da-b6bf-447302a1d14c" /><!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DigiStore | Premium Software Subscriptions</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#6366f1',
                        secondary: '#a855f7',
                        darkBg: '#0f172a',
                        cardBg: '#1e293b'
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a; 
        }
        ::-webkit-scrollbar-thumb {
            background: #334155; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569; 
        }

        .glass-nav {
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .product-card {
            background: linear-gradient(145deg, #1e293b, #0f172a);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }

        .product-card:hover {
            transform: translateY(-5px);
            border-color: rgba(99, 102, 241, 0.5);
            box-shadow: 0 10px 30px -10px rgba(99, 102, 241, 0.3);
        }

        .gradient-text {
            background: linear-gradient(to right, #818cf8, #c084fc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Toast Animation */
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; }
        }
        .toast-enter {
            animation: slideIn 0.3s forwards;
        }
        .toast-exit {
            animation: fadeOut 0.3s forwards;
        }
    </style>
</head>
<body class="antialiased min-h-screen flex flex-col relative overflow-x-hidden">

    <!-- Navigation -->
    <nav class="glass-nav fixed w-full z-50 top-0 transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo -->
                <div class="flex items-center gap-2 cursor-pointer">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center shadow-lg shadow-indigo-500/30">
                        <i data-lucide="layers" class="text-white w-6 h-6"></i>
                    </div>
                    <span class="font-bold text-2xl tracking-tight">Digi<span class="text-indigo-400">Store</span></span>
                </div>

                <!-- Search Bar (Desktop) -->
                <div class="hidden md:flex flex-1 max-w-md mx-8 relative">
                    <i data-lucide="search" class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-5 h-5"></i>
                    <input type="text" id="searchInput" placeholder="Search for software, AI, tools..." 
                           class="w-full bg-slate-800/50 border border-slate-700 text-white rounded-full py-2.5 pl-10 pr-4 focus:outline-none focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500 transition-colors">
                </div>

                <!-- Cart & Actions -->
                <div class="flex items-center gap-4">
                    <button id="cartBtn" class="relative p-2 text-slate-300 hover:text-white transition-colors">
                        <i data-lucide="shopping-cart" class="w-6 h-6"></i>
                        <span id="cartBadge" class="absolute top-0 right-0 -mt-1 -mr-1 bg-indigo-500 text-white text-xs font-bold w-5 h-5 rounded-full flex items-center justify-center transform scale-0 transition-transform duration-200">0</span>
                    </button>
                    <div id="authContainer" class="hidden sm:block">
                        <button onclick="openAuthModal()" class="bg-white text-slate-900 px-5 py-2.5 rounded-full font-semibold hover:bg-slate-200 transition-colors">
                            Sign In
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- Search Bar (Mobile) -->
            <div class="md:hidden pb-4">
                <div class="relative">
                    <i data-lucide="search" class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-4 h-4"></i>
                    <input type="text" id="mobileSearchInput" placeholder="Search products..." 
                           class="w-full bg-slate-800 border border-slate-700 text-white rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-indigo-500 text-sm">
                </div>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <main class="flex-grow pt-28 pb-16 md:pt-36 lg:pb-24">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-3xl mx-auto mb-16">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 text-sm font-medium mb-6">
                    <span class="w-2 h-2 rounded-full bg-indigo-500 animate-pulse"></span>
                    Instant Delivery on All Subscriptions
                </div>
                <h1 class="text-4xl md:text-6xl font-extrabold tracking-tight mb-6 leading-tight">
                    Elevate Your Workflow with <span class="gradient-text">Premium Tools</span>
                </h1>
                <p class="text-lg md:text-xl text-slate-400 mb-8">
                    Get instant access to top-tier AI models, design software, and educational platforms at unbeatable prices. Enhance your productivity today.
                </p>
                
                <!-- Category Pills -->
                <div class="flex flex-wrap justify-center gap-3" id="categoryFilter">
                    <button class="px-4 py-2 rounded-full bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition category-btn active" data-category="all">All Products</button>
                    <button class="px-4 py-2 rounded-full bg-slate-800 text-slate-300 text-sm font-medium hover:bg-slate-700 transition category-btn border border-slate-700" data-category="ai">AI Assistants</button>
                    <button class="px-4 py-2 rounded-full bg-slate-800 text-slate-300 text-sm font-medium hover:bg-slate-700 transition category-btn border border-slate-700" data-category="creative">Creative Tools</button>
                    <button class="px-4 py-2 rounded-full bg-slate-800 text-slate-300 text-sm font-medium hover:bg-slate-700 transition category-btn border border-slate-700" data-category="learning">Learning</button>
                </div>
            </div>

            <!-- Product Grid -->
            <div id="productGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                <!-- Products will be injected here via JS -->
            </div>

            <!-- Empty State for Search -->
            <div id="emptyState" class="hidden flex-col items-center justify-center py-20 text-center">
                <i data-lucide="package-open" class="w-16 h-16 text-slate-600 mb-4"></i>
                <h3 class="text-xl font-semibold text-white mb-2">No products found</h3>
                <p class="text-slate-400">Try adjusting your search terms or filters.</p>
            </div>
        </div>
    </main>

    <!-- Footer -->
    <footer class="border-t border-slate-800 bg-slate-900/50 pt-16 pb-8">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
                <div class="col-span-1 md:col-span-2">
                    <div class="flex items-center gap-2 mb-4">
                        <i data-lucide="layers" class="text-indigo-500 w-6 h-6"></i>
                        <span class="font-bold text-xl">DigiStore</span>
                    </div>
                    <p class="text-slate-400 max-w-sm mb-6">Your premier destination for digital subscriptions, software licenses, and AI tools. Instant delivery, guaranteed.</p>
                    <div class="flex gap-4">
                        <a href="#" class="text-slate-400 hover:text-white transition"><i data-lucide="twitter" class="w-5 h-5"></i></a>
                        <a href="#" class="text-slate-400 hover:text-white transition"><i data-lucide="github" class="w-5 h-5"></i></a>
                        <a href="#" class="text-slate-400 hover:text-white transition"><i data-lucide="linkedin" class="w-5 h-5"></i></a>
                    </div>
                </div>
                <div>
                    <h4 class="text-white font-semibold mb-4">Store</h4>
                    <ul class="space-y-2 text-sm text-slate-400">
                        <li><a href="#" class="hover:text-indigo-400 transition">All Products</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">AI Tools</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">Design Software</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">Online Courses</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-white font-semibold mb-4">Support</h4>
                    <ul class="space-y-2 text-sm text-slate-400">
                        <li><a href="#" class="hover:text-indigo-400 transition">Help Center</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">Terms of Service</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">Privacy Policy</a></li>
                        <li><a href="#" class="hover:text-indigo-400 transition">Contact Us</a></li>
                    </ul>
                </div>
            </div>
            <div class="border-t border-slate-800 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-sm text-slate-500">
                <p>&copy; 2026 DigiStore Inc. All rights reserved.</p>
                <div class="flex items-center gap-2">
                    <span>Secure payments by</span>
                    <i data-lucide="credit-card" class="w-4 h-4"></i>
                </div>
            </div>
        </div>
    </footer>

    <!-- Cart Drawer Modal -->
    <div id="cartOverlay" class="fixed inset-0 bg-black/60 backdrop-blur-sm z- hidden transition-opacity duration-300 opacity-0"></div>
    <div id="cartDrawer" class="fixed top-0 right-0 h-full w-full sm:w-[400px] bg-slate-900 border-l border-slate-800 z- transform translate-x-full transition-transform duration-300 flex flex-col shadow-2xl">
        <!-- Cart Header -->
        <div class="p-6 border-b border-slate-800 flex justify-between items-center bg-slate-900">
            <h2 class="text-xl font-bold flex items-center gap-2">
                <i data-lucide="shopping-bag" class="w-5 h-5 text-indigo-400"></i>
                Your Cart
            </h2>
            <button id="closeCartBtn" class="text-slate-400 hover:text-white transition p-2 bg-slate-800 rounded-full hover:bg-slate-700">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>
        </div>

        <!-- Cart Items Container -->
        <div id="cartItemsContainer" class="flex-grow overflow-y-auto p-6 space-y-4">
            <!-- Items injected by JS -->
        </div>

        <!-- Cart Footer / Checkout -->
        <div class="p-6 border-t border-slate-800 bg-slate-900/90 backdrop-blur">
            <div class="flex justify-between items-center mb-2 text-slate-400">
                <span>Subtotal</span>
                <span id="cartSubtotal" class="font-medium text-white">$0.00</span>
            </div>
            <div class="flex justify-between items-center mb-6 text-slate-400 text-sm">
                <span>Taxes & Fees</span>
                <span>Calculated at checkout</span>
            </div>
            <div class="flex justify-between items-center mb-6 text-lg font-bold">
                <span>Total</span>
                <span id="cartTotal" class="text-indigo-400 text-2xl">$0.00</span>
            </div>
            <button id="checkoutBtn" class="w-full py-4 rounded-xl font-bold text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transform hover:-translate-y-0.5 transition-all shadow-lg shadow-indigo-500/25 disabled:opacity-50 disabled:cursor-not-allowed">
                Proceed to Checkout
            </button>
        </div>
    </div>

    <!-- Product Details Modal -->
    <div id="productModalOverlay" class="fixed inset-0 bg-black/60 backdrop-blur-sm z- hidden transition-opacity duration-300 opacity-0" onclick="closeProductDetails()"></div>
    <div id="productModal" class="fixed top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-2xl bg-slate-900 border border-slate-800 rounded-2xl z- hidden shadow-2xl flex-col max-h-[90vh]">
        <!-- Injected via JS -->
    </div>

    <!-- Toast Notification Container -->
    <div id="toastContainer" class="fixed bottom-5 right-5 z- flex flex-col gap-3 pointer-events-none"></div>

    <script>
        // --- Product Data ---
        const products = [
            {
                id: 'gpt-plus',
                name: 'ChatGPT Plus',
                category: 'ai',
                desc: 'Access to GPT-4, DALL-E 3 image generation, advanced data analysis, and priority access.',
                price: 20.00,
                billing: '/mo',
                imgUrl: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/ChatGPT-Logo.svg/500px-ChatGPT-Logo.svg.png', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-emerald-400',
                bgLight: 'bg-emerald-400/10',
                stock: 45,
                features: ['Access to GPT-4 and GPT-4o models', 'DALL-E 3 Image Generation', 'Advanced Data Analysis & File Uploads', 'Web Browsing capabilities', 'Create and use custom GPTs'],
                howToDeal: 'You will receive an activation link via email within 5 minutes of purchase. Click the link to apply the subscription to your current OpenAI account.'
            },
            {
                id: 'claude-pro',
                name: 'Claude Pro',
                category: 'ai',
                desc: 'Anthropic\'s most powerful AI. Huge context window, advanced reasoning, and coding capabilities.',
                price: 20.00,
                billing: '/mo',
                imgUrl: '[https://placehold.co/100x100/f97316/ffffff?text=Claude](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ9NAHBHbG_tj_AFFrJGCKAWEPDRtvFL28sug&s)', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-orange-400',
                bgLight: 'bg-orange-400/10',
                stock: 0,
                features: ['Access to Claude 3 Opus and Sonnet', '200K token context window (upload large PDFs)', 'Priority access during high-traffic periods', 'Early access to new features'],
                howToDeal: 'We will provide a unique digital key. Log in to your Anthropic account, go to Billing, and enter the key to upgrade to Pro instantly.'
            },
            {
                id: 'gemini-advanced',
                name: 'Gemini Advanced',
                category: 'ai',
                desc: 'Google\'s Ultra 1.0 model. Seamless integration with Workspace apps and elite coding assistance.',
                price: 19.99,
                billing: '/mo',
                imgUrl: 'https://logowik.com/content/uploads/images/google-ai-gemini91216.logowik.com.webp', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-blue-400',
                bgLight: 'bg-blue-400/10',
                stock: 9,
                features: ['Access to Google\'s most capable AI model, Ultra 1.0', 'State-of-the-art coding, reasoning, and creative collaboration', 'Integration with Gmail, Docs, and other Workspace apps', '2TB of Google One cloud storage included'],
                howToDeal: 'You will receive an invitation link to a premium Google One family plan. Accept the invite to unlock Gemini Advanced on your personal Google account.'
            },
            {
                id: 'canva-pro',
                name: 'Canva Pro',
                category: 'creative',
                desc: 'Unlock millions of premium templates, images, brand kits, and Magic Studio AI tools.',
                price: 14.99,
                billing: '/mo',
                imgUrl: 'https://public.canva.site/logo/media/dfb96cc174513093cd6ed61489ccb750.svg', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-cyan-400',
                bgLight: 'bg-cyan-400/10',
                stock: 85,
                features: ['100+ million premium stock photos, videos, and graphics', 'Magic Studio AI tools (Magic Eraser, Magic Edit, etc.)', 'Brand Kit to manage logos, colors, and fonts', 'Background remover with one click'],
                howToDeal: 'We will send a team invitation link to your email. Click it to join our Enterprise team with full Pro features on your own private Canva account.'
            },
            {
                id: 'capcut-pro',
                name: 'CapCut Pro',
                category: 'creative',
                desc: 'Premium video editing tools, advanced AI effects, cloud storage, and watermark removal.',
                price: 9.99,
                billing: '/mo',
                imgUrl: 'https://placehold.co/100x100/ffffff/000000?text=CapCut', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-white',
                bgLight: 'bg-white/10',
                stock: 0,
                features: ['Unlock all Pro effects, transitions, and filters', 'Advanced AI tools (Auto-captions, voice isolation)', '100GB of cloud storage for projects', 'Commercial use license for assets'],
                howToDeal: 'You will receive a digital code. Open the CapCut app (mobile or desktop), navigate to your profile, and click "Redeem Code" to activate.'
            },
            {
                id: 'coursera-plus',
                name: 'Coursera Premium',
                category: 'learning',
                desc: 'Unlimited access to 7,000+ courses, Projects, and Professional Certificates from top universities.',
                price: 39.00,
                billing: '/mo',
                imgUrl: 'https://placehold.co/100x100/2563eb/ffffff?text=Coursera', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-blue-600',
                bgLight: 'bg-blue-500/10',
                stock: 79,
                features: ['Unlimited access to 7,000+ courses and specializations', 'Earn professional certificates from Google, IBM, etc.', 'Learn at your own pace with offline viewing', 'Access to premium guided projects'],
                howToDeal: 'After checkout, you will receive an activation code. Log in to Coursera, go to the redeem page, and enter your code to start learning immediately.'
            },
            {
                id: 'linkedin-learning',
                name: 'LinkedIn Learning',
                category: 'learning',
                desc: 'Develop in-demand skills with 20,000+ expert-led courses. Earn certificates for your profile.',
                price: 29.99,
                billing: '/mo',
                imgUrl: 'https://placehold.co/100x100/60a5fa/ffffff?text=LinkedIn', // <-- PASTE YOUR IMAGE URL HERE
                color: 'text-blue-400',
                bgLight: 'bg-blue-400/10',
                stock: 3,
                features: ['Access to 20,000+ expert-led courses across business, tech, and creative', 'Earn certificates to display directly on your LinkedIn profile', 'Personalized course recommendations based on your career goals', 'Full access to LinkedIn Premium features (if selected)'],
                howToDeal: 'We will send an activation email. Ensure you are logged into your LinkedIn account, click the link, and the premium learning features will be tied to your profile.'
            }
        ];

        // --- State ---
        let cart = [];
        let currentFilter = 'all';
        let searchQuery = '';

        // --- DOM Elements ---
        const productGrid = document.getElementById('productGrid');
        const emptyState = document.getElementById('emptyState');
        const searchInput = document.getElementById('searchInput');
        const mobileSearchInput = document.getElementById('mobileSearchInput');
        const categoryBtns = document.querySelectorAll('.category-btn');
        
        const cartBtn = document.getElementById('cartBtn');
        const closeCartBtn = document.getElementById('closeCartBtn');
        const cartOverlay = document.getElementById('cartOverlay');
        const cartDrawer = document.getElementById('cartDrawer');
        const cartBadge = document.getElementById('cartBadge');
        const cartItemsContainer = document.getElementById('cartItemsContainer');
        const cartSubtotal = document.getElementById('cartSubtotal');
        const cartTotal = document.getElementById('cartTotal');
        const checkoutBtn = document.getElementById('checkoutBtn');
        const toastContainer = document.getElementById('toastContainer');
        const productModalOverlay = document.getElementById('productModalOverlay');
        const productModal = document.getElementById('productModal');

        // --- Initialize ---
        function init() {
            lucide.createIcons();
            renderProducts();
            setupEventListeners();
            loadCart();
        }

        // --- Render Products ---
        function renderProducts() {
            const filteredProducts = products.filter(p => {
                const matchesCategory = currentFilter === 'all' || p.category === currentFilter;
                const matchesSearch = p.name.toLowerCase().includes(searchQuery.toLowerCase()) || 
                                      p.desc.toLowerCase().includes(searchQuery.toLowerCase());
                return matchesCategory && matchesSearch;
            });

            if (filteredProducts.length === 0) {
                productGrid.innerHTML = '';
                emptyState.classList.remove('hidden');
                emptyState.classList.add('flex');
            } else {
                emptyState.classList.add('hidden');
                emptyState.classList.remove('flex');
                
                productGrid.innerHTML = filteredProducts.map(product => {
                    const inStock = product.stock > 0;
                    const stockBadgeClass = inStock ? 'bg-emerald-500/10 text-emerald-400 border-emerald-500/20' : 'bg-red-500/10 text-red-400 border-red-500/20';
                    const stockText = inStock ? `${product.stock} in stock` : 'Out of stock';
                    
                    return `
                    <div class="product-card rounded-2xl p-6 flex flex-col h-full relative group">
                        <div class="absolute top-4 right-4 w-10 h-10 rounded-full ${product.bgLight} flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity">
                            <i data-lucide="arrow-up-right" class="w-5 h-5 ${product.color}"></i>
                        </div>
                        <div class="w-14 h-14 rounded-2xl bg-slate-800 flex items-center justify-center mb-6 mt-2 shadow-inner border border-slate-700 overflow-hidden">
                            <img src="${product.imgUrl}" alt="${product.name} logo" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/100x100/1e293b/ffffff?text=Logo'">
                        </div>
                        <h3 class="text-xl font-bold mb-2">${product.name}</h3>
                        <p class="text-slate-400 text-sm flex-grow mb-6 line-clamp-3">${product.desc}</p>
                        
                        <div class="mt-auto pt-6 border-t border-slate-800/50 flex flex-col gap-4">
                            <div class="flex items-end justify-between">
                                <div>
                                    <span class="text-2xl font-bold text-white">$${product.price}</span>
                                    <span class="text-slate-500 text-sm">${product.billing}</span>
                                </div>
                                <div class="px-2.5 py-1 rounded-full text-xs font-semibold border ${stockBadgeClass}">
                                    ${stockText}
                                </div>
                            </div>
                            <button onclick="openProductDetails('${product.id}')" class="w-full bg-slate-800 hover:bg-slate-700 text-white font-medium py-2.5 rounded-xl transition-colors">
                                View Details
                            </button>
                        </div>
                    </div>
                    `;
                }).join('');
                
                // Re-initialize icons for newly injected HTML
                lucide.createIcons();
            }
        }

        // --- Cart Functions ---
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            if (!product || product.stock === 0) return;

            const existingItem = cart.find(item => item.id === productId);
            if (existingItem) {
                if (existingItem.quantity >= product.stock) {
                    showToast(`Cannot add more. Only ${product.stock} in stock!`);
                    return;
                }
                existingItem.quantity += 1;
                showToast(`Increased ${product.name} quantity`);
            } else {
                cart.push({ ...product, quantity: 1 });
                showToast(`Added ${product.name} to cart`);
            }
            
            saveCart();
            updateCartUI();
            
            // Pop animation on badge
            cartBadge.classList.add('scale-125');
            setTimeout(() => cartBadge.classList.remove('scale-125'), 200);
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            saveCart();
            updateCartUI();
        }

        function updateQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (!item) return;

            const product = products.find(p => p.id === productId);

            if (delta > 0 && item.quantity >= product.stock) {
                showToast(`Cannot add more. Only ${product.stock} in stock!`);
                return;
            }

            item.quantity += delta;
            if (item.quantity <= 0) {
                removeFromCart(productId);
            } else {
                saveCart();
                updateCartUI();
            }
        }

        function updateCartUI() {
            // Update Badge
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartBadge.textContent = totalItems;
            
            if (totalItems > 0) {
                cartBadge.classList.remove('scale-0');
                cartBadge.classList.add('scale-100');
            } else {
                cartBadge.classList.remove('scale-100');
                cartBadge.classList.add('scale-0');
            }

            // Update Cart Drawer Items
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = `
                    <div class="flex flex-col items-center justify-center h-full text-slate-500 py-12">
                        <i data-lucide="shopping-cart" class="w-16 h-16 mb-4 opacity-50"></i>
                        <p class="text-lg">Your cart is empty</p>
                        <button onclick="toggleCart()" class="mt-4 text-indigo-400 hover:text-indigo-300">Continue Shopping</button>
                    </div>
                `;
                checkoutBtn.disabled = true;
            } else {
                cartItemsContainer.innerHTML = cart.map(item => `
                    <div class="flex items-center gap-4 bg-slate-800/50 p-4 rounded-xl border border-slate-700/50 relative group">
                        <button onclick="removeFromCart('${item.id}')" class="absolute -top-2 -right-2 bg-slate-700 text-slate-300 rounded-full p-1 opacity-0 group-hover:opacity-100 transition-opacity hover:bg-red-500 hover:text-white">
                            <i data-lucide="x" class="w-3 h-3"></i>
                        </button>
                        <div class="w-12 h-12 rounded-lg bg-slate-800 flex items-center justify-center flex-shrink-0 overflow-hidden">
                            <img src="${item.imgUrl}" alt="${item.name} logo" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/100x100/1e293b/ffffff?text=Logo'">
                        </div>
                        <div class="flex-grow">
                            <h4 class="font-semibold text-sm truncate pr-4">${item.name}</h4>
                            <div class="text-indigo-400 font-medium text-sm">$${item.price} <span class="text-slate-500 text-xs">${item.billing}</span></div>
                        </div>
                        <div class="flex items-center bg-slate-900 rounded-lg border border-slate-700 h-8">
                            <button onclick="updateQuantity('${item.id}', -1)" class="w-8 flex justify-center text-slate-400 hover:text-white">-</button>
                            <span class="w-6 text-center text-sm font-medium">${item.quantity}</span>
                            <button onclick="updateQuantity('${item.id}', 1)" class="w-8 flex justify-center text-slate-400 hover:text-white">+</button>
                        </div>
                    </div>
                `).join('');
                checkoutBtn.disabled = false;
            }

            // Update Totals
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            cartSubtotal.textContent = `$${total.toFixed(2)}`;
            cartTotal.textContent = `$${total.toFixed(2)}`;
            
            lucide.createIcons();
        }

        function toggleCart() {
            const isClosed = cartDrawer.classList.contains('translate-x-full');
            
            if (isClosed) {
                cartOverlay.classList.remove('hidden');
                // Small delay to allow display:block to apply before changing opacity
                setTimeout(() => {
                    cartOverlay.classList.remove('opacity-0');
                    cartOverlay.classList.add('opacity-100');
                    cartDrawer.classList.remove('translate-x-full');
                }, 10);
                document.body.style.overflow = 'hidden'; // Prevent background scrolling
            } else {
                cartOverlay.classList.remove('opacity-100');
                cartOverlay.classList.add('opacity-0');
                cartDrawer.classList.add('translate-x-full');
                setTimeout(() => {
                    cartOverlay.classList.add('hidden');
                }, 300);
                document.body.style.overflow = '';
            }
        }

        // --- Product Details Functions ---
        function openProductDetails(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            const inStock = product.stock > 0;
            const stockBadgeClass = inStock ? 'bg-emerald-500/10 text-emerald-400 border-emerald-500/20' : 'bg-red-500/10 text-red-400 border-red-500/20';
            const stockText = inStock ? `${product.stock} in stock` : 'Out of stock';
            const btnClass = inStock ? 'bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg shadow-indigo-500/20' : 'bg-slate-700 text-slate-500 cursor-not-allowed';

            productModal.innerHTML = `
                <div class="p-6 border-b border-slate-800 flex justify-between items-start bg-slate-900 rounded-t-2xl flex-shrink-0">
                    <div class="flex items-center gap-4">
                        <div class="w-16 h-16 rounded-2xl bg-slate-800 flex items-center justify-center shadow-inner border border-slate-700 overflow-hidden">
                            <img src="${product.imgUrl}" alt="${product.name} logo" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/100x100/1e293b/ffffff?text=Logo'">
                        </div>
                        <div>
                            <h2 class="text-2xl font-bold text-white">${product.name}</h2>
                            <span class="inline-block px-2.5 py-1 mt-1 rounded-full text-xs font-semibold border ${stockBadgeClass}">${stockText}</span>
                        </div>
                    </div>
                    <button onclick="closeProductDetails()" class="text-slate-400 hover:text-white transition p-2 bg-slate-800 rounded-full hover:bg-slate-700">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                </div>
                <div class="p-6 overflow-y-auto space-y-6 flex-grow">
                    <div>
                        <h3 class="text-lg font-semibold text-white mb-2">Description</h3>
                        <p class="text-slate-400">${product.desc}</p>
                    </div>
                    <div>
                        <h3 class="text-lg font-semibold text-white mb-2">Key Features</h3>
                        <ul class="space-y-2 text-slate-400">
                            ${product.features.map(f => `<li class="flex items-start gap-2"><i data-lucide="check" class="w-5 h-5 text-indigo-400 flex-shrink-0 mt-0.5"></i><span>${f}</span></li>`).join('')}
                        </ul>
                    </div>
                    <div>
                        <h3 class="text-lg font-semibold text-white mb-2">How to Redeem</h3>
                        <div class="bg-slate-800/50 border border-slate-700 p-4 rounded-xl text-slate-400 text-sm">
                            <p class="flex items-start gap-3"><i data-lucide="info" class="w-5 h-5 text-indigo-400 flex-shrink-0 mt-0.5"></i> <span>${product.howToDeal}</span></p>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-lg font-semibold text-white mb-2">Need Support?</h3>
                        <div class="flex flex-col sm:flex-row gap-3">
                            <a href="https://t.me/linktome1" target="_blank" rel="noopener noreferrer" class="flex-1 flex items-center justify-center gap-2 bg-[#2AABEE]/10 hover:bg-[#2AABEE]/20 border border-[#2AABEE]/20 p-3 rounded-xl transition-colors text-[#2AABEE] text-sm font-medium">
                                <i data-lucide="send" class="w-4 h-4"></i>
                                Contact Support
                            </a>
                            <a href="https://t.me/learningadventure" target="_blank" rel="noopener noreferrer" class="flex-1 flex items-center justify-center gap-2 bg-indigo-500/10 hover:bg-indigo-500/20 border border-indigo-500/20 p-3 rounded-xl transition-colors text-indigo-400 text-sm font-medium">
                                <i data-lucide="users" class="w-4 h-4"></i>
                                Join Channel
                            </a>
                        </div>
                    </div>
                </div>
                <div class="p-6 border-t border-slate-800 bg-slate-900 rounded-b-2xl flex items-center justify-between flex-shrink-0">
                    <div>
                        <span class="text-3xl font-bold text-white">$${product.price}</span>
                        <span class="text-slate-500">${product.billing}</span>
                    </div>
                    <button onclick="addToCart('${product.id}'); closeProductDetails()" ${!inStock ? 'disabled' : ''} class="${btnClass} px-6 py-3 rounded-xl font-bold transition-all flex items-center gap-2">
                        <i data-lucide="shopping-cart" class="w-5 h-5"></i>
                        ${inStock ? 'Add to Cart' : 'Out of Stock'}
                    </button>
                </div>
            `;
            
            productModalOverlay.classList.remove('hidden');
            productModal.classList.remove('hidden');
            productModal.classList.add('flex');
            setTimeout(() => {
                productModalOverlay.classList.remove('opacity-0');
                productModalOverlay.classList.add('opacity-100');
            }, 10);
            
            lucide.createIcons();
            document.body.style.overflow = 'hidden';
        }

        function closeProductDetails() {
            productModalOverlay.classList.remove('opacity-100');
            productModalOverlay.classList.add('opacity-0');
            setTimeout(() => {
                productModalOverlay.classList.add('hidden');
                productModal.classList.add('hidden');
                productModal.classList.remove('flex');
            }, 300);
            document.body.style.overflow = '';
        }

        // --- Utility / Toast ---
        function showToast(message) {
            const toast = document.createElement('div');
            toast.className = 'bg-slate-800 border border-slate-700 text-white px-4 py-3 rounded-lg shadow-lg flex items-center gap-3 toast-enter pointer-events-auto';
            toast.innerHTML = `
                <i data-lucide="check-circle" class="w-5 h-5 text-emerald-400"></i>
                <span class="text-sm font-medium">${message}</span>
            `;
            
            toastContainer.appendChild(toast);
            lucide.createIcons();

            setTimeout(() => {
                toast.classList.replace('toast-enter', 'toast-exit');
                setTimeout(() => toast.remove(), 300);
            }, 5000);
        }
        window.showToast = showToast; // Expose for auth module

        // --- Local Storage ---
        function saveCart() {
            // Using in-memory array for this demo context, but would normally use localStorage
            // localStorage.setItem('digistore_cart', JSON.stringify(cart));
        }

        function loadCart() {
            // const savedCart = localStorage.getItem('digistore_cart');
            // if (savedCart) {
            //     cart = JSON.parse(savedCart);
            // }
            updateCartUI();
        }

        // --- Event Listeners ---
        function setupEventListeners() {
            // Search
            const handleSearch = (e) => {
                searchQuery = e.target.value;
                renderProducts();
            };
            searchInput.addEventListener('input', handleSearch);
            mobileSearchInput.addEventListener('input', handleSearch);

            // Categories
            categoryBtns.forEach(btn => {
                btn.addEventListener('click', (e) => {
                    // Update active styling
                    categoryBtns.forEach(b => {
                        b.classList.remove('bg-indigo-600', 'text-white');
                        b.classList.add('bg-slate-800', 'text-slate-300', 'border', 'border-slate-700');
                    });
                    
                    const clickedBtn = e.target;
                    clickedBtn.classList.remove('bg-slate-800', 'text-slate-300', 'border', 'border-slate-700');
                    clickedBtn.classList.add('bg-indigo-600', 'text-white');

                    // Filter
                    currentFilter = clickedBtn.dataset.category;
                    renderProducts();
                });
            });

            // Cart Toggles
            cartBtn.addEventListener('click', toggleCart);
            closeCartBtn.addEventListener('click', toggleCart);
            cartOverlay.addEventListener('click', toggleCart);
            
            // Checkout Mock
            checkoutBtn.addEventListener('click', () => {
                if (cart.length === 0) return;
                
                const btnOriginalText = checkoutBtn.innerText;
                checkoutBtn.innerHTML = '<i data-lucide="loader-2" class="w-5 h-5 animate-spin mx-auto"></i>';
                lucide.createIcons();
                
                setTimeout(() => {
                    toggleCart();
                    cart = [];
                    updateCartUI();
                    checkoutBtn.innerText = btnOriginalText;
                    
                    // Show success modal (simplified as a big toast here)
                    const modal = document.createElement('div');
                    modal.className = 'fixed inset-0 z- flex items-center justify-center p-4 bg-black/80 backdrop-blur-sm toast-enter';
                    modal.innerHTML = `
                        <div class="bg-slate-900 border border-slate-700 p-8 rounded-2xl max-w-sm w-full text-center shadow-2xl">
                            <div class="w-16 h-16 bg-emerald-500/20 rounded-full flex items-center justify-center mx-auto mb-4 text-emerald-400">
                                <i data-lucide="check" class="w-8 h-8"></i>
                            </div>
                            <h2 class="text-2xl font-bold text-white mb-2">Order Confirmed!</h2>
                            <p class="text-slate-400 mb-6">Your license keys and access instructions have been sent to your email.</p>
                            <button onclick="this.parentElement.parentElement.remove()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3 rounded-xl transition-colors">
                                Continue Shopping
                            </button>
                        </div>
                    `;
                    document.body.appendChild(modal);
                    lucide.createIcons();
                }, 1500);
            });
        }

        // Run
        document.addEventListener('DOMContentLoaded', init);
    </script>

    <!-- Auth Modal -->
    <div id="authOverlay" class="fixed inset-0 bg-black/60 backdrop-blur-sm z- hidden transition-opacity duration-300 opacity-0" onclick="closeAuthModal()"></div>
    <div id="authModal" class="fixed top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-md bg-slate-900 border border-slate-800 rounded-2xl z- hidden shadow-2xl flex-col p-8 transition-all duration-300 opacity-0 scale-95">
        <div class="flex justify-between items-center mb-6">
            <h2 id="authTitle" class="text-2xl font-bold text-white">Sign In</h2>
            <button onclick="closeAuthModal()" class="text-slate-400 hover:text-white bg-slate-800 p-2 rounded-full transition-colors"><i data-lucide="x" class="w-5 h-5"></i></button>
        </div>
        
        <button onclick="handleGoogleAuth()" class="w-full bg-white text-slate-900 font-semibold py-3 rounded-xl flex items-center justify-center gap-3 hover:bg-slate-200 transition mb-6 shadow-lg">
            <svg class="w-5 h-5" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/><path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/><path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/><path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/></svg>
            Continue with Google
        </button>

        <div class="flex items-center gap-3 mb-6">
            <div class="flex-1 h-px bg-slate-700"></div>
            <span class="text-slate-500 text-sm">or</span>
            <div class="flex-1 h-px bg-slate-700"></div>
        </div>

        <form onsubmit="handleEmailAuth(event)" class="flex flex-col gap-4">
            <input type="email" id="authEmail" placeholder="Email address" required class="w-full bg-slate-800 border border-slate-700 text-white rounded-xl py-3 px-4 focus:outline-none focus:border-indigo-500 transition-colors">
            <input type="password" id="authPassword" placeholder="Password" required class="w-full bg-slate-800 border border-slate-700 text-white rounded-xl py-3 px-4 focus:outline-none focus:border-indigo-500 transition-colors">
            <button type="submit" id="authSubmitBtn" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-3 rounded-xl transition shadow-lg shadow-indigo-500/20 mt-2 flex justify-center items-center">
                Sign In
            </button>
        </form>

        <p class="text-center text-slate-400 mt-6 text-sm">
            <span id="authSwitchText">Don't have an account?</span> 
            <button onclick="toggleAuthView()" class="text-indigo-400 font-semibold hover:text-indigo-300 ml-1 transition-colors">
                <span id="authSwitchBtnText">Sign Up</span>
            </button>
        </p>
    </div>

    <!-- Firebase Authentication & Database Script -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, GoogleAuthProvider, signInWithPopup, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged, signInWithCustomToken, signInAnonymously } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        
        let app, auth, db;
        try {
            app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);

            // Platform required initial auth
            const initAuth = async () => {
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token).catch(console.error);
                } else {
                    await signInAnonymously(auth).catch(console.error);
                }
            };
            initAuth();
        } catch (e) {
            console.error("Firebase initialization failed:", e);
        }

        let isLoginView = true;
        const overlay = document.getElementById('authOverlay');
        const modal = document.getElementById('authModal');
        const submitBtn = document.getElementById('authSubmitBtn');

        // Global UI Functions
        window.openAuthModal = () => {
            overlay.classList.remove('hidden');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            // Small delay for animation
            setTimeout(() => {
                overlay.classList.remove('opacity-0');
                overlay.classList.add('opacity-100');
                modal.classList.remove('opacity-0', 'scale-95');
                modal.classList.add('opacity-100', 'scale-100');
            }, 10);
            document.body.style.overflow = 'hidden';
            if (window.lucide) window.lucide.createIcons();
        };

        window.closeAuthModal = () => {
            overlay.classList.remove('opacity-100');
            overlay.classList.add('opacity-0');
            modal.classList.remove('opacity-100', 'scale-100');
            modal.classList.add('opacity-0', 'scale-95');
            setTimeout(() => {
                overlay.classList.add('hidden');
                modal.classList.add('hidden');
                modal.classList.remove('flex');
            }, 300);
            document.body.style.overflow = '';
        };

        window.toggleAuthView = () => {
            isLoginView = !isLoginView;
            document.getElementById('authTitle').innerText = isLoginView ? 'Sign In' : 'Create Account';
            document.getElementById('authSubmitBtn').innerText = isLoginView ? 'Sign In' : 'Create Account';
            document.getElementById('authSwitchText').innerText = isLoginView ? "Don't have an account?" : 'Already have an account?';
            document.getElementById('authSwitchBtnText').innerText = isLoginView ? 'Sign Up' : 'Sign In';
        };

        const saveUserProfile = async (user) => {
            if (!db || !user || user.isAnonymous) return;
            try {
                const userRef = doc(db, 'artifacts', appId, 'users', user.uid, 'profile', 'info');
                await setDoc(userRef, {
                    email: user.email,
                    uid: user.uid,
                    displayName: user.displayName || 'User',
                    lastLogin: new Date().toISOString()
                }, { merge: true });
            } catch (error) {
                console.error("Error saving user profile to Database:", error);
            }
        };

        window.handleGoogleAuth = async () => {
            // Fix: Prevent calling signInWithPopup because the preview iframe domain cannot be whitelisted
            // in the Firebase Console, which throws the "auth/unauthorized-domain" console error.
            // We intercept the click and explicitly guide the user to Email/Password instead.
            window.showToast("Google Sign-In is restricted in this preview environment. Please test using Email and Password below.");
        };

        window.handleEmailAuth = async (e) => {
            e.preventDefault();
            if (!auth) return window.showToast("Database configuration error.");
            
            const email = document.getElementById('authEmail').value;
            const password = document.getElementById('authPassword').value;
            const originalBtnText = submitBtn.innerText;
            
            submitBtn.innerHTML = '<i data-lucide="loader-2" class="w-5 h-5 animate-spin"></i>';
            if(window.lucide) window.lucide.createIcons();

            try {
                let userCredential;
                if (isLoginView) {
                    userCredential = await signInWithEmailAndPassword(auth, email, password);
                    window.showToast("Successfully signed in!");
                } else {
                    userCredential = await createUserWithEmailAndPassword(auth, email, password);
                    window.showToast("Account created successfully!");
                }
                
                await saveUserProfile(userCredential.user);
                window.closeAuthModal();
                document.getElementById('authEmail').value = '';
                document.getElementById('authPassword').value = '';
            } catch (error) {
                console.error(error);
                window.showToast("Error: " + error.message);
            } finally {
                submitBtn.innerText = originalBtnText;
            }
        };

        window.handleSignOut = async () => {
            if (!auth) return;
            try {
                await signOut(auth);
                window.showToast("Signed out successfully");
            } catch (error) {
                console.error("Sign out error", error);
            }
        };

        // Listen for authentication state changes
        if (auth) {
            onAuthStateChanged(auth, (user) => {
                const authContainer = document.getElementById('authContainer');
                if (user && user.email) {
                    // User is signed in
                    authContainer.innerHTML = `
                        <div class="relative group cursor-pointer">
                            <div class="flex items-center gap-2 bg-slate-800 border border-slate-700 px-4 py-2 rounded-full hover:bg-slate-700 transition">
                                <div class="w-6 h-6 rounded-full bg-indigo-500 flex items-center justify-center text-xs font-bold text-white uppercase">
                                    ${user.email.charAt(0)}
                                </div>
                                <span class="text-sm font-medium text-slate-200 hidden md:block truncate max-w-[120px]">${user.email.split('@')}</span>
                            </div>
                            <!-- Dropdown -->
                            <div class="absolute right-0 mt-2 w-48 bg-slate-800 border border-slate-700 rounded-xl shadow-xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 z-50 overflow-hidden">
                                <div class="px-4 py-3 border-b border-slate-700">
                                    <p class="text-xs text-slate-400">Signed in as</p>
                                    <p class="text-sm font-medium text-white truncate">${user.email}</p>
                                </div>
                                <button onclick="handleSignOut()" class="w-full text-left px-4 py-3 text-sm text-red-400 hover:bg-slate-700 transition flex items-center gap-2">
                                    <i data-lucide="log-out" class="w-4 h-4"></i> Sign Out
                                </button>
                            </div>
                        </div>
                    `;
                } else {
                    // User is signed out
                    authContainer.innerHTML = `
                        <button onclick="openAuthModal()" class="bg-white text-slate-900 px-5 py-2.5 rounded-full font-semibold hover:bg-slate-200 transition-colors">
                            Sign In
                        </button>
                    `;
                }
                if (window.lucide) window.lucide.createIcons();
            });
        }
    </script>
</body>
</html>
