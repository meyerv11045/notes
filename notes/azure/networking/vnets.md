# Virtual Networks

- Virtual Network- customer's private network within Azure public cloud
  - Have an address space (all resources in the vnet must have addresses in this range)
  - Specify an address space using CIDR notation
    - Specify starting address and number of pits of prefix (called the mask)
    - 10.0.0.0/16 means starting address of 10.0.0.0 and first 16 bits identify the network --> 65k addresses range from 10.0.0.0 to 10.0.255.255
  

- Subnets- vnet is often divided into multiple subnets

  - Additional security in filtering network trafffic between subnets

  - Address space is a subset of the parent vnet's address space




## CIDR Notation

1. Convert the IP address to binary: e.g., `172.31.0.0` in binary is `10101100.00011111.00000000.00000000`
2. The mask tells you how many bits of the binary IP address identify the network (and stay constant for everything in that network) and how many bits identify unique hosts (and therefore, can vary). For a /16 mask, the left-most 16 bits stay constant, while the right-most 16 bits are allowed to vary.
3. Putting that together, `172.31.0.0/16` represents all IP addresses from `10101100.00011111.00000000.00000000` (`172.31.0.0`) to `10101100.00011111.11111111.11111111` (`172.31.255.255`)

- [Read More](https://docs.gruntwork.io/guides/build-it-yourself/vpc/core-concepts/cidr-notation)