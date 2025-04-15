
# GreenEsfinge Framework Experiment

📝 𝗙𝗥𝗘𝗘 𝗔𝗡𝗗 𝗖𝗟𝗔𝗥𝗜𝗙𝗜𝗘𝗗 𝗖𝗢𝗡𝗦𝗘𝗡𝗧 𝗧𝗘𝗥𝗠 (𝗙𝗖𝗖𝗧)

You are invited to take part in a research study that proposes a framework designed to modify the behavior of software applications during execution, aiming to promote more sustainable computing practices.

---

### Participation

This experiment is structured in multiple phases. You will be asked to perform specific tasks using the framework available at: [https://github.com/EsfingeFramework/greensfinge](https://github.com/EsfingeFramework/greensfinge). The detailed instructions for each phase are provided in the following section.

---

### Confidentiality and Anonymity

All information collected during this research will remain strictly confidential. Any data disclosed in scientific events or publications will be used exclusively for academic purposes and will not include any information that could identify the participant(s), except among the researchers directly involved in the study, thereby ensuring complete privacy regarding your participation.

---

### Contact Information

Throughout the study, you are encouraged to ask questions or request clarifications at any time by reaching out to one of the researchers at the email address: [thiagocarvalhobcc@gmail.com](mailto:thiagocarvalhobcc@gmail.com).

---

### Voluntary Participation

Participation in this study is entirely voluntary. You are free to decline to participate or to withdraw from the experiment at any point, without any negative consequences or penalties. The experiment may also serve educational purposes within a development context. In such cases, any decision to share your data in support of the research remains fully optional.

---

### Data Retention

All collected data will be securely stored for a period of 5 years after the conclusion of the project.

---

### Consent Registration

Since the questionnaire will be completed through an online form, you must indicate your agreement to participate by selecting the appropriate checkbox. You may keep a copy of your consent upon completion. A signed copy of this document by the research team can also be provided upon request.

---

## A) Prerequisites

To participate in this experiment, the following prerequisites are recommended:

1. A basic, understanding of Java (version 11 or above) is sufficient for participation, but familiarity with annotations is recommended.
---

## B) Settings

The experiment consists of Java projects in which the volunteer must implement specific tasks as requested in each one. This section explains what you need to configure in your development environment. All Java projects in this experiment are Maven-based, which significantly reduces potential compatibility issues. If you already have a Java environment set up, changes will likely not be necessary.

### JDK

The Java projects in this experiment require JDK 11 or higher to be installed. You can download a version compatible with your operating system at:

[https://adoptium.net/temurin/releases/](https://adoptium.net/temurin/releases/)

### IDE

The experiment has been tested using NetBeans and IntelliJ IDEA on Windows 10, Windows 11, and Ubuntu Linux 24.04.1 LTS.

Don’t worry if your IDE or operating system is different — as long as your IDE supports Java development, you are unlikely to experience any issues.

Some IDEs you may use:
- IntelliJ IDEA
- NetBeans
- Eclipse
- VSCode with Java extensions

### External Access

No external access, firewall configurations, or other network requirements are necessary to run the experiment.

---

## C) Background

Modern software applications often include features that, while valuable, are not always essential for every use case. Examples include real-time statistics, recommendation systems, or visual enhancements — all of which may increase energy consumption during execution.

In scenarios where energy efficiency is a priority — such as on mobile devices, in offline modes, during UI prototyping, or even in production environments where executing certain code paths is unnecessary — it may be beneficial to disable or simulate the execution of these features without altering the application’s core logic.

This experiment introduces a framework that addresses this challenge using a lightweight, annotation-based mechanism in Java. The idea is to allow developers to control optional features at runtime, enabling or disabling them based on external configuration, while preserving the structure and maintainability of the code.

Even though the GreenEsfinge framework is used in this experiment, no prior experience with it is required, but if you want to check, here is the link. [Green Esfinge](https://github.com/EsfingeFramework/greensfinge) The goal is to evaluate whether a simple approach using traditional Java techniques can contribute to more sustainable software by reducing unnecessary computation and, consequently, energy usage.

To help participants understand the concept, the next section presents a complete, practical example demonstrating how to integrate the framework into a Java class and simulate behavior changes dynamically.

---

## D) Example Usage: Conventional vs. Green Framework Approach

This section demonstrates how to configure and use the **GreenEsfinge** framework in a Java project, highlighting the difference between the **Conventional Approach** and the **Green Framework Approach**.

Below, we present both strategies side by side to highlight how the framework can simplify the implementation and reduce code coupling.

### 🧱 Before the Framework: Conventional Approach

Traditionally, to control optional features like displaying product recommendations, developers need to introduce flags, toggles, or environment variables directly into the application's source code. This can lead to logic being scattered across the codebase, increased complexity in testing, and reduced flexibility.

### Step 1: Controller Layer

We start with a simple `Controller` class that delegates the logic to a `Service` class:

   ```java
   public class Controller {
      private final Service service = new Service();
   
       public String doSomething() {
           return service.doSomething();
       }
   }
```

### Step 2: Business Logic with Direct Conditional
In the Service class, we need to change the behavior directly in the business logic, using a conditional check based on an environment variable:

```java
   public class Service {
      
       private final Repository repository = new Repository();
   
       public String doSomething() {
           String product;
   
           if (Boolean.parseBoolean(System.getenv("FEATURE.TOGGLE"))) {
               product = repository.findSomething();
           } else {
               product = "Mocked Value";
           }
   
           return product;
       }
   }
 ```

This approach hardcodes the control logic into the service. In order to simulate or skip part of the functionality, the developer must:

### 🧱 After the Framework: Green Framework Approach

To illustrate the benefits of using the Green Framework, let’s compare how a typical feature toggle is implemented using a **Conventional Approach** versus the **Green Framework Approach**.

### Step 1: Wrap your original class with the framework

To enable dynamic behavior, your target class must be "wrapped" by the framework using the `GreenFactory.greenify()` method.

```java
Service service = GreenFactory.greenify(Service.class); // Wraps your class with GreenEsfinge capabilities
```

This call returns a proxy instance of `Service`, enabling the framework to intercept and control method calls based on the configuration.

### Step 2: Provide a runtime configuration using `GreenConfigurationFacade`

Next, configure the framework to define whether a specific feature should be ignored (skipped or simulated), and what value should be returned instead.

```java
GreenConfigurationFacade facade = new GreenConfigurationFacade();
String mockValue = "Mocking a random value";

facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
        .ignore(true) // Enable skip mode
        .configurationKey("YOUR_KEY_CONFIGURATION") // This key links to the annotation in your class
        .strDefaultValue(mockValue) // Value to return if the feature is disabled
        .build()
);
```

This configuration tells the framework:
- To ignore (skip) the actual execution.
- To return the specified default value instead.
- To apply this configuration only to the feature annotated with the corresponding key.

### Step 3: Use the proxy instance in your code

Now, when you call a method from your proxy instance, the framework will decide whether to execute it or return the configured mock value.

```java
String profile = service.doSomething();
assertEquals(mockValue, profile); // Should return "Mocking a random value" if ignored
```

### Step 4: Annotate your target with `@GreenSwitch` and `@GreenConfigKey`

Finally, annotate the component you want to control dynamically. This is what links the class or method to the configuration key used above.

```java
@GreenConfigKey("YOUR_KEY_CONFIGURATION")
@GreenSwitch
private final Service service = new Service();  // The original class
```

These annotations serve as markers for the framework to determine:
- Which parts of the code are optional (via `@GreenSwitch`).
- How to match them with the runtime configuration (via `@GreenConfigKey`).

### 📝 Summary of Key Points

| Step | What You Do                                     | Purpose                                   |
|------|-------------------------------------------------|-------------------------------------------|
| 1    | Wrap your class with `GreenFactory.greenify()`  | Enable framework control                  |
| 2    | Create a config with `GreenConfigurationFacade` | Define runtime behavior                   |
| 3    | Use the proxy object                            | Automatically apply mock or real behavior |
| 4    | Annotate your original class or method          | Link to runtime config key                |

**Note that the main configuration is the .configurationKey, which will link the facade configuration with the annotation in the class.**

---

## Scenario 1 – Product Recommendation System
Imagine a product recommendation system on an e-commerce platform. Every time a user accesses a product page, the system gathers statistics and displays suggestions based on popularity for an example:

"JBL 510BT Bluetooth Headphones received 1,231 visits this month.
Also check out HyperX Cloud Stinger Headphones!"

These insights are useful but not always essential — especially when the goal is simply to demonstrate the interface, for example.

### ❓ Task
How can we return a simulated message, without using the actual number of accesses, without changing the core business logic?

### 💡 Tips (Step-by-step instructions)

If you're unsure how to complete the task, here’s a simple step-by-step guide:

1. **Use GreenFactory to create the proxy object**

   Instead of using `new`, create your object like this:
   ```java
   RecommendationService service = GreenFactory.greenify(RecommendationService.class);

2. **Add the Annotations to the class or field**
    ```java
   @GreenSwitch
   @GreenConfigKey("YOUR_KEY_CONFIGURATION")
   private final RecommendationService service = new RecommendationService();

3. **Set up the mock behavior using GreenConfigurationFacade**
    ```java
   GreenConfigurationFacade facade = new GreenConfigurationFacade();
   facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
       .ignore(true) // Ignore the actual execution
       .configurationKey("YOUR_KEY_CONFIGURATION") // Same key used in the annotation
       .strDefaultValue("Simulated message here") // Value to be returned instead
       .build()
   );
4. **Verify that the simulated value is returned**
    ```java
    String result = service.findRecommendation();
   
It should now return the mock value instead of executing the real logic.

5. **After that, open the test class and try to make all tests pass.**


---

## Scenario 2 – Article View Counter
Consider a blog that shows the number of views for each article right below the title. By default, this number is updated with each new access:

"This article has been viewed 542 times."

Although this is a real data point, it is not always required. For instance, when focusing only on layout design or browsing offline:

### ❓ Task
How can we make the view counter return a simulated value without altering the actual counting logic?

### 💡 Tips (Step-by-step instructions)

If you're unsure how to complete the task, here’s a simple step-by-step guide:

1. **Use GreenFactory to create the proxy object**

   Instead of using `new`, create your object like this:
   ```java
      ArticleService service = GreenFactory.greenify(ArticleService.class);

2. **Add the Annotations to the class or field**
    ```java
   @GreenSwitch
   @GreenConfigKey("YOUR_KEY_CONFIGURATION")
   private final ArticleService service = new ArticleService();

3. **Set up the mock behavior using GreenConfigurationFacade**
    ```java
   GreenConfigurationFacade facade = new GreenConfigurationFacade();
   facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
       .ignore(true) // Ignore the actual execution
       .configurationKey("YOUR_KEY_CONFIGURATION") // Same key used in the annotation
       .strDefaultValue("Simulated message here") // Value to be returned instead
       .build()
   );
4. **Verify that the simulated value is returned**
    ```java
    String result = service.findRecommendation();
It should now return the mock value instead of executing the real logic.

5. **After that, open the test class and try to make all tests pass.**
---

## E) Experiment
You are required to complete two coding tasks, each using one of the two proposed approaches.

There are two available task groups. **The research team will assign which group you should complete**, so you will not need to choose it yourself.

Once you receive your assigned group, access the corresponding tasks, review the requirements carefully, and record your start and end time for each task.

> ⚠️ **Important:**
> - If you are performing the experiment using the `Scenario1` and `Scenario2` projects, **you must modify the source code** of the application to implement the required behavior.
> - If you are working with the `Scenario1_Green` and `Scenario2_Green` projects, **you must NOT change the application source code**. In these cases, you should rely solely on the configuration mechanisms provided by the GreenEsfinge framework to simulate the behavior.


A detailed explanation of each task is outlined below.

### Start ⏳
To access the task descriptions, follow the links below:

## Group A
1. Start with [Scenario1](https://github.com/GreenEsfingeExperiment/Scenario_1)
2. Then proceed to [Scenario2_Green](https://github.com/GreenEsfingeExperiment/Scenario2_Green)

## Group B
1. Start with [Scenario2](https://github.com/GreenEsfingeExperiment/Scenario_2)
2. Then proceed to [Scenario1_Green](https://github.com/GreenEsfingeExperiment/Scenario1_Green)

## ✅ Final Notes

You are invited to participate in a research study that explores a framework designed to dynamically adapt software behavior at runtime, with the goal of promoting more sustainable computing practices.

We appreciate your participation. Once you’ve completed the tasks, please take a moment to fill out the questionnaire available at the following link: [Link Form](https://forms.gle/r4M7BeECis9mBQqYA)

This study aims to understand how small code adaptations — such as disabling non-essential features — can contribute to energy savings without compromising the main functionality of an application. By observing your interaction with different application scenarios, we hope to gather insights into the practicality and effectiveness of this approach.

Your feedback is essential to improving the framework and identifying potential areas of impact in real-world software development. The results may help guide future tools and practices that prioritize energy efficiency as a first-class concern in software engineering.

---

**GreenEsfinge Framework**  
Research and Development Team  
[https://github.com/EsfingeFramework/greensfinge](https://github.com/EsfingeFramework/greensfinge)
