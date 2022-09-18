# Deployment Strategies

Deployment strategies are practices used to change or upgrade a running instance of an application.  
We will discuss **six** deployment strategies. 

### 1. Basic Deployment
In a basic deployment, all nodes within a target environment are updated at the same time with a new service or artifact version.

| Pros | Cons |
|---|---|
| simple, fast, and cheap |  **not** outage-proof|
| | **do not** provide for easy rollbacks|

### 2. Multi-Service Deployment

In a multi-service deployment, all nodes within a target environment are updated with multiple new services simultaneously.   
This strategy is used for application services that have service or version dependencies, or if you’re deploying off-hours to resources that are not in use.

In this strategy, if we notice one or more services not working in the new deployment, we identity and roll back those services only.


| Pros | Cons |
|---|---|
| simple, fast, and cheap |  **not** outage-proof|
| not as risk-prone as a basic deployment | **slow** to rollback |


### 3. Rolling Deployment

A rolling deployment is a deployment strategy that updates running instances of an application with the new release.   
All nodes in a target environment are incrementally updated with the service or artifact version in integer N batches.

| Pros | Cons |
|---|---|
| simple to roll back |  services **must** support both new and old versions of an artifact|
| not as risk-prone as a basic deployment | **slow** to verify |
| | difficult to implement because of previous cons |

### 4. Blue-Green Deployment

Blue-green deployment is a deployment strategy that utilizes two identical environments, a "blue" (aka staging) and a "green" (aka production) environment with different versions of an application or service. 

* Quality assurance and user acceptance testing are typically done within the blue environment that hosts new versions or changes. 
* User traffic is shifted from the green environment to the blue environment once new changes have been testing and accepted within the blue environment. 
* You can then switch to the new environment once the deployment is successful.

| Pros | Cons |
|---|---|
| simple, fast, well-understood, and easy to implement | **COST**, since you are maintaining two environments |
| Rollback is also straightforward, because you can simply flip traffic back to the old environment in case of any issues. |  QA and UAT may not identify all of the anomalies or regressions either, and so shifting all user traffic at once can present **risks**. |
| | An outage or issue could also have a wide-scale business impact before a rollback is triggered, and depending on the implementation, **in-flight user transactions may be lost** when the shift in traffic is made.|


### 5. Canary Deployment

A canary deployment is a deployment strategy that releases an application or service incrementally to a subset of users.   
All infrastructure in a target environment is updated in small phases (e.g: 2%, 25%, 75%, 100%). 

A canary release is the lowest risk-prone, compared to all other deployment strategies, because of this control.

| Pros | Cons |
|---|---|
| This allows organizations to test in production with real users and use cases and compare different service versions side by side. | testing in production, difficult to sell to stakeholders |
| It’s cheaper than a blue-green deployment because it does not require two production environments. |  **Complex implementation**, Scripting a canary release can be complex |
| fast and safe to trigger a rollback to a previous version of an application | manual verification or testing can take time, and the required monitoring and instrumentation for testing in production may involve additional research|

### 6. A/B Testing

In A/B testing, different versions of the same service run simultaneously as "experiments" in the same environment for a period of time.

* Experiments are either controlled by feature flags toggling, A/B testing tools, or through distinct service deployments. 
* It is the experiment owner’s responsibility to define how user traffic is routed to each experiment and version of an application. 
* Commonly, user traffic is routed based on specific rules or user demographics to perform measurements and comparisons between service versions. 
* Target environments can then be updated with the optimal service version.

The biggest difference between A/B testing and other deployment strategies is that A/B testing is primarily focused on **experimentation and exploration**.  
While other deployment strategies deploy many versions of a service to an environment with the immediate goal of updating all nodes with a specific version, A/B testing is about testing multiple ideas vs. deploying one specific tested idea.

| Pros | Cons |
|---|---|
| standard, easy, and cheap method for testing new features in production | experimental nature  |
| wide tooling available for A/B testing. | Experiments and tests can sometimes break the application, service, or user experience |


