# Micwebsite
<!DOCTYPE html>
<html lang="sw">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mic Shoes - Dukani Kwako la Viatu</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f7f7;
        }
        .product-image-container {
            position: relative;
            overflow: hidden;
            border-radius: 0.75rem; /* rounded-xl */
        }
        .product-image {
            width: 100%;
            height: 250px; /* Fixed height for consistency */
            object-fit: cover;
            transition: transform 0.3s ease-in-out;
        }
        .product-image:hover {
            transform: scale(1.05);
        }
        .zoom-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .zoom-overlay.active {
            display: flex;
        }
        .zoom-overlay img {
            max-width: 90%;
            max-height: 90%;
            border-radius: 0.75rem;
        }
        .close-zoom {
            position: absolute;
            top: 20px;
            right: 20px;
            color: white;
            font-size: 2rem;
            cursor: pointer;
            z-index: 1001;
        }
        .scroll-container {
            max-height: 400px; /* Fixed height for scrollable areas */
            overflow-y: auto;
            border: 1px solid #e0e0e0;
            border-radius: 0.5rem;
            padding: 0.5rem;
        }
        /* Custom scrollbar for better appearance */
        .scroll-container::-webkit-scrollbar {
            width: 8px;
        }
        .scroll-container::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .scroll-container::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }
        .scroll-container::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    </style>
</head>
<body class="text-gray-800">

    <!-- Zoom Image Overlay -->
    <div id="zoomOverlay" class="zoom-overlay hidden">
        <span class="close-zoom" onclick="closeZoom()">&times;</span>
        <img id="zoomedImage" src="" alt="Picha Iliyokuzwa">
    </div>

    <!-- Header -->
    <header class="bg-gradient-to-r from-blue-600 to-indigo-700 text-white p-4 shadow-lg rounded-b-xl">
        <div class="container mx-auto flex justify-between items-center">
            <h1 class="text-3xl font-bold">Mic Shoes</h1>
            <nav>
                <ul class="flex space-x-6 text-lg">
                    <li><a href="#" class="hover:text-blue-200 transition duration-300">Nyumbani</a></li>
                    <li><a href="#" class="hover:text-blue-200 transition duration-300">Viatu</a></li>
                    <li><a href="#" class="hover:text-blue-200 transition duration-300" onclick="showCartModal()">
                        <i class="fas fa-shopping-cart"></i> Kikapu (<span id="cartCount">0</span>)
                    </a></li>
                    <li><a href="#" class="hover:text-blue-200 transition duration-300" onclick="showWishlistModal()">
                        <i class="fas fa-heart"></i> Orodha ya Tamaa (<span id="wishlistCount">0</span>)
                    </a></li>
                    <li><a href="#" class="hover:text-blue-200 transition duration-300">Wasiliana</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto p-6 mt-8">

        <!-- Search and Filter Section -->
        <section class="bg-white p-6 rounded-xl shadow-md mb-8">
            <h2 class="text-2xl font-semibold mb-4 text-center text-blue-700">Tafuta na Chuja Viatu</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                <div>
                    <label for="shoeSize" class="block text-sm font-medium text-gray-700 mb-1">Ukubwa wa Mguu (Size)</label>
                    <select id="shoeSize" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onchange="filterProducts()">
                        <option value="">Yote</option>
                        <option value="38">38</option>
                        <option value="39">39</option>
                        <option value="40">40</option>
                        <option value="41">41</option>
                        <option value="42">42</option>
                        <option value="43">43</option>
                    </select>
                </div>
                <div>
                    <label for="shoeType" class="block text-sm font-medium text-gray-700 mb-1">Aina ya Viatu</label>
                    <select id="shoeType" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onchange="filterProducts()">
                        <option value="">Yote</option>
                        <option value="Raba">Raba</option>
                        <option value="Open Shoes">Open Shoes</option>
                        <option value="Boots">Boots</option>
                        <option value="Sports">Sports</option>
                        <option value="Heels">Heels</option>
                    </select>
                </div>
                <div>
                    <label for="shoeColor" class="block text-sm font-medium text-gray-700 mb-1">Rangi</label>
                    <select id="shoeColor" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onchange="filterProducts()">
                        <option value="">Zote</option>
                        <option value="Nyeusi">Nyeusi</option>
                        <option value="Nyeupe">Nyeupe</option>
                        <option value="Nyekundu">Nyekundu</option>
                        <option value="Bluu">Bluu</option>
                        <option value="Kijani">Kijani</option>
                        <option value="Kahawia">Kahawia</option>
                    </select>
                </div>
                <div>
                    <label for="priceRange" class="block text-sm font-medium text-gray-700 mb-1">Bei (TZS)</label>
                    <select id="priceRange" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onchange="filterProducts()">
                        <option value="">Yote</option>
                        <option value="0-50000">Chini ya 50,000/=</option>
                        <option value="50001-100000">50,000/= - 100,000/=</option>
                        <option value="100001-200000">100,000/= - 200,000/=</option>
                        <option value="200001-inf">Zaidi ya 200,000/=</option>
                    </select>
                </div>
                <div>
                    <label for="shoeBrand" class="block text-sm font-medium text-gray-700 mb-1">Brand</label>
                    <select id="shoeBrand" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onchange="filterProducts()">
                        <option value="">Zote</option>
                        <option value="Nike">Nike</option>
                        <option value="Adidas">Adidas</option>
                        <option value="Puma">Puma</option>
                        <option value="Bata">Bata</option>
                        <option value="Geox">Geox</option>
                    </select>
                </div>
                <div class="col-span-1 md:col-span-2 lg:col-span-3">
                    <label for="searchQuery" class="block text-sm font-medium text-gray-700 mb-1">Tafuta kwa Jina</label>
                    <input type="text" id="searchQuery" placeholder="Mifano: Raba nyeusi, Nike sports" class="mt-1 block w-full pl-3 pr-3 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm" onkeyup="filterProducts()">
                </div>
            </div>
        </section>

        <!-- Product Listing Section -->
        <section class="bg-white p-6 rounded-xl shadow-md">
            <h2 class="text-2xl font-semibold mb-6 text-center text-blue-700">Viatu Vyetu</h2>
            <div id="productList" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
                <!-- Products will be loaded here by JavaScript -->
            </div>
        </section>

        <!-- Delivery Tracker & Pickup Options Section -->
        <section class="bg-white p-6 rounded-xl shadow-md mt-8">
            <h2 class="text-2xl font-semibold mb-4 text-center text-blue-700">Ufuatiliaji wa Oda na Chaguzi za Kuchukua</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Delivery Options -->
                <div>
                    <h3 class="text-xl font-medium mb-3">Chagua Njia ya Uwasilishaji</h3>
                    <div class="space-y-3">
                        <label class="inline-flex items-center">
                            <input type="radio" name="deliveryOption" value="home" class="form-radio text-blue-600 h-5 w-5" checked onchange="toggleDeliveryInputs()">
                            <span class="ml-2 text-gray-700">Home Delivery</span>
                        </label>
                        <div id="homeDeliveryInputs" class="ml-6 mt-2">
                            <label for="deliveryLocation" class="block text-sm font-medium text-gray-700 mb-1">Eneo la Uwasilishaji</label>
                            <input type="text" id="deliveryLocation" placeholder="Mifano: Gongo la Mboto, Kigoma" class="mt-1 block w-full pl-3 pr-3 py-2 border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500">
                        </div>

                        <label class="inline-flex items-center mt-3">
                            <input type="radio" name="deliveryOption" value="pickup" class="form-radio text-blue-600 h-5 w-5" onchange="toggleDeliveryInputs()">
                            <span class="ml-2 text-gray-700">Pickup Point</span>
                        </label>
                        <div id="pickupPointInputs" class="ml-6 mt-2 hidden">
                            <label for="pickupLocation" class="block text-sm font-medium text-gray-700 mb-1">Chagua Mahali pa Kuchukulia</label>
                            <select id="pickupLocation" class="mt-1 block w-full pl-3 pr-10 py-2 border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500">
                                <option value="dukani">Duka Kuu (Dar es Salaam)</option>
                                <option value="ofisi_mwanza">Ofisi (Mwanza)</option>
                                <option value="ghala_arusha">Ghala (Arusha)</option>
                            </select>
                        </div>
                    </div>
                    <button class="mt-6 w-full bg-blue-600 text-white py-3 px-4 rounded-lg hover:bg-blue-700 transition duration-300 shadow-md" onclick="updateOrderStatus('ordered')">Weka Oda (Simulated)</button>
                </div>

                <!-- Order Status -->
                <div>
                    <h3 class="text-xl font-medium mb-3">Hali ya Oda Yako</h3>
                    <div class="bg-gray-50 p-4 rounded-lg border border-gray-200">
                        <p class="text-lg font-bold text-gray-900">Oda #<span id="orderId">12345</span></p>
                        <p class="text-md text-gray-700 mt-2">Hadhi: <span id="orderStatus" class="font-semibold text-blue-600">Hakuna Oda Bado</span></p>
                        <div class="mt-4 flex flex-col space-y-2">
                            <button class="bg-gray-200 text-gray-700 py-2 px-3 rounded-md text-sm hover:bg-gray-300" onclick="updateOrderStatus('prepared')">Andaa Oda</button>
                            <button class="bg-gray-200 text-gray-700 py-2 px-3 rounded-md text-sm hover:bg-gray-300" onclick="updateOrderStatus('shipped')">Tuma Oda</button>
                            <button class="bg-gray-200 text-gray-700 py-2 px-3 rounded-md text-sm hover:bg-gray-300" onclick="updateOrderStatus('delivered')">Oda Imefika</button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Payment Integration Section -->
        <section class="bg-white p-6 rounded-xl shadow-md mt-8">
            <h2 class="text-2xl font-semibold mb-4 text-center text-blue-700">Njia za Malipo</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <h3 class="text-xl font-medium mb-3">Chagua Njia ya Kulipa</h3>
                    <div class="space-y-3">
                        <label class="flex items-center p-3 border border-gray-200 rounded-lg shadow-sm hover:bg-gray-50 transition duration-200">
                            <input type="radio" name="paymentMethod" value="mpesa" class="form-radio text-blue-600 h-5 w-5" checked>
                            <span class="ml-3 text-gray-800 font-medium">M-Pesa</span>
                            <i class="ml-auto fas fa-mobile-alt text-green-500 text-xl"></i>
                        </label>
                        <label class="flex items-center p-3 border border-gray-200 rounded-lg shadow-sm hover:bg-gray-50 transition duration-200">
                            <input type="radio" name="paymentMethod" value="tigopesa" class="form-radio text-blue-600 h-5 w-5">
                            <span class="ml-3 text-gray-800 font-medium">TigoPesa</span>
                            <i class="ml-auto fas fa-mobile-alt text-purple-500 text-xl"></i>
                        </label>
                        <label class="flex items-center p-3 border border-gray-200 rounded-lg shadow-sm hover:bg-gray-50 transition duration-200">
                            <input type="radio" name="paymentMethod" value="airtelmoney" class="form-radio text-blue-600 h-5 w-5">
                            <span class="ml-3 text-gray-800 font-medium">Airtel Money</span>
                            <i class="ml-auto fas fa-mobile-alt text-red-500 text-xl"></i>
                        </label>
                        <label class="flex items-center p-3 border border-gray-200 rounded-lg shadow-sm hover:bg-gray-50 transition duration-200">
                            <input type="radio" name="paymentMethod" value="banktransfer" class="form-radio text-blue-600 h-5 w-5">
                            <span class="ml-3 text-gray-800 font-medium">Bank Transfer</span>
                            <i class="ml-auto fas fa-university text-blue-500 text-xl"></i>
                        </label>
                        <label class="flex items-center p-3 border border-gray-200 rounded-lg shadow-sm hover:bg-gray-50 transition duration-200">
                            <input type="radio" name="paymentMethod" value="card" class="form-radio text-blue-600 h-5 w-5">
                            <span class="ml-3 text-gray-800 font-medium">Card Payment (Visa/MasterCard)</span>
                            <i class="ml-auto fas fa-credit-card text-gray-500 text-xl"></i>
                        </label>
                    </div>
                    <button class="mt-6 w-full bg-blue-600 text-white py-3 px-4 rounded-lg hover:bg-blue-700 transition duration-300 shadow-md" onclick="processPayment()">Lipa Sasa (Simulated)</button>
                </div>
                <!-- Payment Confirmation -->
                <div>
                    <h3 class="text-xl font-medium mb-3">Uthibitisho wa Malipo</h3>
                    <div id="paymentConfirmation" class="bg-gray-50 p-4 rounded-lg border border-gray-200 text-center hidden">
                        <i class="fas fa-check-circle text-green-500 text-4xl mb-3"></i>
                        <p class="text-lg font-semibold text-green-700">Malipo Yamefanikiwa!</p>
                        <p class="text-md text-gray-700 mt-2">Asante kwa kununua na Mic Shoes.</p>
                        <p class="text-sm text-gray-500 mt-1">Njia ya Malipo: <span id="confirmedPaymentMethod" class="font-medium"></span></p>
                    </div>
                    <div id="paymentMessage" class="mt-4 text-center text-red-500 font-semibold hidden">
                        Tafadhali chagua njia ya malipo.
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Floating WhatsApp Button -->
    <a href="https://wa.me/255XXXXXXXXX" target="_blank" class="fixed bottom-6 right-6 bg-green-500 text-white p-4 rounded-full shadow-lg hover:bg-green-600 transition duration-300 z-50 animate-bounce">
        <i class="fab fa-whatsapp text-3xl"></i>
    </a>

    <!-- Shopping Cart Modal -->
    <div id="cartModal" class="fixed inset-0 bg-gray-900 bg-opacity-75 flex items-center justify-center z-50 hidden">
        <div class="bg-white p-8 rounded-lg shadow-xl w-11/12 md:w-3/4 lg:w-1/2 relative">
            <button class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 text-2xl" onclick="closeCartModal()">&times;</button>
            <h2 class="text-3xl font-bold mb-6 text-blue-700 text-center">Kikapu Changu</h2>
            <div id="cartItems" class="space-y-4 scroll-container">
                <!-- Cart items will be loaded here -->
                <p id="emptyCartMessage" class="text-center text-gray-500">Kikapu chako hakina kitu.</p>
            </div>
            <div class="mt-6 pt-4 border-t border-gray-200 flex justify-between items-center text-xl font-semibold">
                <span>Jumla:</span>
                <span id="cartTotal">0.00 TZS</span>
            </div>
            <button class="mt-8 w-full bg-blue-600 text-white py-3 px-4 rounded-lg hover:bg-blue-700 transition duration-300 shadow-md">Endelea Kulipa</button>
        </div>
    </div>

    <!-- Wishlist Modal -->
    <div id="wishlistModal" class="fixed inset-0 bg-gray-900 bg-opacity-75 flex items-center justify-center z-50 hidden">
        <div class="bg-white p-8 rounded-lg shadow-xl w-11/12 md:w-3/4 lg:w-1/2 relative">
            <button class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 text-2xl" onclick="closeWishlistModal()">&times;</button>
            <h2 class="text-3xl font-bold mb-6 text-red-600 text-center">Orodha ya Tamaa</h2>
            <div id="wishlistItems" class="space-y-4 scroll-container">
                <!-- Wishlist items will be loaded here -->
                <p id="emptyWishlistMessage" class="text-center text-gray-500">Orodha yako ya tamaa haina kitu.</p>
            </div>
            <button class="mt-8 w-full bg-red-500 text-white py-3 px-4 rounded-lg hover:bg-red-600 transition duration-300 shadow-md" onclick="closeWishlistModal()">Endelea Kununua</button>
        </div>
    </div>

    <script>
        // Sample Product Data
        const products = [
            { id: 'shoe1', name: 'Raba ya Michezo ya Nike', type: 'Sports', size: '42', color: 'Nyeusi', brand: 'Nike', price: 95000, description: 'Raba maridadi na imara kwa ajili ya michezo.', images: ['https://placehold.co/600x400/FF0000/FFFFFF?text=Raba+Nyeusi+1', 'https://placehold.co/600x400/0000FF/FFFFFF?text=Raba+Nyeusi+2'], video: 'https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1&mute=1&loop=1&playlist=dQw4w9WgXcQ' }, // Example YouTube embed
            { id: 'shoe2', name: 'Open Shoes za Bata', type: 'Open Shoes', size: '39', color: 'Kahawia', brand: 'Bata', price: 48000, description: 'Open shoes za ngozi halisi, nzuri kwa matembezi.', images: ['https://placehold.co/600x400/8B4513/FFFFFF?text=Open+Shoes+1', 'https://placehold.co/600x400/A0522D/FFFFFF?text=Open+Shoes+2'], video: '' },
            { id: 'shoe3', name: 'Boots za Baridi za Adidas', type: 'Boots', size: '43', color: 'Nyeusi', brand: 'Adidas', price: 180000, description: 'Boots zenye joto kwa ajili ya baridi kali na matumizi ya kudumu.', images: ['https://placehold.co/600x400/000000/FFFFFF?text=Boots+Nyeusi+1', 'https://placehold.co/600x400/333333/FFFFFF?text=Boots+Nyeusi+2'], video: '' },
            { id: 'shoe4', name: 'Raba Nyeupe za Kawaida', type: 'Raba', size: '40', color: 'Nyeupe', brand: 'Puma', price: 70000, description: 'Raba nyepesi na safi kwa matumizi ya kila siku.', images: ['https://placehold.co/600x400/FFFFFF/000000?text=Raba+Nyeupe+1', 'https://placehold.co/600x400/F0F0F0/000000?text=Raba+Nyeupe+2'], video: '' },
            { id: 'shoe5', name: 'High Heels Nyekundu', type: 'Heels', size: '38', color: 'Nyekundu', brand: 'Geox', price: 120000, description: 'High heels za kupendeza kwa sherehe na hafla maalum.', images: ['https://placehold.co/600x400/FF0000/FFFFFF?text=Heels+Nyekundu+1', 'https://placehold.co/600x400/CC0000/FFFFFF?text=Heels+Nyekundu+2'], video: '' },
            { id: 'shoe6', name: 'Raba za Blue za Mazoezi', type: 'Sports', size: '41', color: 'Bluu', brand: 'Nike', price: 110000, description: 'Raba za kisasa kwa mazoezi, zinazotoa faraja na utulivu.', images: ['https://placehold.co/600x400/0000FF/FFFFFF?text=Raba+Bluu+1', 'https://placehold.co/600x400/3333FF/FFFFFF?text=Raba+Bluu+2'], video: '' },
            { id: 'shoe7', name: 'Open Shoes za Kijani', type: 'Open Shoes', size: '39', color: 'Kijani', brand: 'Adidas', price: 55000, description: 'Open shoes zenye rangi ya kijani, nzuri kwa mtindo wa kipekee.', images: ['https://placehold.co/600x400/008000/FFFFFF?text=Open+Shoes+Kijani+1', 'https://placehold.co/600x400/228B22/FFFFFF?text=Open+Shoes+Kijani+2'], video: '' },
            { id: 'shoe8', name: 'Boots za Wanawake Kahawia', type: 'Boots', size: '40', color: 'Kahawia', brand: 'Bata', price: 98000, description: 'Boots za mtindo kwa wanawake, zinafaa kwa misimu yote.', images: ['https://placehold.co/600x400/A0522D/FFFFFF?text=Boots+Kahawia+1', 'https://placehold.co/600x400/CD853F/FFFFFF?text=Boots+Kahawia+2'], video: '' },
        ];

        let cart = [];
        let wishlist = [];

        // Function to format price
        function formatPrice(price) {
            return new Intl.NumberFormat('en-TZ', { style: 'currency', currency: 'TZS' }).format(price);
        }

        // Function to render products
        function renderProducts(filteredProducts) {
            const productListDiv = document.getElementById('productList');
            productListDiv.innerHTML = ''; // Clear existing products

            if (filteredProducts.length === 0) {
                productListDiv.innerHTML = '<p class="text-center text-lg text-gray-500 col-span-full">Hakuna viatu vinavyolingana na vigezo vyako.</p>';
                return;
            }

            filteredProducts.forEach(product => {
                const productCard = `
                    <div class="bg-gray-50 rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition duration-300">
                        <div class="product-image-container cursor-pointer" onclick="showProductDetails('${product.id}')">
                            <img src="${product.images[0] || 'https://placehold.co/600x400/CCCCCC/333333?text=Hakuna+Picha'}" alt="${product.name}" class="product-image">
                        </div>
                        <div class="p-4">
                            <h3 class="text-xl font-semibold text-blue-800 truncate">${product.name}</h3>
                            <p class="text-gray-600 text-sm mt-1">${product.type} | Size: ${product.size} | Rangi: ${product.color}</p>
                            <p class="text-gray-900 font-bold text-lg mt-2">${formatPrice(product.price)}</p>
                            <div class="flex justify-between items-center mt-4">
                                <button class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition duration-300 text-sm" onclick="addToCart('${product.id}')">
                                    <i class="fas fa-cart-plus mr-2"></i>Weka Kikapuni
                                </button>
                                <button class="bg-gray-200 text-gray-700 px-3 py-2 rounded-lg hover:bg-gray-300 transition duration-300 text-sm" onclick="addToWishlist('${product.id}')">
                                    <i class="fas fa-heart"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                `;
                productListDiv.innerHTML += productCard;
            });
        }

        // Filter Products
        function filterProducts() {
            const size = document.getElementById('shoeSize').value;
            const type = document.getElementById('shoeType').value;
            const color = document.getElementById('shoeColor').value;
            const priceRange = document.getElementById('priceRange').value;
            const brand = document.getElementById('shoeBrand').value;
            const searchQuery = document.getElementById('searchQuery').value.toLowerCase();

            const filtered = products.filter(product => {
                let matches = true;

                if (size && product.size !== size) matches = false;
                if (type && product.type !== type) matches = false;
                if (color && product.color !== color) matches = false;
                if (brand && product.brand !== brand) matches = false;

                if (priceRange) {
                    const [min, max] = priceRange.split('-').map(Number);
                    if (product.price < min || (max && product.price > max)) matches = false;
                }

                if (searchQuery && !product.name.toLowerCase().includes(searchQuery) &&
                    !product.description.toLowerCase().includes(searchQuery) &&
                    !product.brand.toLowerCase().includes(searchQuery)) {
                    matches = false;
                }

                return matches;
            });
            renderProducts(filtered);
        }

        // Add to Cart
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            if (product) {
                const existingItem = cart.find(item => item.id === productId);
                if (existingItem) {
                    existingItem.quantity++;
                } else {
                    cart.push({ ...product, quantity: 1 });
                }
                updateCartCount();
                renderCartItems();
                alertMessage(`'${product.name}' imeongezwa kikapuni!`);
            }
        }

        // Update Cart Count in Header
        function updateCartCount() {
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartCount').innerText = totalItems;
        }

        // Render Cart Items in Modal
        function renderCartItems() {
            const cartItemsDiv = document.getElementById('cartItems');
            cartItemsDiv.innerHTML = '';
            let total = 0;

            if (cart.length === 0) {
                document.getElementById('emptyCartMessage').style.display = 'block';
            } else {
                document.getElementById('emptyCartMessage').style.display = 'none';
                cart.forEach(item => {
                    const itemElement = `
                        <div class="flex items-center justify-between p-3 bg-gray-100 rounded-lg shadow-sm">
                            <div class="flex items-center">
                                <img src="${item.images[0]}" alt="${item.name}" class="w-16 h-16 rounded-md object-cover mr-4">
                                <div>
                                    <p class="font-semibold text-gray-900">${item.name}</p>
                                    <p class="text-sm text-gray-600">${formatPrice(item.price)} x ${item.quantity}</p>
                                </div>
                            </div>
                            <div class="flex items-center space-x-2">
                                <button class="text-blue-600 hover:text-blue-800 text-lg" onclick="changeCartQuantity('${item.id}', 1)">+</button>
                                <span class="font-medium">${item.quantity}</span>
                                <button class="text-red-600 hover:text-red-800 text-lg" onclick="changeCartQuantity('${item.id}', -1)">-</button>
                                <button class="text-gray-500 hover:text-gray-700 ml-4" onclick="removeFromCart('${item.id}')">
                                    <i class="fas fa-trash-alt"></i>
                                </button>
                            </div>
                        </div>
                    `;
                    cartItemsDiv.innerHTML += itemElement;
                    total += item.price * item.quantity;
                });
            }
            document.getElementById('cartTotal').innerText = formatPrice(total);
        }

        function changeCartQuantity(productId, change) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += change;
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    renderCartItems();
                    updateCartCount();
                }
            }
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartCount();
            renderCartItems();
            alertMessage('Bidhaa imeondolewa kikapuni.');
        }

        // Show/Hide Cart Modal
        function showCartModal() {
            document.getElementById('cartModal').classList.remove('hidden');
            renderCartItems(); // Render items when modal opens
        }

        function closeCartModal() {
            document.getElementById('cartModal').classList.add('hidden');
        }

        // Add to Wishlist
        function addToWishlist(productId) {
            const product = products.find(p => p.id === productId);
            if (product && !wishlist.some(item => item.id === productId)) {
                wishlist.push(product);
                updateWishlistCount();
                renderWishlistItems();
                alertMessage(`'${product.name}' imeongezwa kwenye orodha ya tamaa!`);
            } else if (product) {
                alertMessage(`'${product.name}' tayari ipo kwenye orodha ya tamaa.`);
            }
        }

        // Update Wishlist Count in Header
        function updateWishlistCount() {
            document.getElementById('wishlistCount').innerText = wishlist.length;
        }

        // Render Wishlist Items in Modal
        function renderWishlistItems() {
            const wishlistItemsDiv = document.getElementById('wishlistItems');
            wishlistItemsDiv.innerHTML = '';

            if (wishlist.length === 0) {
                document.getElementById('emptyWishlistMessage').style.display = 'block';
            } else {
                document.getElementById('emptyWishlistMessage').style.display = 'none';
                wishlist.forEach(item => {
                    const itemElement = `
                        <div class="flex items-center justify-between p-3 bg-gray-100 rounded-lg shadow-sm">
                            <div class="flex items-center">
                                <img src="${item.images[0]}" alt="${item.name}" class="w-16 h-16 rounded-md object-cover mr-4">
                                <div>
                                    <p class="font-semibold text-gray-900">${item.name}</p>
                                    <p class="text-sm text-gray-600">${formatPrice(item.price)}</p>
                                </div>
                            </div>
                            <div class="flex items-center space-x-2">
                                <button class="text-blue-600 hover:text-blue-800 text-sm px-2 py-1 rounded bg-blue-200" onclick="addToCartFromWishlist('${item.id}')">
                                    Weka Kikapuni
                                </button>
                                <button class="text-gray-500 hover:text-gray-700" onclick="removeFromWishlist('${item.id}')">
                                    <i class="fas fa-trash-alt"></i>
                                </button>
                            </div>
                        </div>
                    `;
                    wishlistItemsDiv.innerHTML += itemElement;
                });
            }
        }

        function removeFromWishlist(productId) {
            wishlist = wishlist.filter(item => item.id !== productId);
            updateWishlistCount();
            renderWishlistItems();
            alertMessage('Bidhaa imeondolewa kwenye orodha ya tamaa.');
        }

        function addToCartFromWishlist(productId) {
            addToCart(productId);
            removeFromWishlist(productId);
            alertMessage('Bidhaa imehamishwa kutoka orodha ya tamaa kwenda kikapuni.');
        }

        // Show/Hide Wishlist Modal
        function showWishlistModal() {
            document.getElementById('wishlistModal').classList.remove('hidden');
            renderWishlistItems(); // Render items when modal opens
        }

        function closeWishlistModal() {
            document.getElementById('wishlistModal').classList.add('hidden');
        }

        // Product Details Modal (Simulated)
        function showProductDetails(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            // Create a temporary modal for product details
            const modal = document.createElement('div');
            modal.id = 'productDetailsModal';
            modal.className = 'fixed inset-0 bg-gray-900 bg-opacity-75 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white p-6 rounded-lg shadow-xl w-11/12 md:w-3/4 lg:w-2/3 xl:w-1/2 relative">
                    <button class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 text-2xl" onclick="document.getElementById('productDetailsModal').remove()">&times;</button>
                    <h2 class="text-3xl font-bold mb-4 text-blue-700 text-center">${product.name}</h2>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                        <!-- Product Images -->
                        <div class="flex flex-col items-center">
                            <img id="mainProductImage" src="${product.images[0]}" alt="${product.name}" class="w-full h-80 object-cover rounded-lg shadow-md mb-4 cursor-pointer" onclick="openZoom(this.src)">
                            <div class="flex space-x-2 overflow-x-auto w-full justify-center">
                                ${product.images.map(imgSrc => `<img src="${imgSrc}" class="w-20 h-20 object-cover rounded-md cursor-pointer border-2 border-transparent hover:border-blue-500 transition duration-200" onclick="document.getElementById('mainProductImage').src='${imgSrc}'">`).join('')}
                            </div>
                            ${product.video ? `<div class="mt-4 w-full h-48 rounded-lg overflow-hidden shadow-md">
                                <iframe width="100%" height="100%" src="${product.video}" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                            </div>` : ''}
                        </div>
                        <!-- Product Info -->
                        <div>
                            <p class="text-lg text-gray-700 mb-3">${product.description}</p>
                            <p class="text-lg font-semibold mb-2">Aina: <span class="font-normal">${product.type}</span></p>
                            <p class="text-lg font-semibold mb-2">Ukubwa: <span class="font-normal">${product.size}</span></p>
                            <p class="text-lg font-semibold mb-2">Rangi: <span class="font-normal">${product.color}</span></p>
                            <p class="text-lg font-semibold mb-2">Brand: <span class="font-normal">${product.brand}</span></p>
                            <p class="text-4xl font-bold text-gray-900 mt-4">${formatPrice(product.price)}</p>
                            <button class="mt-6 w-full bg-blue-600 text-white py-3 px-4 rounded-lg hover:bg-blue-700 transition duration-300 shadow-md" onclick="addToCart('${product.id}'); document.getElementById('productDetailsModal').remove();">
                                <i class="fas fa-cart-plus mr-2"></i>Weka Kikapuni
                            </button>
                            <button class="mt-3 w-full bg-gray-200 text-gray-700 py-3 px-4 rounded-lg hover:bg-gray-300 transition duration-300 shadow-md" onclick="addToWishlist('${product.id}')">
                                <i class="fas fa-heart mr-2"></i>Weka Kwenye Orodha ya Tamaa
                            </button>
                        </div>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        // Image Zoom Functionality
        function openZoom(imageSrc) {
            const zoomOverlay = document.getElementById('zoomOverlay');
            const zoomedImage = document.getElementById('zoomedImage');
            zoomedImage.src = imageSrc;
            zoomOverlay.classList.add('active');
            zoomOverlay.classList.remove('hidden');
        }

        function closeZoom() {
            document.getElementById('zoomOverlay').classList.remove('active');
            document.getElementById('zoomOverlay').classList.add('hidden');
        }

        // Delivery Tracker & Pickup Options Logic
        function toggleDeliveryInputs() {
            const homeDeliveryChecked = document.querySelector('input[name="deliveryOption"]:checked').value === 'home';
            document.getElementById('homeDeliveryInputs').classList.toggle('hidden', !homeDeliveryChecked);
            document.getElementById('pickupPointInputs').classList.toggle('hidden', homeDeliveryChecked);
        }

        function updateOrderStatus(status) {
            const orderStatusSpan = document.getElementById('orderStatus');
            const orderIdSpan = document.getElementById('orderId');
            orderIdSpan.innerText = Math.floor(Math.random() * 100000) + 10000; // Generate a random order ID

            let statusText = '';
            let statusColor = '';

            switch(status) {
                case 'ordered':
                    statusText = 'Oda Imewekwa';
                    statusColor = 'text-blue-600';
                    alertMessage('Oda yako imewekwa!');
                    break;
                case 'prepared':
                    statusText = 'Oda Inaandaliwa';
                    statusColor = 'text-yellow-600';
                    alertMessage('Oda inaandaliwa...');
                    break;
                case 'shipped':
                    statusText = 'Oda Imetumwa';
                    statusColor = 'text-purple-600';
                    alertMessage('Oda yako imetumwa!');
                    break;
                case 'delivered':
                    statusText = 'Oda Imefika';
                    statusColor = 'text-green-600';
                    alertMessage('Oda imefika, tafadhali chukua.');
                    break;
                default:
                    statusText = 'Hali Isiyojulikana';
                    statusColor = 'text-gray-600';
            }
            orderStatusSpan.innerText = statusText;
            orderStatusSpan.className = `font-semibold ${statusColor}`;
        }

        // Payment Integration Logic
        function processPayment() {
            const paymentMethod = document.querySelector('input[name="paymentMethod"]:checked');
            const paymentConfirmationDiv = document.getElementById('paymentConfirmation');
            const paymentMessageDiv = document.getElementById('paymentMessage');
            const confirmedPaymentMethodSpan = document.getElementById('confirmedPaymentMethod');

            if (paymentMethod) {
                paymentMessageDiv.classList.add('hidden');
                confirmedPaymentMethodSpan.innerText = paymentMethod.value.toUpperCase().replace('PESA', ' Pesa');
                paymentConfirmationDiv.classList.remove('hidden');
                alertMessage(`Malipo kwa ${paymentMethod.value.toUpperCase().replace('PESA', ' Pesa')} yamefanikiwa!`);
            } else {
                paymentConfirmationDiv.classList.add('hidden');
                paymentMessageDiv.classList.remove('hidden');
            }
        }

        // Custom Alert Message (instead of window.alert)
        function alertMessage(message, type = 'success') {
            const existingAlert = document.getElementById('customAlert');
            if (existingAlert) existingAlert.remove();

            const alertDiv = document.createElement('div');
            alertDiv.id = 'customAlert';
            alertDiv.className = `fixed top-6 left-1/2 -translate-x-1/2 p-4 rounded-lg shadow-lg text-white text-center z-50 transition-all duration-500 ease-out transform scale-0 opacity-0`;

            let bgColor = '';
            if (type === 'success') {
                bgColor = 'bg-green-500';
            } else if (type === 'info') {
                bgColor = 'bg-blue-500';
            } else if (type === 'error') {
                bgColor = 'bg-red-500';
            }

            alertDiv.classList.add(bgColor);
            alertDiv.innerHTML = `<p>${message}</p>`;
            document.body.appendChild(alertDiv);

            // Animate in
            setTimeout(() => {
                alertDiv.classList.remove('scale-0', 'opacity-0');
                alertDiv.classList.add('scale-100', 'opacity-100');
            }, 50); // Small delay to ensure transition works

            // Animate out and remove
            setTimeout(() => {
                alertDiv.classList.remove('scale-100', 'opacity-100');
                alertDiv.classList.add('scale-0', 'opacity-0');
                setTimeout(() => alertDiv.remove(), 500); // Remove after transition
            }, 3000);
        }

        // Initial render on page load
        document.addEventListener('DOMContentLoaded', () => {
            renderProducts(products);
            updateCartCount();
            updateWishlistCount();
            toggleDeliveryInputs(); // Initialize delivery input visibility
        });
    </script>
</body>
</html
