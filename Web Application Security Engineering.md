# Life Cycle Approach
- **Design guidelines**: Establish recommendations addressing key engineering decisions based on software vendor suggestions, corporate policies, industry practices, and patterns.
- **Architecture and design review**: Evaluate design against functional, nonfunctional, and technological requirements early in the development cycle to shape the design effectively.
- **Code review**: Conduct manual reviews to identify quality issues contextually, considering usage scenarios and likely conditions.
- **Testing**: Establish executable contracts between code and requirements, including functional, nonfunctional, and constraint testing, optimizing for quality attributes with measurable objectives.
- **Deployment review**: Evaluate the application's behavior in deployment, assessing the impact of configuration settings and reducing surprises before production.
# Security Engineering Baseline Activity
- **Objectives**: Set boundaries and constraints for security efforts, prioritizing security based on project context and importance.
- **Threat Modeling**: Identify and rationalize threats, attacks, and vulnerabilities to shape software design decisions effectively.
- **Design Guidelines**: Gather and organize proven security design principles, practices, and patterns for the development team.
- **Architecture and Design Review**: Prioritize and scope security design decisions through focused reviews, optimizing efficiency and effectiveness.
- **Code Review**: Analyze source code to ensure it meets security objectives, applying contextual analysis and identifying vulnerabilities.
- **Testing**: Align security testing with security objectives and threat models, focusing on effective and efficient testing methods.
- **Deployment Review**: Evaluate application behavior in deployment scenarios to eliminate surprises and ensure compliance with security requirements

![[Pasted image 20240512204258.png]]
- **Web Application Security Frame**: Organizes recurring security issues into categories such as input and data validation, authentication, authorization, configuration management, cryptography, sensitive data handling, exception management, session management, and auditing/logging.
- **Context Precision**: Emphasizes the importance of considering the specific context of a problem, including application type (e.g., Web application, Web service, component/library, desktop application, mobile application), deployment scenario (intranet, extranet, Internet), project type (in-house IT, third party, shrink-wrapped software), and life cycle (RUP, MSF, XP, Waterfall, Agile, Spiral).
- **Advantages of Security-Specific Activities**:
    - **Focus**: Allows for the right amount of effort in the right places, optimizing techniques for improved security.
    - **Efficiency**: Helps reduce information overload and leverage expertise in an organized manner, leading to more effective results.
- **Examples**:
    - _Input and Data Validation_: Encapsulates the principle of not trusting client input and focuses on defining good input rather than attempting to define all variations of bad input.
    - _Threat Modeling_: Varies techniques based on application type, deployment scenario, and project type, leading to more relevant and impactful results.
- **Conclusion**: Separating security into its own set of activities enables better prioritization, optimization, and refinement of techniques, ultimately enhancing software engineering practices.