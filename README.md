<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Portfolio</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: #0f172a;
      color: #e2e8f0;
      line-height: 1.6;
    }

    header {
      background: #020617;
      padding: 20px;
      text-align: center;
      position: sticky;
      top: 0;
    }

    header h1 {
      color: #38bdf8;
    }

    nav a {
      margin: 0 10px;
      color: #cbd5f5;
      text-decoration: none;
    }

    nav a:hover {
      color: #38bdf8;
    }

    section {
      padding: 60px 20px;
      max-width: 900px;
      margin: auto;
    }

    .hero {
      text-align: center;
      padding-top: 80px;
    }

    .hero h2 {
      font-size: 2.5rem;
      color: #38bdf8;
    }

    .projects {
      display: grid;
      gap: 20px;
    }

    .card {
      background: #1e293b;
      padding: 20px;
      border-radius: 10px;
      transition: 0.3s;
    }

    .card:hover {
      transform: translateY(-5px);
      background: #334155;
    }

    .btn {
      display: inline-block;
      margin-top: 10px;
      padding: 10px 15px;
      background: #38bdf8;
      color: black;
      text-decoration: none;
      border-radius: 5px;
    }

    footer {
      text-align: center;
      padding: 20px;
      background: #020617;
      margin-top: 40px;
    }
  </style>
</head>

<body>

<header>
  <h1>Your Name</h1>
  <nav>
    <a href="#about">About</a>
    <a href="#projects">Projects</a>
    <a href="#contact">Contact</a>
  </nav>
</header>

<section class="hero">
  <h2>Hi, I'm Jason 👋</h2>
  <p>Aspiring Developer | Cybersecurity | Data Projects</p>
</section>

<section id="about">
  <h2>About Me</h2>
  <p>
    I'm a university student interested in cybersecurity, data analytics, and building real-world projects.
    I enjoy creating applications, experimenting with security labs, and learning new technologies.
  </p>
</section>

<section id="projects">
  <h2>Projects</h2>

  <div class="projects">
    <div class="card">
      <h3>Cybersecurity Lab</h3>
      <p>Simulated vulnerabilities and penetration testing scenarios.</p>
      <a href="#" class="btn">View Project</a>
    </div>

    <div class="card">
      <h3>Data Analysis Project</h3>
      <p>Analyzed datasets using Python and visualized insights.</p>
      <a href="#" class="btn">View Project</a>
    </div>

    <div class="card">
      <h3>Portfolio Website</h3>
      <p>This website showcasing my work and skills.</p>
      <a href="#" class="btn">View Project</a>
    </div>
  </div>
</section>

<section id="contact">
  <h2>Contact</h2>
  <p>Email: your@email.com</p>
  <p>GitHub: github.com/yourusername</p>
</section>

<footer>
  <p>© 2026 Your Name</p>
</footer>

<script>
  console.log("Portfolio Loaded 🚀");
</script>

</body>
</html>
