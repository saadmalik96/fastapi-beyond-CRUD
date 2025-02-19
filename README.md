## CI/CD Workflows

### Conventional Commits Enforcement

To maintain commit message consistency, a GitHub Actions workflow is set up to enforce [Conventional Commits](https://www.conventionalcommits.org/). The workflow performs the following steps:

1. **Repository Setup**  
   - Fork the repository and configure it to run locally using `docker compose up`, ensuring all required environment variables are set.

2. **Email Notification Setup**  
   - An [Ethereal Email](https://ethereal.email/) account is used to send outbound email notifications.

3. **GitHub Actions Workflow**  
   - A GitHub Actions workflow checks whether a PR follows the Conventional Commits format using an existing package.
   - If the PR adheres to the format, an email notification is sent to a predefined recipient.
   - If the PR does not follow the format, an email notification is sent indicating failure, and the PR is automatically closed.

### Nightly Build Workflow

A nightly build workflow is implemented to ensure the integrity and stability of the project. The workflow follows these steps:

1. **Service Setup**  
   - Starts a **PostgreSQL** database and a **Redis** cache.

2. **Project Setup & Testing**  
   - Installs all required Python packages.
   - Runs database migrations.
   - Executes test cases to verify functionality.
   - Troubleshoots package installations and environment variable configurations to ensure proper execution within GitHub Actions.

3. **Containerization & Deployment**  
   - Builds a **Docker image** of the project.
   - Pushes the image to **GitHub Packages** (instead of Docker Hub, due to authentication issues with tokens).

4. **Failure Notification**  
   - Any failed steps trigger an email notification using the same **Ethereal Email** setup as in the Conventional Commits workflow.

These workflows help automate code quality checks, maintain commit message consistency, and ensure the project is continuously tested and built.
