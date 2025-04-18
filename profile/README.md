
# GreenEsfinge Framework Experiment

📝 FREE AND CLARIFIED CONSENT TERM (FCCT)

You are invited to participate in a research study that proposes a framework designed to modify the behavior of software applications during execution, aiming to promote more sustainable computing practices.

---

### Participation

This experiment is structured in multiple phases. You will be asked to perform specific tasks using the framework available at: [https://github.com/EsfingeFramework/greensfinge](https://github.com/EsfingeFramework/greensfinge). Detailed instructions for each phase are provided in the following section.

---

### Confidentiality and Anonymity

All information collected during this research will remain strictly confidential. Any data disclosed at scientific events or in publications will be used exclusively for academic purposes and will not include any information that could identify the participant(s), except among the researchers directly involved in the study, ensuring complete privacy regarding your participation.

---

### Contact Information

Throughout the study, you are encouraged to ask questions or request clarifications at any time by contacting one of the researchers at the email address: thiagocarvalhobcc@gmail.com.

---

### Voluntary Participation

Participation in this study is entirely voluntary. You are free to decline or withdraw from the experiment at any time, without any negative consequences or penalties. The experiment may also serve educational purposes within a development context. In such cases, any decision to share your data in support of the research remains fully optional.

---

### Data Retention

All collected data will be securely stored for a period of 2 years after the conclusion of the project.

---

### Consent Registration

Since the questionnaire will be completed through an online form, you must indicate your agreement to participate by selecting the appropriate checkbox. You may keep a copy of your consent upon completion. A signed copy of this document by the research team can also be provided upon request.

---

## A) Prerequisites

To participate in this experiment, the following prerequisites are recommended:

1. A basic understanding of Java (version 11 or above) is sufficient for participation, but familiarity with annotations is recommended.

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

Even though the GreenEsfinge framework is used in this experiment, no prior experience with it is required. However, if you want to check, here is the link: Green Esfinge. The goal is to evaluate whether a simple approach using traditional Java techniques can contribute to more sustainable software by reducing unnecessary computation and, consequently, energy usage.

To help participants understand the concept, the next section presents a complete, practical example demonstrating how to integrate the framework into a Java class and simulate behavior changes dynamically.

---

## D) Example Usage

This section demonstrates how to configure and use the GreenEsfinge framework in a Java project.

### Step 1: Wrap your original class with the framework

To enable dynamic behavior, your target class must be "wrapped" by the framework using the `GreenFactory.greenify()` method.

```java
Service service = GreenFactory.greenify(Service.class); // Wraps your class with GreenEsfinge capabilities
```

This call returns a proxy instance of `Service`, enabling the framework to intercept and control method calls based on the configuration.

### Step 2: Annotate your target with `@GreenReturnWhenSwitchOff` and `@GreenConfigKey`

Finally, annotate the component you want to control dynamically. This is what links the class or method to the configuration key used above.

```java
public class Service { // The original class
   @GreenConfigKey("YOUR_KEY_CONFIGURATION")
   @GreenReturnWhenSwitchOff
   public void doSomething(StringBuilder strParameter) {
      strParameter.append("something very high");
   }    
} 
```

### Step 3: Provide a runtime configuration using `GreenConfigurationFacade`

Next, configure the framework to define whether a specific feature should be ignored (skipped or simulated), and what value should be returned instead.

```java
GreenConfigurationFacade facade = new GreenConfigurationFacade();

facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
        .ignore(true) // Enable skip mode
        .configurationKey("YOUR_KEY_CONFIGURATION") // This key links to the annotation in your class
        .build()
);
```

Below a complete code for an example

```java

import net.sf.esfinge.greenframework.configuration.GreenFactory;
import net.sf.esfinge.greenframework.configuration.facade.GreenConfigurationFacade;
import net.sf.esfinge.greenframework.dto.annotation.GreenSwitchConfiguration;
import net.sf.esfinge.greenframework.annotation.GreenConfigKey;
import net.sf.esfinge.greenframework.annotation.GreenSwitch;

public class UserService {

   @GreenConfigKey("methodConfigKey")
   @GreenReturnWhenSwitchOff
   public void doSomethingWithHighConsumeEnergy(StringBuilder strParameter) {
      strParameter.append("something very high");
   }
}

public class Main {
    
    public static void main(String[] args) {
       UserService userService = GreenFactory.greenify(UserService.class);
       GreenConfigurationFacade facade = new GreenConfigurationFacade();

       facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
               .ignore(true)
               .configurationKey("methodConfigKey")
               .build()
       );
       
       StringBuilder sbParam = new StringBuilder();
       sbParam.append("testValue");
       userService.doSomethingWithHighConsumeEnergy(sbParam);
       System.out.println(sbParam.toString());
       //And you'll see the output is only testValue
    }    
}
```

This configuration tells the framework:

 - To ignore (skip) the actual execution.
 - To apply this configuration only to the feature annotated with the corresponding key.



These annotations serve as markers for the framework to determine:
- Which parts of the code are optional (via `@GreenReturnWhenSwitchOff`).
- How to match them with the runtime configuration (via `@GreenConfigKey`).

### 📝 Summary of Key Points

| Step | What You Do                                     | Purpose                                   |
|------|-------------------------------------------------|-------------------------------------------|
| 1    | Wrap your class with `GreenFactory.greenify()`  | Enable framework control                  |
| 2    | Annotate your original class or method          | Link to runtime config key                |
| 3    | Create a config with `GreenConfigurationFacade` | Define runtime behavior                   |


**Note that the main configuration is the .configurationKey, which will link the facade configuration with the annotation in the class.**

---

## Scenario 1 – Product Recommendation System
Imagine a product recommendation system on an e-commerce platform. Every time a user accesses a product page, the system gathers statistics and displays suggestions based on popularity for an example:

"JBL 510BT Bluetooth Headphones received 1,231 visits this month.
Also check out HyperX Cloud Stinger Headphones!"

These insights are useful but not always essential — especially when the goal is simply to demonstrate the interface, for example.

### ❓ Task
How can we ignore the execution without actually invoking business logic method?

---

## Scenario 2 – Article View Counter
Consider a blog that shows the number of views for each article right below the title. By default, this number is updated with each new access:

"This article has been viewed 542 times."

Although this is a real data point, it is not always required. For instance, when focusing only on layout design or browsing offline:

### ❓ Task
How can we prevent the view counter from being executed without altering the actual counting logic?

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
