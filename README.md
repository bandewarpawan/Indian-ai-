# Indian-ai-
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hamen duniya Ka AI Chat</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.3/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
    <!-- AdMob Script -->
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-XXXXXXXXXXXXXXXX"
     crossorigin="anonymous"></script>
    <style>
        body {
            background-color: #f0f4f8;
            transition: all 0.3s ease;
        }
        #chatbox {
            background-color: #e0f7fa;
            border-radius: 1rem;
            max-height: 500px;
            overflow-y: auto;
        }
        input {
            background-color: #4db6ac;
            transition: all 0.3s ease;
        }
        input::placeholder {
            color: #ffffff;
        }
        .language-selector {
            position: absolute;
            top: 10px;
            right: 10px;
            display: flex;
            gap: 5px;
        }
        .language-flag {
            width: 30px;
            height: 20px;
            cursor: pointer;
            border: 1px solid #ccc;
            transition: all 0.2s;
        }
        .language-flag:hover {
            transform: scale(1.1);
        }
        .btn-animate {
            transition: all 0.2s;
        }
        .btn-animate:active {
            transform: scale(0.95);
        }
        .message-animate {
            animation: fadeInUp 0.3s;
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        #refreshButton {
            background: rgba(255,255,255,0.3);
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            margin-left: 10px;
        }
        #refreshButton:hover {
            background: rgba(255,255,255,0.5);
        }
        .input-container {
            display: flex;
            align-items: center;
            width: 100%;
        }
        .message-input {
            flex-grow: 1;
        }
        .ad-container {
            width: 100%;
            text-align: center;
            margin: 10px 0;
            min-height: 90px;
        }
        .ad-label {
            font-size: 12px;
            color: #666;
            margin-bottom: 5px;
        }
    </style>
</head>
<body class="flex flex-col items-center">
    <header class="bg-yellow-300 w-full p-4 text-center text-black font-bold text-xl relative">
        <div id="header-text">Welcome to AI Chat! 😊</div>
        <div class="language-selector">
            <img src="https://flagcdn.com/w20/gb.png" alt="English" class="language-flag" data-lang="en">
            <img src="https://flagcdn.com/w20/in.png" alt="Hindi" class="language-flag" data-lang="hi">
            <img src="https://flagcdn.com/w20/es.png" alt="Spanish" class="language-flag" data-lang="es">
            <img src="https://flagcdn.com/w20/fr.png" alt="French" class="language-flag" data-lang="fr">
            <img src="https://flagcdn.com/w20/de.png" alt="German" class="language-flag" data-lang="de">
            <img src="https://flagcdn.com/w20/jp.png" alt="Japanese" class="language-flag" data-lang="ja">
        </div>
    </header>
    
    <div class="flex justify-center mt-5 w-full px-2">
        <div class="px-2 w-full max-w-2xl">
            <div id="chatbox" class="flex flex-col items-start p-4"></div>
            
            <!-- Ad Container -->
            <div id="adContainer" class="ad-container">
                <div class="ad-label">Advertisement</div>
                <!-- AdMob Ad will be inserted here -->
            </div>
            
            <div class="flex flex-row my-5 items-center">
                <div class="input-container">
                    <input
                        class="shadow rounded p-2 mr-2 text-white message-input"
                        id="messageInput"
                        type="text"
                        placeholder="Ask me anything!"
                    />
                    <button
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded btn-animate"
                        id="sendButton"
                    >
                        Send
                    </button>
                    <button id="refreshButton" title="Refresh Chat">↻</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Language dictionary
        const translations = {
            en: {
                welcome: "Welcome to AI Chat! 😊",
                placeholder: "Ask me anything!",
                send: "Send",
                refresh: "Refresh Chat",
                ad: "Advertisement"
            },
            hi: {
                welcome: "AI चैट में आपका स्वागत है! 😊",
                placeholder: "मुझसे कुछ भी पूछें!",
                send: "भेजें",
                refresh: "चैट रिफ्रेश करें",
                ad: "विज्ञापन"
            },
            es: {
                welcome: "¡Bienvenido al Chat AI! 😊",
                placeholder: "¡Pregúntame cualquier cosa!",
                send: "Enviar",
                refresh: "Actualizar chat",
                ad: "Publicidad"
            },
            fr: {
                welcome: "Bienvenue sur le Chat IA ! 😊",
                placeholder: "Demandez-moi n'importe quoi !",
                send: "Envoyer",
                refresh: "Rafraîchir le chat",
                ad: "Publicité"
            },
            de: {
                welcome: "Willkommen beim KI-Chat! 😊",
                placeholder: "Frag mich alles!",
                send: "Senden",
                refresh: "Chat aktualisieren",
                ad: "Werbung"
            },
            ja: {
                welcome: "AIチャットへようこそ！😊",
                placeholder: "何でも聞いてください！",
                send: "送信",
                refresh: "チャットを更新",
                ad: "広告"
            }
        };

        // DOM elements
        const chatbox = document.getElementById("chatbox");
        const messageInput = document.getElementById("messageInput");
        const sendButton = document.getElementById("sendButton");
        const headerText = document.getElementById("header-text");
        const refreshButton = document.getElementById("refreshButton");
        const languageFlags = document.querySelectorAll(".language-flag");
        const adContainer = document.getElementById("adContainer");
        const adLabel = document.querySelector(".ad-label");
        
        // State management
        let chatId = crypto.randomUUID();
        let receiving = false;
        let currentLanguage = localStorage.getItem('language') || 'en';
        let adTimer;
        let lastAdTime = 0;
        
        // System prompts (multilingual)
        const systemPrompts = {
            en: "You are an all-knowing AI who can provide information on anything in the world and generate images to fully illustrate your responses. This AI can tell everything about the world, available in every language and should be advanced for the future.",
            hi: "आप एक सर्वज्ञ AI हैं जो दुनिया में किसी भी चीज़ के बारे में जानकारी प्रदान कर सकते हैं और अपनी प्रतिक्रियाओं को पूरी तरह से चित्रित करने के लिए छवियां उत्पन्न कर सकते हैं। यह AI दुनिया की सभी बातें बता सकता है, हर भाषा में उपलब्ध होना चाहिए और भविष्य के लिए उन्नत होना चाहिए।",
            es: "Eres una IA que lo sabe todo y puede proporcionar información sobre cualquier cosa en el mundo y generar imágenes para ilustrar completamente tus respuestas. Esta IA puede contar todo sobre el mundo, estar disponible en todos los idiomas y debe ser avanzada para el futuro.",
            fr: "Vous êtes une IA omnisciente qui peut fournir des informations sur tout ce qui se passe dans le monde et générer des images pour illustrer pleinement vos réponses. Cette IA peut tout raconter sur le monde, être disponible dans toutes les langues et devrait être avancée pour l'avenir.",
            de: "Sie sind eine allwissende KI, die Informationen über alles auf der Welt bereitstellen und Bilder generieren kann, um Ihre Antworten vollständig zu veranschaulichen. Diese KI kann alles über die Welt erzählen, in jeder Sprache verfügbar sein und sollte für die Zukunft fortgeschritten sein.",
            ja: "あなたは、世界のあらゆるものについての情報を提供し、回答を完全に説明するための画像を生成できる全知のAIです。 このAIは、世界についてすべてを語ることができ、すべての言語で利用可能であり、将来に向けて高度である必要があります。"
        };

        // Initialize the UI with current language
        function updateUIForLanguage() {
            const lang = translations[currentLanguage];
            headerText.textContent = lang.welcome;
            messageInput.placeholder = lang.placeholder;
            sendButton.textContent = lang.send;
            refreshButton.title = lang.refresh;
            adLabel.textContent = lang.ad;
        }

        // Create message element with animation
        function createMessageElement(text, alignment) {
            const messageElement = document.createElement("div");
            messageElement.className = `inline-block my-2.5 p-2.5 rounded-lg border message-animate ${
                alignment === "left" ? "self-start bg-green-200" : "self-end bg-purple-200"
            }`;
            messageElement.textContent = text;
            return messageElement;
        }

        // Show AdMob ad
        function showAd() {
            // Clear previous ad if any
            adContainer.innerHTML = '<div class="ad-label">' + translations[currentLanguage].ad + '</div>';
            
            // Create new ad element
            const adElement = document.createElement('ins');
            adElement.className = 'adsbygoogle';
            adElement.style.display = 'block';
            adElement.dataset.adClient = 'ca-pub-XXXXXXXXXXXXXXXX'; // Replace with your AdMob publisher ID
            adElement.dataset.adSlot = 'XXXXXXXXXX'; // Replace with your ad slot ID
            adElement.dataset.adFormat = 'auto';
            adElement.dataset.fullWidthResponsive = 'true';
            
            adContainer.appendChild(adElement);
            
            // Push the ad to AdMob
            try {
                (adsbygoogle = window.adsbygoogle || []).push({});
                console.log('Ad loaded successfully');
            } catch (e) {
                console.error('Error loading ad:', e);
            }
            
            // Update last ad time
            lastAdTime = Date.now();
        }

        // Start ad timer (show ad every 2 minutes)
        function startAdTimer() {
            // Clear existing timer if any
            if (adTimer) {
                clearInterval(adTimer);
            }
            
            // Show first ad immediately
            showAd();
            
            // Set interval for subsequent ads (2 minutes = 120000 milliseconds)
            adTimer = setInterval(showAd, 120000);
        }

        // WebSocket connection for chat
        function connectWebSocket(message) {
            receiving = true;
            const url = "wss://backend.buildpicoapps.com/api/chatbot/chat";
            const websocket = new WebSocket(url);

            websocket.addEventListener("open", () => {
                websocket.send(
                    JSON.stringify({
                        chatId: chatId,
                        appId: "cup-role",
                        systemPrompt: systemPrompts[currentLanguage] || systemPrompts.en,
                        message: message,
                    })
                );
            });

            const messageElement = createMessageElement("", "left");
            chatbox.appendChild(messageElement);

            websocket.onmessage = (event) => {
                messageElement.innerText += event.data;
                chatbox.scrollTop = chatbox.scrollHeight;
            };

            websocket.onclose = (event) => {
                if (event.code === 1000) {
                    receiving = false;
                } else {
                    messageElement.textContent += translations[currentLanguage].error || "Error getting response from server. Refresh the page and try again.";
                    chatbox.scrollTop = chatbox.scrollHeight;
                    receiving = false;
                }
            };
        }

        // Refresh chat function
        function refreshChat() {
            chatbox.innerHTML = '';
            chatId = crypto.randomUUID();
            
            // Add a welcome message in the selected language
            const welcomeMessage = createMessageElement(
                currentLanguage === 'hi' ? 
                "नमस्ते! मैं आपकी कैसे मदद कर सकता हूँ?" :
                currentLanguage === 'es' ? 
                "¡Hola! ¿Cómo puedo ayudarte hoy?" :
                currentLanguage === 'fr' ? 
                "Bonjour ! Comment puis-je vous aider aujourd'hui ?" :
                currentLanguage === 'de' ? 
                "Hallo! Wie kann ich Ihnen heute helfen?" :
                currentLanguage === 'ja' ? 
                "こんにちは！今日はどのようなご用件ですか？" :
                "Hello! How can I help you today?", 
                "left"
            );
            chatbox.appendChild(welcomeMessage);
        }

        // Event listeners
        sendButton.addEventListener("click", () => {
            if (!receiving && messageInput.value.trim() !== "") {
                const messageText = messageInput.value.trim();
                messageInput.value = "";
                const messageElement = createMessageElement(messageText, "right");
                chatbox.appendChild(messageElement);
                chatbox.scrollTop = chatbox.scrollHeight;

                connectWebSocket(messageText);
            }
        });

        messageInput.addEventListener("keydown", (event) => {
            if (event.key === "Enter" && !receiving && messageInput.value.trim() !== "") {
                event.preventDefault();
                sendButton.click();
            }
        });

        // Language selection
        languageFlags.forEach(flag => {
            flag.addEventListener("click", () => {
                currentLanguage = flag.getAttribute("data-lang");
                localStorage.setItem('language', currentLanguage);
                updateUIForLanguage();
                refreshChat();
            });
        });

        // Refresh button
        refreshButton.addEventListener("click", refreshChat);

        // Initialize the app
        updateUIForLanguage();
        refreshChat();
        startAdTimer();
    </script>
</body>
</html>
