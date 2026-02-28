# Development Enviornment
Table Tap has a separate frontend and backend running on different ports. Docker is used to containerize those two elements together and have them work seamlessly.

# Prerequisites
- [Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install/)
- [Git](https://git-scm.com/downloads) (v2.x or higher recommended)

# Running the application on docker
> Docker must be installed and running before you try to build the containers.
1. Open your terminal and clone the 3 repositories down below:
    - Frontend
    ```bash
    git clone https://github.com/TableTapET/TableTap-Frontend.git
    ```
    - Backend
    ```bash
    git clone https://github.com/TableTapET/TableTap-Backend.git
    ```
    - Deployment Enviornment
    ```bash
    git clone https://github.com/TableTapET/TableTap-Deployment.git
    ```
2. Navigate to the root directory of the Deployment Enviornment repository
    ```
    cd <path/to/deployment/environment>/TableTap-Development
    ```
3. Setup and build the containers using the command ```docker-compose -f docker-compose.dev.yml build```
4. To run the web app, use the command ```docker-compose -f docker-compose.dev.yml up -d```
    - The website should be running on: http://localhost:5002
5. If you want to shutdown the web app, run the command ```docker-compose down``` in your root directory of the deployment terminal

## CI/CD Pipelines

TableTap uses GitHub Actions for continuous integration and deployment.
- **Frontend CI:** Runs `npm run test` and `npm run build` on PRs and pushes to `main`.
- **Backend CI:** Spins up PostgreSQL/MongoDB services and runs `run_tests.py --all` on PRs and pushes to `main`.
- **Deployment CD:** Automatically pulls the latest code and rebuilds production Docker containers when changes are pushed to - Dry run CD for now `main`.

**Required GitHub Secrets for Deployment:**
- `SERVER_IP`: Production server IP address (Once prod server is available)
- `SERVER_USER`: SSH username
- `SSH_PRIVATE_KEY`: Private key for SSH access