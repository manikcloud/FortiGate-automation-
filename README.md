# FortiGate-automation-
FortiGate automation 

# Deploying FortiGate VM on AWS and Generating API Token

This guide provides step-by-step instructions to launch a FortiGate VM from AWS Marketplace, configure it, and generate an API token for API access.

## Prerequisites

- **AWS CLI**: Command Line Interface for interacting with AWS services.
- **AWS Account**: An active AWS account.
- **Web Browser**: For accessing the AWS Management Console and FortiGate Web GUI.

## Steps

### 1. Launch FortiGate VM from AWS Marketplace

1. **Sign in to AWS Management Console**:
   - Go to the [AWS Management Console](https://aws.amazon.com/console/) and sign in with your credentials.

2. **Search for FortiGate in AWS Marketplace**:
   - Navigate to [AWS Marketplace](https://aws.amazon.com/marketplace/) and search for "FortiGate".

3. **Select a FortiGate Product**:
   - Choose the appropriate FortiGate product that suits your needs (e.g., FortiGate Next-Generation Firewall).

4. **Subscribe to the Product**:
   - Click on the product and subscribe to it.

5. **Configure the Instance**:
   - Click on "Continue to Configuration".
   - Select the software version and region.
   - Click on "Continue to Launch".

6. **Launch the Instance**:
   - Choose "Launch through EC2" and configure the instance details (instance type, VPC, subnets, security groups, etc.).
   - Click on "Launch" to deploy the instance.

### 2. Configure FortiGate VM

1. **Access the FortiGate VM**:
   - Obtain the public IP address or DNS name of the FortiGate instance from the AWS EC2 console.
   - Access the FortiGate Web GUI by navigating to `https://<Public-IP>` in a web browser.

2. **Log in to FortiGate**:
   - Use the default username and password to log in (usually `admin` with no password). You will be prompted to set a new password.

### 3. Generate API Token

1. **Enable API Access**:
   - In the FortiGate Web GUI, go to **System** > **Administrators**.
   - Click **Create New** and select **REST API Admin**.

2. **Create an API Admin**:
   - Enter a name for the API admin.
   - Enable **Read/Write** permissions.
   - Click **OK**.

3. **Generate API Token**:
   - After creating the API admin, a token will be displayed. Copy this token and store it securely as it will not be shown again.

### Example Script for FortiGate Configuration via API

```sh
#!/bin/bash

# FortiGate IP and API token
FGT_IP="your_fortigate_ip"
API_TOKEN="your_api_token"

# Example API request to retrieve system status
curl -s -k -X GET "https://${FGT_IP}/api/v2/monitor/system/status" \
    -H "Authorization: Bearer ${API_TOKEN}" \
    -H "Content-Type: application/json"
