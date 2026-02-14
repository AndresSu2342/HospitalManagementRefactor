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

<br>

<details open>
<summary><strong>1. Tight Coupling</strong></summary>

<br>

<p><strong>Location:</strong> Multiple Controllers and DAOs</p>

<p><strong>Description:</strong> Controllers are directly coupled to concrete implementations instead of interfaces.</p>

<p><strong>Example:</strong></p>

<pre>
@Autowired
DeleteOpdDao dao1;

@Autowired
OpdDetailsDao dao2;

@Autowired
PatientPrescriptionDao dao3;
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Difficult unit testing (mocks cannot be easily created)</li>
<li>Violates Dependency Inversion Principle (SOLID)</li>
<li>Low flexibility and maintainability</li>
<li>Hard to replace implementations</li>
</ul>

</details>

<br>

<details>
<summary><strong>2. God Class</strong></summary>

<br>

<p><strong>Location:</strong> LoginDao.java</p>

<p><strong>Description:</strong> The LoginDao class contains multiple unrelated responsibilities (validation, logging, self-injection).</p>

<pre>
@Autowired
LoginDao infoLog;  // Self-injection - bad practice
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Violates Single Responsibility Principle (SRP)</li>
<li>Difficult to test and maintain</li>
<li>Confusing class purpose</li>
</ul>

</details>

<br>

<details>
<summary><strong>3. Poor Exception Handling</strong></summary>

<br>

<p><strong>Location:</strong> Multiple Controllers and DAOs</p>

<p><strong>Examples:</strong></p>

<pre>
// Incorrect null check and generic exception
if (!e1.getEid().equals(null)) {
    ...
} else {
    throw new Exception();
}
</pre>

<pre>
// Exception swallowed
catch (Exception e) {
    infoLog.logActivities("in DeleteOpdDao-delete: " + e);
    return 0;
}
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Loss of error information</li>
<li>Difficult debugging</li>
<li>Poor production traceability</li>
<li>Bad user experience</li>
</ul>

</details>

<br>

<details>
<summary><strong>4. Commented Out Code</strong></summary>

<br>

<p><strong>Location:</strong> AddPatientDao.java, LoginDao.java</p>

<pre>
// try {
//     ...
// } catch (Exception e) {
//     return false;
// }
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Code clutter</li>
<li>Confusion for developers</li>
<li>Version control should manage history, not source files</li>
</ul>

</details>

<br>

<details>
<summary><strong>5. Hardcoded Values / Magic Numbers</strong></summary>

<br>

<p><strong>Location:</strong> Multiple classes</p>

<pre>
q1.setParameter("s", 0);
q1.setParameter("s", 1);

if (i == 1) { ... }
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Not self-documenting</li>
<li>Error-prone</li>
<li>Difficult to maintain</li>
</ul>

</details>

<br>

<details>
<summary><strong>6. Missing DTOs</strong></summary>

<br>

<p><strong>Location:</strong> Entire system</p>

<p><strong>Description:</strong> JPA entities are exposed directly to the presentation layer.</p>

<p><strong>Impact:</strong></p>

<ul>
<li>Possible LazyInitializationException</li>
<li>Tight coupling between layers</li>
<li>Exposure of sensitive data</li>
<li>Difficult API versioning</li>
</ul>

</details>

<br>

<details>
<summary><strong>7. Lack of Proper Logging</strong></summary>

<br>

<pre>
public void logActivities(String s) {
    // System.out.println("@"+s);
}
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>No production logs</li>
<li>No log levels (INFO, DEBUG, ERROR)</li>
<li>Impossible debugging</li>
<li>No external configuration</li>
</ul>

</details>

<br>

<details>
<summary><strong>8. Inconsistent Null Checking</strong></summary>

<br>

<pre>
if (!e1.getEid().equals(null))  // Incorrect
if (!patients.equals(null))    // Incorrect
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Possible NullPointerException</li>
<li>Confusing inverted logic</li>
</ul>

</details>

<br>

<details>
<summary><strong>9. Primitive DTOs / Array Misuse</strong></summary>

<br>

<pre>
String[] temp = new String[3];
temp[0] = ...
temp[1] = ...
temp[2] = ...
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Not type-safe</li>
<li>Hard to understand</li>
<li>Index-based errors</li>
</ul>

</details>

<br>

<details>
<summary><strong>10. Potential N+1 Query Problem</strong></summary>

<br>

<pre>
for (Opd opd : l1) {
    temp[1] = dao2.searchDoctorAssigned(did);
}
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Performance degradation</li>
<li>Multiple unnecessary DB queries</li>
</ul>

</details>

<br>

<details>
<summary><strong>11. Unused Imports and Variables</strong></summary>

<br>

<pre>
import com.project.entity.Login;

int i = 0, j = 0;
</pre>

<p><strong>Impact:</strong></p>

<ul>
<li>Code clutter</li>
<li>Reduced readability</li>
<li>Poor code hygiene</li>
</ul>

</details>

<br>

<details>
<summary><strong>12. Missing Unit Tests</strong></summary>

<br>

<p><strong>Observation:</strong> No test files were found in the repository.</p>

<p><strong>Impact:</strong></p>

<ul>
<li>No quality guarantee</li>
<li>Risky refactoring</li>
<li>Hard to detect regressions</li>
</ul>

</details>


<p align="right"><a href="#top">⬆ Back to top</a></p>

<hr>

<h2 id="refactoring">🔧 Refactoring Techniques Proposed</h2>

<details>

<summary><strong>Planned Refactoring Techniques</strong></summary>

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

<br>

<details open>
<summary><strong>1: Extract Interface</strong></summary>

<br>

<p><strong>Apply to:</strong> All DAOs</p>

<p><strong>Before:</strong></p>

<pre>
@Autowired
DeleteOpdDao dao1;
</pre>

<p><strong>After:</strong></p>

<pre>
public interface OpdService {
    int delete(String pid);
}

@Autowired
private OpdService opdService;
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Reduces coupling</li>
<li>Improves testability with mocks</li>
<li>Complies with Dependency Inversion Principle</li>
<li>Encourages clean architecture</li>
<li>Improves flexibility for future implementations</li>
</ul>

</details>

<br>

<details>
<summary><strong>2: Replace Magic Numbers with Constants</strong></summary>

<br>

<p><strong>Apply to:</strong> Entire system</p>

<p><strong>Before:</strong></p>

<pre>
q1.setParameter("s", 0);
if(i == 1) { }
</pre>

<p><strong>After:</strong></p>

<pre>
public class OpdStatus {
    public static final int DONE = 0;
    public static final int PENDING = 1;
    public static final int PRINTING = 2;
}

q1.setParameter("s", OpdStatus.DONE);
if(i == OperationResult.SUCCESS) { }
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Self-documenting code</li>
<li>Improved readability</li>
<li>Reduced risk of logical errors</li>
<li>Centralized status management</li>
<li>Easier future modifications</li>
</ul>

</details>

<br>

<details>
<summary><strong>3: Extract Method</strong></summary>

<br>

<p><strong>Apply to:</strong> Long DAO methods</p>

<p><strong>Before (AddPatientDao.java):</strong></p>

<pre>
public boolean add(Patient p1) {
    // 30+ lines of code
    // Save patient
    // Increment ID
    // Multiple responsibilities
}
</pre>

<p><strong>After:</strong></p>

<pre>
public boolean add(Patient p1) {
    savePatient(p1);
    incrementPatientId();
    return true;
}

private void savePatient(Patient p1) { /* ... */ }
private void incrementPatientId() { /* ... */ }
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Improved readability</li>
<li>Single Responsibility compliance</li>
<li>Better unit testing</li>
<li>Easier debugging</li>
<li>Encourages code reuse</li>
</ul>

</details>

<br>

<details>
<summary><strong>4: Introduce Service Layer</strong></summary>

<br>

<p><strong>Apply to:</strong> Controllers calling DAOs directly</p>

<p><strong>Before:</strong></p>

<pre>
@Controller
public class DeleteOpdController {

    @Autowired DeleteOpdDao dao1;
    @Autowired OpdDetailsDao dao2;

    public ModelAndView delete(String pid) {
        dao1.delete(pid);
        dao2.opdQueue();
    }
}
</pre>

<p><strong>After:</strong></p>

<pre>
@Controller
public class OpdController {

    @Autowired
    private OpdService opdService;

    public ModelAndView delete(String pid) {
        opdService.deleteOpd(pid);
    }
}

@Service
public class OpdServiceImpl implements OpdService {
    // Business logic here
}
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Clear separation of concerns</li>
<li>Better layering (Controller → Service → DAO)</li>
<li>Centralized business logic</li>
<li>Improved maintainability</li>
<li>Easier testing of business logic</li>
</ul>

</details>

<br>

<details>
<summary><strong>5: Replace Conditional Logic with Strategy Pattern</strong></summary>

<br>

<p><strong>Apply to:</strong> OPD state logic</p>

<p><strong>Description:</strong> Replace large conditional blocks depending on status with strategy classes.</p>

<p><strong>Example Structure:</strong></p>

<pre>
public interface OpdStateStrategy {
    void process(Opd opd);
}

public class PendingState implements OpdStateStrategy {
    public void process(Opd opd) {
        // Logic for pending
    }
}
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Eliminates complex conditional blocks</li>
<li>Open/Closed Principle compliance</li>
<li>Easier extension for new states</li>
<li>Cleaner and more scalable design</li>
<li>Improved maintainability</li>
</ul>

</details>

<br>

<details>
<summary><strong>6: Introduce DTOs</strong></summary>

<br>

<p><strong>Before:</strong></p>

<pre>
mv.addObject("employee", e1); // Direct entity exposure
</pre>

<p><strong>After:</strong></p>

<pre>
EmployeeDTO dto = employeeMapper.toDTO(e1);
mv.addObject("employee", dto);
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Prevents LazyInitializationException</li>
<li>Avoids exposing sensitive data</li>
<li>Better API versioning support</li>
<li>Clear separation between layers</li>
<li>Improved security and encapsulation</li>
</ul>

</details>

<br>

<details>
<summary><strong>7: Replace Custom Logging with SLF4J / Logback</strong></summary>

<br>

<p><strong>Before:</strong></p>

<pre>
infoLog.logActivities("in DeleteOpdDao-delete: got= " + pid);
</pre>

<p><strong>After:</strong></p>

<pre>
private static final Logger logger =
    LoggerFactory.getLogger(DeleteOpdDao.class);

logger.debug("Deleting OPD with pid: {}", pid);
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Structured logging</li>
<li>Log levels support (INFO, DEBUG, ERROR)</li>
<li>External configuration capability</li>
<li>Production-ready logging</li>
<li>Better monitoring and observability</li>
</ul>

</details>

<br>

<details>
<summary><strong>8: Null Object Pattern</strong></summary>

<br>

<p><strong>Apply to:</strong> Null validations</p>

<p><strong>Before:</strong></p>

<pre>
if(!e1.getEid().equals(null)) { }
</pre>

<p><strong>After:</strong></p>

<pre>
if(e1 != null && StringUtils.isNotEmpty(e1.getEid())) { }
// Or use Optional<Employee>
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Prevents NullPointerException</li>
<li>Cleaner validation logic</li>
<li>Improved robustness</li>
<li>More readable conditions</li>
<li>Safer null handling strategy</li>
</ul>

</details>

<br>

<details>
<summary><strong>9: Repository Pattern</strong></summary>

<br>

<p><strong>Description:</strong> Introduce a repository layer between services and data access logic.</p>

<pre>
public interface PatientRepository extends JpaRepository&lt;Patient, Long&gt; {
}
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Encapsulates persistence logic</li>
<li>Improves abstraction</li>
<li>Reduces boilerplate DAO code</li>
<li>Better integration with Spring Data</li>
<li>Cleaner separation of layers</li>
</ul>

</details>

<br>

<details>
<summary><strong>10: Global Exception Handler</strong></summary>

<br>

<p><strong>Implementation:</strong></p>

<pre>
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EntityNotFoundException.class)
    public ModelAndView handleNotFound(EntityNotFoundException ex) {
        // Centralized exception handling
    }
}
</pre>

<p><strong>Benefits:</strong></p>

<ul>
<li>Centralized error handling</li>
<li>Cleaner controllers</li>
<li>Consistent error responses</li>
<li>Improved maintainability</li>
<li>Better user experience</li>
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
