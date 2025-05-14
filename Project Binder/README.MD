# Protein Structure, Charge-Map & Interaction Explorer

A cloud-native platform for protein structure prediction, visualization, and analysis, featuring a teacher-student distillation pipeline for AlphaFold-level accuracy with faster inference.

## Features

- **Public Showcase & Research Workspace**: Interactive 3D visualization of protein structures with electrostatic surface maps and interaction networks
- **Dual API Access**: Both REST and GraphQL endpoints for programmatic integration
- **Teacher-Student Distillation**: Continuous learning system that benchmarks against AlphaFold/OpenFold
- **Secure Architecture**: Enterprise-grade security with auth, encryption, and compliance features

## Quick Start

### Prerequisites

- Docker and Docker Compose
- Git
- Node.js 18+ (for local frontend development)
- Python 3.12+ (for local API development)
- NVIDIA GPU with CUDA 12.0+ (for GPU-accelerated folding)

### Development Setup

1. Clone the repository:

```bash
git clone https://github.com/yourusername/protein-explorer.git
cd protein-explorer

Set up environment variables:

cp .env.example .env
# Edit .env file with your configurations

Start the development environment:

docker-compose up -d

Seed the database with demo data:

docker-compose exec api python seed_db.py

Access the application:

Frontend: http://localhost:3000
API Docs: http://localhost:8000/api/docs
GraphQL Playground: http://localhost:8000/api/graphql
MinIO Console: http://localhost:9001
Grafana Dashboard: http://localhost:3001



Default Credentials

Demo User:

Email: demo@protein-explorer.com
Password: demopassword


Admin User:

Email: admin@protein-explorer.com
Password: adminpassword



GPU Deployment
For GPU-accelerated protein folding, follow these steps:

Ensure NVIDIA drivers and Docker GPU support are installed:

# Check GPU is available to Docker
docker run --gpus all nvidia/cuda:12.0-base nvidia-smi

Start the GPU-enabled services:

docker-compose -f docker-compose.yml -f docker-compose.gpu.yml up -d worker-gpu

Production Deployment
For production deployment to AWS:

Set up infrastructure with Terraform:

cd infra/terraform/production
terraform init
terraform apply

Deploy to EKS cluster:

# Configure kubectl
aws eks update-kubeconfig --name protein-explorer-production --region us-west-2

# Deploy with Helm
cd infra/helm
helm upgrade --install protein-explorer ./charts/protein-explorer -f ./values/production.yaml

Project Structure

frontend/: Next.js application with Three.js for 3D visualization
api/: FastAPI backend providing REST and GraphQL endpoints
worker/: Celery workers for protein folding and analysis
ingest/: Data ingestion pipelines from public sources
distillation/: Teacher-student model training framework
infra/: Infrastructure as code (Terraform, Helm charts)
docs/: Documentation and architecture diagrams

Security Hardening Checklist

 TLS 1.3 enforced for all connections
 JWT tokens with short expiry and rotation
 Multi-factor authentication (MFA) support
 Role-based access control (RBAC)
 S3 objects encrypted with AES-256
 Secrets management with AWS Secrets Manager
 Network micro-segmentation with K8s policies
 Regular security scanning with CodeQL and Trivy
 GDPR/CCPA compliance with user data deletion
 SLSA Level 3 provenance (optional flag --slsa)
 K-anonymity for sensitive data (optional flag --privacy-preserving)
 Zero-trust security model (optional flag --zero-trust)

Customization Options
Adding New Data Sources
To add a new data source connector, create a new connector class in the ingest/connectors/ directory:

# ingest/connectors/your_source.py

from ingest.core.connector import BaseConnector

class YourSourceConnector(BaseConnector):
    def __init__(self, config):
        super().__init__(config)
        # Initialize your connector
        
    def get_data(self):
        # Implement data retrieval
        pass
        
    def process_data(self, data):
        # Implement data processing
        pass

Training Custom Models
To customize the student model architecture:

Modify distillation/models/student/architecture.py
Adjust training parameters in distillation/training/config.py
Run the training script:
python -m distillation.training.train --config=custom_config.yaml

Contributing
Contributions are welcome! Please see CONTRIBUTING.md for details.
License
This project is licensed under the MIT License - see the LICENSE file for details.