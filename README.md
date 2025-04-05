
```bash
#!/bin/bash

# Environment variables
ENVIRONMENT=$1

# Function to check if the script has the necessary argument
check_num_of_args() {
    # Checking the number of arguments
    if [ "$#" -ne 1 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
}

# Function to activate environment based on the argument
activate_infra_environment() {
    # Acting based on the argument value
    if [ "$ENVIRONMENT" == "local" ]; then
        echo "Running script for Local Environment..."
    elif [ "$ENVIRONMENT" == "testing" ]; then
        echo "Running script for Testing Environment..."
    elif [ "$ENVIRONMENT" == "production" ]; then
        echo "Running script for Production Environment..."
    else
        echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
        exit 2
    fi
}

# Function to check if AWS CLI is installed
check_aws_cli() {
    if ! command -v aws &> /dev/null; then
        echo "AWS CLI is not installed. Please install it before proceeding."
        exit 3
    fi
}

# Function to check if AWS profile is set
check_aws_profile() {
    if [ -z "$AWS_PROFILE" ]; then
        echo "AWS profile environment variable is not set."
        exit 4
    fi
}

# Calling functions
check_num_of_args
activate_infra_environment
check_aws_cli
check_aws_profile

# You can add further code here to automate EC2 instance creation and S3 bucket setup
```

### Breakdown of the script:
1. **check_num_of_args**: This function checks if exactly one argument is passed to the script, which represents the environment (local, testing, or production).
2. **activate_infra_environment**: This function decides which environment to set up based on the argument provided.
3. **check_aws_cli**: This function verifies if the AWS CLI is installed on the system by using the `command -v aws` check. If not, it exits with a message prompting the user to install AWS CLI.
4. **check_aws_profile**: This function checks if the AWS profile environment variable (`AWS_PROFILE`) is set. If it's not set, the script exits with an error message.

This structure ensures that the script is modular, easy to maintain, and checks for critical dependencies (AWS CLI and AWS profile) before proceeding with the infrastructure setup. You can add more functionality for EC2 and S3 setup by integrating AWS CLI commands after the checks.
