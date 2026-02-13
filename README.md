<a id="top"></a>

<h1 align="center">🏥 Hospital Management System - Technical Debt Analysis</h1>

<p align="center">
Technical documentation focused on analyzing, identifying, and improving technical debt within the Hospital Management System.
</p>

<hr>

<h2>📋 Table of Contents</h2>

<ul>
  <li><a href="#project-description">📌 Project Description</a></li>
  <li><a href="#technical-debt">🔍 Technical Debt Analysis</a></li>
  <li><a href="#code-smells">🚨 Code Smells Identified</a></li>
  <li><a href="#refactoring">🔧 Refactoring Techniques</a></li>
  <li><a href="#implementation">✅ Implementation Plan</a></li>
  <li><a href="#git-workflow">📊 Git Workflow</a></li>
  <li><a href="#configuration">🛠 Project Configuration</a></li>
  <li><a href="#technologies">💻 Technologies</a></li>
  <li><a href="#contributing">📝 Contributing</a></li>
</ul>

<hr>

<h2 id="project-description">📌 Project Description</h2>

<p>
A web-based system designed to replace traditional paper-based hospital workflows with a secure and efficient digital platform.
</p>

<h3>Main Features</h3>

<ul>
<li>Patient and staff management</li>
<li>Automatic PDF prescription generation</li>
<li>OPD queue management</li>
<li>Role-based modules for doctors, receptionists, and administrators</li>
</ul>

<h3>📄 Original Documentation</h3>

<ul>
<li><a href="https://drive.google.com/file/d/1L6zUvNPXV4mYNnl2zLYyxvyz2RwoUt1G/view?usp=sharing">PPT Presentation</a></li>
<li><a href="https://drive.google.com/file/d/11DQDP_ZN2h7Cq3hiIRw3pCzPhR_VCL8p/view?usp=sharing">Project SRS</a></li>
<li><a href="https://drive.google.com/file/d/128Qn3pqBFj84w6OXBSwuWXYpag_Wn0dT/view?usp=sharing">Project Report</a></li>
<li><a href="https://youtu.be/SwE4mxQxhEI">Demo Video</a></li>
</ul>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="technical-debt">🔍 Technical Debt Analysis</h2>

<details>
<summary><strong>Analysis Methodology</strong></summary>

<br>

<ul>
<li>Manual source code review</li>
<li>Anti-pattern detection</li>
<li>Architecture evaluation</li>
<li>SOLID principles validation</li>
<li>Spring MVC & Hibernate best practices</li>
</ul>

<p><strong>TODO:</strong> Analyze the codebase and document technical debt issues.</p>

</details>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="code-smells">🚨 Code Smells Identified</h2>

<details open>
<summary><strong>Example: Tight Coupling</strong></summary>

<br>

<p><strong>Description:</strong> Controllers are tightly coupled with concrete service and DAO implementations.</p>

<p><strong>Location:</strong> <code>DoctorController.java</code></p>

<pre>
public class DoctorController {
    private DoctorServiceImpl doctorService;
    private PatientDAOImpl patientDAO;
}
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Harder unit testing</li>
<li>Low flexibility</li>
<li>Violates Dependency Inversion Principle</li>
</ul>

<p><strong>Recommendation:</strong> Use interfaces with dependency injection.</p>

</details>

<br>

<details>
<summary><strong>Common Code Smells To Evaluate</strong></summary>

<ul>
<li>God Classes</li>
<li>Long Methods</li>
<li>Code Duplication</li>
<li>Poor Exception Handling</li>
<li>Hardcoded Values</li>
<li>N+1 Queries</li>
<li>Missing DTOs</li>
<li>Lack of Logging</li>
<li>Missing Unit Tests</li>
</ul>

</details>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="refactoring">🔧 Refactoring Techniques Proposed</h2>

<details open>
<summary><strong>Extract Method Refactoring</strong></summary>

<br>

<p><strong>Purpose:</strong> Break long methods into smaller cohesive methods.</p>

<p><strong>Benefits:</strong></p>

<ul>
<li>Improved readability</li>
<li>Better testability</li>
<li>Higher maintainability</li>
<li>Increased reuse</li>
</ul>

</details>

<br>

<details>
<summary><strong>Other Planned Refactoring Techniques</strong></summary>

<ul>
<li>Extract Class</li>
<li>Introduce Parameter Object</li>
<li>Replace Conditional with Polymorphism</li>
<li>Repository Pattern</li>
<li>DTO Pattern</li>
<li>Dependency Injection</li>
<li>Global Exception Handling</li>
<li>Bean Validation</li>
<li>Query Optimization</li>
</ul>

</details>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="implementation">✅ Implementation Plan</h2>

<h3>Phase 1 – Low Risk</h3>

<ul>
<li>Logging integration</li>
<li>Constants classes</li>
<li>Bean validation</li>
<li>Code documentation</li>
</ul>

<h3>Phase 2 – Service Refactoring</h3>

<ul>
<li>Extract long methods</li>
<li>DTO implementation</li>
<li>Mapper creation</li>
</ul>

<h3>Phase 3 – Architecture Improvements</h3>

<ul>
<li>Repository pattern</li>
<li>Global exception handlers</li>
<li>Hibernate optimization</li>
</ul>

<h3>Phase 4 – Testing & Security</h3>

<ul>
<li>Unit tests</li>
<li>Integration tests</li>
<li>Security review</li>
<li>External configuration</li>
</ul>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="git-workflow">📊 Git Workflow</h2>

<pre>
git checkout main
git pull
git checkout -b feature/technical-debt-fixes
git add .
git commit -m "refactor: improve service separation"
git push origin feature/technical-debt-fixes
</pre>

<h3>Commit Convention</h3>

<ul>
<li>feat – New feature</li>
<li>fix – Bug fix</li>
<li>refactor – Code improvement</li>
<li>docs – Documentation</li>
<li>test – Testing</li>
<li>perf – Performance improvement</li>
</ul>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="configuration">🛠 Project Configuration</h2>

<details>
<summary><strong>Prerequisites</strong></summary>

<ul>
<li>JDK 8+</li>
<li>Apache Tomcat</li>
<li>MySQL</li>
<li>Maven</li>
<li>Eclipse IDE</li>
</ul>

</details>

<details>
<summary><strong>Run Steps</strong></summary>

<pre>
git clone &lt;repository-url&gt;
cd HospitalManagement
</pre>

<p>Import Maven project → Configure database → Run on Tomcat</p>

</details>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="technologies">💻 Technologies Used</h2>

<h3>Frontend</h3>
<ul>
<li>HTML5</li>
<li>CSS3</li>
<li>Bootstrap</li>
<li>JavaScript</li>
<li>jQuery</li>
</ul>

<h3>Backend</h3>
<ul>
<li>Java</li>
<li>Spring MVC</li>
<li>Hibernate</li>
<li>Spring Security</li>
<li>BCrypt</li>
</ul>

<h3>Database</h3>
<ul>
<li>MySQL</li>
</ul>

<h3>Tools</h3>
<ul>
<li>Maven</li>
<li>Git</li>
<li>Postman</li>
</ul>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<h2 id="contributing">📝 Contributing</h2>

<ol>
<li>Fork the repository</li>
<li>Create feature branch</li>
<li>Commit changes</li>
<li>Push branch</li>
<li>Create Pull Request</li>
</ol>

<h3>Code Guidelines</h3>

<ul>
<li>Follow Java naming conventions</li>
<li>Document public methods</li>
<li>Write tests</li>
<li>Single Responsibility Principle</li>
<li>Dependency Injection</li>
</ul>

<p align="right"><a href="#top">⬆ Back to top</a></p>

<h2 align="center">🤝 Team & Contact</h2>

<p align="center">
Create a GitHub issue for suggestions or questions.
</p>

<hr>

<p align="center">
<strong>Made with ❤️ to improve hospital management</strong>
</p>

<p align="center">
<em>Technical Debt Documentation – February 2026</em>
</p>
