## 📄 Resume Generator Web Application (Forked & Customized)

###  Why Forking This Repository Was Important

Forking the original repository allowed me to create an **independent copy of the codebase** where I could safely experiment, customize, and enhance the application without impacting the original project.

By forking the repository, I was able to:
- Understand the existing project structure and deployment flow
- Make design and functionality changes freely
- Demonstrate ownership and customization of an open-source codebase
- Apply real-world DevOps and CI/CD practices on a forked project

This approach closely mirrors **enterprise development workflows**, where developers fork repositories, implement changes, and later raise pull requests.

---

## ✏️ Customization Overview

After forking the repository, I customized the application to function as a **dynamic resume generator web page**.

The main enhancement includes:
- Modifying the `index.jsp` file
- Replacing the default UI with a **responsive, modern resume layout**
- Adding structured sections such as:
  - About Me
  - Experience
  - Projects
  - Technical Skills
- Integrating external fonts and icons for better UI/UX
- Enabling resume download functionality

This change transforms the application from a basic JSP page into a **production-style personal portfolio and resume generator**.

---

## 🧩 Technical Highlights

- Frontend: HTML5, CSS3, Font Awesome, Google Fonts
- Backend: Java Web Application (JSP)
- DevOps: Git, GitHub, Jenkins, Docker
- Deployment Ready: Compatible with Apache Tomcat

---

## 🚀 Outcome

The forked and customized project now serves as:
- A **personal resume website**
- A **CI/CD deployment demo**
- A **hands-on DevOps learning project**
- A **portfolio artifact** showcasing real-world development practices

This demonstrates my ability to:
- Work with existing codebases
- Apply meaningful enhancements
- Follow industry-standard Git workflows
- Build and deploy end-to-end applications

Below is the code for web deplyment

```
# Navigate to the webapp directory
cd src/main/webapp

# Backup the existing index.jsp
cp index.jsp index.jsp.bak

# Replace index.jsp with the resume-generating HTML
cat << 'EOF' > index.jsp
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Siddhi Paswan | Data Engineer</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Fonts & Icons -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: #f4f6f8;
      color: #333;
    }

    header {
      background: linear-gradient(120deg, #2c3e50, #3498db);
      color: white;
      padding: 30px 40px;
    }

    .header-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 20px;
    }

    .intro h1 {
      margin: 0;
      font-size: 36px;
    }

    .intro p {
      margin: 6px 0 12px;
      font-size: 18px;
    }

    .download-btn {
      display: inline-block;
      padding: 10px 20px;
      background: #ffffff;
      color: #3498db;
      border-radius: 6px;
      font-weight: 600;
      text-decoration: none;
    }

    nav {
      background: white;
      display: flex;
      justify-content: center;
      gap: 20px;
      padding: 15px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    section {
      max-width: 1000px;
      margin: auto;
      padding: 40px 20px;
    }

    .card {
      background: white;
      padding: 20px;
      border-radius: 8px;
      margin-bottom: 20px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.08);
    }

    footer {
      background: #2c3e50;
      color: white;
      text-align: center;
      padding: 20px;
    }
  </style>
</head>

<body>

<header>
  <div class="header-container">
    <div class="intro">
      <h1>Siddhi Paswan</h1>
      <p>Data Engineer | Palantir Foundry | DevOps & Cloud</p>
      <a href="Siddhi_Paswan_Resume.pdf" download class="download-btn">
        <i class="fas fa-download"></i> Download Resume
      </a>
    </div>
  </div>
</header>

<section>
  <div class="card">
    Data Engineer with 3+ years of experience in scalable data pipelines,
    governance frameworks, cloud infrastructure, and DevOps automation.
  </div>
</section>

<footer>
  © 2026 Siddhi Paswan | CI/CD Powered Resume 🚀
</footer>

</body>
</html>
EOF

# Verify changes
git status

```