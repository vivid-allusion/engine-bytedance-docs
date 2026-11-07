---
title: "CLI overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CLI_overview"
---

## AgentKit CLI overview

The AgentKit CLI is a command\-line tool for simplifying full lifecycle management of agent applications. It covers the entire workflow in the terminal: scaffolding projects, building and deploying runtimes, and invoking deployed agents. It also manages MCP services, knowledge bases, memories, sandboxes, skills, and evaluations. [Learn more](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh)

The CLI provides the following preset agent templates. You can also use your own code:

* Basic Agent App: The simplest agent application for quick start.

* Basic Stream Agent App: An agent application that supports streaming output, powered by VeADK.

## Advantages

* **Declarative configurations**: All configurations are managed via a single `agentkit.yaml` file, ensuring clarity, portability, and easy version control.

* **Multi\-environment deployment**: Seamlessly supports three modes (local development, hybrid deployment, and cloud deployment) to meet diverse scenario requirements.

* **One\-click operations**: Advanced commands such as `agentkit launch` consolidate multiple steps (such as building and deployment) into one, significantly boosting efficiency.

* **Template\-based project initialization**: Built\-in application templates enable quick project startup without starting from scratch.

* **Interactive guidance**: Wizards such as `agentkit config` guide you through configuration and reduce the learning curve.

## Main commands

The AgentKit CLI provides intuitive commands for managing your **agent** applications. These commands use the standard syntax: `agentkit <command> [arguments] [options]`. [Learn more](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands)

### Core commands

|**Command** |Description |
|---|---|
|`agentkit init` |Initialize a new agent project using one of the available templates. |
|`agentkit add` |Generate and incrementally update the harness configuration file, or add a credential. |
|`agentkit list` |List runtimes deployed in harness mode, or list credentials. |
|`agentkit delete` |Delete a credential by name. |
|`agentkit config` |Configure the agentkit.yaml file via an interactive wizard. |
|`agentkit build` |Build your Agent application into a Docker image. |
|`agentkit deploy` |Deploy the built image to the target environment (local or cloud). |
|`agentkit launch` |Complete build and deployment in one click. It is the most frequently used command in development. |
|`agentkit invoke` |Interact with the deployed agent for quick testing. |
|`agentkit status` |Check the running status and endpoint of the agent. |
|`agentkit destroy` |Stop and destroy agent instances to release related resources. |

### Platform service commands

|**Command** |**Description** |
|---|---|
|`agentkit memory` |Manage AgentKit memory collections. |
|`agentkit knowledge` |Manage the AgentKit knowledge base. |
|`agentkit tools` |Manage AgentKit tools and sessions. |
|`agentkit runtime` |Manage AgentKit runtime instances. |

### General commands

|**Command** |**Description** |
|---|---|
|`--help` |View detailed descriptions and parameters for any command. |
|`--version` |Display the CLI version information. |

## Deployment modes

The **AgentKit CLI** supports flexible launch modes tailored to different stages from development to production. [Learn more](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/agentkit-yaml#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%85%8D%E7%BD%AE)

### Local mode (Local)

Build and deploy entirely on your local machine, ideal for rapid development and testing.

* **Workflow**: Source code → Local Docker build → Local container execution

* **Advantages**: Fast iteration, offline support, and convenient direct testing.

### Cloud mode (Cloud)

Fully hosting code builds and deployments on **AgentKit** is a best practice for production environments.

* **Workflow**: Source code → Automated cloud build → Cloud Container Registry → Production\-grade runtime

* **Advantages**: No local Docker environment required, built\-in observability, high environment consistency, and enhanced security and reliability.

### Hybrid mode (Hybrid)

Build the image locally, then push it to **AgentKit** in the cloud for deployment. This mode combines the benefits of local control and cloud\-based capabilities.

* **Workflow**: Source code → Local Docker build → Upload to Container Registry in the cloud → Production\-grade runtime

* **Advantages**: Balance the flexibility of local build with the stability of cloud running environments, suitable for scenarios requiring customized build processes.

## Configuration file (agentkit.yaml)

`agentkit.yaml` is the core of an **AgentKit** project, defining all application configurations in a declarative manner. We highly recommend that you use the `agentkit config` command to manage this file. [Learn more](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/agentkit-yaml)

```Bash
# General configuration
common:
  agent_name: my-agent
  entry_point: app.py
  python_version: '3.12'
  launch_type: cloud # Define the default deployment mode.

# Specific configuration for different deployment modes
launch_types:
  cloud:
    region: ap-southeast-1
    image_tag: latest
    runtime_envs:
      MODEL_API_KEY: "your-api-key"
```

## Environment requirements

### Basic environment (all modes)

* **Python version**: 3.10 or later

* **Operating system**: Linux, macOS

* **Package manager**: We recommend that you use `uv` or `pip`.

* The **AgentKit SDK** is installed.

### Python development environment

* Python version: 3.10, 3.11, 3.12, and 3.13.

* We recommend that you use `requirements.txt` to manage dependencies.

### Golang development environment

* Golang 1.24 is supported.

* Use `go.mod` to manage dependencies.

* Suitable for high\-performance scenarios.

### Local development (Local/Hybrid mode)

* Docker Desktop or Docker Engine 20.10+.

* Make sure that the Docker service is started.

### Cloud deployment (Cloud/Hybrid mode)

* A registered BytePlus account

* Configured access credentials (AK/SK). We recommend that you use secure global configurations.

   ```Bash
   # Initialize the global configuration.
   agentkit config --global --init
   
   # Configure access credentials.
   agentkit config --global --set byteplus.access_key="your_access_key"
   agentkit config --global --set byteplus.secret_key="your_secret_key"
   ```

## Quick start

Deploy your first **agent** in minutes.

```Bash
# 1. Initialize a project (select the Basic App template).
mkdir my-first-agent && cd my-first-agent
agentkit init my-first-agent

# Or specify a specific template.
agentkit init my-first-agent --template basic_stream  # Streaming output template
agentkit init my-first-agent --template a2a           # A2A protocol template

# 2. Configure the application (via interactive wizard).
agentkit config

# 3. Deploy to the cloud with one click.
agentkit launch

# 4. Test your agent.
agentkit invoke "Hello！"

# 5. Check the running status.
agentkit status

# 6. Clean up resources (optional).
agentkit destroy
```

## Explore more features

* [Initialize a project (init)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/init): View built\-in templates and generate a project scaffold. You can also package an existing Python agent file as a deployable project.

* [agentkit.yaml](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/agentkit-yaml): Learn about lifecycle configuration fields. Configure `launch_type`, runtime environment variables, and build/deployment parameters correctly to avoid issues where the agent runs locally but fails in the cloud.

* [Manage runtimes (runtime)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/runtime): List runtimes, view details and version history, pull logs, update configurations, and publish new versions.

* [Manage knowledge bases (knowledge)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/knowledge): Create knowledge bases and upload or register documents to provide agents with searchable external resources.

* [Manage memories (memory)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/memory): Create and query memories. Associate a memory ID at runtime to enable long\-term memory storage and retrieval across sessions.

* [Manage MCP services (mcp service)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/mcp): Deploy MCP servers as cloud resources and configure networking and inbound authentication (API Key/Custom JWT).

* [Use sandboxes (sandbox)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/sandbox): Create sandbox tools or sessions to execute commands, transfer files, and open web previews. This feature is suitable for development, testing, and capability verification.

* [Manage platform skills and local skill packages (skill/skills)](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/commands/skill): View platform skills and versions, and manage skills spaces. Upload or download skill packages and generate secure wrapper for installation in hosted environments.

## Updates and iterations

The AgentKit CLI continually releases new versions to improve commands, fix issues, and increase stability. To view the specific changes in each version, such as new commands, parameter adjustments, and compatibility notes, see the [changelog](https://docs.veadk.xyz/productions/agentkit-cli/preview/zh/changelog).
