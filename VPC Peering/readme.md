# VPC Peering Setup

This guide details the steps for setting up VPC peering between a default VPC and a custom VPC (vpc-1). We created route tables, internet gateway, and subnets, and tested connectivity between instances in both VPCs.

## Steps

### 1. Create VPCs
- **Default VPC**: Use the existing default VPC.
- **Custom VPC (vpc-1)**: Create a new VPC.

### 2. Create Subnet for vpc-1
- Create a subnet within the custom VPC (vpc-1).

### 3. Create and Attach Internet Gateway to vpc-1
- Create an Internet Gateway.
- Attach the Internet Gateway to vpc-1.

### 4. Create and Configure Route Table for vpc-1
- Create a new route table for vpc-1.
- Add a route to the internet via the Internet Gateway.
- Associate the route table with the subnet created in vpc-1.

### 5. Launch EC2 Instances
- **Default VPC**: Launch an instance.
- **Custom VPC (vpc-1)**: Launch another instance.

### 6. Test Initial Connectivity
- Test connecting from the instance in the default VPC to the instance in vpc-1. (This should fail.)

### 7. Create VPC Peering Connection
- Create a VPC peering connection between the default VPC and vpc-1.
- Accept the VPC peering connection request.

### 8. Update Route Tables for Peering
- **Default VPC Route Table**: Add a route to vpc-1's CIDR block via the VPC peering connection.
- **vpc-1 Route Table**: Add a route to the default VPC's CIDR block via the VPC peering connection.

### 9. Test Connectivity After Peering
- Test connecting from the instance in the default VPC to the instance in vpc-1. (This should now work.)

## Verification

1. **Default VPC Route Table**:
    - Ensure there is a route to vpc-1's CIDR block via the VPC peering connection.
2. **vpc-1 Route Table**:
    - Ensure there is a route to the default VPC's CIDR block via the VPC peering connection.
3. **Security Groups**:
    - Ensure security groups allow traffic between instances.

## Conclusion
With the VPC peering setup and appropriate route table configurations, instances in the default VPC and the custom VPC (vpc-1) can communicate with each other.

