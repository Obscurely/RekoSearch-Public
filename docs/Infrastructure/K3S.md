# K3S Architecture 

![Architecture Diagram](../../assets/diagrams/k3s.png "K3S Architecture Diagram")

Now, to break it down a little:

- Auto Scaling Groups: These groups are for the server and worker nodes so that
  the cluster can adjust to the traffic. This gives us multiple nodes across
  different regions, making the cluster highly available. The ASGs combine
  on-demand and spot instances (according to your configuration preferences) to
  achieve the most cost efficiency.
- Launch Templates: with all the configuration needed and user scripts for
  turning an EC2 instance into a fully-fledged production-ready K3s node.
- SSH Key Pair: for secure shell access to all of the nodes.
- IAM Instance Profile: Restricted permissions for the nodes in order to
  interact with the EC2, SSM, ASG, SM and ECR services.
- AWS Secrets Manager: For securely uploading and storing the kube
  configuration.
- Internal Network Load Balancer: for fast communication between the nodes
  without external communication.
- External Application Load Balancer: for optimized HTTPS access to the cluster
  (and Kube API). The HTTPS access is restricted to only CloudFront (either the
  distribution created by the module or an externally created one) and your IP
  for extra protection.
- ACM: For AWS-managed TLS certificates. There is no need to worry about
  provisioning and renewing TLS certificates within the cluster.
- EventBridge Rules: Two event rules, one for Spot Instance interruption and one
  for Spot Instance request fulfillment and 2 SQS queues for them to send these
  events and be taken care of.
- Lambda: This function handles the termination of spot instances. It removes
  nodes from the cluster and adds new nodes, making the transition between Spot
  Instances seamless. Also, Lambda is serverless, which makes it cost-efficient.
  Additionally, the IAM role permissions are restrictive for security.
- Security Groups: There are three of them: one for the ASG, one for the
  External Load Balancer and one for Lambda. None of these allow direct public
  traffic. The only public access to this cluster comes from CloudFront (on port
  443), making it secure.
- Cloudfront: As mentioned above, it stays in front of the load balancer. I've
  configured it with the best security settings. Or you there is option of using
  an externally created one.
- Route53: Two records are created, one with the FQDN given for accessing the
  application you have hosted on the cluster and a k3s.${fqdn} record for
  accessing the server nodes using kubectl over port 6443 (the incoming traffic
  is only allowed from your IP)
