#  The 12-Factors App
## 1. Codebase 
-   **A twelve-factor app is always tracked in a version control system**
- There is only a  one codebase per app
- The codebase is the same across all deploys, although different versions may be active in each deploy
## 2. Dependencies
-   **A twelve-factor app never relies on implicit existence of system-wide packages**
- Every dependency should be  declares a clear versio for stability and shoud be cloned into the code repo
## 3. Config
-  **Store config in the environment ( .env file)**
## 4. Backing services
-  **Backing services should be treated as attached resources.**
-  We should be able to swap between local and third party services without any changes to app's code
-  We use environment variables to configure backing services
## 5. Build, Release and Run
- **Strictly separate build and run stages**
- You must strictly separate the Build (binary), Release (binary and + env config) and Run (exec runtime) stages
- Our instances are immutable so we can't make change upstream
- We take advantage of Docker and Kubernetes for this factor
## 6. Processes
- **Execute the app as one or more stateless processes.**
- Any data that needs to persist must be stored xin a stateful backing service.
## 7. Port Binding
- **Export services via port binding**
- If we said in the backing service pattern that every service should be accessed via URL, that includes our app. Exporting services via port binding will allow us to become a backing service for another app via URL.
- We define ports for all services in Dockerfile.
## 8. Concurrency 
- **Scale out via the process model**
- Processes in the twelve-factor app take strong cues from the unix process model for running service daemons
## 9. Disposability 
- **Minimize the startup time and shut down them gracefully.**
- We should's stop an application when it's writing  to a backing services
- To do so, our app must be able to capture signals, ensure that we finish calls, and then stop the app.
## 10. Dev/prod parity 
- **Keep development, staging, and production as similar as possible.**
- The twelve-factor app is designed for continuous deployment by keeping the gap between development and production small. Looking at the three gaps described above:
    1. Make time gap smal: write code to deploy just minutes later.
    2. Make the personal gap small:developers who wrote code are closely involved in deploying it and watching its behavior in production.
    3. Make tools gap small.
- We achieve this using CI/CD flow with Docker containers. Every time developers merge to develop/master branch; this will be deployed automatically to development/production environment

## 11. Logs 
- **Treat logs as event streams.**
- Logs provide visibility into the behavior of a running application.
-Twelve-factor app principles advocate separating the log generation and processing the log's information.
## 12. Admin Process 
- **Run admin/management tasks as one-off processes**
- It's not an admin dashboard. An admin process is a way to interact with your app process to do one-off administrative or maintenance tasks for the app.
- We invole one-off admin processes by a direct shell commnand