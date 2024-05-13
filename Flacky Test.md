
Flacky tests: test that cause spurious failures without any code changes, does not behave deterministically


Order dependency is main reason 59% of the 7571  flacky test
28% test infrastructure
13% use of network and rondomness API

95% confidence that a passing test is not flacky requires 170 reruns
# Flakiness
1. **Types of Flakiness**: Researchers have identified several categories of flakiness, including Async Wait, Concurrency, Test Order Dependency, Resource Leak, Network, Time, IO, Randomness, Floating Point Operations, Unordered Collections, Too Restrictive Range, Test Case Timeout, Platform Dependency, and Test Suite Timeout.
    
2. **Order-dependent Flakiness**: Flakiness caused by order dependencies between test cases can be categorized further into victim-polluter relationships and brittle-state-setter relationships. In the victim-polluter scenario, a test fails due to changes made by another test to a shared state. In the brittle-state-setter scenario, a test fails because it requires another test to set up a necessary state.
    
3. **Infrastructure Flakiness**: This category describes flakiness caused by issues outside of the project's code but within the test execution environment. Examples include failing installations of dependencies due to network issues, permission errors, or lack of disk space. Infrastructure flakiness is distinct from other types of flakiness as it is caused by external components and is a form of transitively induced flakiness.
    
4. **Identification Strategies**: Various strategies are used to identify and address flakiness, including rerunning tests multiple times with the same or different orders, searching for commits fixing flaky tests, searching in issue trackers, and using data-flow analysis for order-dependent flakiness.
# Detecting Flaky Test
## Search for Flaky
- Identify commits that likely fix flaky tests or issues reporting flaky test
- **Rerun Tests Multiple Times**: Tests are rerun up to a certain number of times, and researchers check whether the verdicts change between runs. This method aims to automate the process of identifying flaky tests.

Drawback: make flacky failures less likely
It might hide problems that should actually be fixed
Third this wast resources
## Efforts to Address the Gap
The current study aims to address this gap by rerunning test 400 times. This extensive rerunning seeks to derive a proper estimation of the number of reruns needed to build a representative dataset of flaky tests.

# Mitigating Flakiness
## **Detection Techniques**:
 - **DEFLAKER**: Analyzes coverage information and test verdicts from prior runs to detect flaky tests without re-executing tests. This approach offers performance advantages over repetitive reruns.
-  **IDFLAKIES**: Uses a smart random-order rerun strategy to detect flaky tests and partially classify the root cause of flakiness. It distinguishes between order-dependent and non-order-dependent flaky tests.
## **Techniques for Order-Dependent Tests**:
- **PRADET**: Detects order-dependent flaky tests using data-flow analysis to filter test orders containing potential dependencies, reducing the number of test runs needed.
- **IFIXFLAKIES**: Automatically fixes order-dependent flaky tests by suggesting patches extracted from other test code.
## **Fine-Grained Classification**:
- **ROOTFINDER**: Aims to derive a more detailed classification for non-order-dependent flaky tests. It collects distinctive information about test execution using a binary instrumentation framework and compares it between passing and failing runs to find patterns predicting test failure.
- **Ziftci et al.'s Approach**: Helps identify the root cause of flakiness by comparing the execution of passing and failing runs, pointing out the first line of code where the two executions diverge. While these approaches provide support, they do not fully automate finding the root causes of flakiness.

# Types of Flakiness in Python
Difference of flakiness in python and the general ones are due to these reasons.
1. **Floating point flakiness**: Unlike some other programming languages, such as those using IEEE-754 floating point arithmetic, Python's floating point arithmetic is deterministic. Therefore, flakiness caused by floating point operations is not a concern in Python.
2. **Platform dependency**: Python abstracts away many system-level details from the user, but differences in underlying platforms can still impact Python executions. For example, the size of objects may vary between 32-bit and 64-bit systems, leading to potential platform-dependent behavior.
3. **Unordered collections**: Python's handling of unordered collections, such as sets, has evolved. Prior to Python 3.2, the `__hash__` function used to determine the internal ordering of sets was deterministic. However, starting from Python 3.2, the `__hash__` function was randomly seeded for security reasons, making the ordering non-deterministic. Since Python 3.3, unordered collections are the default behavior. Additionally, Python 3.8 introduced order-preserving dictionaries, which further impacts the behavior of collections.
# Result
1. **Prevalence of Flakiness in Python (RQ1):**
    - The study found 7,571 tests exhibiting non-deterministic behavior in 1,006 projects, which represents about 0.86% of all investigated tests being flaky.
    - Flakiness was observed to be more common in projects with higher levels of maturity, as well as in projects from the scientific and engineering domain.
2. **Types of Flakiness in Python (RQ2):**
    - The study identified different categories of flakiness, with infrastructure issues and test order dependencies being the most common.
    - Other types of flakiness included network issues, randomness, asynchronous waiting, system time dependencies, and issues related to fuzzing tools.
3. **Degree of Flakiness (RQ3):**
    - The study analyzed the statistical chance of unveiling flakiness after a certain number of reruns.
    - It found that for non-order-dependent (NOD) flakiness, only one rerun is needed for a 95% confidence level, while for order-dependent (OD) flakiness, three reruns are needed for the same confidence level.
    - Flaky tests in Python have a low failure rate, requiring a low number of reruns to check for flakiness, but a high number of reruns to identify if a test contains flakiness in general.
4. **Comparison with Previous Studies:**
    - The study compared its findings with a previous dataset from iDFlakies.
    - While iDFlakies dataset had a lower prevalence of flaky tests, this study found a higher prevalence, especially in terms of infrastructure flakiness.