# Music-website.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Music Website with Sign-In</title>
    <style>
        /* General Styles */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: #181818;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            transition: background 0.3s, color 0.3s;
        }

        body.dark-mode {
            background: #121212;
            color: #fff;
        }

        /* Sign-In Container */
        .signin-container {
            background: #1e1e1e;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.9);
            text-align: center;
            width: 300px;
        }

        .signin-container h2 {
            margin-bottom: 20px;
        }

        .signin-container input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            background: #333;
            color: white;
        }

        .signin-container button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            background: #f90;
            color: white;
            cursor: pointer;
        }

        .signin-container button:hover {
            background: #e68000;
        }

        .remember-me {
            display: flex;
            align-items: center;
            margin: 10px 0;
        }

        .remember-me input {
            margin-right: 10px;
        }

        .social-login {
            margin-top: 20px;
        }

        .social-login a {
            margin: 0 10px;
            color: white;
            text-decoration: none;
        }

        .social-login a:hover {
            color: #f90;
        }

        .forgot-password {
            margin-top: 10px;
            color: #f90;
            text-decoration: none;
        }

        .forgot-password:hover {
            text-decoration: underline;
        }

        /* Music Website (Hidden Initially) */
        .music-website {
            display: none;
            width: 100%;
            height: 100%;
        }

        .music-website header {
            background: #1e1e1e;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .music-website .logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .music-website .logo svg {
            width: 40px;
            height: 40px;
        }

        .music-website .music-card {
            background: #1e1e1e;
            border: 1px solid #333;
            border-radius: 10px;
            padding: 15px;
            margin: 20px auto;
            max-width: 600px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .music-website audio {
            width: 100%;
            margin-top: 10px;
        }

        .music-website .progress-bar {
            width: 100%;
            height: 5px;
            background: #333;
            border-radius: 5px;
            margin-top: 10px;
            overflow: hidden;
        }

        .music-website .progress {
            height: 100%;
            background: #6b5b95;
            width: 0%;
            transition: width 0.1s;
        }

        .dark-mode-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #1e1e1e;
            border: 1px solid #333;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .dark-mode-toggle svg {
            width: 20px;
            height: 20px;
            fill: white;
        }

        .logout-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            padding: 10px 20px;
            background: #f90;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <!-- Sign-In Page -->
    <div class="signin-container" id="signin-container">
        <h2>SIGN IN</h2>
        <input type="text" placeholder="Username" id="username">
        <input type="password" placeholder="Password" id="password">
        <div class="remember-me">
            <input type="checkbox" id="rememberMe">
            <label for="rememberMe">Remember Me</label>
        </div>
        <button onclick="login()">Login</button>
        <div class="social-login">
            <a href="#">Google</a>
            <a href="#">Facebook</a>
            <a href="#">TikTok</a>
        </div>
        <a href="#" class="forgot-password">Forgot Password?</a>
    </div>

    <!-- Music Website (Hidden Initially) -->
    <div class="music-website" id="music-website">
        <header>
            <div class="logo">
                <svg viewBox="0 0 24 24">
                    <path d="M12 3v10.55c-.59-.34-1.27-.55-2-.55-2.21 0-4 1.79-4 4s1.79 4 4 4 4-1.79 4-4V7h4V3h-6z"/>
                </svg>
                <h1>Music Website</h1>
            </div>
        </header>

        <main>
            <div class="music-card">
                <strong>Song Title</strong> by Artist
                <audio id="audio" controls>
                    <source src="sample.mp3" type="audio/mpeg">
                    Your browser does not support the audio element.
                </audio>
                <div class="progress-bar">
                    <div class="progress" id="progress"></div>
                </div>
            </div>
        </main>

        <div class="dark-mode-toggle" id="dark-mode-toggle">
            <svg viewBox="0 0 24 24">
                <path d="M12 3c.132 0 .263 0 .393 0a7.5 7.5 0 0 0 7.92 12.446a9 9 0 1 1-8.313-12.454z"/>
            </svg>
        </div>

        <button class="logout-button" onclick="logout()">Logout</button>
    </div>

    <script>
        // Sign-In Functionality
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const rememberMe = document.getElementById('rememberMe').checked;

            // Simple validation (replace with actual authentication logic)
            if (username && password) {
                // Save credentials if "Remember Me" is checked
                if (rememberMe) {
                    localStorage.setItem('username', username);
                    localStorage.setItem('password', password);
                } else {
                    localStorage.removeItem('username');
                    localStorage.removeItem('password');
                }

                // Hide Sign-In Page and Show Music Website
                document.getElementById('signin-container').style.display = 'none';
                document.getElementById('music-website').style.display = 'block';
            } else {
                alert('Please enter a username and password.');
            }
        }

        // Load saved credentials if "Remember Me" was checked
        const savedUsername = localStorage.getItem('username');
        const savedPassword = localStorage.getItem('password');
        if (savedUsername && savedPassword) {
            document.getElementById('username').value = savedUsername;
            document.getElementById('password').value = savedPassword;
            document.getElementById('rememberMe').checked = true;
        }

        // Logout Functionality
        function logout() {
            // Hide Music Website and Show Sign-In Page
            document.getElementById('music-website').style.display = 'none';
            document.getElementById('signin-container').style.display = 'block';
        }

        // Dark Mode Toggle
        const toggle = document.getElementById('dark-mode-toggle');
        toggle.addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
            localStorage.setItem('theme', document.body.classList.contains('dark-mode') ? 'dark' : 'light');
        });

        // Load saved theme
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme === 'dark') document.body.classList.add('dark-mode');

        // Audio Progress Bar
        const audio = document.getElementById('audio');
        const progress = document.getElementById('progress');
        audio.addEventListener('timeupdate', () => {
            const percent = (audio.currentTime / audio.duration) * 100;
            progress.style.width = `${percent}%`;
        });
    </script>
</body>
</html>
