# sre-helm-chart
The SRE Technical Challenge is a project designed to deploy a simple Elixir Phoenix application using Kubernetes and Helm. It aims to showcase the deployment of a containerized Elixir application, including configuring environment variables, running database migrations, setting up health probes, and enabling ingress for public access.

Project Components:
Elixir Phoenix Application: The core of the project is a Phoenix web application written in Elixir. It provides a basic web interface with CRUD functionality for todo items.

Docker Container: The application is containerized using Docker, making it easy to deploy consistently across different environments.

Helm Chart: The Helm chart defines the Kubernetes deployment for the Elixir application. It includes configuration options for various aspects of the deployment.

PostgreSQL Database: The project uses a PostgreSQL database for data storage. It is deployed as a separate service in Kubernetes.

Documentation for Setup and Review:
To set up and review the SRE Technical Challenge project, please follow these steps:

Clone the Repository:
Clone the project's Git repository from [repository URL] to your local machine.

Prerequisites:
Ensure you have the following tools installed:
Docker
Kubernetes
Helm
kubectl
Deploy the PostgreSQL Database:

Use Helm to install the PostgreSQL database. Run the following command:

NAMESPACE=stord
helm install sre-db oci://registry-1.docker.io/bitnamicharts/postgresql \
  --create-namespace \
  --namespace $NAMESPACE \
  --set auth.database=sre-technical-challenge \
  --set auth.postgresPassword=password
  
Build and Push the Elixir Application Container:
Build the Docker container for the Elixir application using the provided Dockerfile.
Push the container to a container registry (e.g., Docker Hub, GitHub Container Registry, etc.). Ensure you have appropriate permissions.

Configure Helm Values:
Update the values.yaml file to match your specific configuration, including image repository, environment variables, and other settings.
Deploy the Elixir Application:

Use Helm to deploy the Elixir application. Run the following command:

helm install sre-app ./ \
  --debug \
  --namespace $NAMESPACE \
  --values values.yaml
Validate the Deployment:

After deployment, run the following commands to validate the setup:
For the database:

kubectl port-forward svc/sre-db-postgresql 55432:5432
psql postgresql://postgres:password@127.0.0.1:55432/sre-technical-challenge
For the application:

kubectl port-forward svc/sre-app-sre-technical-challenge 8080:80
Visit http://localhost:8080/todos in your browser.

Review the Documentation:
Detailed documentation about the project structure, configuration options, and deployment process can be found in the project's README.md file.

Review the Helm Chart:
Explore the Helm chart in the ./my-elixir-app directory. Review the YAML files for each Kubernetes resource to understand how the application is deployed.

Perform Code Review:
Review the source code of the Elixir Phoenix application to understand its functionality and implementation details.

Testing:
Perform testing, including unit tests and any additional tests relevant to the application.

Logging and Monitoring:
Implement logging and monitoring solutions as needed to track the application's behavior and performance.

Security Review:
Conduct a security review of the application and Kubernetes configuration to identify and address potential vulnerabilities.

Documentation for Future Maintenance:
Document any relevant information for future maintenance and updates of the application and infrastructure.

Deployment to Production:
If necessary, adapt the configuration for production deployment, including scaling, load balancing, and security considerations.

Final Review:
Once everything is set up and reviewed, conduct a final review to ensure the project meets all requirements and is ready for production use.
