# Types of QA Testing

## There are several types of testing in QA that are performed to ensure the quality and reliability of software applications. Here are some common types of QA testing examples using Java, JUnit4, Selenium WebDriver and OWASP ZAP.

#### 1. Unit Testing: This type of testing focuses on testing individual components or units of code in isolation to verify that they function correctly. This example displays a *Math class* with a simple add method and the corresponding unit test defines the *MathTest class*. After executing the test, the testing framework will provide a report indicating whether the test passed or failed, along with any additional information about the failures.

```java
// Math.java

public class Math {
    public static int add(int a, int b) {
        return a + b;
    }
}
```
```java
// MathTest.java

import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class MathTest {

    @Test
    public void testAdd() {
        int result = Math.add(2, 3);
        int expected = 5;
        assertEquals(expected, result);
    }
}
```

#### 2. Integration Testing: Integration testing is performed to test the interaction between different components or modules of an application. It ensures that the integrated components work together as expected. In this example, we have a **UserService** class that simulates fetching user data from a database or API. The *getUserById method* returns the name of the user with the given ID or null if the user is not found.

```java
// UserService.java

public class UserService {
    public String getUserById(int userId) {
        // Simulate fetching user data from a database or API
        if (userId == 1) {
            return "John Doe";
        } else {
            return null;
        }
    }
}
```
```java
// UserServiceIntegrationTest.java

import org.junit.Test;
import static org.junit.Assert.*;

public class UserServiceIntegrationTest {

    @Test
    public void testGetUserById() {
        UserService userService = new UserService();
        String user = userService.getUserById(1);
        assertNotNull(user);
        assertEquals("John Doe", user);
    }
}
```

#### 3. Functional Testing: Functional testing verifies that the software application meets the specified functional requirements. It involves testing the application's features and functionalities against the expected behavior. In this example, we have a *FunctionalTest class* that performs a functional test on a login form. We use Selenium WebDriver to interact with the web page and perform actions like entering input, clicking buttons, and verifying expected outcomes.

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;

import static org.junit.Assert.assertEquals;

public class FunctionalTest {

    private WebDriver driver;

    @Before
    public void setUp() {
        // Set up the WebDriver instance
        System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver");
        driver = new ChromeDriver();
    }

    @Test
    public void testLoginForm() {
        // Navigate to the login page
        driver.get("http://example.com/login");

        // Find the username and password input fields
        WebElement usernameInput = driver.findElement(By.id("username"));
        WebElement passwordInput = driver.findElement(By.id("password"));

        // Enter the username and password
        usernameInput.sendKeys("testuser");
        passwordInput.sendKeys("password");

        // Submit the form
        WebElement loginButton = driver.findElement(By.id("login-button"));
        loginButton.click();

        // Verify the login success message
        WebElement successMessage = driver.findElement(By.id("success-message"));
        String actualMessage = successMessage.getText();
        String expectedMessage = "Login successful";
        assertEquals(expectedMessage, actualMessage);
    }

    @After
    public void tearDown() {
        // Close the WebDriver instance
        driver.quit();
    }
}
```
#### 4. Performance Testing: Performance testing evaluates how well the application performs under various load conditions. It measures factors like response time, scalability, reliability, and resource usage to ensure that the application meets performance requirements. In this example, we have a *PerformanceTestRunner class* responsible for running the performance test. It uses JUnitCore to execute the *PerformanceTest class* and use *assertTrue* from JUnit to assert that the response time is within the acceptable limits. If the response time exceeds the maximum threshold, the test will fail.

```java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class PerformanceTestRunner {

    public static void main(String[] args) {
        Result result = JUnitCore.runClasses(PerformanceTest.class);

        if (result.wasSuccessful()) {
            System.out.println("Performance test passed successfully.");
        } else {
            System.out.println("Performance test failed:");
            for (Failure failure : result.getFailures()) {
                System.out.println(failure.toString());
            }
        }
    }
}
```
```java
import org.junit.Test;
import static org.junit.Assert.assertTrue;

public class PerformanceTest {

    @Test
    public void testResponseTime() throws InterruptedException {
        long startTime = System.currentTimeMillis();

        // Execute the performance test logic here
        // For example, make HTTP requests, perform database operations, etc.
        // Simulate a delay of 2 seconds
        Thread.sleep(2000);

        long endTime = System.currentTimeMillis();
        long responseTime = endTime - startTime;

        // Set the maximum response time in milliseconds
        long maxResponseTime = 3000;

        // Assert that the response time is within acceptable limits
        assertTrue("Response time exceeds the maximum threshold.", responseTime <= maxResponseTime);
    }
}
```
#### 5. Security Testing: Security testing is performed to identify vulnerabilities and weaknesses in the application's security controls. It involves testing for potential threats, unauthorized access, data breaches, and other security risks. In this example, we have a SecurityTest class responsible for running the security test. It uses the OWASP ZAP API to perform an active scan on the target URL.

```java
import java.io.File;
import java.io.IOException;
import java.net.MalformedURLException;
import java.net.URL;

import org.junit.AfterClass;
import org.junit.BeforeClass;
import org.junit.Test;
import org.zaproxy.clientapi.core.ClientApi;
import org.zaproxy.clientapi.core.ClientApiException;

import static org.junit.Assert.assertEquals;

public class SecurityTest {

    private static final String ZAP_PROXY_HOST = "localhost";
    private static final int ZAP_PROXY_PORT = 8080;
    private static final String TARGET_URL = "http://localhost:8081";
    private static final String API_KEY = null; // Set this to your ZAP API key if necessary
    private static ClientApi zapClient;

    @BeforeClass
    public static void setUp() throws ClientApiException, MalformedURLException {
        zapClient = new ClientApi(ZAP_PROXY_HOST, ZAP_PROXY_PORT);

        // Start a new session and spider the target URL
        zapClient.core.newSession();
        zapClient.spider.scan(TARGET_URL, null, null, null, null);

        // Wait for the spider to finish
        int progress;
        do {
            progress = Integer.parseInt(zapClient.spider.status(TARGET_URL));
        } while (progress < 100);

        // Save the ZAP session file for future use
        zapClient.core.saveSession("my-session", new File("my-session.session"), API_KEY);
    }

    @Test
    public void testSecurityScan() throws ClientApiException, IOException {
        // Load the saved session and perform an active scan on the target URL
        zapClient.core.loadSession("my-session", new File("my-session.session"), API_KEY);
        zapClient.ascan.scan(TARGET_URL, "True", "False", null, null, null, API_KEY);

        // Wait for the scan to finish
        int progress;
        do {
            progress = Integer.parseInt(zapClient.ascan.status());
        } while (progress < 100);

        // Get the number of alerts generated by the scan
        int numAlerts = zapClient.core.numberOfAlerts(TARGET_URL, null, null, API_KEY);

        // Assert that no high or medium severity alerts were generated
        assertEquals("Security test detected high or medium severity issues.", 0, numAlerts);
    }

    @AfterClass
    public static void tearDown() throws ClientApiException {
        // Shutdown the ZAP proxy
        zapClient.core.shutdown(API_KEY);
    }
}
```

#### 6. Regression Testing: Regression testing is done to ensure that recent changes or updates in the application do not introduce new bugs or issues and that existing functionality continues to work as expected.

#### 7. Usability Testing: Usability testing evaluates the application's user-friendliness and how easily users can interact with it. It focuses on aspects like user interface, navigation, user experience, and overall user satisfaction.

#### 8. Compatibility Testing: Compatibility testing checks the application's compatibility across different environments, platforms, browsers, and devices. It ensures that the application works correctly and consistently across a variety of configurations.

#### 9. Acceptance Testing: Acceptance testing is performed to determine whether the application meets the business requirements and is ready for deployment. It involves validating the application against user expectations and requirements.

#### 10. Exploratory Testing: Exploratory testing is a freestyle testing approach where testers explore the application without any predefined test cases. Testers use their domain knowledge and experience to uncover defects and gain insights into the application's behavior.

