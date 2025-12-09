__**3D E-Commerce Platform Architecture on AWS: High Availability Design**__

<img width="491" height="564" alt="image" src="https://github.com/user-attachments/assets/42d26ccf-5b30-4529-8bc9-83188ab02771" />

---

__**Overview & Core Design Principles**__

This architecture supports a global 3D e-commerce platform where users interact with high-resolution 3D product models. The design strictly adheres to the AWS Well-Architected Framework, focusing on the following pillars:

<img width="831" height="395" alt="image" src="https://github.com/user-attachments/assets/be1eb2cd-8d09-4ca8-a288-2cd0a1844b73" />

___

__**Key AWS Services Used and Rationale**__

<img width="600" height="816" alt="image" src="https://github.com/user-attachments/assets/6a981064-7bde-4873-be70-364d033fec74" />
<img width="599" height="89" alt="image" src="https://github.com/user-attachments/assets/e5bc6390-5f70-4efd-b0e8-81b48cfff176" />


___

__**How the Architecture Meets the 5 Requirements**__

__1. High Availability__
   
      •	Multi-AZ Deployment: RDS (Aurora) and the EC2 Auto Scaling Group span multiple Availability Zones within an AWS Region.
      
      •	Decentralized Delivery: CloudFront caches content at edge locations, reducing dependency on a single region or origin.
      
      •	Automatic Failover: Route 53 health checks automatically re-route traffic away from unhealthy endpoints.

__2. Scalability__

        •	Horizontal Scaling: EC2 Auto Scaling dynamically adds or removes instances based on demand (CPU utilization, queue length).
      
        •	Serverless Scaling: Lambda and DynamoDB offer near-instant, massive, and automatic scaling capabilities.

        •	Elastic Storage: S3 and CloudFront provide virtually unlimited, auto-scaling capacity for global asset storage and delivery.
    
__5. Performance__
      
       •	Edge Caching: CloudFront significantly reduces the load on the origin (S3/EC2) and provides the fastest possible delivery to end-users worldwide.
      
       •	Specialized Databases: DynamoDB is optimized for sub-10ms product lookups, keeping the user experience snappy.
      
       •	Efficient Routing: ALB intelligently distributes traffic for optimal server resource usage.

__6. Security__ 
  
       •	VPC Isolation: Backend resources (EC2, RDS) are isolated in private subnets, only accessible via the ALB.
       
       •	Least Privilege: IAM Roles and policies enforce granular access control for all services.
       
       •	Data Protection: RDS enforces data-at-rest encryption. CloudFront OAC restricts S3 access only to CloudFront.

__7. Cost Optimization__ 

        •	Pay-as-you-go: Utilizing Lambda and DynamoDB eliminates idle compute costs for sporadic workloads.
        
        •	Caching Efficiency: CloudFront minimizes expensive requests to the origin (EC2/S3) by serving content from cheaper edge caches.
        
        •	Resource Right-Sizing: The Auto Scaling Group and DynamoDB auto-scaling ensure resources precisely match the current load, preventing over-provisioning.

___

__**Trade-offs and Challenges**__

<img width="601" height="388" alt="image" src="https://github.com/user-attachments/assets/e67da36e-a368-49ae-bf91-3cfbd0158398" />
<img width="600" height="110" alt="image" src="https://github.com/user-attachments/assets/f094bf64-4db1-4814-90aa-3cb79c2a8c32" />

___

__**Insight**__

This taught us how to integrate and optimize AWS services to solve the complex technical challenges of a global, high-demand platform as this research serves as a practical lesson in designing a modern, highly available, and scalable cloud application using AWS.

___

__**Conclusion**__

The proposed architecture successfully leverages a suite of AWS managed services—particularly the combination of CloudFront, S3, Auto Scaling compute, and a specialized database layer (DynamoDB/RDS)—to create a global, highly available, and cost-effective foundation for a high-traffic 3D e-commerce platform. This design minimizes operational overhead while ensuring resilience against both sudden traffic spikes and component failures.
