<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SMM Panel - The Google SMM Clone</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
</head>
<body>

<!-- Navigation -->
<header>
    <nav>
        <div class="logo">The Google SMM</div>
        <ul class="menu">
            <li><a href="#login">Sign In</a></li>
            <li><a href="#signup">Sign Up</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#faq">FAQ</a></li>
        </ul>
    </nav>
</header>

<!-- Hero / Login Section -->
<section id="login" class="hero">
    <h1>Boost Your Online Presence!</h1>
    <form class="login-form">
        <input type="text" placeholder="Username or Email" required>
        <input type="password" placeholder="Password" required>
        <button type="submit">Sign In</button>
        <p><a href="#">Forgot Password?</a> | <a href="#signup">Sign Up</a></p>
    </form>
</section>

<!-- Why Choose Us -->
<section class="features">
    <h2>Why Choose Us?</h2>
    <div class="feature-grid">
        <div class="feature">Superb Quality</div>
        <div class="feature">Different Payment Options</div>
        <div class="feature">Extra Affordable</div>
        <div class="feature">Delivered Quickly</div>
    </div>
</section>

<!-- How It Works -->
<section class="how-it-works">
    <h2>How It Works</h2>
    <div class="steps">
        <div class="step">Sign Up</div>
        <div class="step">Add Funds</div>
        <div class="step">Select Services</div>
        <div class="step">Enjoy Results</div>
    </div>
</section>

<!-- Testimonials -->
<section class="testimonials">
    <h2>Success Stories</h2>
    <div class="testimonial">“This is the best solution for affordable social media growth!” – Jane K.</div>
    <div class="testimonial">“Fast delivery and cheap prices!” – Olivia J.</div>
</section>

<!-- FAQ -->
<section id="faq" class="faq">
    <h2>Top Questions</h2>
    <div class="question">What is an SMM panel?</div>
    <div class="answer">An online platform to buy social media services.</div>
    <div class="question">Are services safe?</div>
    <div class="answer">Yes – safe and account friendly.</div>
</section>

<!-- Footer -->
<footer>
    <p>&copy; 2025 The Google SMM Clone</p>
</footer>

</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #f9f9f9;
    color: #333;
}

/* Header */
header {
    background: #1e1e2f;
    padding: 15px;
}

header nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

header .logo {
    color: white;
    font-size: 24px;
    font-weight: bold;
}

header .menu li {
    display: inline;
    margin: 0 15px;
}

header .menu li a {
    color: white;
    text-decoration: none;
}

/* Hero */
.hero {
    padding: 60px 20px;
    text-align: center;
    background: #4b4b6e;
    color: white;
}

.hero h1 {
    margin-bottom: 20px;
}

.login-form input {
    width: 250px;
    padding: 10px;
    margin: 5px;
    border: none;
}

.login-form button {
    padding: 10px 20px;
    background: #f9c74f;
    border: none;
    cursor: pointer;
    font-weight: bold;
}

/* Features */
.features {
    padding: 40px 20px;
    text-align: center;
}

.feature-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
}

.feature {
    background: #fff;
    padding: 15px;
    border: 1px solid #ddd;
}

/* How It Works */
.how-it-works {
    padding: 40px 20px;
}

.steps {
    display: flex;
    justify-content: space-around;
}

.step {
    background: #ffbb00;
    padding: 15px;
    width: 150px;
    text-align: center;
    color: #1e1e1e;
}

/* Testimonials */
.testimonials {
    padding: 40px 20px;
    background: #fff;
}

.testimonials .testimonial {
    padding: 10px 0;
}

/* FAQ */
.faq {
    padding: 40px 20px;
}

.question {
    font-weight: bold;
    margin-top: 20px;
}


