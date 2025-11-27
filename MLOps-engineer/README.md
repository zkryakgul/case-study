# Case Study: MLOps Infrastructure & Serving (Mini ML Cluster)

**Role:**  MLOps Engineer**Level:**  Mid-Senior**Time:**  \~4-6 Hours

## 1. Scenario

The Data Science team has developed a new Sentiment Analysis model (`BERT-tiny` based). Currently, they are running it manually in a Jupyter Notebook. Your task is to build a robust, scalable, and observable infrastructure to serve this model in a production-like environment.

## 2. The Challenge

You are required to provision a local Kubernetes cluster, containerize the model, deploy it with high availability, and implement specific monitoring for ML metrics.

### Part A: Infrastructure Provisioning

- **Tooling:**  Use ​**Terraform**​, ​**Ansible**​, or **Kind** (Kubernetes in Docker) to provision a local Kubernetes cluster.
- **Requirement:**  The cluster must have at least **one master** and **two worker nodes** (simulated).
- **Ingress:**  Configure an Ingress Controller (Nginx or Traefik) to route external traffic to your services.

### Part B: Model Serving (The Application)

- **Model:**  Create a simple Python application (FastAPI or Flask) that loads a dummy model (you can use a pre-trained `scikit-learn`​ or `transformers` model, or even a mock function that sleeps for 0.5s to simulate inference).
- **API:**

  - ​`POST /predict`: Accepts JSON text, returns a sentiment score.
  - ​`GET /health`: Returns service health status.
- **Containerization:**  Create a `Dockerfile`.

  - **Constraint:**  Machine Learning images can be huge. Optimize the image size (e.g., use multi-stage builds, slim base images).

### Part C: Deployment & Orchestration

- **Manifests:**  Create Kubernetes manifests (Deployment, Service, Ingress, HPA) or a ​**Helm Chart**.
- **Resource Management:**  Define `requests`​ and `limits` for CPU and Memory.

  - *Bonus:*  Add a node selector or toleration to simulate scheduling the pod on a "GPU-enabled" node.
- **Scalability:**  Configure a ​**Horizontal Pod Autoscaler (HPA)** .

  - *MLOps Specific:*  The HPA should scale based on a custom metric (e.g., `requests_per_second`​ or `avg_inference_latency`), not just CPU usage.

### Part D: MLOps Observability (Critical)

Unlike standard web apps, ML models can fail silently (data drift).

- **Metrics:**  Implement a `/metrics`​ endpoint using the **Prometheus** client. Expose:

  - ​`inference_latency_seconds` (Histogram)
  - ​`prediction_count_total` (Counter)
  - ​`model_confidence_score` (Gauge - simulate a random score between 0.0 and 1.0)
- **Visualisation:**  Deploy a simple **Grafana** instance pre-configured with a dashboard showing these metrics.

## 3. Deliverables

Please provide a GitHub repository containing:

1. ​ **​`/infrastructure`​**: Code to spin up the cluster (Kind config, Terraform, etc.).
2. ​ **​`/model-service`​**: Source code and Dockerfile for the ML app.
3. ​ **​`/deploy`​**: Helm charts or K8s manifests.
4. ​**​`README.md`​**: A clear guide on how to:

    - Prerequisites.
    - Command to start the cluster.
    - Command to deploy the model.
    - Command to generate load (e.g., `hey`​ or `k6` script) to demonstrate Autoscaling.

## 4. Evaluation Criteria

We will look for:

- **Separation of Concerns:**  Is infrastructure code separated from application code?
- **ML Awareness:**  Did you handle the heavy dependencies (PyTorch/Scikit) efficiently in the Dockerfile?
- **Observability:**  Can we see the "Confidence Score" in Grafana? This shows you understand that ML monitoring goes beyond CPU/RAM.
- **Automation:**  How easy is it to stand up the environment? (Ideally one or two scripts).
