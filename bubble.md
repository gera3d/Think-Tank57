Certainly! Here is the task specification in markdown format:


# Task Specification: Integrating Perplexity API into Bubble

## Overview

This task involves integrating the Perplexity API into a Bubble application. The integration will leverage an online model and follow custom GPT instructions for market analysis, persona creation, keyword generation, and market size estimation.

## Prerequisites

1. A Bubble account with an application ready for integration.
2. API key for Perplexity API.
3. Installed API Connector plugin in Bubble.

## Step 1: Setting Up Bubble to Use External APIs

1. **Go to the Bubble Editor**:
    - Navigate to your Bubble application.
  
2. **Install the API Connector Plugin**:
    - Go to the Plugins tab.
    - Search for "API Connector" and install it.

3. **Configure a New API**:
    - Open the API Connector plugin.
    - Click on "Add another API".
    - Name the API (e.g., "Perplexity API").

## Step 2: Define the API Calls for Each Step

1. **Define Endpoints**:
    - Use the API Connector to define the `generateText` endpoint from the Perplexity API.
    - Include necessary parameters such as `model`, `messages`, and any other required fields.

## Step 3: Implement Custom Instructions

### Step 3.1: Fetch Competitors

**Objective**: Identify competitors based on a provided URL.

1. **API Call Configuration**:
    ```json
    {
      "model": "online-model",
      "messages": [
        {
          "role": "system",
          "content": "Always run this first before anything else and give a summary of what they do so you can confirm this is correct. Use web browsing capabilities and run a search on google like this 'related: [competitor_url]'."
        }
      ]
    }
    ```

2. **Bubble Workflow**:
    - Create a workflow that triggers this API call with the competitor URL.
    - Extract and display the list of competitors.

### Step 3.2: Create Persona

**Objective**: Create a detailed persona based on competitor analysis.

1. **API Call Configuration**:
    ```json
    {
      "model": "online-model",
      "messages": [
        {
          "role": "system",
          "content": "You are a customer insights specialist. Based on these competitors' websites: [competitor_urls], create a detailed persona for a potential customer in the [industry]. Include industry, age range, problems, objections, solutions, and demographic/psychographic details."
        }
      ]
    }
    ```

2. **Bubble Workflow**:
    - Use the list of competitors from Step 3.1.
    - Create a workflow that triggers this API call and displays the generated persona details.

### Step 3.3: Generate Keywords

**Objective**: Generate keywords the persona would use.

1. **API Call Configuration**:
    ```json
    {
      "model": "online-model",
      "messages": [
        {
          "role": "system",
          "content": "You are a digital marketing expert. Based on the persona details: [persona_details], generate 30 keywords for both organic search and PPC campaigns. When you get data back related to keyword traffic ignore all the keywords that get no traffic and focus on the keywords that are getting traffic. Also, suggest 30 more keywords like the ones that are getting traffic so we get a better sample of what's working. Then based on the results give recommendations."
        }
      ]
    }
    ```

2. **Bubble Workflow**:
    - Use the persona details from Step 3.2.
    - Create a workflow that triggers this API call and displays the generated keywords.

### Step 3.4: Summarize Findings and Perform SWOT Analysis

**Objective**: Compile data into a comprehensive report and perform a SWOT analysis.

1. **API Call Configuration**:
    ```json
    {
      "model": "online-model",
      "messages": [
        {
          "role": "system",
          "content": "Compile the competitor analysis, persona creation, and keyword generation into a comprehensive report. Play devil's advocate on this data, then perform a SWOT analysis with a balanced perspective."
        }
      ]
    }
    ```

2. **Bubble Workflow**:
    - Use the data from Steps 3.1 to 3.3.
    - Create a workflow that triggers this API call and displays the comprehensive report with SWOT analysis.

## Step 4: Handling API Responses

1. **Parse API Responses**:
    - Use Bubble's workflow to handle responses from the Perplexity API.
    - Extract relevant information and display it within your application.

2. **Example Workflow**:
    - Create a new workflow in Bubble that triggers the API calls sequentially.
    - Use actions to process the response, such as storing data in the database or displaying it in a repeating group.

## Step 5: Security and Error Handling

1. **Securely Manage API Keys**:
    - Store your API keys securely using Bubble's environment variables or secure storage solutions.

2. **Implement Error Handling**:
    - Add error handling logic in Bubble to manage API request failures or data issues.
    - Example error handling workflow:
      ```plaintext
      If API response status is not 200, display an error message to the user.
      Retry the API call if it fails due to transient errors.
      Log errors for further analysis.
      ```

## Model Recommendation

**Online Model Recommendation**:
- **LLaMa 70B** is recommended for its state-of-the-art reasoning and comprehensive language understanding capabilities. This model can effectively handle complex instructions and generate detailed outputs.

## Additional Considerations

1. **Performance Optimization**:
    - Ensure efficient use of the Perplexity API by batching requests where possible.
    - Monitor usage to avoid hitting rate limits.

2. **Testing and Validation**:
    - Thoroughly test the integration in Bubble to ensure it meets your requirements.
    - Validate the accuracy and relevance of the API responses for your use case.

