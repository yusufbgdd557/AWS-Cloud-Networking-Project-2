# AWS VPC Project 2

In this project, I continued my VPC journey by extending the network to include a Private Subnet. The goal was to create an isolated subnet that is not directly connected to the internet while maintaining internal communication within the VPC. This is part of my larger project series where I build out my VPC in a structured and secure way.

## Project Overview
![Private VPC888](https://github.com/user-attachments/assets/40a1eda6-8837-4ca2-90da-eb2f934ef36a)

I created a Private Subnet within my existing VPC that cannot communicate with the internet directly. To ensure proper routing and security, I set up a dedicated Route Table for the Private Subnet and configured a Network Access Control List (NACL) to restrict traffic. Additionally, I chose a different availability zone for the Private Subnet to improve redundancy and fault tolerance.

## Steps I Took

### Step 1: Created the Private Subnet

The first step was to create a Private Subnet within the same VPC where my Public Subnet already exists. I ensured that the CIDR block was unique and did not overlap with any other subnets in my VPC. Additionally, I selected a different availability zone for the Private Subnet to enhance redundancy and fault tolerance.

- **Subnet Name:** my-private-subnet-01
- **VPC:** Selected my existing VPC.
- **Availability Zone:** Chose a different availability zone from the Public Subnet (e.g., `us-east-1b` while the Public Subnet is in `us-east-1a`).
- **CIDR Block:** `10.0.1.0/24`

After creating the subnet, I verified that the CIDR blocks across all subnets in the VPC did not overlap to prevent routing issues and ensure smooth communication between the subnets.

### Step 2: Created a Route Table for the Private Subnet

Once the Private Subnet was established, I created a new Route Table specifically for it. Since this subnet should not have direct internet access, I did not associate an Internet Gateway with the Route Table.

- **Route Table Name:** my-private-route-table
- **VPC:** Selected my VPC.

I added routes to ensure that the Private Subnet could communicate internally within the VPC and reach other private resources:

- **Destination:** `10.0.0.0/16` (The entire VPC CIDR block for internal communication)
- **Target:** Local (This enables communication between subnets within the VPC).

**I associated** this Route Table with the Private Subnet to ensure that all traffic from the subnet was routed internally.

### Step 3: Configured the NACL for the Private Subnet

To ensure maximum security for my Private Subnet, I configured a Network Access Control List (NACL) that blocks all inbound and outbound traffic from any IPv4 address (`0.0.0.0/0`). This effectively isolates the Private Subnet from any external traffic, making it fully protected.

Here’s what I did:

- **NACL Name:** My Private Network ACL
- **VPC:** Selected my VPC.
- **Inbound Rules:** Blocked all inbound traffic by denying access from `0.0.0.0/0` (which means all IP addresses are denied by default).
- **Outbound Rules:** Similarly, blocked all outbound traffic by denying access to `0.0.0.0/0`.

**I associated** this NACL with the Private Subnet, ensuring that no external traffic could enter or leave the subnet.

### Reflection

By completing this project, I successfully created a Private Subnet that is isolated from the internet and secured by strict NACL rules. This setup provides an extra layer of security, particularly for sensitive resources that don’t require direct internet access, such as databases or internal services.

This was another step forward in my VPC project series. In the next step, I plan to launch instances into the Private Subnet and explore internal communication and resource access.

## Project Screenshots

1- Private Subnet Creation
![create private subnet](https://github.com/user-attachments/assets/fdaab235-d4fa-47aa-9712-b9cebf1567cc)

2- Inbound & Outbound Rules
![inbound rules](https://github.com/user-attachments/assets/69c90dde-4f5f-4de7-9ddd-a5bd4101f82b)

![outbound rules](https://github.com/user-attachments/assets/632e15cc-5631-4117-a196-edacec58e1b1)

3- Resource Map
![image](https://github.com/user-attachments/assets/668687f9-d408-4b8b-ac14-c8fe3a868403)
