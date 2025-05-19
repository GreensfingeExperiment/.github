
# Greensfinge Framework Experiment

📝 FREE AND CLARIFIED CONSENT TERM (FCCT)

You are invited to participate in a research study that proposes a framework designed to modify the behavior of software applications during execution, aiming to promote more sustainable computing practices.

---

### Participation

- This experiment is organized into several phases. You will be required to complete specific tasks using the framework available at https://github.com/EsfingeFramework/greensfinge. 
- After completing the task, **`please email us a zip file containing all of your work related to the experiment`** (the contact information can be found in the "Contact Information" section).
- Detailed instructions for each phase are provided in the following section.
---

### Confidentiality and Anonymity

All information collected during this research will remain strictly confidential. Any data disclosed at scientific events or in publications will be used exclusively for academic purposes and will not include any information that could identify the participant(s), except among the researchers directly involved in the study, ensuring complete privacy regarding your participation.

---

### Contact Information

Throughout the study, you are encouraged to ask questions or request clarifications at any time by contacting one of the researchers at the email address: **thiagocarvalhobcc@gmail.com**.

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

In scenarios where energy efficiency is a priority — such as on mobile devices, in offline modes, during UI prototyping, or even in production environments where executing certain code paths is unnecessary — it may be beneficial to disable these features without altering the application’s core logic.

**`This experiment introduces a framework that addresses this challenge using a lightweight, annotation-based mechanism in Java. The goal is to allow developers to control optional features at runtime—enabling or disabling them based on external configuration—while preserving code structure and maintainability. This simple approach, which relies on traditional Java techniques, can contribute to more sustainable software by reducing unnecessary computation and, consequently, energy usage.`**

Even though the Greensfinge framework is used in this experiment, no prior experience with it is required. However, if you want to check, here is the link: [Greensfinge](https://github.com/EsfingeFramework/greensfinge). The goal is to evaluate whether a simple approach using traditional Java techniques can contribute to more sustainable software by reducing unnecessary computation and, consequently, energy usage.

To help participants understand the concept, the next section presents a complete, practical example demonstrating how to integrate the framework into a Java class and simulate behavior changes dynamically.

---

## D) Experiment General View
You are required to complete two coding tasks, one using normal code practice (called the conventional approach) and the other using the Greensfinge Framework.

There are four available task groups. **The research team will assign your group**, so you will not choose it yourself. If you do not know your group, ask the person responsible for the experiment.

Once you receive your assigned group, check in the corresponding group what tasks and in which order you need to perform. The order in which you perform the task is important, so please do not change it.

Before starting the experiment, generate a participant ID using the following link: https://www.uuidgenerator.net/ - You will need to provide this ID when you fill out the form and when you send your code.

For each task, you need to follow the following steps:
> 1. Read all the instructions until the end.
> 2. Download the initial code of the scenario.
> 3. Open it in your favorite IDE and build.
> 4. Run the unit tests and make sure that their result are the same as shown on the description of the scenario (some tests should pass and other don't).
> 5. When you're ready to start, start the timer.
> 6. Implement the task (a detailed explanation of each task is outlined below):
>    1. If you are performing the experiment using the Scenario1 and Scenario2 projects, you should modify the source code of the application to implement the required behavior using the coding practices that you know.
>    2. If you are working with the Scenario1_Green and Scenario2_Green projects, you should rely solely on using the Greensfinge framework to implement the behavior.
> 7. The task is implemented when all the tests pass. When that happens, stop the timer and take note of the time used to execute the task. This time will be asked when you answer the form.
> 
>**`IMPORTANT: If you need to interrupt the task execution for some reason, pause the timer and start it again when you resume the task. This information will be asked when you fill the form.`**
> 
> When both tasks are finished:
> 
> a. Fill the form by entering the generated participant ID
> b. Send an email to thiagocarvalhobcc@gmail.com with your group and participant ID in the subject

---

## E) Example Usage

This section demonstrates how to configure and use the Greensfinge framework in a Java project. It shows how the Greensfinge framework can be used to activate and deactivate features using annotations and configuration.

### Explanation Using Green Framework
Using the Green Framework, you only need to follow 3 steps to configure it, without making any changes to the application's business logic.

- Step 1: Create an object of your class encapsulated by the framework with the framework method `GreenFactory.greenify(UserService.class)` passing your class as a parameter. This step wraps the object in a way that the framework can interfere in its calls, making possible to deactivate and activate method calls to the original object.
- Step 2: Annotate methods in your target class with `@GreenReturnWhenSwitchOff`, to configure that this method has a functionality that can be deactivated, and with `@GreenConfigKey`, to configure a string key that will be associated with that method.
- Step 3: Provide a runtime configuration using `GreenConfigurationFacade`. This step is used to set a configuration associated with a string key that will activate or deactivate all methods associated with it. 

```java

import net.sf.esfinge.greenframework.configuration.GreenFactory;
import net.sf.esfinge.greenframework.configuration.facade.GreenConfigurationFacade;
import net.sf.esfinge.greenframework.dto.annotation.GreenSwitchConfiguration;

public class MainService {

   //Step 1 - Use GreenFactory.greenif() to proxy the Object
   private UserService userService = GreenFactory.greenify(UserService.class);

   public String mainOperation(){
   	   StringBuilder sbParam = new StringBuilder();
       sbParam.append("before processing");

       userService.doSomethingWithHighConsumeEnergy(sbParam);
       
       sbParam.append("after processing");
       return sbParam.toString();
   }

   //Step 3 - Create the configuration to enable ou disable the invocation method
   public void optimizeEnergyConsumption(boolean config){
       GreenConfigurationFacade facade = new GreenConfigurationFacade();

       facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
        .ignore(config) 
        .configurationKey("OPTIONAL") // This key links to the annotation in your class
        .build()
       );
   }
}

import net.sf.esfinge.greenframework.annotation.GreenConfigKey;
import net.sf.esfinge.greenframework.annotation.GreenReturnWhenSwitchOff;

public class UserService {

   //Step 2 - Use the annotations to tell the framework who and how to dynamically change behavior
   @GreenConfigKey("OPTIONAL")
   @GreenReturnWhenSwitchOff
   public void optionalFunctionalityWithHighEnergyConsumption(StringBuilder strParameter) {
      strParameter.append("something very high");
   }
}
```

This configuration tells the framework:

- To ignore (skip) or not the execution of the annotated methods.
- To apply the configuration only in the methods associated with the corresponding key.

These annotations serve as markers for the framework to determine:
- Which parts of the code are optional (via `@GreenReturnWhenSwitchOff`).
- How to match them with the runtime configuration (via `@GreenConfigKey`).

### 📝 Summary of Key Points

| Step | What You Do                                     | Purpose                                   |
|------|-------------------------------------------------|-------------------------------------------|
| 1    | Wrap your class with `GreenFactory.greenify()`  | Enable framework control                  |
| 2    | Annotate your original class or method          | Link to runtime config key                |
| 3    | Create a config with `GreenConfigurationFacade` | Define runtime behavior                   |


---

## Scenario 1 – Product Recommendation System
Imagine a product recommendation system on an e-commerce platform. Every time a user accesses a product page, the system gathers statistics and displays suggestions based on popularity for an example:

"JBL 510BT Bluetooth Headphones received 1,231 visits this month.
Also check out HyperX Cloud Stinger Headphones!"

These insights are useful but not always essential — especially when the goal is simply to demonstrate the interface, for example.

### ❓ Task

The search for the product and the number of visits is always mandatory, but the search for the "other product" is optional — so how can we ignore the execution to find the other product without actually invoking the business logic method?

---

## Scenario 2 – Article View Counter
Consider a blog that shows the number of views for each article right below the title. By default, this number is updated with each new access:

"This article has been viewed 542 times."

Although this is a real data point, it is not always required. For instance, when focusing only on layout design or browsing offline:

### ❓ Task
How can we prevent the view counter from being executed without altering the actual counting logic?

---

### Start ⏳
To access the task descriptions, follow the links below:

## Group A
1. Start with [Scenario1](https://github.com/GreensfingeExperiment/Scenario_1)
2. Then proceed to [Scenario2_Green](https://github.com/GreensfingeExperiment/Scenario2_Green)

## Group B
1. Start with [Scenario2](https://github.com/GreensfingeExperiment/Scenario_2)
2. Then proceed to [Scenario1_Green](https://github.com/GreensfingeExperiment/Scenario1_Green)

## Group C
1. Start with [Scenario2_Green](https://github.com/GreensfingeExperiment/Scenario2_Green)
2. Then proceed to [Scenario1](https://github.com/GreensfingeExperiment/Scenario_1)

## Group D
1. Start with [Scenario1_Green](https://github.com/GreensfingeExperiment/Scenario1_Green)
2. Then proceed to [Scenario2](https://github.com/GreensfingeExperiment/Scenario_2)

## ✅ Final Notes

Thank you for participating! After completing the tasks, please fill out the questionnaire at: [Link Form](https://forms.gle/r4M7BeECis9mBQqYA).

This study explores how small code adaptations, like disabling non-essential features, can save energy without affecting core functionality. 

Your feedback will help us improve the framework and guide future energy-efficient software practices — `please also send your results to us via email.` (can be found in the "Contact Information" section)

---

**Greensfinge Framework**  
Research and Development Team  
[https://github.com/EsfingeFramework/greensfinge](https://github.com/EsfingeFramework/greensfinge)
