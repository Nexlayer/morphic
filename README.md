<div style="margin: 20px;">
  <img src="docs/images/nexlayer_lowercase.png" alt="Nexlayer GitHub Banner">
</div>

# Morphic

This repository is a fork of [miurla/morphic](https://github.com/miurla/morphic), enhanced with Nexlayer integration via a `nexlayer.yaml` configuration file.

## Table of Contents

1. [Demo Morphic](#demo-morphic)
2. [Modifying the Morphic `nexlayer.yaml` file](#the-morphic-nexlayeryaml-file)
3. [`nexlayer.yaml` Pod Configuration Schema](#nexlayeryaml-pod-configuration-schema)

## Demo Morphic

Ready to see Morphic in action? Follow these simple steps to demo the application:
1. **Fork this repository** to create a personal copy.
2. **Run the following cURL command** in the morphic directory. This will generate a URL to view your Morphic application:
```bash
curl -X POST https://app.nexlayer.io/startUserDeployment -H "Content-type: text/x-yaml" --data-binary @nexlayer.yaml
```

**Launch Your Demo**: Once deployed, click on the provided URL to explore your Morphic application live! NOTE: The Ollama Deepseek-r1 model is provided in this demo.  To use other models, please see the `nexlayer.yaml` file.

## The Morphic `nexlayer.yaml` File

### Important Note on Images Used
The `nexlayer.yaml` file includes references to two key images from this repository: the `morphic` client image and the `morphic-searxng` image.  
- The `morphic-searxng` image packages the [`searxng-setting.yml`](https://github.com/Nexlayer/morphic/blob/main/searxng-settings.yml) file into the `searxng/searxng:2025.3.11-3fe602a46` image for cloud deployment.
- The `morphic` image includes an updated [`models.json`](https://github.com/Nexlayer/morphic/blob/main/public/config/models.json) file which allows for the deepseek-r1 1.5b model to be queried from the `katieharris/ollama:deepseek-r1` image (also included in the `nexlayer.yaml` file).

### Environment Variables
Shown below are the set environment variables for the `morphic` pod.  Some important notes:
- The `BASE_URL` variable is set to the Nexlayer provided `<% URL %>` scriptlet.  Nexlayer will replace this scriptlet with the URL of your deployed site.
- Connecting to other pods: variables such as `LOCAL_REDIS_URL`, `SEARXNG_API_URL` and `OLLAMA_BASE_URL` include connection strings to other pods in the deployment.  Here, each uses the Nexlayer `<podName>.pod` notation to set the hostname of the pod to connect to.  For example, `LOCAL_REDIS_URL` is set to `redis://redis.pod:6379` where `redis` is the name given to the pod we want to connect to.  `redis.pod` in turn provides the hostname at which we can reach the `redis` pod at.

### `nexlayer.yaml`
```yaml
vars:
  BASE_URL: <% URL %>
  # OpenAI API key retrieved here: https://platform.openai.com/api-keys
  #OPENAI_API_KEY: [YOUR_OPENAI_API_KEY]
  # Search Configuration
  #TAVILY_API_KEY: [YOUR_TAVILY_API_KEY]  # Get your API key at: https://app.tavily.com/home
  ENABLE_SAVE_CHAT_HISTORY: true
  USE_LOCAL_REDIS: true
  LOCAL_REDIS_URL: redis://redis.pod:6379
  #------------------------------------------------------------------------------
  # Additional AI Providers
  # Enable alternative AI models by configuring these providers
  #------------------------------------------------------------------------------
  # Google Generative AI
  # GOOGLE_GENERATIVE_AI_API_KEY: [YOUR_GOOGLE_GENERATIVE_AI_API_KEY]

  # Anthropic (Claude)
  # ANTHROPIC_API_KEY: [YOUR_ANTHROPIC_API_KEY]

  # Groq
  # GROQ_API_KEY: [YOUR_GROQ_API_KEY]

  # Ollama
  OLLAMA_BASE_URL: http://ollama.pod:11434

  # Azure OpenAI
  # AZURE_API_KEY:
  # AZURE_RESOURCE_NAME:

  # DeepSeek
  # DEEPSEEK_API_KEY: [YOUR_DEEPSEEK_API_KEY]

  # Fireworks
  # FIREWORKS_API_KEY: [YOUR_FIREWORKS_API_KEY]

  # xAI (Grok)
  # XAI_API_KEY: [YOUR_XAI_API_KEY]

  # OpenAI Compatible Model
  # OPENAI_COMPATIBLE_API_KEY:
  # OPENAI_COMPATIBLE_API_BASE_URL:

  #------------------------------------------------------------------------------
  # Alternative Search Providers
  # Configure different search backends (default: Tavily)
  #------------------------------------------------------------------------------
  SEARCH_API: searxng
  SEARXNG_API_URL: http://searxng.pod:8080
  SEARXNG_SECRET: "1hsfl3++1FEgQjwuDK0rTg5wRlv1bIFVRuVfnKCQ9wM="  # generate a secret key e.g. openssl rand -base64 32
  SEARXNG_PORT: 8080
  SEARXNG_BIND_ADDRESS: "0.0.0.0"
  SEARXNG_IMAGE_PROXY: true
  SEARXNG_LIMITER: false
  SEARXNG_DEFAULT_DEPTH: basic
  SEARXNG_MAX_RESULTS: 50
  SEARXNG_ENGINES: "google,bing,duckduckgo,wikipedia"
  SEARXNG_TIME_RANGE: None
  SEARXNG_SAFESEARCH: 0
```

Want more information?  View the Nexlayer template documentation [here](https://github.com/Nexlayer/templates/blob/main/README.md).

## `nexlayer.yaml` Pod Configuration Schema
| Key | Definition | Why it matters | Examples |
|-----|------------|----------------|----------|
| **name** | A unique name to identify this service. | Each little machine (pod) must work correctly for your app to run—if one machine breaks, your whole app might not work and your friends wouldn't be able to use it. | `name: morphic` |
| **image** | Specifies the Docker container image (including repository info) to deploy for that pod. | This tells Nexlayer exactly which pre-built container to use for your live app. Choosing a solid image means your app runs in a proven, ready-to-go environment for all your users. | `image: "ghcr.io/nexlayer/morphic:eb48a3d-2025-03-13"` |
| **path** | For web-facing pods, defines the external URL route where users access the service. | This sets the web address path where users access your service. A well-defined path means your website, service or API is easily found, making your app look friendly and professional on Nexlayer Cloud. | `path: "/"` or `path: "/api"` |
| **servicePorts** | Defines the ports for external access or inter-service communication. | These ports are like the doorways that let users (or other services) connect to your app. Set them correctly, and your live app will be easily accessible and reliable on the web. | `servicePorts:`<br>`- 3000` |
| **vars** | Runtime environment variables defined as direct key-value pairs. Use `<pod-name>.pod` to reference other pods or `<% URL %>` for the deployment's base URL. | These are the settings that tell your live app how to connect to databases, APIs, and more. When they're set up right, your app adapts perfectly to the cloud environment, keeping your users happy. | `vars:`<br>`  BASE_URL: <% URL %>`<br>`  ENABLE_SAVE_CHAT_HISTORY: true`<br>`  USE_LOCAL_REDIS: true`<br>`  LOCAL_REDIS_URL: redis://redis.pod:6379` |
| **volumes** | Optional persistent storage settings that ensure data isn't lost between restarts. Each volume includes a name, size, and a mountPath. | Volumes are like cloud hard drives for your app. They store important data (like database files) so that nothing is lost when your app updates or restarts, keeping your users' data safe. | `volumes:`<br>`- name: searxng-data`<br>`  size: 10Gi`<br>`  mountPath: /data` |
| **mountPath** | Within a volume configuration, specifies the internal file system location where the volume attaches. Must start with a "/". | This tells Nexlayer exactly where to plug in your volume within a running container. When set correctly, your live app can read and save data smoothly—ensuring a seamless user experience. | `mountPath: "/data"` |
