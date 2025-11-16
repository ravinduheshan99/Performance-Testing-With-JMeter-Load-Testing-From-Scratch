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

## Section 01 – Introduction  
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

## Section 02 – Recording JMeter Scripts  
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

## Section 03 – Applying Load and Analysing Performance  
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

These notes summarize the foundational topics covered in Sections 01 to 03. They serve as a reference for building and analysing performance test plans throughout this repository.
