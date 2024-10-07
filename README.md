<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AlikKosarevskiy GitHub.io Page</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Welcome to My GitHub.io Page</h1>
  </header>

  <nav>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <section id="about">
    <h2>About Me</h2>
    <p>Write a brief introduction about yourself or your project.</p>
  </section>

  <section id="projects">
    <h2>My Projects</h2>
    <ul>
      <li><a href="https://github.com/user1/project1">Project 1</a></li>
      <li><a href="https://github.com/user1/project2">Project 2</a></li>
      <li><a href="https://github.com/user1/project3">Project 3</a></li>
    </ul>
  </section>

  <section id="contact">
    <h2>Contact Me</h2>
    <p>Email: user@example.com</p>
    <p>Phone: 123-456-7890</p>
  </section>

  <!-- JavaScript Demo Section -->
  <section id="js-demo">
    <h2>JavaScript Demo</h2>
    <p id="demo-text">Click the button to see some magic!</p>
    <button onclick="changeText()">Click Me</button>
  </section>

  <footer>
    <p>&copy; 2023 AlikKosarevskiy</p>
  </footer>

  <script>
    // Простая функция для изменения текста
    function changeText() {
      document.getElementById('demo-text').innerText = "You clicked the button! JavaScript is working!";
    }
  </script>
</body>
</html>
