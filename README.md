# VPC with VPN Access To On-Prem Network
The instructions to create a VPC with a private subnet only and hardware VPN access as described [here](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Scenario4.html) are a great starting place for setting up this infrastructure, be it with IAAS (Infrastructure As Code) or via the AWS Console.

The last few steps however, took me quite a while to setup and configure in terraform-
> A custom route table associated with the subnet. The route table contains a route that enables instances in the subnet to communicate with other instances in the VPC, and a route that enables instances in the subnet to communicate directly with your network.

As simple as that sounds, going through 2 different examples on setting this up, http://www.cakesolutions.net/teamblogs/multi-vpn-on-aws-via-ipsec and https://ypoonawala.wordpress.com/2014/11/26/setting-up-a-hardware-vpn-connection-to-your-aws-vpc-using-cloudformation-for-dummies/ involved the creation of a `AWS::EC2::VPNGatewayRoutePropagation` and a `AWS::EC2::VPNConnectionRoute` resources.

The first resource creation, `AWS::EC2::VPNGatewayRoutePropagation` ensures the VPN Gateway (Virtual Private Gateway) will be able to propagate routes to the VPC's route table.

The second resource, `AWS::EC2::VPNConnectionRoute` is created to ensure that traffic can flow from the VPN Gateway to the Customer Gateway, i.e the VPC traffic destined for an on-prem subnet/host can reach it's destination via the VPN connection.
