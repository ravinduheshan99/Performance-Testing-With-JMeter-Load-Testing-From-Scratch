# Performance Testing With JMeter - Load Testing From Scratch

A comprehensive repository documenting my learning and practical exercises from the Top-Class JMeter Load Testing course. This project focuses on building skills in performance and load testing for web applications and REST APIs using Apache JMeter. It also includes scripting, data-driven testing, correlation techniques, and Selenium integration.

---

## 📘 Course Overview

This repository is based on a complete JMeter training program that takes the learner from basic setup to advanced performance testing. The course covers UI components, Thread Groups, Listeners, Controllers, Assertions, Timers, correlation methods, and Beanshell scripting, along with Selenium integration for real scenarios.

By the end of the course, the learner is expected to design stable performance test cases, monitor how an application behaves under load, and prepare reports that support performance analysis.

---

## 🎯 Learning Objectives

This project helps develop the following skills:

- Setting up JMeter and understanding its UI  
- Recording and replaying scenarios with HTTP Proxy  
- Designing Thread Groups and applying load  
- Monitoring performance through Listeners and reporting plugins  
- Implementing Assertions and Controllers  
- Using Timers, including Constant Throughput Timer  
- Running data-driven tests with external files  
- Extracting dynamic values with Regular Expressions and correlation  
- Managing cookies and parsing links  
- Writing Beanshell scripts inside test elements  
- Integrating Selenium test cases with JMeter  
- Performing REST API load testing and studying response trends  

---

# 📚 Notes

The following notes cover theory and explanations from Sections 01 to 03 of the course. They summarize the core ideas of JMeter, including installation, recording, thread groups, and performance metrics.

---

## Section 01 - Introduction  
### Introduction to JMeter

Apache JMeter is an open-source tool used to measure performance and apply load on web applications, APIs, and backend systems. It is widely used for HTTP and REST API testing, but it also supports JDBC, FTP, SMTP, SOAP, JMS, and other protocols.

---

### Advantages of JMeter

- Open source and free to use  
- Supports many protocols  
- Runs on any operating system with Java  
- Extensible through plugins  
- Works well with CI/CD pipelines  
- Good support for scripting and parameterization  
- Clear interface for building test plans  

---

### Installation and Setup

JMeter requires a Java installation. After downloading JMeter from the Apache website, extract the archive and run it using the provided scripts:

- Windows: `jmeter.bat`  
- macOS / Linux: `jmeter.sh`  

No system-level installation is required.

---

### JMeter Interface Overview

JMeter uses a simple and structured interface built around test elements.

- **Test Plan**  
  Main container that holds all elements.

- **Workbench**  
  A temporary area that does not get saved.  
  Contains the **HTTP(S) Test Script Recorder** for capturing browser traffic.

---

### Recording and Playback Overview

Recording helps capture real browser interactions and convert them into a script.

Reasons to record:

- Captures real user behaviour  
- Speeds up creation of test plans  
- Helps build accurate load models  

Recorded traffic may include images, scripts, and cached assets. These should be cleaned after recording.

---

### Requirements for Recording

1. JMeter  
2. Firefox or Chrome  
3. Correct proxy configuration  
4. Installed JMeter certificate for HTTPS recording  

---

### Handling HTTPS

JMeter generates a certificate in the `bin` folder. Import it into the browser to avoid security warnings when capturing HTTPS traffic.

---

### Recording Using Chrome (BlazeMeter Extension)

The BlazeMeter extension provides a simpler recording option:

- No manual proxy setup  
- Works well with HTTPS  
- Exports recordings as `.jmx` files  
- Easy for beginners  

Extension link:  
https://chrome.google.com/webstore/detail/blazemeter-the-load-testi/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en

---

### Version Notes

UI and plugin availability may vary across versions. Larger test examples may include:

- 500 or more virtual users  
- Multiple iterations  
- Long-duration load scenarios  

These examples help understand scaling and throughput behaviour.

---

## Section 02 - Recording JMeter Scripts  
### Effective Learning Tips

- Record several scenarios for practice  
- Remove unnecessary requests  
- Validate scripts with a small load  
- Use View Results Tree to debug  

---

### Recording the Application Under Test

Typical workflow:

1. Start JMeter or BlazeMeter recorder  
2. Record the user flow in the browser  
3. Verify the captured samplers  
4. Remove unnecessary elements  
5. Add controllers and timers  
6. Validate the script before applying load  

---

### Playback of Recorded Scripts

When replaying:

- Check status codes  
- Validate response data  
- Organize samplers into logical groups  
- Confirm behaviour before high load execution  

---

## Section 03 - Applying Load and Analysing Performance  
### Thread Groups

A Thread Group defines the virtual user configuration.

Core settings:

- **Threads (Users)**  
- **Ramp-up Period**  
- **Loop Count**  

Example:  
100 users with a 10-second ramp-up results in 10 users starting each second.

---

### Applying Load

Load is shaped by:

- User count  
- Ramp-up speed  
- Loop behaviour  

Each virtual user runs independently through the same samplers.

---

### Understanding Listeners

Listeners collect execution data and display results.

Common listeners:

- **View Results Tree**  
  Debugging and inspecting responses.

- **Aggregate Report**  
  Shows averages, minimums, maximums, errors, and throughput.

- **Graph Results**  
  Simple visual summary.

---

### Key Metrics

- **Samples**  
  Number of executed requests.

- **Average Response Time**  
  Mean time taken for requests.

- **Minimum and Maximum**  
  Fastest and slowest responses.

- **Standard Deviation**  
  Variation in response times.

- **Error Percentage**  
  Ratio of failed samples.

- **Throughput**  
  Requests processed per second, minute, or hour.

- **Median**  
  Middle value in response times.

- **90th Percentile**  
  Time within which 90 percent of responses completed. Important for performance assessment.

---

### JMeter Plugins

Plugins provide more control and flexibility.

Useful plugins:

- Concurrency Thread Group  
- Ultimate Thread Group  

Install through the JMeter Plugins Manager:  
https://jmeter-plugins.org/wiki/PluginsManager/

---

### Example Analysis Notes

- A 200 response code does not always confirm success. The response body must be checked.  
- For sample times such as 12 ms, 15 ms, and 30 ms:  
  - Average = 19  
  - Minimum = 12  
  - Maximum = 30  

Example under heavy load:

- Around 100 virtual users  
- Throughput near 300 requests per second  
- Roughly 200 requests processed for a specific sampler  

Throughput helps determine how well a server handles increased load.

---

## Section 04 - Advanced Thread Group Methods for Real-Time Load  

This section introduces additional JMeter plugins that enable realistic and flexible load patterns. These tools allow precise control over how users start, hold, and stop during a test. They are especially useful for modeling production-like scenarios.

---

### Additional Plugins for Advanced Load Models  

JMeter’s plugin manager provides extended thread groups that simulate complex load behavior, including gradual user growth, constant concurrency, and staged spikes. These thread groups are ideal for long-duration or multi-stage load tests.  

**Installation:**  
Install through the JMeter Plugins Manager. After installation, the new thread groups appear in the **Thread Group** menu of the Test Plan.

---

### Concurrency Thread Group  

The Concurrency Thread Group focuses on maintaining a steady number of active virtual users, rather than just controlling the total number of threads.  

**Key Settings:**  
- Target Concurrency  
- Ramp-up Time  
- Hold Target Rate Time  
- Ramp-down Time  
- Steps (optional)  

**Behavior:**  
The plugin keeps the number of active threads equal to the target concurrency. If a thread finishes early, a new one starts automatically to maintain the load.  

**Example:**  
- Target concurrency: 50  
- Ramp-up: 20 seconds  
- Hold: 2 minutes  
- Ramp-down: 15 seconds  

This configuration gradually ramps up to 50 users, maintains the load for 2 minutes, then ramps down smoothly.  

**Use Cases:**  
- Steady-state load testing  
- Baseline performance checks  
- Scenarios requiring consistent active user counts  

---

### Ultimate Thread Group  

The Ultimate Thread Group provides precise, multi-stage load control. Each stage can be configured with exact user count, ramp-up, hold, and ramp-down durations.  

**Configuration Parameters:**  
- Number of users  
- Ramp-up duration  
- Hold duration  
- Ramp-down duration  

**Example Scenario:**  

| Stage | Users | Ramp-up | Hold | Ramp-down |  
|-------|-------|---------|------|-----------|  
| 1     | 30    | 10s     | 1m   | 10s       |  
| 2     | 50    | 20s     | 2m   | 20s       |  

This simulates a staged increase in load, producing realistic server stress patterns.  

**Use Cases:**  
- Capacity planning  
- Stress tests with multiple waves  
- Long-running endurance testing  
- Production-like load simulation  

---

### Why Advanced Thread Groups Matter  

Default Thread Groups are sufficient for simple tests, but cannot model real-world traffic accurately. Advanced thread groups:  

- Maintain steady concurrency for meaningful measurements  
- Simulate gradual or staged load changes  
- Prevent unrealistic spikes from simultaneous user starts  
- Allow long-duration tests that reveal performance trends  

Using these thread groups results in more accurate performance data and insights relevant to real-world scenarios.

---

## Section 05 - HTTP Cookie Manager to Capture Sessions

HTTP Cookie Manager allows JMeter to store and send cookies automatically while executing requests. This simulates a real browser’s behavior and is essential for applications that maintain session state across multiple requests.

---

### Why We Need a Cookie Manager

- Many web applications use cookies to track user sessions.  
- Without a cookie manager, requests may appear as separate users, causing test failures or inaccurate results.  
- Ensures continuity of login sessions, shopping carts, and other user-specific flows.  

---

### Usage of Cookie Manager in JMeter Tests

1. Add **HTTP Cookie Manager** to your Test Plan or Thread Group.  
2. By default, it stores cookies sent by the server and automatically includes them in subsequent requests.  
3. You can configure it to:  
   - Clear cookies each iteration  
   - Use a specific policy (standard, Netscape, or best-match)  
   - Store cookies for multiple domains  

**Example:**  
- User logs in → Server sends session cookie  
- Cookie Manager saves the session cookie  
- Subsequent requests include the cookie → Server recognizes the user session  

**Use Cases:**  
- Login/logout scenarios  
- Maintaining sessions across multiple pages  
- E-commerce flows with shopping carts  
- Any scenario requiring session continuity

---

## Section 06 – Assertions in JMeter

Assertions in JMeter are used to validate responses and determine whether a request has passed or failed. They are essential for ensuring that the application behaves as expected under load.

---

### How to Validate JMeter Tests – Pass/Fail Status

- Assertions evaluate the response of a sampler.  
- If the response does not meet the defined criteria, the sampler is marked as **failed**.  
- Results can be observed in listeners such as **View Results Tree** or **Aggregate Report**.

---

### Types of Assertions

JMeter provides several types of assertions to validate test results:

1. **Response Assertion**  
   - Checks if the response contains, matches, or does not contain a specific string or pattern.  
   - Example: Validate that the login response contains "Welcome, user".  

2. **Size Assertion**  
   - Validates the size of the response in bytes.  
   - Example: Ensure that the response payload is exactly 1024 bytes.  

3. **Duration Assertion**  
   - Checks that the response time is within an expected limit.  
   - Example: Fail the request if it takes longer than 500 ms.  

**Use Cases:**  
- Verify correct page content is returned  
- Ensure API responses are within acceptable size limits  
- Monitor performance thresholds and response times  

By adding assertions, your JMeter test becomes more reliable and provides meaningful Pass/Fail results during load testing.

---

## Section 07 - JMeter Controllers for Module-Wise Metrics  

### Understanding Controllers in Performance Tests  
Controllers shape test flow and let separate parts of a script act like real modules of an application. As test plans grow, controllers make it easier to organise samplers, compare the performance of different user paths, and track module-level behaviour.

---

### Module Controller and Include Controller  
Use these controllers to reuse test fragments and keep large test plans modular and maintainable.

**Module Controller**  
- Selects and runs another Controller or sampler defined elsewhere in the same Test Plan.  
- Useful for calling a common module, for example, a login flow, from multiple places without duplicating samplers.  
- Keep the target module inside a named controller or Test Fragment and point the Module Controller to it.

**Include Controller**  
- Loads an external `.jmx` test fragment at runtime.  
- Helps split large test suites across files and share common modules across projects.  
- The included file should contain the module under a Simple Controller or Test Fragment.

**Test Fragment**  
- A special container intended for reusable modules.  
- Not executed on its own. Use Module Controller or Include Controller to invoke it.

**Example usage**  
1. Create a Test Fragment or Simple Controller named `Login Module` with login samplers.  
2. Add a Module Controller in each place where login is needed and select `Login Module` as the target.  
3. To reuse `Login Module` across repositories, move it to `login-module.jmx` and use an Include Controller to load it.

**Benefits**  
- Single source of truth for common flows  
- Easier updates and debugging  
- Cleaner metrics per module when used with Transaction Controllers

---

### Transaction Controller  
A Transaction Controller groups several samplers and records a single time for the group. This helps measure the end-to-end response time of a complete user action, such as login, profile load, or booking.

Key notes:  
- Measures the combined time of child samplers  
- Can include or exclude the time of child controllers  
- Useful for module-wise performance tracking  

Example:  
A login flow with three requests can be placed under one Transaction Controller to compare the full login time against other modules.

---

### Simple Controller  
A Simple Controller keeps related samplers together for readability. It does not create extra metrics by itself.

Used for:  
- Structuring scripts  
- Keeping modules separate  
- Cleaning complex test plans  

Example:  
A “Search Module” can sit inside a Simple Controller to hold the search page load, search action, and item selection requests.

---

### Interleave Controller  
The Interleave Controller runs one child element per loop. This helps mimic users who move across different modules during a session.

Typical use cases:  
- Running “A → B → C” samplers in rotation  
- Simulating alternating user flows  
- Reducing repetitive execution of large blocks  

---

### Runtime Controller  
A Runtime Controller runs its child samplers for a fixed length of time.

This is helpful when:  
- You need constant activity under a time budget  
- Certain modules must run for a set duration  
- Planning stress scenarios where some calls must be repeated for long periods  

Example:  
Run a search request for 60 seconds while other modules continue normally.

---

### Random Controller  
A Random Controller selects one of its child samplers at random for each loop.

Used for:  
- Creating variation in test flows  
- Simulating unpredictable user behaviour  
- Avoiding too-rigid sequences during load tests  

---

### If Controller  
The If Controller runs its children when a condition is true. It supports JMeter variables and functions.

Helpful for:  
- Conditional navigation  
- Testing flows based on dynamic server responses  
- Running samplers only when certain values exist  

Example:  
If a response contains a session token, run the next step.

---

### Loop Controller  
A Loop Controller repeats its child samplers any number of times.

Used to:  
- Stress-test specific modules  
- Repeat a particular request inside a larger flow  
- Increase load on one part of the application  

Example:  
Repeat a search action 50 times inside a single user session.

---

### Practical Example in WebTours Demo  
The WebTours sample application shows how controllers can separate login, search, booking, and sign-off modules. Each module can be grouped under Transaction Controllers, with a reusable login placed in a Test Fragment and invoked by Module Controllers. This arrangement makes it easy to measure which module slows down under load and to reuse common flows across scenarios.

---

This section explains how controllers produce readable, scalable scripts and how they support module-wise performance analysis as test plans grow more advanced.

---

## Section 08 - Timers in JMeter  

### Understanding Timers  
Timers in JMeter are used to introduce delays between requests. This helps simulate real user behavior, as users do not send requests continuously without pause. Proper use of timers ensures a more realistic load and prevents servers from being overloaded unnaturally.  

---

### Common Timer Types

1. **Constant Timer**  
   - Adds a fixed delay between requests.  
   - Example: A 2-second delay between each sampler to simulate user think time.  

2. **Gaussian Random Timer**  
   - Adds a variable delay based on a Gaussian distribution.  
   - Produces a more natural, realistic delay pattern.  
   - Example: Average delay = 2000 ms, deviation = 500 ms → most delays fall between 1500–2500 ms.  

3. **Constant Throughput Timer**  
   - Controls throughput rather than individual delays.  
   - Ensures that a target number of requests per minute/second is maintained.  
   - Example: Target throughput = 60 requests per minute → timer adjusts delays dynamically to maintain this rate.  

---

### Why Timers Matter

- Prevents sending all requests at once, which can overload the server.  
- Simulates real user think time.  
- Helps maintain consistent throughput for performance testing.  
- Works with different Thread Groups and Controllers to shape load effectively.  

---

### Practical Example

- Scenario: Login → Search → Booking  
- Apply a Constant Timer of 2 seconds between each sampler to mimic the user's reading/thinking time.  
- Use Gaussian Random Timer on search requests to simulate variation in user input speed.  
- Apply Constant Throughput Timer on the booking module to maintain a steady request rate under heavy load.  

Timers make your test scenarios closer to real-life usage, resulting in more accurate performance measurements.

---

## Section 09 - Importance of Regular Expressions in JMeter

This section explains why regular expression extractors are essential in JMeter when working with dynamic response data. Many applications return values that change during each run, such as session IDs, tokens, search results, booking references, or any parameter generated at runtime. Regular expression extractors help capture these values from server responses so that they can be reused in later requests.

### Why We Use Regular Expression Extractors

Regular expression extractors allow us to:

- Capture dynamic values from HTML, JSON, XML, or plain text responses.
- Correlate server responses with future requests.
- Handle values that change between test runs, which makes scripts stable and reusable.
- Work with patterns that appear multiple times in a response.
- Validate captured values using debug samplers.

They form the core of correlation in performance testing.

### Practical Example: Flight Search Application

In this exercise, we work with a flight search workflow where the server returns several dynamic fields after a search request. The script uses a Regular Expression Extractor to capture values such as:

- Flight ID
- Price
- Airline code
- Session token

These extracted values are then used in later samplers to complete the booking flow.

### Combining Multiple Expressions Into a Single Extractor

A single Regular Expression Extractor can extract more than one variable by defining groups within one pattern. This helps keep the script clean and reduces the number of extractors in the test plan.

For example:

- A single pattern may capture flight code, price, and seat class.
- Group references such as `$1`, `$2`, `$3` store the captured values.
- Each group is assigned to its own JMeter variable.

This method is efficient when the response structure is predictable.

### Extracting Multiple Variables With One Extractor (Using Debug Samplers)

To confirm that extracted variables contain correct values, Debug Samplers are added to the test plan. They help validate:

- Correct matching of the regular expression.
- Proper assignment of variables.
- Handling of multiple matches if the server returns lists of values.

This step is important to ensure accuracy before scaling the load test.

---

## Section 10 - Data Driven Testing With JMeter

This section explains how to design HTTP request samplers manually and drive them with external data. Data-driven testing is useful when you need to simulate many users, repeat workflows with different inputs, or automate large batches of registrations or transactions in a short time.

### Creating HTTP Request Samplers Without Recording

The tests start with samplers built by hand instead of using the recorder. Each request is added with the needed method, path, headers, and parameters. This gives full control of the structure of the test plan and keeps the script clear and predictable.

### Feeding Data Into the Application

JMeter supports data-driven testing through the CSV Data Set Config element. This element reads values from a CSV file and loads them into variables at runtime. Each row represents one user or one set of inputs, and JMeter moves through each row during execution.

### Defining Variables With CSV Data Set Config

CSV Data Set Config allows you to map each column in the CSV file to a variable name. These variables hold values such as usernames, passwords, email addresses, or profile details. The sampler uses these variables during each loop, allowing the script to simulate many unique user flows.

### Using Variables Inside Manually Created HTTP Requests

Variables defined in the CSV element can be used within any sampler by calling them with the standard JMeter syntax. This keeps the HTTP requests dynamic because each run picks the next row from the CSV file. It also prevents duplication of samplers when testing multiple input sets.

### Automating Bulk User Registration With JMeter

Once the CSV file and manual HTTP samplers are in place, JMeter can generate many user registrations in a short time. The test plan loops through every row of the CSV file and invokes the registration request with different inputs. This approach is effective for load preparation, data setup, or mass account creation.

---

### Section 11 - Introduction to BeanShell Scripting in JMeter

This section introduces BeanShell scripting and shows how it adds flexible logic to JMeter test plans. BeanShell helps when a test needs decisions based on data, response handling, or custom variable updates that go beyond standard components.

#### Why BeanShell Scripting Is Useful
Many performance scenarios depend on values that change during execution. BeanShell allows you to:
- Prepare dynamic values before a sampler runs  
- Apply conditions based on input data  
- Read sampler results and save information for later use  
- Create small logic blocks that guide test flow  

This makes the test plan more adaptable when dealing with dynamic systems.

#### Where BeanShell Fits in JMeter
JMeter provides two main BeanShell elements:
- **BeanShell PreProcessor** runs before a sampler. It is suitable for setting variables, preparing request data, or building conditions that decide what the sampler should send.
- **BeanShell PostProcessor** runs after a sampler. It helps read the response, capture details for following samplers, or add custom logs.

These components give you finer control over how each request behaves.

#### Important BeanShell Variables
JMeter exposes several built-in objects for scripting:
- `vars` holds JMeter variables and allows reading with `vars.get()` and writing with `vars.put()`.
- `props` stores JMeter properties that remain available across the entire test.
- `ctx` gives access to the current sampler context.
- `prev` represents the previous sampler result and allows reading response data and status.

They support logic that depends on request and response information.

---

## Section 12 - Handling Dynamic Responses

Dynamic values often appear in real applications, especially in flows that involve authentication, session handling, or server-generated tokens. These values change with every request, so they cannot be hardcoded. JMeter needs a way to extract these values from earlier responses and reuse them in later requests. This process is known as correlation.

### End-to-End Flow Example: Flight Reservation

In the flight reservation workflow, several requests depend on data returned from earlier steps. One common example is the **userSession** value returned before the login call. If this value is not captured and passed correctly, the login request will fail.

### Identifying Dynamic Values

When a request fails or behaves unexpectedly, inspect the response of the previous sampler. Look for items such as:

- Session IDs  
- Tokens  
- Request IDs  
- Hidden form fields  
- Dynamic query parameters  

If the application regenerates these for every new session, they must be correlated.

### Using a Regular Expression Extractor for Correlation

Once a dynamic value is identified, extract it using a **Regular Expression Extractor**. This allows JMeter to store the captured value as a variable and pass it into later samplers.

### Example: Capturing `userSession`

In the flight reservation example, login fails because `userSession` is generated in a request made *before* the login call.

**Fix:**  
1. Open the sampler that returns the session in its response.  
2. Add a **Regular Expression Extractor**.  
3. Configure it to capture the `userSession` value.  
4. Store it in a variable, such as `${userSession}`.  
5. Replace the hardcoded session in the login request with this variable.

This ensures the correct session value is passed each time, allowing login to succeed with the fresh dynamic value.

### Summary

Correlation is essential in performance testing for any application that generates dynamic data. Proper extraction and variable handling ensure that the test flow behaves like a real user session and avoids invalid session errors.

---

## Section 13 - JMeter Validations in Non-GUI Mode

Running tests in non-GUI mode is the standard approach for stable and efficient performance execution. It reduces memory usage and avoids the overhead of UI rendering during high load.

### Commands to Run Tests in Non-GUI Mode

**Basic execution**
```
jmeter -n -t TestPlan.jmx
```

**Run and store results**
```
jmeter -n -t TestPlan.jmx -l results.jtl
```

**Run with custom properties**
```
jmeter -n -t TestPlan.jmx -l results.jtl -q custom.properties
```

**Run with user-defined properties**
```
jmeter -n -t TestPlan.jmx -l results.jtl -Jthreads=200 -Jrampup=30
```

These variations allow flexible control in CI pipelines or scripted executions.

### Monitoring Results in Non-GUI Execution

Since no UI elements run in this mode, results must be tracked through:

**1. JTL Files**  
JTL output contains sampler results, response codes, errors, latency, and throughput. These files can be opened later in the GUI using listeners like Aggregate Report or Summary Report.

**2. Console Summary Output**  
During execution, JMeter prints periodic summaries such as:
```
Summary +  40 in 00:00:10 =  4.0/s Avg: 250 Min: 210 Max: 410 Err: 0
```

This helps confirm load progression and detect errors early.

**3. Backend Listener Dashboards**  
When linked with InfluxDB and Grafana, live dashboards can show active metrics during non-GUI execution.

### Importance of BlazeMeter for Cloud Execution

BlazeMeter supports distributed cloud-based load execution, which removes the need to maintain large test rigs. It is useful when you need:

* Load from multiple geographic regions  
* High concurrency that exceeds local hardware limits  
* Built-in dashboards and trend analysis  
* Integration with CI environments  
* Easy execution of JMeter scripts without installing JMeter locally  

After uploading the JMX file and data files, you configure load settings, start the test, monitor live charts, and download the final report.



## Section 14 - JMeter Distributed Mode on Slave Machines

Distributed mode allows a single master to coordinate multiple slave machines to generate higher loads. All machines share the same test plan and communicate using JMeter’s client-server architecture.

### Importance of the Client-Server Mechanism

This mechanism allows:

* Central control from a single master  
* Parallel load generation from several slaves  
* Higher total throughput  
* Ability to scale load without upgrading a single machine  

Each slave runs a JMeter server instance. The master sends instructions, starts the test, synchronizes execution, and collects results.

### Step-by-Step Example to Run Tests on Slave Machines

**1. Install JMeter on All Hosts**  
Master and all slaves must use the same JMeter version and Java version.

**2. Start JMeter Server on Each Slave**  
On each slave machine run:
```
jmeter-server
```
or specify the advertised IP:
```
jmeter-server -Djava.rmi.server.hostname=<slave-ip>
```

**3. Configure Slaves in Master Properties**  
Edit the file:
```
/bin/jmeter.properties
```
Set:
```
remote_hosts=192.168.1.10,192.168.1.11
```

**4. Ensure Network Connectivity**  
Master must reach each slave on RMI-related ports, such as 1099 and the JMeter server port range.

**5. Start the Test from the Master**  
Run:
```
jmeter -n -t TestPlan.jmx -R 192.168.1.10,192.168.1.11 -l results.jtl
```

**6. Validate Logs**  
Review the master’s console output and JTL file. Check each slave’s log if communication issues appear. This helps confirm that the distributed test executed correctly.



## Section 15 - Monitoring Server Performance

Performance testing requires both client-side metrics from JMeter and server-side insights. Monitoring the server provides the information needed to identify bottlenecks and validate system health under load.

### Importance of Server Monitoring

Monitoring allows you to track:

* CPU usage levels and saturation  
* Memory allocation patterns and leaks  
* Disk I/O behavior  
* Thread pool usage and blocking  
* Database connection usage  
* System limits that degrade application response time  

Without this information, you cannot accurately locate the root cause of performance issues.

### YourKit Profiler Tool for Server Monitoring

YourKit is a profiler that provides detailed visibility into Java application behavior. It can attach to a running JVM and reveal:

* CPU hotspots  
* Memory allocation and garbage collection activity  
* Live thread states and potential deadlocks  
* Method call timings  
* Object retention and reference chains  
* Slow SQL executed within the JVM  

**Typical workflow**

1. Start the application server with the YourKit agent enabled.  
2. Open the YourKit UI and connect to the JVM.  
3. Begin the JMeter load test.  
4. Observe CPU load, memory allocation, thread activity, and garbage collection during the test.  
5. Capture snapshots to compare behavior across different test runs.

This helps identify whether issues originate from code, thread contention, slow queries, or other dependencies.

### Example Showing Different Server Performance Behaviors

**Healthy Server During Load**

* CPU at moderate levels with short spikes  
* Memory rising slightly and then stabilizing  
* GC pauses are short and stable  
* Response time steady with low variance  
* Thread pool operating within limits  

**Signs of Stress**

* CPU climbing near saturation  
* Memory increasing without recovery  
* Longer GC pauses  
* Response times are rising steadily  
* Thread pools queuing requests  

**Critical State**

* CPU pinned at 100 percent  
* Frequent full GC freezes  
* Out of memory errors  
* High number of 5xx responses  

Combining JMeter outputs with server monitoring tools provides a complete picture of system behavior and allows accurate diagnosis of performance issues.
