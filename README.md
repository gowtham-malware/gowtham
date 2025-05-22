import os
import zipfile

# Define the project structure
project_name = "gowtham-portfolio"
base_path = f"/mnt/data/{project_name}"
folders = [
    "public",
    "src",
    "src/components",
]
files = {
    "public/index.html": """<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Gowtham Reddy Portfolio</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
""",
    "src/index.js": """import React from "react";
import ReactDOM from "react-dom/client";
import Portfolio from "./components/Portfolio";
import "./index.css";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Portfolio />);
""",
    "src/components/Portfolio.js": """import React from "react";

export default function Portfolio() {
  return (
    <main className="p-6 max-w-5xl mx-auto">
      <section className="mb-12">
        <h1 className="text-4xl font-bold">Gowtham Reddy</h1>
        <p className="text-lg text-gray-600">Software Engineer | Full-Stack Developer</p>
        <p className="mt-2">📍 Irving, TX | 📧 gowthamkumar.ks98@gmail.com | 📞 +1 716-986-1568</p>
        <a className="text-blue-500 underline" href="#">LinkedIn</a>
      </section>

      <section className="mb-12">
        <h2 className="text-2xl font-semibold mb-2">About Me</h2>
        <p>
          Software Engineer with 4 years of experience in end-to-end development using Java,
          Spring Framework, React, and various databases. Experienced in deploying containerized
          applications on AWS EKS with Docker and Kubernetes. Passionate about building scalable,
          maintainable systems.
        </p>
      </section>

      <section className="mb-12">
        <h2 className="text-2xl font-semibold mb-2">Skills</h2>
        <ul className="list-disc list-inside">
          <li>Languages: Java, JavaScript, TypeScript, SQL</li>
          <li>Frameworks: Spring Boot, React, Node.js</li>
          <li>Cloud & DevOps: AWS (EKS, EC2, Lambda), Docker, Kubernetes</li>
          <li>Databases: MySQL, PostgreSQL, MongoDB, Neo4j</li>
          <li>Tools: Maven, Git, Jenkins, Swagger, Postman</li>
        </ul>
      </section>

      <section className="mb-12">
        <h2 className="text-2xl font-semibold mb-2">Projects</h2>
        <div className="mb-6">
          <h3 className="text-xl font-bold">Financial Microservices Platform</h3>
          <p>Built microservices using Spring Boot and React, integrated with REST and GraphQL APIs, and optimized DB queries for high transaction volumes.</p>
        </div>
        <div className="mb-6">
          <h3 className="text-xl font-bold">Vehicle Diagnostics Portal</h3>
          <p>Developed Angular-based dashboard with Spring Boot backend and integrated AWS services like DynamoDB, CodePipeline.</p>
        </div>
      </section>

      <section className="mb-12">
        <h2 className="text-2xl font-semibold mb-2">Experience</h2>
        <div className="mb-4">
          <h3 className="text-xl font-bold">M&T Bank, NY</h3>
          <p className="italic">Software Engineer | July 2023 – Present</p>
          <ul className="list-disc list-inside">
            <li>Built scalable microservices with Spring Boot</li>
            <li>Developed reusable React components</li>
            <li>Integrated APIs with REST and GraphQL</li>
          </ul>
        </div>
        <div className="mb-4">
          <h3 className="text-xl font-bold">Kpit Technologies, India</h3>
          <p className="italic">Software Engineer | July 2019 – June 2022</p>
          <ul className="list-disc list-inside">
            <li>Built Angular apps and Spring Boot microservices</li>
            <li>Automated deployment with AWS CodePipeline</li>
            <li>Implemented OAuth 2.0 and DynamoDB integration</li>
          </ul>
        </div>
      </section>

      <section>
        <h2 className="text-2xl font-semibold mb-2">Education</h2>
        <p>Master of Science in Computer Engineering, University at Buffalo, SUNY – June 2023</p>
      </section>
    </main>
  );
}
""",
    "src/index.css": """body {
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
  color: #333;
  margin: 0;
  padding: 0;
}
main {
  padding: 2rem;
}
""",
    "package.json": """{
  "name": "gowtham-portfolio",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
"""
}

# Create folders
for folder in folders:
    os.makedirs(os.path.join(base_path, folder), exist_ok=True)

# Create files
for path, content in files.items():
    with open(os.path.join(base_path, path), "w") as f:
        f.write(content)

# Zip the folder
zip_path = f"{base_path}.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as zipf:
    for root, _, filenames in os.walk(base_path):
        for filename in filenames:
            file_path = os.path.join(root, filename)
            zipf.write(file_path, os.path.relpath(file_path, base_path))

zip_path

