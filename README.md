Markdown

# Obliviate: The MLOps Simplification Tool 🪄

**Project Overview:** `Obliviate` is an end-to-end MLOps platform that automates the deployment and optimization of Hugging Face models. It solves the "last mile problem" of machine learning by providing a declarative, intelligent, and scalable system that bridges the gap between a data scientist's model and a production environment. The platform is built on a two-tier architecture that combines the power of a Go-based Kubernetes operator with a Python-based API gateway.

`Obliviate` is not just a tool; it's a strategic platform that automates an MLOps engineer's workflow. It eliminates the manual, error-prone processes that hold a team back and provides a single, consistent approach to managing the entire MLOps lifecycle.

### Key Features ✨

* **Trino-Powered Data Layer:** Uses a Trino cluster to get real-time, data-driven insights that inform model deployment and optimization. `Obliviate` can query a customer's data lake to determine the most common shape of the input data, and then use that information to configure the model's optimal batch size.
* **AI-Driven Deployment and Health Checks:** An intelligent Kubernetes operator automates the deployment of a `Truss`-packaged model and uses an LLM to proactively monitor its health. This turns a manual troubleshooting process into a proactive, automated one.
* **Model Optimization:** The platform automates the optimization of Hugging Face models using **TensorRT** for GPU acceleration. This could involve converting the model to a faster format and applying specific tuning configurations based on the Trino-provided data.
* **Production-Ready Packaging:** The platform uses the open-source **Truss** library to provide a standard, reproducible way to package a machine learning model. This abstracts away the complexity of building a production-ready container image.

### Architecture 🏗️

The architecture of `Obliviate` is a two-tier system with a clear separation of concerns. This design is what makes it resilient, scalable, and easy to maintain.

1.  **The Control Plane (`Obliviate-Operator`):** This is a Go-based Kubernetes operator. Its primary responsibility is to manage the lifecycle of your machine learning models. It takes a high-level `Obliviate` custom resource (CR) and, through its reconciliation loop, automatically deploys a `Deployment` and a `Service` for each model.
2.  **The Data Plane (`Obliviate-Router` Microservice):** This is a Python-based API gateway. It's a decoupled microservice that acts as the intelligent front end for your system. Its job is to handle all client requests, use the Trino-powered data layer to make smart routing decisions, and then forward the request to the correct model that your operator has deployed.
3.  **The Inference Layer (the Model Pods):** This is the backend workhorse. It's a set of microservices that perform the actual, resource-intensive task of running machine learning inference. The `Obliviate-Router` communicates with these services, which are optimized for high throughput and low latency.

### High-Level Implementation Steps 🛠️

1.  **Go Operator:** Build a Go operator that manages a custom `TrussModel` custom resource. The operator's reconciliation loop should automatically build a Docker image from a `Truss` configuration and deploy it to a Kubernetes cluster.
2.  **Trino Integration:** Implement a scheduled Python service that uses the `trino-python-client` to run a query that analyzes a sample of the production data.
3.  **Model Optimization:** The Go operator should trigger a multi-stage Docker build. The build process would use `TensorRT` to optimize the Hugging Face model and save the optimized model to a file.
4.  **Deployment:** The Go operator would then deploy the optimized model as a `Deployment` and `Service` in a Kubernetes cluster.

### Getting Started 🚀

To get started with `Obliviate`, clone this repository, install the necessary dependencies, and set up your environment variables for your Trino cluster and LLM.

```bash
git clone [https://github.com/joshuaFordyce/Obliviate.git](https://github.com/joshuaFordyce/Obliviate.git)
cd Obliviate
pip install -r requirements.txt
Contributing 🤝
This is an open-source project, and contributions are highly welcome. If you have an idea for a new feature or a bug fix, please feel free to submit a pull request. To get started, please see our contributing guide.

License 📜
This project is licensed under the Apache 2.0 License.
