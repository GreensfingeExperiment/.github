
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

In this experiment, you will be given tasks related to Java projects that utilize the Green Esfinge Framework. However, prior experience or specific knowledge of this framework is not required.

If you wish to explore the framework beforehand, you can access the documentation here: [Green Esfinge](https://github.com/EsfingeFramework/greensfinge).

This experiment is based on the challenge of modifying an application’s behavior at runtime. To help participants better understand the necessary concepts, a complete example application will be presented in this section.

The goal is to provide all the foundational knowledge you’ll need to perform the tasks proposed later in the experiment.

---

## D) Example Usage
Here is a snippet of code to configure the framework so that you can provide the values.

    Service service = GreenFactory.greenify(Service.class)  // Your Class
    GreenConfigurationFacade facade = new GreenConfigurationFacade();
    String mockValue = "Mocking a random value";
    facade.setGeneralConfiguration(GreenSwitchConfiguration.builder()
                .ignore(true)
                .configurationKey(YOUR_KEY_CONFIGURATION")
                .strDefaultValue(mockValue)
        .build());

    String profile = service.doSomething();
    assertEquals(mockValue, profile);

Here is another code snippet on how to use the framework in your project.

    @GreenConfigKey("YOUR_KEY_CONFIGURATION")
    @GreenSwitch
    private final Service service = new Service();  // Your Class

Note that the main configuration is the .configurationKey, which will link the facade configuration with the annotation in the class.

---

## Scenario 1 – Product Recommendation System
Imagine a product recommendation system on an e-commerce platform. Every time a user accesses a product page, the system gathers statistics and displays suggestions based on popularity for an example:

"JBL 510BT Bluetooth Headphones received 1,231 visits this month.
Also check out HyperX Cloud Stinger Headphones!"

These insights are useful but not always essential — especially when the goal is simply to demonstrate the interface, for example.

### ❓ Problem
How can we return a simulated message, without using the actual number of accesses, without changing the core business logic?

---

## Scenario 2 – Article View Counter
Consider a blog that shows the number of views for each article right below the title. By default, this number is updated with each new access:

"This article has been viewed 542 times."

Although this is a real data point, it is not always required. For instance, when focusing only on layout design or browsing offline:

### ❓ Problem
How can we make the view counter return a simulated value without altering the actual counting logic?

---

## E) Experiment
You are required to complete two coding tasks, each using one of the two proposed approaches.

There are two available task groups; choose one group and complete all tasks within it.

Access the tasks from your selected group, review the requirements carefully, and record your start and end time for each task.

A detailed explanation of each task is outlined below.

### Start ⏳
To access the task descriptions, follow the links below:

## Group A
1. Start with Scenario1
2. Then proceed to Scenario2_Green

## Group B
1. Start with Scenario2
2. Then proceed to Scenario1_Green

## ✅ Final Notes

You are invited to take part in a research study that proposes a framework designed to modify the behavior of software applications during execution, aiming to promote more sustainable computing practices.

We thank you for your participation, and after completing the tasks, please fill out the questionnaire at the following link: **[LINK_FORM]**

---

**GreenEsfinge Framework**  
Research and Development Team  
[https://github.com/EsfingeFramework/greensfinge](https://github.com/EsfingeFramework/greensfinge)
