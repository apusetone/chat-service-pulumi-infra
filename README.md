# chat-service-pulumi-infra
This repository contains the Pulumi infrastructure code for managing a chat service. It includes configurations for various AWS services such as VPC, ECS, RDS, ElastiCache, SNS, SES, SSM, CloudWatch, Lambda, ECR, CodeBuild, Athena, and S3. The infrastructure is designed to be deployed across different environments (development, staging, production) with environment-specific configurations.

## Key Components

- **VPC and Subnets**: Configures the network infrastructure including VPC, subnets, and NAT Gateway.
- **Application Load Balancer**: Sets up an ALB for distributing traffic.
- **ECS Cluster and Services**: Manages ECS clusters, task definitions, and services for containerized applications.
- **Aurora Database**: Configures an Aurora MySQL database cluster.
- **ElastiCache for Redis**: Sets up a Redis cluster for caching.
- **SNS and SES**: Configures SNS for notifications and SES for email services.
- **SSM Parameter Store**: Manages secure storage of configuration parameters.
- **CloudWatch**: Sets up CloudWatch alarms and log groups for monitoring and logging.
- **Lambda Functions**: Deploys Lambda functions for serverless computing.
- **ECR Repository**: Manages an ECR repository for storing Docker images.
- **CodeBuild Project**: Configures a CodeBuild project for CI/CD integration with GitHub.
- **Athena Workgroup**: Sets up an Athena workgroup for querying data.
- **S3 Bucket**: Manages an S3 bucket for storing Athena query results.
- **EventBridge Rule**: Configures scheduled execution of Lambda functions.

## Directory Structure

```
chat-service-pulumi-infra/
│
├── Pulumi.yaml
├── README.md
├── requirements.txt
│
├── src/
│   ├── __init__.py
│   ├── config.py
│   ├── network.py
│   ├── compute.py
│   ├── database.py
│   ├── storage.py
│   ├── monitoring.py
│   └── security.py
│
├── environments/
│   ├── dev/
│   │   ├── Pulumi.dev.yaml
│   │   └── __main__.py
│   ├── staging/
│   │   ├── Pulumi.staging.yaml
│   │   └── __main__.py
│   └── prod/
│       ├── Pulumi.prod.yaml
│       └── __main__.py
│
├── scripts/
│   ├── deploy.sh
│   └── destroy.sh
│
└── tests/
    ├── unit/
    │   └── test_network.py
    └── integration/
        └── test_deployment.py
```

## Project Setup

### Installing Dependencies

This project uses Python. To install the dependencies, run the following command:

```sh
pip install -r requirements.txt
```

### Pulumi Configuration

The Pulumi configuration file is located in `Pulumi.yaml`. Configuration files for each environment (dev, staging, prod) are located in the `environments/` directory.

## Directory Description

- `src/`: Contains Python scripts defining the infrastructure components (network, compute, database, storage, monitoring, security).
- `environments/`: Contains Pulumi configuration files and entry-point scripts for each environment (dev, staging, prod).
- `scripts/`: Contains shell scripts for deploying and destroying the infrastructure.
- `tests/`: Contains unit and integration tests.

## Deployment

To deploy to each environment, use the following commands:

### General Deployment Steps

1. Set Pulumi configuration:

    ```sh
    pulumi config set-all --path Pulumi.<env>.yaml
    pulumi config set aws:region <region>
    pulumi config set env <env>
    pulumi config set db_password <password> --secret
    ```

2. Select the Pulumi stack:

    ```sh
    pulumi stack select <env>
    ```

3. Deploy the stack:

    ```sh
    pulumi up
    ```

### Example: Deploy to Development Environment

```sh
pulumi stack select dev
pulumi config set aws:region us-west-2
pulumi config set env dev
pulumi config set db_password myDevPassword --secret
pulumi up
```

## Destroy

To destroy the resources in each environment, use the following commands:

### Destroy Development Environment

```sh
./scripts/destroy.sh dev
```

### Destroy Staging Environment

```sh
./scripts/destroy.sh staging
```

### Destroy Production Environment

```sh
./scripts/destroy.sh prod
```

## Testing

To run unit and integration tests, use the following commands:

### Unit Tests

```sh
pytest tests/unit
```

### Integration Tests

```sh
pytest tests/integration
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.
