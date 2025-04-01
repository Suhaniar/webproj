# webproj
this is my portfolio webdev project
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vibrant Portfolio</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:wght@400;500;600&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --ease: cubic-bezier(0.76, 0, 0.24, 1);
            --transition-time: 1s;
            --text-light: rgba(255, 255, 255, 0.95);
            --text-dark: rgba(0, 0, 0, 0.88);
            --primary-bg: #0f0e17;
            --card-bg: #181825;
            --card-light-bg: #ffffff;
            --accent-color: #7f5af0;
            --secondary-accent: #2cb67d;
            --highlight-color: #ff8906;
            --gradient-1: linear-gradient(135deg, #7f5af0, #2cb67d);
            --gradient-2: linear-gradient(135deg, #ff8906, #e53170);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-font-smoothing: antialiased;
        }
        
        ::selection {
            background: var(--accent-color);
            color: var(--text-light);
        }
        
        body {
            font-family: 'Poppins', 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            color: var(--text-light);
            overflow-x: hidden;
            line-height: 1.6;
            background: var(--primary-bg);
        }

        /* Background Effects */
        .particles-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        
        .particle {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            pointer-events: none;
            z-index: 0;
        }
        
        .noise-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml;utf8,<svg viewBox="0 0 250 250" xmlns="http://www.w3.org/2000/svg"><filter id="noise"><feTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" stitchTiles="stitch"/><feColorMatrix type="saturate" values="0"/></filter><rect width="100%" height="100%" filter="url(%23noise)" opacity="0.05"/></svg>');
            pointer-events: none;
            z-index: 10;
            mix-blend-mode: overlay;
        }
        
        .mesh-gradient {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle at 70% 30%, rgba(127, 90, 240, 0.15), transparent 40%),
                        radial-gradient(circle at 30% 70%, rgba(44, 182, 125, 0.1), transparent 50%);
        }
        
        .nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 2rem 3rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            mix-blend-mode: difference;
            color: var(--text-light);
        }
        
        .nav-logo {
            font-family: 'Playfair Display', serif;
            font-weight: 600;
            font-size: 1.5rem;
            cursor: pointer;
            letter-spacing: 0.05em;
            position: relative;
            color: var(--text-light);
            display: inline-block;
        }
        
        .nav-logo::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 2px;
            background: var(--gradient-1);
            transform: scaleX(0.7);
            transform-origin: right;
            transition: transform 0.4s var(--ease);
        }
        
        .nav-logo:hover::after {
            transform: scaleX(1);
            transform-origin: left;
        }
        
        .nav-links {
            display: flex;
            gap: 2.5rem;
        }
        
        .nav-link {
            cursor: pointer;
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 0.15em;
            font-weight: 500;
            position: relative;
            padding-bottom: 0.5rem;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient-2);
            transition: width 0.6s var(--ease);
        }
        
        .nav-link:hover::after {
            width: 100%;
        }

        /* Hero section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            padding: 0 5vw;
            background: radial-gradient(circle at 70% 30%, rgba(127, 90, 240, 0.15), transparent 70%),
                        radial-gradient(circle at 30% 70%, rgba(44, 182, 125, 0.1), transparent 70%);
            overflow: hidden;
        }
        
        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle at center, rgba(127, 90, 240, 0.05) 0%, transparent 25%);
            animation: rotate 30s linear infinite;
            z-index: 0;
        }
        
        @keyframes rotate {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }
        
        .hero-content {
            max-width: 1200px;
            width: 100%;
            text-align: center;
            position: relative;
            z-index: 1;
        }
        
        .hero h1 {
            font-family: 'Playfair Display', serif;
            font-size: clamp(3rem, 10vw, 7.5rem);
            font-weight: 600;
            margin-bottom: 1rem;
            line-height: 1;
            letter-spacing: -0.02em;
            background-image: var(--gradient-1);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            animation: gradientShift 8s ease infinite;
            background-size: 200% 200%;
        }
        
        @keyframes gradientShift {
            0% {
                background-position: 0% 50%;
            }
            50% {
                background-position: 100% 50%;
            }
            100% {
                background-position: 0% 50%;
            }
        }
        
        .hero p {
            font-size: clamp(1.1rem, 2vw, 1.4rem);
            opacity: 0.9;
            max-width: 700px;
            margin: 1.5rem auto;
        }
        
        .hero-buttons {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin-top: 2.5rem;
        }
        
        .hero-button {
            padding: 1rem 2.5rem;
            background: var(--accent-color);
            border: none;
            border-radius: 50px;
            color: var(--text-light);
            font-size: 1rem;
            font-weight: 500;
            text-decoration: none;
            transition: all 0.3s var(--ease);
            cursor: pointer;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .hero-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--secondary-accent);
            transform: translateX(-100%);
            transition: transform 0.4s var(--ease);
            z-index: -1;
        }
        
        .hero-button:hover::before {
            transform: translateX(0);
        }
        
        .hero-button.outline {
            background: transparent;
            border: 2px solid var(--accent-color);
            overflow: hidden;
        }
        
        .hero-button.outline::before {
            background: var(--highlight-color);
        }
        
        .hero-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        /* Floating shapes */
        .floating-shapes {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        
        .shape {
            position: absolute;
            border-radius: 50%;
            background: var(--accent-color);
            opacity: 0.3;
            filter: blur(40px);
            animation: float 15s ease-in-out infinite;
        }
        
        .shape-1 {
            width: 300px;
            height: 300px;
            top: 20%;
            left: 10%;
            background: var(--accent-color);
            animation-delay: 0s;
        }
        
        .shape-2 {
            width: 200px;
            height: 200px;
            top: 60%;
            right: 15%;
            background: var(--secondary-accent);
            animation-delay: 5s;
        }
        
        .shape-3 {
            width: 150px;
            height: 150px;
            bottom: 10%;
            left: 20%;
            background: var(--highlight-color);
            animation-delay: 2.5s;
        }
        
        @keyframes float {
            0%, 100% {
                transform: translateY(0) scale(1);
            }
            50% {
                transform: translateY(-20px) scale(1.05);
            }
        }
        
        /* Project cards section */
        .projects-container {
            position: relative;
            padding: 10vh 0 20vh;
            background: linear-gradient(to bottom, var(--primary-bg), var(--card-bg));
        }
        
        .project-section-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            font-weight: 600;
            margin-bottom: 15vh;
            text-align: center;
            letter-spacing: -0.01em;
            position: relative;
            z-index: 1;
        }
        
        .project-section-title::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: var(--gradient-2);
            border-radius: 2px;
        }
        
        .cards-container {
            position: relative;
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 5vw;
        }
        
        .project-card {
            position: relative;
            width: 100%;
            height: 80vh;
            margin-bottom: 25vh;
            overflow: hidden;
            border-radius: 20px;
            transform-origin: center center;
            will-change: transform;
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.3);
            transition: transform 0.5s var(--ease);
        }
        
        .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4), 0 0 30px rgba(127, 90, 240, 0.3);
        }
        
        .card-content {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 5rem;
            z-index: 3;
        }
        
        .card-content .category {
            font-size: 1rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--highlight-color);
            margin-bottom: 0.5rem;
            font-weight: 600;
            display: inline-block;
            padding: 0.5rem 1.5rem;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 50px;
            backdrop-filter: blur(10px);
        }
        
        .card-content h2 {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            font-weight: 600;
            margin-bottom: 1.5rem;
            line-height: 1.1;
        }
        
        .card-content p {
            font-size: clamp(1rem, 1.5vw, 1.25rem);
            max-width: 500px;
            opacity: 0.9;
            margin-bottom: 2rem;
        }
        
        .card-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-position: center;
            background-size: cover;
            background-repeat: no-repeat;
            z-index: 1;
            transition: transform 1s var(--ease);
        }
        
        .project-card:hover .card-bg {
            transform: scale(1.05);
        }
        
        .card-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 2;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.5) 40%, rgba(0,0,0,0.3) 100%);
        }
        
        .card-button {
            display: inline-flex;
            align-items: center;
            padding: 1rem 2rem;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid var(--highlight-color);
            border-radius: 50px;
            color: var(--text-light);
            font-size: 0.9rem;
            font-weight: 500;
            text-decoration: none;
            transition: all 0.3s var(--ease);
            backdrop-filter: blur(10px);
            cursor: pointer;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .card-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--highlight-color);
            transform: translateX(-100%);
            transition: transform 0.4s var(--ease);
            z-index: -1;
        }
        
        .card-button:hover::before {
            transform: translateX(0);
        }
        
        .card-button:hover {
            color: var(--text-light);
            transform: translateY(-2px);
        }
        
        .card-button svg {
            margin-left: 0.5rem;
            width: 24px;
            height: 24px;
            transition: transform 0.3s var(--ease);
        }
        
        .card-button:hover svg {
            transform: translateX(4px);
        }
        
        /* About section */
        .about-section {
            padding: 15vh 5vw;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: radial-gradient(circle at 30% 40%, rgba(44, 182, 125, 0.1), transparent 70%),
                        radial-gradient(circle at 70% 60%, rgba(127, 90, 240, 0.1), transparent 70%);
        }
        
        .about-content {
            max-width: 1000px;
            margin: 0 auto;
            text-align: center;
            position: relative;
        }
        
        .about-content h2 {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            margin-bottom: 2rem;
            position: relative;
            display: inline-block;
        }
        
        .about-content h2::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--gradient-1);
            border-radius: 2px;
        }
        
        .about-content p {
            font-size: clamp(1rem, 1.5vw, 1.2rem);
            line-height: 1.8;
            margin-bottom: 1.5rem;
        }
        
        .skill-tags {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 1rem;
            margin-top: 3rem;
        }
        
        .skill-tag {
            padding: 0.5rem 1.5rem;
            background: var(--card-bg);
            border: 1px solid var(--accent-color);
            border-radius: 50px;
            font-size: 0.9rem;
            color: var(--text-light);
            transition: all 0.3s var(--ease);
        }
        
        .skill-tag:hover {
            background: var(--accent-color);
            transform: translateY(-5px);
        }
        
        /* Contact section */
        .contact-section {
            padding: 15vh 5vw;
            background: var(--card-bg);
            border-radius: 30px 30px 0 0;
            position: relative;
            overflow: hidden;
        }
        
        .contact-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 70% 30%, rgba(255, 137, 6, 0.1), transparent 70%),
                        radial-gradient(circle at 30% 70%, rgba(229, 49, 112, 0.1), transparent 70%);
            pointer-events: none;
        }
        
        .contact-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            z-index: 1;
        }
        
        .contact-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            margin-bottom: 3rem;
            text-align: center;
            position: relative;
            display: inline-block;
        }
        
        .contact-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--gradient-2);
            border-radius: 2px;
        }
        
        .contact-form {
            width: 100%;
            max-width: 600px;
            position: relative;
            padding: 2.5rem;
            background: rgba(24, 24, 37, 0.8);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .form-group {
            margin-bottom: 1.5rem;
        }
        
        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.9rem;
            font-weight: 500;
            color: var(--text-light);
        }
        
        .form-input {
            width: 100%;
            padding: 1rem 1.5rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            color: var(--text-light);
            font-family: inherit;
            font-size: 1rem;
            transition: all 0.3s var(--ease);
        }
        
        .form-input:focus {
            outline: none;
            border-color: var(--accent-color);
            background: rgba(255, 255, 255, 0.1);
            box-shadow: 0 0 0 3px rgba(127, 90, 240, 0.2);
        }
        
        .form-textarea {
            min-height: 150px;
            resize: vertical;
        }
        
        .submit-button {
            padding: 1rem 2.5rem;
            background: var(--accent-color);
            border: none;
            border-radius: 50px;
            color: var(--text-light);
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s var(--ease);
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .submit-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--highlight-color);
            transform: translateX(-100%);
            transition: transform 0.4s var(--ease);
            z-index: -1;
        }
        
        .submit-button:hover::before {
            transform: translateX(0);
        }
        
        .submit-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        /* Footer */
        .footer {
            padding: 5vh 5vw;
            background: var(--card-bg);
            text-align: center;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .footer p {
            opacity: 0.7;
            font-size: 0.9rem;
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin: 2rem 0;
        }
        
        .social-link {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.05);
            color: var(--text-light);
            transition: all 0.3s var(--ease);
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .social-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--gradient-1);
            opacity: 0;
            transition: opacity 0.3s var(--ease);
            z-index: -1;
        }
        
        .social-link:hover::before {
            opacity: 1;
        }
        
        .social-link:hover {
            transform: translateY(-5px);
            border-color: transparent;
        }
        
        .scroll-hint {
            position: fixed;
            bottom: 2.5rem;
            left: 50%;
            transform: translateX(-50%);
            z-index: 900;
            color: var(--text-light);
            mix-blend-mode: difference;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.25em;
            animation: bounce 2s infinite;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
        }
        
        .scroll-hint::after {
            content: '';
            width: 1px;
            height: 3.5rem;
            background: currentColor;
            opacity: 0.6;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {
                transform: translateY(0) translateX(-50%);
            }
            40% {
                transform: translateY(-0.5rem) translateX(-50%);
            }
            60% {
                transform: translateY(-0.25rem) translateX(-50%);
            }
        }
        
        /* Media Queries */
        @media (max-width: 768px) {
            .nav {
                padding: 1.75rem;
            }
            
            .nav-links {
                gap: 1.25rem;
            }
            
            .card-content {
                padding: 2.5rem 1.5rem;
            }
            
            .project-card {
                height: 60vh;
                margin-bottom: 15vh;
            }
            
            .hero h1 {
                font-size: 3rem;
            }
            
            .hero p {
                font-size: 1.1rem;
            }
            
            .about-content,
            .contact-container {
                padding: 0 1rem;
            }
            
            .skill-tags {
                gap: 0.75rem;
            }
            
            .skill-tag {
                padding: 0.4rem 1.2rem;
                font-size: 0.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <div class="nav">
        <div class="nav-logo">Portfolio</div>
        <div class="nav-links">
            <div class="nav-link" data-target="home">Home</div>
            <div class="nav-link" data-target="portfolio">Projects</div>
            <div class="nav-link" data-target="about">About</div>
            <div class="nav-link" data-target="contact">Contact</div>
        </div>
    </div>
    
    <div class="scroll-hint">Scroll</div>
    
    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="floating-shapes">
            <div class="shape shape-1"></div>
            <div class="shape shape-2"></div>
            <div class="shape shape-3"></div>
        </div>
        <div class="hero-content">
            <h1>Web-Dev Project</h1>
            <p>Building stunning web designs with HTML, CSS, and JavaScript--suhani</p>
            <div class="hero-buttons">
                <a href="#portfolio" class="hero-button">View Projects</a>
                <a href="#contact" class="hero-button outline">Get in Touch</a>
            </div>
        </div>
    </section>
    
    <!-- Projects Section -->
    <section class="projects-container" id="portfolio">
        <h2 class="project-section-title">Selected Projects</h2>
        
        <div class="cards-container">
            <!-- Project Card 1 -->
            <div class="project-card">
                <div class="card-bg" style="background-image: url('https://picsum.photos/1400/840?random=1');"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                    <div class="category">Web Exercises</div>
                    <h2>Web Development Fundamentals</h2>
                    <p>Take a sneak-peek into what my favourite professor has taught us about the core principles of web development.</p>
                    <a href="C:\Users\suhan\OneDrive\Desktop\project\labexer.html" class="card-button">
                        View Project
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <line x1="5" y1="12" x2="19" y2="12"></line>
                            <polyline points="12 5 19 12 12 19"></polyline>
                        </svg>
                    </a>
                </div>
            </div>
            
            <!-- Project Card 2 -->
            <div class="project-card">
                <div class="card-bg" style="background-image: url('https://picsum.photos/1400/840?random=2');"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                    <div class="category">Advanced Projects</div>
                    <h2>Interactive Web Applications</h2>
                    <p>Explore my creative space where I develop complex, interactive web applications using modern front-end technologies.</p>
                    <a href="C:\Users\suhan\OneDrive\Desktop\project\allexer.html" class="card-button">
                        View Project
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <line x1="5" y1="12" x2="19" y2="12"></line>
                            <polyline points="12 5 19 12 12 19"></polyline>
                        </svg>
                    </a>
                </div>
            </div>
        </div>
    </section>
    
    <!-- About Section -->
    <section class="about-section" id="about">
        <div class="about-content">
            <h2>About Me</h2>
            <p>I'm a passionate web developer with a keen eye for design and a love for creating engaging user experiences. My journey in web development started with simple HTML and CSS projects, and has evolved to include modern JavaScript frameworks and animation libraries.</p>
            <p>I believe that great web design is about finding the perfect balance between beautiful aesthetics and intuitive functionality. Every project I work on is built with careful attention to detail, performance, and user experience.</p>
            <p>When I'm not coding, you can find me exploring new design trends, learning new technologies, or contributing to open-source projects.</p>
            
                    </div>
    </section>
    
    <!-- Contact Section -->
    <!-- Replace your existing contact section with this code -->
<section class="contact-section" id="contact">
    <div class="contact-container">
        <h2 class="contact-title">Get In Touch</h2>
        <form id="contactForm" class="contact-form" action="https://formspree.io/f/mzzeanzz" method="POST">
            <div class="form-group">
                <label for="name" class="form-label">Name</label>
                <input type="text" id="name" name="name" class="form-input" placeholder="Your name" required>
            </div>
            <div class="form-group">
                <label for="email" class="form-label">Email</label>
                <input type="email" id="email" name="email" class="form-input" placeholder="Your email" required>
            </div>
            
            <div class="form-group">
                <label for="message" class="form-label">Message</label>
                <textarea id="message" name="message" class="form-input form-textarea" placeholder="Your message" required></textarea>
            </div>
            <div style="text-align: center;">
                <button type="submit" class="submit-button">
                    <span class="button-text">Send Message</span>
                    <span class="button-loader" style="display: none;">
                        <svg width="24" height="24" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path d="M12,1A11,11,0,1,0,23,12,11,11,0,0,0,12,1Zm0,19a8,8,0,1,1,8-8A8,8,0,0,1,12,20Z" opacity=".25"/>
                            <path d="M12,4a8,8,0,0,1,7.89,6.7A1.53,1.53,0,0,0,21.38,12h0a1.5,1.5,0,0,0,1.48-1.75,11,11,0,0,0-21.72,0A1.5,1.5,0,0,0,2.62,12h0a1.53,1.53,0,0,0,1.49-1.3A8,8,0,0,1,12,4Z">
                                <animateTransform attributeName="transform" type="rotate" dur="0.75s" values="0 12 12;360 12 12" repeatCount="indefinite"/>
                            </path>
                        </svg>
                    </span>
                </button>
            </div>
            <div id="form-status" style="text-align: center; margin-top: 1rem;"></div>
        </form>
    </div>
</section>

<script>
    // Form submission handling
    const form = document.getElementById('contactForm');
    const status = document.getElementById('form-status');
    const submitButton = form.querySelector('button[type="submit"]');
    const buttonText = submitButton.querySelector('.button-text');
    const buttonLoader = submitButton.querySelector('.button-loader');
    
    async function handleSubmit(event) {
        event.preventDefault();
        
        // Show loading state
        buttonText.style.display = 'none';
        buttonLoader.style.display = 'inline-block';
        submitButton.disabled = true;
        
        try {
            const formData = new FormData(form);
            const response = await fetch(form.action, {
                method: 'POST',
                body: formData,
                headers: {
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                status.innerHTML = '<p style="color: var(--secondary-accent)">Thanks for your message! I\'ll get back to you soon.</p>';
                form.reset();
            } else {
                const error = await response.json();
                if (error.errors) {
                    status.innerHTML = `<p style="color: var(--highlight-color)">${error.errors.map(e => e.message).join(', ')}</p>`;
                } else {
                    throw new Error(response.statusText);
                }
            }
        } catch (error) {
            status.innerHTML = `<p style="color: var(--highlight-color)">Oops! There was a problem sending your message. Please try again later.</p>`;
        } finally {
            // Reset button state
            buttonText.style.display = 'inline-block';
            buttonLoader.style.display = 'none';
            submitButton.disabled = false;
            
            // Hide status message after 5 seconds
            setTimeout(() => {
                status.innerHTML = '';
            }, 5000);
        }
    }
    
    form.addEventListener('submit', handleSubmit);

<!-- Add this JavaScript right before the closing </body> tag -->
<script>
    // Smooth scrolling for navigation links
    document.querySelectorAll('.nav-link').forEach(link => {
        link.addEventListener('click', function(e) {
            e.preventDefault();
            const targetId = this.getAttribute('data-target');
            const targetSection = document.getElementById(targetId);
            
            if (targetSection) {
                window.scrollTo({
                    top: targetSection.offsetTop - 80, // Adjust for fixed header
                    behavior: 'smooth'
                });
                
                // Update URL without refreshing
                history.pushState(null, null, `#${targetId}`);
            }
        });
    });

    // Form submission handling (keep your existing form code)
    const form = document.getElementById('contactForm');
    const status = document.getElementById('form-status');
    const submitButton = form.querySelector('button[type="submit"]');
    const buttonText = submitButton.querySelector('.button-text');
    const buttonLoader = submitButton.querySelector('.button-loader');
    
    async function handleSubmit(event) {
        event.preventDefault();
        
        // Show loading state
        buttonText.style.display = 'none';
        buttonLoader.style.display = 'inline-block';
        submitButton.disabled = true;
        
        try {
            const formData = new FormData(form);
            const response = await fetch(form.action, {
                method: 'POST',
                body: formData,
                headers: {
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                status.innerHTML = '<p style="color: var(--secondary-accent)">Thanks for your message! I\'ll get back to you soon.</p>';
                form.reset();
            } else {
                const error = await response.json();
                if (error.errors) {
                    status.innerHTML = `<p style="color: var(--highlight-color)">${error.errors.map(e => e.message).join(', ')}</p>`;
                } else {
                    throw new Error(response.statusText);
                }
            }
        } catch (error) {
            status.innerHTML = `<p style="color: var(--highlight-color)">Oops! There was a problem sending your message. Please try again later.</p>`;
        } finally {
            // Reset button state
            buttonText.style.display = 'inline-block';
            buttonLoader.style.display = 'none';
            submitButton.disabled = false;
            
            // Hide status message after 5 seconds
            setTimeout(() => {
                status.innerHTML = '';
            }, 5000);
        }
    }
    
    if (form) {
        form.addEventListener('submit', handleSubmit);
    }
</script>
</script>
    </section>
    
    <!-- Footer -->
    <footer class="footer">
        <div class="social-links">
            <a href="#" class="social-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
                </svg>
            </a>
            <a href="https://www.instagram.com/qr/" class="social-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                    <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                    <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                </svg>
            </a>
            <a href="www.linkedin.com/in/suhani-ranadive-6a4810228" class="social-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path>
                    <rect x="2" y="9" width="4" height="12"></rect>
                    <circle cx="4" cy="4" r="2"></circle>
                </svg>
            </a>
            <a href="#" class="social-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M22 4.01c-1 .49-1.98.689-3 .99-1.121-




</footer>
