<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teacher Q&A - Hormone Lesson</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
            background: #f5f7fa;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            max-width: 1400px;
            width: 100%;
            height: 90vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .header {
            background: #ffffff;
            border-bottom: 1px solid #e5e7eb;
            color: #1f2937;
            padding: 20px 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 20px;
            margin-bottom: 4px;
            font-weight: 600;
            color: #111827;
        }

        .header p {
            font-size: 13px;
            color: #6b7280;
            font-weight: 400;
        }

        .name-screen {
            display: flex;
            padding: 60px 40px;
            text-align: center;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 24px;
        }

        .name-screen h2 {
            color: #111827;
            font-size: 24px;
            margin: 0;
            font-weight: 600;
        }

        .name-screen p {
            color: #6b7280;
            font-size: 15px;
        }

        .name-input-container {
            width: 100%;
            max-width: 400px;
        }

        .name-input-container input {
            width: 100%;
            padding: 12px 16px;
            font-size: 15px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            outline: none;
            transition: all 0.2s ease;
            font-family: inherit;
        }

        .name-input-container input:focus {
            border-color: #10b981;
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
        }

        .name-submit-btn {
            margin-top: 16px;
            padding: 12px 32px;
            font-size: 15px;
            background: #10b981;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-weight: 500;
            font-family: inherit;
        }

        .name-submit-btn:hover {
            background: #059669;
            transform: translateY(-1px);
        }

        .name-submit-btn:active {
            transform: translateY(0);
        }

        .name-submit-btn:disabled {
            background: #d1d5db;
            cursor: not-allowed;
            transform: none;
        }

        .connecting-screen {
            display: none;
            padding: 60px 40px;
            text-align: center;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 24px;
        }

        .connecting-screen h2 {
            color: #111827;
            font-size: 22px;
            margin: 0;
            font-weight: 500;
        }

        .connecting-icon {
            font-size: 48px;
            opacity: 0.3;
            animation: fadeInOut 2s ease-in-out infinite;
        }

        @keyframes fadeInOut {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 0.4; }
        }

        .connecting-dots {
            font-size: 18px;
            color: #9ca3af;
            letter-spacing: 3px;
        }

        .chat-container {
            display: none;
            flex-direction: row;
            height: 100%;
        }

        .slide-panel {
            width: 50%;
            background: #fafafa;
            border-right: 1px solid #e5e7eb;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            padding: 0;
        }

        .slide-image {
            width: 100%;
            height: 100%;
            padding: 0;
            box-sizing: border-box;
            display: flex;
            align-items: center;
            justify-content: center;
            background: #ffffff;
        }

        .slide-image img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .chat-panel {
            width: 50%;
            display: flex;
            flex-direction: column;
            background: #ffffff;
        }

        .messages {
            flex: 1;
            overflow-y: auto;
            padding: 24px;
            background: #fafafa;
        }

        .message {
            margin-bottom: 20px;
            display: flex;
            animation: fadeIn 0.2s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(4px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .message.assistant {
            justify-content: flex-start;
            gap: 12px;
        }

        .message.user {
            justify-content: flex-end;
        }

        .message-content {
            max-width: 70%;
            padding: 12px 16px;
            border-radius: 12px;
            word-wrap: break-word;
            line-height: 1.5;
        }

        .message.assistant .message-content {
            background: #ffffff;
            color: #1f2937;
            border: 1px solid #e5e7eb;
        }

        .message.user .message-content {
            background: #10b981;
            color: white;
        }

        .message.system {
            justify-content: center;
            margin: 16px 0;
        }

        .message.system .message-content {
            background: #f0fdf4;
            color: #166534;
            border: 1px solid #bbf7d0;
            border-radius: 8px;
            padding: 10px 16px;
            font-size: 13px;
            font-weight: 500;
            max-width: 80%;
            text-align: center;
        }

        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            flex-shrink: 0;
            background: #10b981;
            align-self: flex-start;
            color: white;
            font-weight: 600;
            position: relative;
        }

        .avatar-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            min-width: 60px;
        }

        .avatar-info {
            font-size: 9px;
            color: #6b7280;
            text-align: center;
            line-height: 1.3;
            max-width: 60px;
        }

        .avatar-name {
            font-weight: 600;
            color: #374151;
        }

        .avatar-location {
            color: #9ca3af;
        }

        .input-area {
            padding: 20px 24px;
            background: white;
            border-top: 1px solid #e5e7eb;
        }

        .input-container {
            display: flex;
            gap: 10px;
        }

        #userInput {
            flex: 1;
            padding: 10px 16px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            font-size: 14px;
            outline: none;
            transition: all 0.2s ease;
            font-family: inherit;
        }

        #userInput:focus {
            border-color: #10b981;
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
        }

        #sendBtn {
            padding: 10px 24px;
            background: #10b981;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.2s ease;
            font-family: inherit;
            font-size: 14px;
        }

        #sendBtn:hover {
            background: #059669;
        }

        #sendBtn:active {
            transform: scale(0.98);
        }

        #sendBtn:disabled {
            background: #d1d5db;
            cursor: not-allowed;
            transform: none;
        }

        .download-notification {
            display: none;
            position: fixed;
            top: 20px;
            right: 20px;
            background: #10b981;
            color: white;
            padding: 12px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            z-index: 1000;
            animation: slideIn 0.2s ease-out;
            font-size: 14px;
        }

        @keyframes slideIn {
            from { transform: translateX(400px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
    </style>
</head>
<body>
    <div class="download-notification" id="downloadNotification">
        ✓ Conversation logs downloaded!
    </div>
    
    <div class="container">
        <div class="header">
            <h1>Hormone Lesson Q&A</h1>
            <p>Chat with Your Teacher</p>
        </div>

        <div class="name-screen" id="nameScreen">
            <h2>Welcome!</h2>
            <p>Before we begin, please enter your name</p>
            <div class="name-input-container">
                <input type="text" id="nameInput" placeholder="Enter your name..." />
                <button class="name-submit-btn" id="nameSubmitBtn" onclick="submitName()">Continue</button>
            </div>
        </div>

        <div class="connecting-screen" id="connectingScreen">
            <div class="connecting-icon">⋯</div>
            <h2>Connecting you to a teacher</h2>
            <div class="connecting-dots">...</div>
        </div>

        <div class="chat-container" id="chatContainer">
            <!-- Left side: Slide Image Only -->
            <div class="slide-panel">
                <div class="slide-image">
                    <!-- Replace this src with your actual slide image URL -->
                    <img id="lessonSlide" src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='800' height='600' viewBox='0 0 800 600'%3E%3Crect width='800' height='600' fill='%23ffffff'/%3E%3Ctext x='400' y='250' font-family='Arial' font-size='24' fill='%23333' text-anchor='middle'%3EHormone Lesson Slide%3C/text%3E%3Ctext x='400' y='290' font-family='Arial' font-size='16' fill='%23666' text-anchor='middle'%3EReplace this with your actual slide image%3C/text%3E%3Ctext x='400' y='340' font-family='Arial' font-size='14' fill='%23999' text-anchor='middle'%3EInstructions:%3C/text%3E%3Ctext x='400' y='365' font-family='Arial' font-size='12' fill='%23999' text-anchor='middle'%3E1. Save your slide as an image (PNG or JPG)%3C/text%3E%3Ctext x='400' y='385' font-family='Arial' font-size='12' fill='%23999' text-anchor='middle'%3E2. Upload it to an image host (Imgur, Google Drive, etc.)%3C/text%3E%3Ctext x='400' y='405' font-family='Arial' font-size='12' fill='%23999' text-anchor='middle'%3E3. Replace the img src with your image URL%3C/text%3E%3C/svg%3E" alt="Lesson Slide" />
                </div>
            </div>

            <!-- Right side: Chat Panel -->
            <div class="chat-panel">
                <div class="messages" id="messages"></div>
                <div class="input-area">
                    <div class="input-container">
                        <input type="text" id="userInput" placeholder="Type your question here..." />
                        <button id="sendBtn" onclick="sendMessage()">Send</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // IMPORTANT: Replace this with your Google Apps Script Web App URL
        const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycby_8wbcGRC6dYPuF16xIymOJC_YKwcCUsfd9qUMGcifhKBSo3c7yo7W4vsTk6S5hHAZ/exec';
        
        let studentName = '';
        let conversationLog = [];
        let sessionStartTime = null;
        
        // Slide management
        let currentSlide = 1;
        const totalSlides = 4;
        const slideTopics = {
            1: {
                name: "HPG Axis",
                keywords: ["hpg", "axis", "hypothalamic", "pituitary", "gonadal", "gnrh", "lh", "fsh", "gametogenesis"],
                followUp: "Do you have any other questions about the HPG axis?"
            },
            2: {
                name: "Gonadal Feedback System",
                keywords: ["feedback", "negative", "positive", "estrogen", "progesterone", "testosterone", "regulate", "cycle"],
                followUp: "Do you have any other questions about the gonadal feedback system?"
            },
            3: {
                name: "Hormone-Receptor Pathway Network",
                keywords: ["receptor", "pathway", "intracellular", "membrane", "camp", "transcription", "gene", "cell", "signal"],
                followUp: "Do you have any other questions about hormone-receptor pathways?"
            },
            4: {
                name: "Circadian-Reproductive Timing System",
                keywords: ["circadian", "rhythm", "timing", "melatonin", "kisspeptin", "sleep", "light", "clock", "daily"],
                followUp: "Do you have any other questions about circadian-reproductive timing?"
            }
        };
        
        // Predefined Q&A pairs
        const qaDatabase = {
            "hpg axis": "The HPG axis stands for the Hypothalamic-Pituitary-Gonadal axis. It's a communication system in your body where the hypothalamus (a region in your brain) releases hormones that signal the pituitary gland, which then signals your gonads (ovaries or testes) to produce sex hormones. This system controls development, reproduction, and puberty.",
            "what is gnrh": "GnRH stands for Gonadotropin-Releasing Hormone. It's released by the hypothalamus in rhythmic pulses and travels to the pituitary gland, where it stimulates the release of LH and FSH.",
            "what is lh": "LH stands for Luteinizing Hormone. It's produced by the pituitary gland and travels through your bloodstream to stimulate hormone production in the gonads. In females, it triggers ovulation, and in males, it stimulates testosterone production.",
            "what is fsh": "FSH stands for Follicle-Stimulating Hormone. It's also produced by the pituitary gland and works alongside LH to control reproductive functions. It helps with the development of eggs in females and sperm production in males.",
            "negative feedback": "Negative feedback is when hormones produced by the gonads (like estrogen, progesterone, or testosterone) travel back to the brain and signal it to reduce hormone production. It's like a thermostat turning off the heat when a room gets too warm.",
            "positive feedback": "Positive feedback is the opposite of negative feedback. Instead of reducing hormone production, high levels of certain hormones (especially estrogen at certain times) actually increase the release of other hormones. This happens briefly during the menstrual cycle and helps trigger ovulation.",
            "what is estrogen": "Estrogen is a sex hormone produced mainly by the ovaries. It plays important roles in puberty, the menstrual cycle, bone health, and many other body functions. It's one of the main hormones that gives females their physical characteristics.",
            "what is testosterone": "Testosterone is a sex hormone produced mainly by the testes in males and in smaller amounts by the ovaries in females. It's responsible for male physical characteristics, muscle development, bone strength, and the production of sperm.",
            "what is progesterone": "Progesterone is a hormone produced mainly by the ovaries after ovulation. It prepares the uterus for pregnancy and helps maintain a pregnancy if one occurs. It also provides negative feedback to the brain to regulate the menstrual cycle.",
            "hormone receptors": "Hormone receptors are like locks on cells that only specific hormone 'keys' can open. When a hormone binds to its receptor, it triggers changes inside the cell. Steroid hormones can bind to receptors inside cells or on cell membranes.",
            "how do hormones work": "Hormones are chemical messengers that travel through your bloodstream to reach target cells. When they arrive, they bind to specific receptors on or in these cells, which triggers a response. The response might include activating genes, changing cell behavior, or producing other substances.",
            "circadian rhythm": "Circadian rhythms are your body's internal 24-hour clock. They control when you feel sleepy or awake, and they also affect hormone release. Many reproductive hormones follow daily patterns that are coordinated with light exposure and sleep.",
            "what is melatonin": "Melatonin is a hormone produced by the pineal gland in your brain, mainly at night. It helps regulate your sleep-wake cycle and also influences other hormones, including reproductive hormones. Light exposure suppresses melatonin production.",
            "what is kisspeptin": "Kisspeptin is a protein that plays a crucial role in activating the reproductive system, especially during puberty. It signals to GnRH neurons to start or increase hormone production. Its levels can be affected by nutrition, stress, and circadian rhythms.",
            "what is puberty": "Puberty is the process of physical changes through which a child's body matures into an adult body capable of reproduction. It's triggered by increased activity of the HPG axis, which leads to increased production of sex hormones.",
            "when does puberty start": "Puberty typically starts between ages 8-13 for girls and ages 9-14 for boys, though the exact timing varies widely. It's triggered when the brain begins releasing more GnRH, which starts the cascade of hormonal changes.",
            "adrenal system": "The adrenal glands sit on top of your kidneys and produce several hormones, including cortisol (a stress hormone) and small amounts of sex hormones. While the adrenal system isn't the main focus of today's lesson on the HPG axis, it does interact with reproductive hormones, especially during stress.",
            "what is cortisol": "Cortisol is often called the 'stress hormone.' It's produced by the adrenal glands and helps your body respond to stress. High cortisol levels from chronic stress can interfere with reproductive hormones and affect the menstrual cycle.",
            "what are hormones": "Hormones are chemical messengers produced by glands in your body. They travel through your bloodstream to organs and tissues, delivering messages that tell your body what to do and when to do it. They control many functions including growth, metabolism, reproduction, and mood.",
            "gametogenesis": "Gametogenesis is the process of creating gametes - that means sperm in males (spermatogenesis) and eggs in females (oogenesis). This process is controlled by FSH and LH from the pituitary gland.",
        };

        function submitName() {
            const nameInput = document.getElementById('nameInput');
            const name = nameInput.value.trim();
            
            if (name === '') {
                alert('Please enter your name to continue');
                return;
            }
            
            studentName = name;
            startChat();
        }

        function startChat() {
            // Hide name screen
            document.getElementById('nameScreen').style.display = 'none';
            
            // Initialize session
            sessionStartTime = new Date();
            conversationLog.push({
                timestamp: sessionStartTime.toISOString(),
                event: 'session_start',
                student_name: studentName,
                condition: 'teacher'
            });
            
            // Show connecting screen
            document.getElementById('connectingScreen').style.display = 'flex';
            
            // After 3 seconds, show the chat
            setTimeout(() => {
                document.getElementById('connectingScreen').style.display = 'none';
                document.getElementById('chatContainer').style.display = 'flex';
                
                // Show system notification after 3 seconds
                setTimeout(() => {
                    addSystemMessage('You have been connected with a teacher: Vera Brown');
                    
                    // After 2 more seconds, show typing indicator
                    setTimeout(() => {
                        addTypingMessage();
                        
                        // After 5 seconds of typing, show the welcome message
                        setTimeout(() => {
                            removeTypingMessage();
                            switchSlide(1); // Start with slide 1
                            const welcomeMessage = `Hello! My name is Vera Brown, and I am a high school science teacher from Dorchester. On the left side of your screen, you have Slide 1 covering the ${slideTopics[1].name}. Please let me know if you have any questions about this part. I will be typing my responses, so please give me a few seconds or a minute until I respond. Feel free to ask me anything about what you've learned!`;
                            addMessage(welcomeMessage, 'assistant');
                        }, 5000);
                    }, 2000);
                }, 3000);
            }, 3000);
        }

        function addMessage(text, sender) {
            const messagesDiv = document.getElementById('messages');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${sender}`;
            
            // Log the message
            conversationLog.push({
                timestamp: new Date().toISOString(),
                sender: sender,
                message: text
            });
            
            // Add avatar container for assistant messages
            if (sender === 'assistant') {
                const avatarContainer = document.createElement('div');
                avatarContainer.className = 'avatar-container';
                
                const avatar = document.createElement('div');
                avatar.className = 'avatar';
                avatar.textContent = 'VB';
                
                const avatarInfo = document.createElement('div');
                avatarInfo.className = 'avatar-info';
                avatarInfo.innerHTML = '<div class="avatar-name">Vera Brown</div><div class="avatar-location">Dorchester, MA</div>';
                
                avatarContainer.appendChild(avatar);
                avatarContainer.appendChild(avatarInfo);
                messageDiv.appendChild(avatarContainer);
            }
            
            const contentDiv = document.createElement('div');
            contentDiv.className = 'message-content';
            contentDiv.textContent = text;
            
            messageDiv.appendChild(contentDiv);
            messagesDiv.appendChild(messageDiv);
            
            // Scroll to bottom
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }

        function addSystemMessage(text) {
            const messagesDiv = document.getElementById('messages');
            const messageDiv = document.createElement('div');
            messageDiv.className = 'message system';
            
            const contentDiv = document.createElement('div');
            contentDiv.className = 'message-content';
            contentDiv.textContent = text;
            
            messageDiv.appendChild(contentDiv);
            messagesDiv.appendChild(messageDiv);
            
            // Scroll to bottom
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }

        function addTypingMessage() {
            const messagesDiv = document.getElementById('messages');
            const messageDiv = document.createElement('div');
            messageDiv.className = 'message assistant';
            messageDiv.id = 'tempTypingMessage';
            
            const avatarContainer = document.createElement('div');
            avatarContainer.className = 'avatar-container';
            
            const avatar = document.createElement('div');
            avatar.className = 'avatar';
            avatar.textContent = 'VB';
            
            const avatarInfo = document.createElement('div');
            avatarInfo.className = 'avatar-info';
            avatarInfo.innerHTML = '<div class="avatar-name">Vera Brown</div><div class="avatar-location">Dorchester, MA</div>';
            
            avatarContainer.appendChild(avatar);
            avatarContainer.appendChild(avatarInfo);
            messageDiv.appendChild(avatarContainer);
            
            const contentDiv = document.createElement('div');
            contentDiv.className = 'message-content';
            contentDiv.style.fontStyle = 'italic';
            contentDiv.style.color = '#666';
            contentDiv.textContent = 'Vera Brown typing...';
            
            messageDiv.appendChild(contentDiv);
            messagesDiv.appendChild(messageDiv);
            
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }

        function removeTypingMessage() {
            const typingMsg = document.getElementById('tempTypingMessage');
            if (typingMsg) {
                typingMsg.remove();
            }
        }

        function findAnswer(question) {
            const normalizedQuestion = question.toLowerCase().trim();
            
            for (let key in qaDatabase) {
                if (normalizedQuestion.includes(key)) {
                    return qaDatabase[key];
                }
            }
            
            return null;
        }

        function detectQuestionTopic(question) {
            const normalized = question.toLowerCase();
            
            for (let slideNum in slideTopics) {
                const keywords = slideTopics[slideNum].keywords;
                for (let keyword of keywords) {
                    if (normalized.includes(keyword)) {
                        return parseInt(slideNum);
                    }
                }
            }
            return currentSlide; // Default to current slide if no match
        }

        function switchSlide(slideNumber) {
            currentSlide = slideNumber;
            const slideImage = document.getElementById('lessonSlide');
            
            // Update slide image source based on slide number
            // You'll replace these with your actual slide images
            const slideImages = {
                1: 'SLIDE_1_IMAGE_URL', // HPG Axis
                2: 'SLIDE_2_IMAGE_URL', // Feedback System
                3: 'SLIDE_3_IMAGE_URL', // Receptor Pathways
                4: 'SLIDE_4_IMAGE_URL'  // Circadian Timing
            };
            
            // Only update if you've added actual images
            // slideImage.src = slideImages[slideNumber];
            
            // Update slide indicator
            updateSlideIndicator();
        }

        function updateSlideIndicator() {
            let indicator = document.getElementById('slideIndicator');
            if (!indicator) {
                indicator = document.createElement('div');
                indicator.id = 'slideIndicator';
                indicator.style.cssText = 'position: absolute; top: 10px; right: 10px; background: rgba(16, 185, 129, 0.9); color: white; padding: 6px 12px; border-radius: 6px; font-size: 12px; font-weight: 500; z-index: 10;';
                document.querySelector('.slide-image').appendChild(indicator);
            }
            indicator.textContent = `Slide ${currentSlide}/${totalSlides}`;
        }

        // Natural fallback responses when answer not found
        const fallbackResponses = [
            "I unfortunately do not have an answer to that question. Do you have another question about the lesson?",
            "That's a good question, but I don't have that specific information with me right now. Can I help you with something else about hormones?",
            "Hmm, I'm not sure about that one. Is there another aspect of the lesson you'd like to explore?",
            "I don't have information on that particular topic in my notes. Would you like to ask about something else from today's lesson?",
            "That's outside of what we covered in today's lesson. Do you have any other questions about the reproductive hormones or the HPG axis?",
            "I'm not able to answer that one right now. What else would you like to know about the endocrine system?",
            "I don't have the details on that handy. Can I help with another question about what we learned today?"
        ];

        let lastFallbackIndex = -1;

        function getFallbackResponse() {
            // Get a different fallback than the last one used
            let index;
            do {
                index = Math.floor(Math.random() * fallbackResponses.length);
            } while (index === lastFallbackIndex && fallbackResponses.length > 1);
            
            lastFallbackIndex = index;
            return fallbackResponses[index];
        }

        function sendMessage() {
            const input = document.getElementById('userInput');
            const message = input.value.trim();
            
            if (message === '') return;
            
            addMessage(message, 'user');
            const normalizedMessage = message.toLowerCase();
            input.value = '';
            
            document.getElementById('sendBtn').disabled = true;
            
            // Check if user said "no" to follow-up question
            if (normalizedMessage === 'no' || normalizedMessage === 'nope' || normalizedMessage === 'no thanks' || normalizedMessage === 'no thank you') {
                handleNoResponse();
                document.getElementById('sendBtn').disabled = false;
                return;
            }
            
            // Detect which topic this question is about
            const detectedSlide = detectQuestionTopic(message);
            
            setTimeout(() => {
                addTypingMessage();
                
                setTimeout(() => {
                    removeTypingMessage();
                    
                    const answer = findAnswer(message);
                    let response = answer || getFallbackResponse();
                    
                    // Add follow-up question for the current slide topic
                    if (answer) {
                        response += ` ${slideTopics[detectedSlide].followUp}`;
                    }
                    
                    addMessage(response, 'assistant');
                    
                    // Re-enable send button
                    document.getElementById('sendBtn').disabled = false;
                    input.focus();
                }, 5000);
                
            }, 2000); // 2 seconds delay before showing typing indicator
        }

        // Handle "no" responses to move to next slide
        function handleNoResponse() {
            if (currentSlide < totalSlides) {
                setTimeout(() => {
                    addTypingMessage();
                    
                    setTimeout(() => {
                        removeTypingMessage();
                        
                        // Move to next slide
                        const nextSlide = currentSlide + 1;
                        switchSlide(nextSlide);
                        
                        const slideName = slideTopics[nextSlide].name;
                        const response = `Great! Now you can see the slide on ${slideName}. Let me know if you have any questions about this part.`;
                        
                        addMessage(response, 'assistant');
                    }, 3000);
                }, 500);
            } else {
                // All slides completed
                setTimeout(() => {
                    addTypingMessage();
                    
                    setTimeout(() => {
                        removeTypingMessage();
                        addMessage("We've covered all four parts of the lesson! Feel free to ask me any questions about any of the topics we discussed.", 'assistant');
                    }, 3000);
                }, 500);
            }
        }

        function downloadConversation() {
            // Add session end event
            const sessionEndTime = new Date();
            conversationLog.push({
                timestamp: sessionEndTime.toISOString(),
                event: 'download_triggered',
                session_duration_seconds: Math.floor((sessionEndTime - sessionStartTime) / 1000)
            });
            
            // Create formatted text version
            let textContent = "CONVERSATION LOG - TEACHER CONDITION\n";
            textContent += "=" .repeat(50) + "\n\n";
            textContent += `Student Name: ${studentName}\n`;
            textContent += `Session Start: ${sessionStartTime.toLocaleString()}\n`;
            textContent += `Session End: ${sessionEndTime.toLocaleString()}\n`;
            textContent += `Duration: ${Math.floor((sessionEndTime - sessionStartTime) / 1000)} seconds\n`;
            textContent += "\n" + "=" .repeat(50) + "\n\n";
            
            conversationLog.forEach((entry, index) => {
                if (entry.event === 'session_start') {
                    textContent += `[SESSION STARTED]\n\n`;
                } else if (entry.sender) {
                    const time = new Date(entry.timestamp).toLocaleTimeString();
                    const sender = entry.sender === 'user' ? studentName : 'Teacher Vera Brown';
                    textContent += `[${time}] ${sender}:\n${entry.message}\n\n`;
                }
            });
            
            // Create JSON version
            const jsonData = {
                condition: 'teacher',
                student_name: studentName,
                session_start: sessionStartTime.toISOString(),
                session_end: sessionEndTime.toISOString(),
                duration_seconds: Math.floor((sessionEndTime - sessionStartTime) / 1000),
                conversation: conversationLog
            };
            
            // Download text version
            const textBlob = new Blob([textContent], { type: 'text/plain' });
            const textUrl = URL.createObjectURL(textBlob);
            const textLink = document.createElement('a');
            textLink.href = textUrl;
            textLink.download = `conversation_teacher_${studentName}_${sessionStartTime.toISOString().replace(/[:.]/g, '-')}.txt`;
            document.body.appendChild(textLink);
            textLink.click();
            document.body.removeChild(textLink);
            
            // Download JSON version
            setTimeout(() => {
                const jsonBlob = new Blob([JSON.stringify(jsonData, null, 2)], { type: 'application/json' });
                const jsonUrl = URL.createObjectURL(jsonBlob);
                const jsonLink = document.createElement('a');
                jsonLink.href = jsonUrl;
                jsonLink.download = `conversation_teacher_${studentName}_${sessionStartTime.toISOString().replace(/[:.]/g, '-')}.json`;
                document.body.appendChild(jsonLink);
                jsonLink.click();
                document.body.removeChild(jsonLink);
            }, 500);
            
            alert('Conversation logs downloaded! Check your Downloads folder for both .txt and .json files.');
        }

        // Auto-save conversation to Google Sheets
        function saveToGoogleSheets() {
            if (!GOOGLE_SCRIPT_URL || GOOGLE_SCRIPT_URL === 'PASTE_YOUR_GOOGLE_SCRIPT_URL_HERE') {
                console.log('Google Sheets not configured. Skipping auto-save.');
                return;
            }

            const sessionEndTime = new Date();
            const messages = conversationLog.filter(entry => entry.sender).map(entry => ({
                sender: entry.sender,
                message: entry.message,
                timestamp: entry.timestamp
            }));

            const data = {
                condition: 'teacher',
                student_name: studentName,
                session_start: sessionStartTime.toISOString(),
                session_end: sessionEndTime.toISOString(),
                duration_seconds: Math.floor((sessionEndTime - sessionStartTime) / 1000),
                messages: messages
            };

            fetch(GOOGLE_SCRIPT_URL, {
                method: 'POST',
                mode: 'no-cors',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(data)
            }).then(() => {
                console.log('Data saved to Google Sheets');
            }).catch(error => {
                console.error('Error saving to Google Sheets:', error);
            });
        }

        // Auto-save when page is about to close
        window.addEventListener('beforeunload', function(e) {
            if (conversationLog.length > 1) { // More than just session start
                saveToGoogleSheets();
            }
        });

        // Auto-save every 30 seconds during active session
        setInterval(function() {
            if (sessionStartTime && conversationLog.length > 1) {
                saveToGoogleSheets();
            }
        }, 30000); // 30 seconds

        // Secret keyboard shortcut: Ctrl+Shift+D to download conversation
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey && e.shiftKey && e.key === 'D') {
                e.preventDefault();
                if (conversationLog.length > 0) {
                    downloadConversation();
                    
                    // Show notification
                    const notification = document.getElementById('downloadNotification');
                    notification.style.display = 'block';
                    setTimeout(() => {
                        notification.style.display = 'none';
                    }, 3000);
                }
            }
        });

        // Allow Enter key to send message
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('userInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendMessage();
                }
            });
            
            document.getElementById('nameInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    submitName();
                }
            });
        });
    </script>
</body>
</html>
