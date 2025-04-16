## Introduction

This workshop is designed to teach you about the Azure AI Agents Service and the associated SDK. It consists of multiple labs, each highlighting a specific feature of the Azure AI Agents Service. The labs are meant to be completed in order, as each one builds on the knowledge and work from the previous lab.

## Prerequisites

1. Access to an Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
1. You need a GitHub account. If you don’t have one, create it at [GitHub](https://github.com/join).

## Open the Workshop

The preferred way to run this workshop is using GitHub Codespaces. This option provides a pre-configured environment with all the tools and resources needed to complete the workshop. 

Select **Open in GitHub Codespaces** to open the project in GitHub Codespaces.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/anahitaafsh/build-your-first-agent-with-azure-ai-agent-service-workshop)

!!! Warning "Building the Codespace will take several minutes. You can continue reading the instructions while it builds."

## Authenticate with Azure

You need to authenticate with Azure so the agent app can access the Azure AI Agents Service and models. Follow these steps:

1. Ensure the Codespace has been created.
1. In the Codespace, open a new terminal window by selecting **Terminal** > **New Terminal** from the **VS Code menu**.
1. Run the following command to authenticate with Azure:

    ```shell
    az login --use-device-code
    ```

    !!! note
        You'll be prompted to open a browser link and log in to your Azure account. Be sure to copy the authentication code first.

        1. A browser window will open automatically, select your account type and click **Next**.
        2. Sign in with your Azure subscription **Username** and **Password**.
        3. **Paste** the authentication code.
        4. Select **OK**, then **Done**.

    !!! warning
        If you have multiple Azure tenants, then you will need to select the appropriate tenant when authenticating.

        ```shell
        az login --use-device-code --tenant <tenant_id>
        ```

1. Next, select the appropriate subscription from the command line.
1. Leave the terminal window open for the next steps.

## Deploy the Azure Resources

The following resources will be created in the `rg-contoso-agent-workshop` resource group in your Azure subscription.

- An **Azure AI Foundry hub** named **agent-wksp**
- An **Azure AI Foundry project** named **Agent Service Workshop**
- A **Serverless (pay-as-you-go) GPT-4o model deployment** named **gpt-4o (Global 2024-08-06)**. See pricing details [here](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).
- A **Grounding with Bing Search** resource. See the [documentation](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/bing-grounding) and [pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing) for details.

!!! warning "If you get quota issues, review your quota availability in the [AI Foundry Management Center](https://ai.azure.com/managementCenter/quota)."

We have provided a bash script to automate the deployment of the resources required for the workshop. Alternatively, you may deploy resources manually using Azure AI Foundry studio.

The script `deploy.sh` deploys to the `eastus2` region by default; edit the file to change the region or resource names. To run the script, open the VS Code terminal and run the following command:

```bash
cd infra && ./deploy.sh
```

### Workshop Configuration

The deploy script generates the **.env** file, which contains the project connection string, model deployment name, and Bing connection name.

Your **.env** file should look similar to this but with your project connection string.

```python
MODEL_DEPLOYMENT_NAME="gpt-4o"
BING_CONNECTION_NAME="groundingwithbingsearch"
PROJECT_CONNECTION_STRING="<your_project_connection_string>"
```

1. From the **VS Code menu**, select **File** > **Open Workspace from File**.
2. Select the **.vscode/python-workspace.code-workspace** file.

## Project Structure

Be sure to familiarize yourself with the key **subfolders** and **files** you’ll be working with throughout the workshop.

### The workshop folder

- The **main.py** file: The entry point for the app, containing its main logic.
- The **sales_data.py** file: The function logic to execute dynamic SQL queries against the SQLite database.
- The **stream_event_handler.py** file: Contains the event handler logic for token streaming.

### The shared folder

- The **files** folder: Contains the files created by the agent app.
- The **fonts** folder: Contains the multilingual fonts used by Code Interpreter.
- The **instructions** folder: Contains the instructions passed to the LLM.

![Lab folder structure](../media/project-structure-self-guided-python.png)