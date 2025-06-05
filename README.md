<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chats Quinceañera Monterrey</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Montserrat:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style id="app-style">
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #FFF5F7;
            background-image: url("https://cdn.pixabay.com/photo/2017/08/06/10/26/gold-2591967_1280.jpg");
            background-size: 300px;
            background-blend-mode: overlay;
            background-attachment: fixed;
        }
        
        .app-container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .app-title {
            font-family: 'Dancing Script', cursive;
            color: #E83E8C;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
        }
        
        .nav-link {
            position: relative;
            transition: all 0.3s ease;
        }
        
        .nav-link.active {
            color: #E83E8C;
            font-weight: bold;
        }
        
        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 3px;
            background-color: #E83E8C;
            border-radius: 2px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #E83E8C 0%, #FF6B6B 100%);
            border: none;
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(232, 62, 140, 0.3);
        }
        
        .festive-card {
            background: white;
            border-radius: 12px;
            border: 1px solid #FFD700;
            overflow: hidden;
            transition: all 0.3s ease;
            position: relative;
        }
        
        .festive-card::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, transparent 50%, #FFD700 50%);
            border-radius: 0 0 0 8px;
        }
        
        .festive-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(232, 62, 140, 0.2);
        }
        
        .festive-card-title {
            font-weight: 600;
            color: #E83E8C;
        }
        
        .festive-link {
            color: #4A6FA5;
            word-break: break-all;
        }
        
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
        }
        
        .form-input {
            border: 2px solid #E2E8F0;
            transition: all 0.3s ease;
        }
        
        .form-input:focus {
            border-color: #E83E8C;
            box-shadow: 0 0 0 3px rgba(232, 62, 140, 0.2);
        }
        
        .error-message {
            color: #E53E3E;
            font-size: 0.875rem;
            margin-top: 0.25rem;
        }
        
        .main-buttons {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            border: 3px solid #FFD700;
            padding: 2rem;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #FFD700;
            border-radius: 50%;
            animation: fall 5s linear infinite;
        }
        
        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        .success-message {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            z-index: 1000;
            text-align: center;
            border: 3px solid #FFD700;
        }
        
        /* Add styles for the three-dots menu */
        .card-menu i {
            font-size: 1.5rem;
            padding: 5px;
        }
        
        .card-menu {
            position: absolute;
            top: 10px;
            right: 10px;
            cursor: pointer;
            z-index: 5;
            padding: 5px;
            border-radius: 50%;
            width: 35px;
            height: 35px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .card-menu:hover {
            background-color: rgba(0,0,0,0.05);
        }
        
        .context-menu {
            position: absolute;
            top: 30px;
            right: 0;
            background: white;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            display: none;
            z-index: 10;
        }
        
        .context-menu.show {
            display: block;
        }
        
        .context-menu-item {
            padding: 8px 12px;
            cursor: pointer;
            white-space: nowrap;
        }
        
        .context-menu-item:hover {
            background-color: #f8f8f8;
            color: #E83E8C;
        }
        
        /* Modal styles */
        .max-h-90vh {
            max-height: 90vh;
        }
        
        #modal-image-container img {
            max-height: 300px;
            max-width: 100%;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        /* Animation for modal */
        @keyframes modalFadeIn {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }
        
        #chat-detail-modal .bg-white {
            animation: modalFadeIn 0.3s ease-out;
        }
        
        /* Add styles for ad banner */
        #ad-banner {
            background: linear-gradient(135deg, #fff5f7 0%, #fff8e1 100%);
            border: 2px solid #FFD700;
            border-radius: 12px;
            padding: 1.5rem;
            margin-top: 2rem;
            box-shadow: 0 4px 12px rgba(232, 62, 140, 0.15);
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            max-width: 1000px;
            margin-left: auto;
            margin-right: auto;
        }
        
        #ad-banner h3 {
            color: #E83E8C;
            margin-bottom: 0.75rem;
        }
        
        #ad-banner img {
            max-width: 100%;
            max-height: 120px;
            border-radius: 8px;
            margin: 0.5rem 0;
        }
        
        #ad-banner .ad-content {
            width: 100%;
        }
        
        #ad-banner .ad-disclaimer {
            font-size: 0.75rem;
            color: #888;
            margin-top: 0.5rem;
        }
    </style>
</head>
<body class="min-h-screen">
    <header class="bg-white shadow-md py-4 sticky top-0 z-10">
        <div class="app-container px-4 flex justify-between items-center">
            <h1 class="app-title text-3xl md:text-4xl">Quinceañera Chats MTY</h1>
            <nav class="flex space-x-6 mr-6">
                <a href="javascript:void(0)" class="nav-link active" data-target="home">Inicio</a>
                <a href="javascript:void(0)" class="nav-link" data-target="all-chats">Todos los Chats</a>
                <a href="javascript:void(0)" class="nav-link" data-target="user-chats">Tus Chats</a>
            </nav>
        </div>
    </header>

    <main class="app-container px-4 py-8">
        <!-- Home Page -->
        <div id="home" class="page active">
            <div class="flex flex-col items-center justify-center min-h-[70vh]">
                <div class="main-buttons w-full max-w-md text-center">
                    <h2 class="text-2xl md:text-3xl font-bold mb-8 text-pink-600">¡Comparte tu chat de Quinceañera!</h2>
                    <div class="flex flex-col space-y-6">
                        <button id="upload-btn" class="btn-primary text-white py-4 px-8 rounded-full text-xl font-bold shadow-lg">
                            <i class="fas fa-upload mr-2"></i> Subir tu chat
                        </button>
                        <button id="view-all-btn" class="btn-primary text-white py-4 px-8 rounded-full text-xl font-bold shadow-lg">
                            <i class="fas fa-list-alt mr-2"></i> Todos los chats
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Upload Form Page -->
        <div id="upload-form" class="page">
            <div class="max-w-md mx-auto bg-white p-8 rounded-lg shadow-lg border-2 border-pink-300">
                <h2 class="text-2xl font-bold mb-6 text-center text-pink-600">Subir Nuevo Chat</h2>
                <form id="chat-form">
                    <div class="mb-6">
                        <label for="chat-title" class="block text-gray-700 font-medium mb-2">Título del chat</label>
                        <input 
                            type="text" 
                            id="chat-title" 
                            class="form-input w-full px-4 py-2 rounded-lg" 
                            placeholder="Ej: Quinceañera de Sofia - Familia"
                            required
                        >
                        <div class="error-message hidden" id="title-error">El título es obligatorio</div>
                    </div>
                    <div class="mb-6">
                        <label for="chat-link" class="block text-gray-700 font-medium mb-2">Link de WhatsApp</label>
                        <input 
                            type="url" 
                            id="chat-link" 
                            class="form-input w-full px-4 py-2 rounded-lg" 
                            placeholder="https://chat.whatsapp.com/..."
                            required
                        >
                        <div class="error-message hidden" id="link-error">Introduce un link de WhatsApp válido</div>
                    </div>
                    <div class="mb-6">
                        <label for="chat-image" class="block text-gray-700 font-medium mb-2">Sube tu imagen (opcional)</label>
                        <input 
                            type="file" 
                            id="chat-image" 
                            class="form-input w-full px-4 py-2 rounded-lg" 
                            accept="image/*"
                        >
                        <div class="error-message hidden" id="image-error">El archivo debe ser una imagen válida</div>
                    </div>
                    <button 
                        type="submit" 
                        id="publish-btn" 
                        class="btn-primary w-full py-3 px-4 rounded-lg text-white font-bold text-lg"
                    >
                        <span id="btn-text">Publicar</span>
                        <span id="btn-loading" class="hidden">
                            <i class="fas fa-spinner fa-spin"></i> Publicando...
                        </span>
                    </button>
                </form>
            </div>
        </div>

        <!-- All Chats Page -->
        <div id="all-chats" class="page">
            <h2 class="text-2xl md:text-3xl font-bold mb-8 text-center text-pink-600">Todos los Chats de Quinceañeras</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="chats-container">
                <!-- Chat cards will be loaded here -->
                <p class="text-center col-span-full text-gray-500 italic">Cargando chats...</p>
            </div>
        </div>

        <!-- Add new User Chats Page -->
        <div id="user-chats" class="page">
            <h2 class="text-2xl md:text-3xl font-bold mb-8 text-center text-pink-600">Tus Chats de Quinceañeras</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="user-chats-container">
                <!-- User's chat cards will be loaded here -->
                <p class="text-center col-span-full text-gray-500 italic">Cargando tus chats...</p>
            </div>
        </div>
    </main>

    <div class="success-message" id="success-message">
        <i class="fas fa-check-circle text-5xl text-green-500 mb-4"></i>
        <h3 class="text-xl font-bold mb-2">¡Chat publicado con éxito!</h3>
        <p class="mb-4">Tu chat ya está disponible para todos</p>
        <button id="success-close" class="btn-primary text-white py-2 px-6 rounded-full">Continuar</button>
    </div>

    <footer class="bg-gray-800 text-white py-6 mt-12">
        <div class="app-container px-4 text-center">
            <p>© 2025 Quinceañera Chats Monterrey. Todos los derechos reservados.</p>
        </div>
    </footer>

    <div id="chat-detail-modal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-lg shadow-xl max-w-lg w-full p-6 relative max-h-90vh overflow-auto">
            <button id="close-modal" class="absolute top-4 right-4 text-gray-500 hover:text-pink-600">
                <i class="fas fa-times text-xl"></i>
            </button>
            <div class="modal-content text-center">
                <h3 id="modal-title" class="text-2xl font-bold text-pink-600 mb-4"></h3>
                <div id="modal-image-container" class="flex items-center justify-center my-6">
                    <!-- Image will be inserted here -->
                </div>
                <p class="text-gray-600 mb-2">Link de WhatsApp:</p>
                <a id="modal-link" href="#" class="text-blue-600 hover:underline break-all mb-6 block" target="_blank"></a>
                <button id="join-chat-btn" class="btn-primary text-white py-2 px-6 rounded-full">
                    <i class="fab fa-whatsapp mr-2"></i> Unirse al Chat
                </button>
            </div>
        </div>
    </div>

    <script id="app-script">
        // Generate or retrieve userId
        function getUserId() {
            let userId = localStorage.getItem('userId');
            if (!userId) {
                userId = 'user_' + Math.random().toString(36).substr(2, 9);
                localStorage.setItem('userId', userId);
            }
            return userId;
        }
        
        // Navigation functionality
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function() {
                // Update active nav link
                document.querySelectorAll('.nav-link').forEach(el => el.classList.remove('active'));
                this.classList.add('active');
                
                // Show the corresponding page
                const targetId = this.getAttribute('data-target');
                document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
                document.getElementById(targetId).classList.add('active');
                
                // If navigating to all-chats, load the chats
                if (targetId === 'all-chats') {
                    loadChats();
                }
                
                // If navigating to user-chats, load user's chats
                if (targetId === 'user-chats') {
                    loadUserChats();
                }
            });
        });
        
        // Button navigation
        document.getElementById('upload-btn').addEventListener('click', function() {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById('upload-form').classList.add('active');
            
            document.querySelectorAll('.nav-link').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-link')[0].classList.add('active');
        });
        
        document.getElementById('view-all-btn').addEventListener('click', function() {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById('all-chats').classList.add('active');
            
            document.querySelectorAll('.nav-link').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-link')[1].classList.add('active');
            
            loadChats();
        });
        
        // Form validation and submission
        const chatForm = document.getElementById('chat-form');
        
        chatForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const titleInput = document.getElementById('chat-title');
            const linkInput = document.getElementById('chat-link');
            const imageInput = document.getElementById('chat-image');
            const titleError = document.getElementById('title-error');
            const linkError = document.getElementById('link-error');
            const imageError = document.getElementById('image-error');
            
            // Reset errors
            titleError.classList.add('hidden');
            linkError.classList.add('hidden');
            imageError.classList.add('hidden');
            
            let isValid = true;
            
            // Validate title
            if (!titleInput.value.trim()) {
                titleError.classList.remove('hidden');
                isValid = false;
            }
            
            // Validate link
            const linkValue = linkInput.value.trim();
            if (!linkValue || !linkValue.startsWith('https://chat.whatsapp.com/')) {
                linkError.classList.remove('hidden');
                isValid = false;
            }
            
            // Validate image (if provided)
            let imageUrl = null;
            if (imageInput.files.length > 0) {
                const file = imageInput.files[0];
                if (!file.type.startsWith('image/')) {
                    imageError.classList.remove('hidden');
                    isValid = false;
                } else {
                    // Create object URL for preview
                    imageUrl = URL.createObjectURL(file);
                }
            }
            
            if (isValid) {
                // Show loading state
                document.getElementById('btn-text').classList.add('hidden');
                document.getElementById('btn-loading').classList.remove('hidden');
                
                // Save to localStorage
                const chatData = {
                    title: titleInput.value.trim(),
                    link: linkValue,
                    image: imageUrl,
                    userId: getUserId(), // Add userId to chat data
                    timestamp: Date.now() // Add timestamp for sorting
                };
                
                // Get existing chats or initialize empty array
                const existingChats = JSON.parse(localStorage.getItem('whatsappChats') || '[]');
                
                // Add new chat
                existingChats.push(chatData);
                
                // Save back to localStorage
                localStorage.setItem('whatsappChats', JSON.stringify(existingChats));
                
                // Save the chat to the Loops API
                saveToWhatsAppChatLoop(chatData.title, chatData.link);
                
                // Hide loading state after short delay
                setTimeout(() => {
                    document.getElementById('btn-text').classList.remove('hidden');
                    document.getElementById('btn-loading').classList.add('hidden');
                    
                    // Show success message
                    document.getElementById('success-message').style.display = 'block';
                    
                    // Reset form
                    chatForm.reset();
                    
                    // Create confetti effect
                    createConfetti();
                }, 1000);
            }
        });
        
        // Function to save chat to Loops API
        async function saveToWhatsAppChatLoop(title, link) {
            try {
                // Replace with the SaveChatLink Loop ID
                const response = await fetch('https://magicloops.dev/api/loop/a2b86b65-5ba7-434c-9ec0-a6fb49b9188b/run', {
                    method: 'POST',
                    body: JSON.stringify({ 
                        "title": title, 
                        "link": link 
                    }),
                });
                
                const responseJson = await response.json();
                console.log('Saved to Loops:', responseJson);
            } catch (error) {
                console.error('Error saving to Loops:', error);
            }
        }
        
        // Success message close button
        document.getElementById('success-close').addEventListener('click', function() {
            document.getElementById('success-message').style.display = 'none';
            
            // Navigate to all chats
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById('all-chats').classList.add('active');
            
            document.querySelectorAll('.nav-link').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-link')[1].classList.add('active');
            
            loadChats();
        });
        
        // Load chats function (now using localStorage)
        function loadChats() {
            const container = document.getElementById('chats-container');
            
            // Show loading state
            container.innerHTML = '<p class="text-center col-span-full text-gray-500 italic">Cargando chats...</p>';
            
            // Short timeout to show loading state
            setTimeout(() => {
                // Clear loading message
                container.innerHTML = '';
                
                // Get chats from localStorage
                const savedChats = JSON.parse(localStorage.getItem('whatsappChats') || '[]');
                
                // Filter out chats with title 'Quinceaños Carolina'
                const filteredChats = savedChats.filter(chat => chat.title !== 'Quinceaños Carolina');
                
                if (filteredChats.length === 0) {
                    // Show message if no chats found
                    container.innerHTML = '<p class="text-center col-span-full text-gray-500">No hay chats disponibles. ¡Sé el primero en compartir uno!</p>';
                    return;
                }
                
                // Track unique timestamps to prevent duplicates
                const addedTimestamps = new Set();
                
                // Create chat cards
                filteredChats.forEach(chat => {
                    // Only add the chat if its timestamp hasn't been seen before
                    if (!addedTimestamps.has(chat.timestamp)) {
                        addedTimestamps.add(chat.timestamp);
                        const card = createChatCard(chat, false);
                        container.appendChild(card);
                    }
                });
                
                // If after deduplication we have no chats left, show the empty message
                if (container.children.length === 0) {
                    container.innerHTML = '<p class="text-center col-span-full text-gray-500">No hay chats disponibles. ¡Sé el primero en compartir uno!</p>';
                }
            }, 1000);
        }
        
        // Load user chats function
        function loadUserChats() {
            const container = document.getElementById('user-chats-container');
            const userId = getUserId();
            
            // Show loading state
            container.innerHTML = '<p class="text-center col-span-full text-gray-500 italic">Cargando tus chats...</p>';
            
            // Short timeout to show loading state
            setTimeout(() => {
                // Clear loading message
                container.innerHTML = '';
                
                // Get chats from localStorage
                const savedChats = JSON.parse(localStorage.getItem('whatsappChats') || '[]');
                
                // Filter chats by userId and exclude 'Quinceaños Carolina'
                const userChats = savedChats.filter(chat => 
                    chat.userId === userId && chat.title !== 'Quinceaños Carolina'
                );
                
                if (userChats.length === 0) {
                    // Show message if no user chats found
                    container.innerHTML = '<p class="text-center col-span-full text-gray-500">No has compartido ningún chat todavía.</p>';
                    return;
                }
                
                // Create chat cards
                userChats.forEach(chat => {
                    const card = createChatCard(chat, true);
                    container.appendChild(card);
                });
            }, 1000);
        }
        
        // Create chat card function (reusable for both views)
        function createChatCard(chat, isUserChat) {
            const card = document.createElement('div');
            card.className = 'festive-card p-6 flex flex-col h-64 relative cursor-pointer';
            card.dataset.chatId = chat.timestamp; // Use timestamp as unique identifier
            
            // Add three-dots menu for user chats
            let menuHtml = '';
            if (isUserChat) {
                menuHtml = `
                    <div class="card-menu">
                        <i class="fas fa-ellipsis-v"></i>
                        <div class="context-menu">
                            <div class="context-menu-item delete-chat">
                                <i class="fas fa-trash-alt mr-2 text-red-500"></i> Eliminar
                            </div>
                        </div>
                    </div>
                `;
            }
            
            // Generate card content with optional image
            let cardContent = `
                ${menuHtml}
                <h3 class="festive-card-title text-xl mb-4">${chat.title}</h3>
            `;
            
            // Add image if available
            if (chat.image) {
                cardContent += `
                    <div class="flex-grow flex items-center justify-center mb-4">
                        <img src="${chat.image}" alt="${chat.title}" class="max-h-20 max-w-full rounded-lg shadow-sm" />
                    </div>
                `;
            } else {
                // Add spacer if no image
                cardContent += `<div class="flex-grow"></div>`;
            }
            
            // Add link section
            cardContent += `
                <div class="mt-auto">
                    <p class="text-gray-600 mb-2">Link de WhatsApp:</p>
                    <a href="${chat.link}" class="festive-link text-blue-600 hover:underline break-all" target="_blank">
                        ${chat.link}
                    </a>
                </div>
            `;
            
            card.innerHTML = cardContent;
            
            // Add event listener to open modal when card is clicked
            card.addEventListener('click', function(e) {
                // Don't open modal if clicking on menu or link
                if (e.target.closest('.card-menu') || e.target.closest('a')) {
                    return;
                }
                
                openChatModal(chat);
            });
            
            // Add event listeners for menu if it's a user chat
            if (isUserChat) {
                const menuButton = card.querySelector('.card-menu');
                const contextMenu = card.querySelector('.context-menu');
                const deleteButton = card.querySelector('.delete-chat');
                
                // Toggle context menu
                menuButton.addEventListener('click', function(e) {
                    e.stopPropagation();
                    contextMenu.classList.toggle('show');
                });
                
                // Handle delete action
                deleteButton.addEventListener('click', function() {
                    deleteChat(chat.timestamp);
                });
                
                // Close menu when clicking elsewhere
                document.addEventListener('click', function() {
                    contextMenu.classList.remove('show');
                });
            }
            
            return card;
        }
        
        // Delete chat function
        function deleteChat(chatId) {
            // Get chats from localStorage
            const savedChats = JSON.parse(localStorage.getItem('whatsappChats') || '[]');
            
            // Filter out the chat to delete and any 'Quinceaños Carolina' chat
            const updatedChats = savedChats.filter(chat => 
                chat.timestamp !== chatId && chat.title !== 'Quinceaños Carolina'
            );
            
            // Save back to localStorage
            localStorage.setItem('whatsappChats', JSON.stringify(updatedChats));
            
            // Remove from the DOM in user chats view
            const userChatCard = document.querySelector(`#user-chats-container .festive-card[data-chat-id="${chatId}"]`);
            if (userChatCard) {
                userChatCard.remove();
            }
            
            // Check if there are any user chats left
            const userChatsContainer = document.getElementById('user-chats-container');
            if (userChatsContainer.children.length === 0) {
                userChatsContainer.innerHTML = '<p class="text-center col-span-full text-gray-500">No has compartido ningún chat todavía.</p>';
            }
            
            // If all chats view is also visible, update it too
            const allChatsContainer = document.getElementById('chats-container');
            const allChatCard = document.querySelector(`#chats-container .festive-card[data-chat-id="${chatId}"]`);
            if (allChatCard) {
                allChatCard.remove();
            }
            
            // Check if there are any chats left
            if (allChatsContainer.children.length === 0) {
                allChatsContainer.innerHTML = '<p class="text-center col-span-full text-gray-500">No hay chats disponibles. ¡Sé el primero en compartir uno!</p>';
            }
        }
        
        // Create confetti effect
        function createConfetti() {
            const confettiCount = 100;
            const colors = ['#FFD700', '#E83E8C', '#FF6B6B', '#4A6FA5', '#00BFA6'];
            
            for (let i = 0; i < confettiCount; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.width = Math.random() * 10 + 5 + 'px';
                confetti.style.height = confetti.style.width;
                confetti.style.animationDuration = Math.random() * 3 + 2 + 's';
                confetti.style.animationDelay = Math.random() * 2 + 's';
                
                document.body.appendChild(confetti);
                
                // Remove confetti after animation
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }
        
        // Add new function to open chat detail modal
        function openChatModal(chat) {
            const modal = document.getElementById('chat-detail-modal');
            const modalTitle = document.getElementById('modal-title');
            const modalImageContainer = document.getElementById('modal-image-container');
            const modalLink = document.getElementById('modal-link');
            const joinChatBtn = document.getElementById('join-chat-btn');
            
            // Set modal content
            modalTitle.textContent = chat.title;
            modalLink.textContent = chat.link;
            modalLink.href = chat.link;
            joinChatBtn.onclick = function() {
                window.open(chat.link, '_blank');
            };
            
            // Handle image
            if (chat.image) {
                modalImageContainer.innerHTML = `<img src="${chat.image}" alt="${chat.title}" />`;
                modalImageContainer.style.display = 'flex';
            } else {
                modalImageContainer.style.display = 'none';
            }
            
            // Show modal
            modal.classList.remove('hidden');
            
            // Prevent scrolling on body
            document.body.style.overflow = 'hidden';
        }
        
        // Add event listeners for modal close
        document.addEventListener('DOMContentLoaded', function() {
            const modal = document.getElementById('chat-detail-modal');
            const closeModalBtn = document.getElementById('close-modal');
            
            // Close with the X button
            closeModalBtn.addEventListener('click', closeModal);
            
            // Close when clicking outside the modal content
            modal.addEventListener('click', function(e) {
                if (e.target === modal) {
                    closeModal();
                }
            });
            
            // Close with ESC key
            document.addEventListener('keydown', function(e) {
                if (e.key === 'Escape' && !modal.classList.contains('hidden')) {
                    closeModal();
                }
            });
            
            function closeModal() {
                modal.classList.add('hidden');
                document.body.style.overflow = '';
            }
        });
    </script>
</body>
</html>
