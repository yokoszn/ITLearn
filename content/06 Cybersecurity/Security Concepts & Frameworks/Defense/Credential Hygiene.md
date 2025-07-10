[[3. Knowledge Base Home]]
It is generally considered bad practice to include passwords, SSH keys, API keys, or any other sensitive information directly in Docker files or GitHub repositories. This is because these files can easily be exposed to unauthorized users, especially if stored in public repositories or insecure environments.

Here are common methods developers use to hide or obfuscate sensitive information such as SSH keys, OpenAI API keys, or passwords in Docker files and GitHub repositories:

---
Risk Impact:

Attackers highly seek credentials to access valuable resources and enable malicious activities. Engineering environments offer multiple opportunities for attackers to obtain credentials. Human error and knowledge gaps in credential management can increase the risk of credential exposure and compromise of critical resources.

Recommendations:

1. Ensure that credentials follow the principle of least privilege from code to deployment.
2. Avoid sharing the same credentials across multiple contexts to maintain accountability and simplify privilege management.
3. Use temporary credentials whenever possible, and establish procedures to rotate static credentials and detect stale credentials periodically.
4. Ensure credentials are only used under predefined conditions, such as limiting usage to a specific IP address or identity.  
    
5. Detect secrets pushed to and stored in code repositories using Integrated Development Environments (IDE) plugins, automatic scanning, and periodic repository commit scans.
6. Use built-in vendor options or third-party tools to prevent secrets from being printed to console outputs during builds and ensure existing outputs do not contain secrets.
7. Verify that secrets are removed from artifacts, such as container image layers and binaries.

Organizations should consider implementing the above best practices to mitigate the risks of insufficient credential hygiene.

Environment Variables and Best Practices:

The use of environment variables is an excellent method of promoting credential hygiene. As part of software development and deployment processes, environment variables are commonly used to store and manage configuration information. They store sensitive information, such as API keys, passwords, and other credentials. You can manage environment variables securely by following these best practices:

1. Avoid hardcoding sensitive information in code; use environment variables instead.
2. Regularly review and rotate credentials stored in environment variables.
3. Limit access to environment variables to authorized personnel only.  
    
4. Environment variables should be set according to the principle of least privilege.
5. Implement monitoring and auditing mechanisms to track changes to environment variables.
6. If implementing a secrets manager solution (explained in the next task), review its encryption mechanisms and if it's a good fit for your development environments.

**Note:** Implementing environment variables does not mean you are free from compromise. Following best practices is essential for ensuring they are appropriately implemented.
### 1. **Environment Variables**

- **Docker Files:** Instead of hardcoding sensitive information in Docker files, you can use environment variables to pass these values securely at runtime.
    
    - In your `Dockerfile`, you can use `ENV` to define environment variables.
    - **Example:**
        
        dockerfile
        
        Copy code
        
        `ENV OPENAI_API_KEY=${OPENAI_API_KEY}`
        
    - Then, at runtime, you pass the API key or secret value using `docker run`:
        
        bash
        
        Copy code
        
        `docker run -e OPENAI_API_KEY=your-secret-key image-name`
        
- **GitHub Actions/Workflows:** GitHub allows the use of **secrets** for storing sensitive data. These secrets are injected as environment variables into the workflow.
    
    - Go to your GitHub repository → Settings → Secrets → Actions → Add a new secret.
    - You can then reference the secret in your GitHub Actions workflow like so:
        
        yaml
        
        Copy code
        
        `env:   OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}`
        

### 2. **Docker Secrets (for Swarm Mode)**

If you're using Docker Swarm, you can use **Docker Secrets** to manage sensitive information securely.

- **Example:**
    1. Create a secret:
        
        bash
        
        Copy code
        
        `echo "your-secret" | docker secret create openai_api_key -`
        
    2. Reference the secret in your `docker-compose.yml` file:
        
        yaml
        
        Copy code
        
        `version: '3.1' services:   myservice:     image: my-image     secrets:       - openai_api_key secrets:   openai_api_key:     external: true`
        

### 3. **.env Files**

- Use a `.env` file to store your sensitive information locally and reference it in your code or Docker setup. However, make sure you **add this file to your `.gitignore`** so that it is not pushed to GitHub.
    - Example `.env` file:
        
        makefile
        
        Copy code
        
        `OPENAI_API_KEY=your-secret-key`
        
    - Load the environment variables in your Docker Compose file:
        
        yaml
        
        Copy code
        
        `version: '3' services:   app:     environment:       - OPENAI_API_KEY=${OPENAI_API_KEY}`
        

### 4. **GitHub Secrets (for CI/CD)**

In GitHub workflows, you can store sensitive information securely using GitHub Secrets:

- In your repository's settings, you can store API keys and other secrets, then access them through your CI/CD workflows without exposing them in the source code.

**Example in GitHub Actions:**

yaml

Copy code

`name: Example Workflow on: [push] jobs:   build:     runs-on: ubuntu-latest     steps:     - name: Checkout code       uses: actions/checkout@v2     - name: Use API key       run: echo "Using API key: ${{ secrets.OPENAI_API_KEY }}"`

### 5. **HashiCorp Vault**

Some organizations use external secret management solutions like **HashiCorp Vault**, which provides a secure way to store, access, and manage sensitive information dynamically. This can integrate with CI/CD pipelines to fetch secrets at runtime without exposing them in the source code.

### 6. **AWS Secrets Manager / Azure Key Vault / GCP Secret Manager**

Cloud providers like AWS, Azure, and GCP provide native secret management solutions where you can securely store and access sensitive information:

- **AWS Secrets Manager** or **Parameter Store**: Securely stores API keys and credentials.
- **Azure Key Vault**: Protects and manages access to secrets.
- **Google Secret Manager**: Centralizes and manages sensitive data.

### 7. **Private Repositories and Access Control**

If you must include sensitive information (not recommended), make sure your repository is private and apply strict access control policies. However, even in private repositories, it is best to avoid committing sensitive data directly.

### 8. **GitHub Pre-Commit Hooks for Secret Scanning**

Tools like **pre-commit hooks** (e.g., `git-secrets`, `truffleHog`) can help scan for potential API keys, passwords, or secrets before pushing to a remote repository. These tools can alert or block commits that contain sensitive information.

### Best Practices Summary:

- **Never hardcode sensitive information** like passwords, SSH keys, or API keys in your code, Docker files, or version control.
- Use **environment variables** or secret management tools to securely pass sensitive data at runtime.
- Add files that contain sensitive data to your `.gitignore` file.
- Leverage GitHub Secrets or other **secret management systems** (like AWS Secrets Manager, Azure Key Vault, etc.) for secure storage and access during CI/CD workflows.
- Use **pre-commit hooks** or secret scanning tools to avoid committing secrets.

By following these practices, you can keep your sensitive information secure while developing and deploying applications.