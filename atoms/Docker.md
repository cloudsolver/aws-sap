### Summary of Docker
Containerization that supports modern microservices architecture, lift-and-shift. 

### Docker Details
[[ECS]], [[EKS]], [Fargate](Fargate), and [[ECR]] are Container Management services on AWS.

- Containers share the host kernel.
- Not a good choice for applications that need persistent data storage 
- Not a good choice for applications have complex networking, routing, or security requirements

- `DockerFile`builds an image.
- Push an image to the repo.
- You can pull images from the repo.
- Use for compute-intensive applications.
