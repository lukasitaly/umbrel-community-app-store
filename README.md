## Umbrel Community App Store Template

This repository is a template to create an Umbrel Community App Store. These additional app stores allow developers to distribute applications without submitting to the [Official Umbrel App Store](https://github.com/getumbrel/umbrel-apps).

## How to use:

1. Start by clicking the "Use this template" button located above.
2. Assign an ID and name to your app store within the `umbrel-app-store.yml` file. This file specifies two important attributes:
    - `id` - Acts as a unique prefix for every app within your Community App Store. You must start your application's ID with your app store's ID. For instance, in this template, the app store ID is `sparkles`, and there's an app named `hello world`. Consequently, the app's ID should be: `sparkles-hello-world`.
    - `name` - This is the name of the Community App Store displayed in the umbrelOS UI.
3. Change the name of the `sparkles-hello-world` folder to match your app's ID. The app ID is for you to decide. For example, if your app store ID is `whistles`, and your app is named My Video Downloader, you could set its app ID to `whistles-my-video-downloader`, and rename the folder accordingly.
4. Next, enter your app's listing details in the `whistles-my-video-downloader/umbrel-app.yml`. These are displayed in the umbrelOS UI.
5. Include the necessary Docker services in `whistles-my-video-downloader/docker-compose.yml`.
6. OPTIONAL: exports.sh - A shell script to export environment variables used within `docker-compose.yml` and share with other installed apps
7. That's it! Your Community App Store, featuring your unique app, is now set up and ready to go. To use your Community App Store, you can add its GitHub url the umbrelOS user interface as shown in the following demo:

The exports.sh shell script is a simple script to export environmental variables that your docker-compose.yml can read. These environment variables are also accessible when other apps start through their docker-compose.yml files. Most applications will not require this feature.

https://user-images.githubusercontent.com/10330103/197889452-e5cd7e96-3233-4a09-b475-94b754adc7a3.mp4
## Volumes

| Variables | Description |
| --- | --- |
| `${APP_DATA_DIR}` | Represents the main application directory, equivalent to the current working directory (./). This variable is used to define where the app's persistent data will be stored. Example usage: ${APP_DATA_DIR}/foo:/foo mounts the foo directory from the app data directory to the container's /foo path. |
| `${APP_LIGHTNING_NODE_DATA_DIR}` |  The directory where data for the Lightning Network Daemon (LND) is stored. This is essential for applications that interact with the Lightning Network, allowing them to access necessary data. |
| `${APP_BITCOIN_DATA_DIR}` |  The directory where Bitcoin Core's data is stored. This is crucial for applications that require access to the Bitcoin blockchain data managed by Bitcoin Core. |

## Variables
### System Level Environment Variables
| Variables | Description |
| --- | --- |
| `$DEVICE_HOSTNAME` | The hostname of the Umbrel server device, typically a simple name like "umbrel". This is used for network identification and communication. |
| `$DEVICE_DOMAIN_NAME` | A local domain name for the Umbrel server, often in the format of a .local address (e.g., "umbrel.local"). This allows for easier access to the server within a local network. |

### Tor Proxy Environment Variables
| Variables | Description |
| --- | --- |
| `$TOR_PROXY_IP` | The local IP address of the Tor proxy. This is used by applications to route traffic through the Tor network for enhanced privacy and security. |
| `$TOR_PROXY_PORT` | The port number on which the Tor proxy is listening. This is necessary for applications to connect to the Tor network correctly. |

### App Specific Environment Variables
| Variables | Description |
| --- | --- |
| `$APP_HIDDEN_SERVICE` | The address of the Tor hidden service where your application will be accessible |
| `$APP_PASSWORD` | A unique plain text password used for authenticating users in your application. This password is displayed to users in the Umbrel UI, facilitating easy access. |
| `$APP_SEED` | A unique 256-bit hexadecimal string (128 bits of entropy) that is deterministically derived from the user's Umbrel seed and the app's ID. This seed can be used for cryptographic purposes or to generate unique identifiers within the app. |


## App Manifest YAML

| Variables | Description |
| --- | --- |
| `manifestVersion` | There are currently two manifest versions: `1` and `1.1`. Version `1` is the basic version and is sufficient for most apps. However, if your app requires the use of hooks (scripts that are run at different stages of the app lifecycle), you need to use version `1.1`. Hooks allow you to perform custom actions at different stages of the app's lifecycle, such as before the app starts (pre-start), after the app installs (post-install), and more. If your app doesn't need to use hooks, you can stick with manifest version `1`. |
| `id` | A unique identifier for the application, typically formatted as app-id-application-name (e.g., sparkles-hello-world). This ID must match the one defined in the umbrel-app-store.yml file to ensure proper recognition within the app store. |
| `category` | The category under which the application will be listed in the Umbrel app store (e.g., finance, media, social). This helps users find the app based on their interests. |
| `name` | 	The official name of the application as it will appear in the app store (e.g., Hello World). This should be concise and descriptive. |
| `version` | The current version of the application, following semantic versioning conventions (e.g., "3.3.0"). This helps users identify updates and changes in the app. |
| `tagline` | 	A brief, catchy phrase that summarizes the essence of the application (e.g., Simple hello-world application). This tagline should entice users and provide a quick understanding of the app's purpose. |
| `description` | A detailed description of the application, outlining its features, functionalities, and benefits. This section should provide potential users with a comprehensive understanding of what the app does and why they should use it. |
| `releaseNotes` | Notes detailing the changes, improvements, and fixes made in the latest release of the application. This section informs users about new features and updates, enhancing transparency and user experience. |
| `developer` | The name of the individual or organization that developed the application (e.g., Umbrel). This provides credit to the creators and can help users identify the source of the app. |
| `website` | The official website for the application, where users can find more information, documentation, or support (e.g., umbrel.com). This link serves as a resource for users seeking additional details. |
| `dependencies` | A list of other app IDs that must be installed prior to installing this application. This ensures that all necessary components are available for the app to function correctly. |
| `repo` | The URL of the application's source code repository (e.g., https://github.com/getumbrel/umbrel-community-app-store). This allows users to access the code, contribute, or report issues. |
| `support` | A link to the support resources for the application, such as a GitHub issues page or community forum (e.g., https://github.com/getumbrel/umbrel-community-app-store/issues). This provides users with a way to seek help or report problems. |
| `port` | The network port on which the application will run. |
| `gallery` | A list of image filenames that will be displayed in the app store to showcase the application visually. These images should highlight key features or the user interface of the app. |
| `path` | The file path where the application is located within the Umbrel system. This is typically left empty unless a specific path is required for the app's operation. |
| `defaultUsername` | The default username for accessing the application, if predefined. This can help users get started quickly without needing to create an account. |
| `defaultPassword` | The default password for accessing the application, if predefined. This should be communicated clearly to users to ensure they can log in successfully.  |
| `submitter` | The name of the individual or organization that submitted the app to the Umbrel app store (e.g., Umbrel). This provides context about who is responsible for the app's inclusion. |
| `submission` | A link to the submission request or pull request for the application (e.g., https://github.com/getumbrel/umbrel/pull/334). This allows users to view the development process and any discussions related to the app's submission. |

## Header

<img width="467" alt="Screenshot_1" src="https://github.com/user-attachments/assets/80809a10-ff96-4dc4-8a12-c84b8bb19d9e">

## Gallery

<img width="976" alt="Screenshot_2" src="https://github.com/user-attachments/assets/4b5300cc-82d5-4e32-890c-02eac94331f7">

## Footer

<img width="983" alt="Screenshot_3" src="https://github.com/user-attachments/assets/a05697d4-ea3e-47e1-89f2-eac47512b807">


### An example of a manifest YAML file
```yaml
manifestVersion: 1
id: btc-rpc-explorer
category: finance
name: BTC RPC Explorer
version: "3.3.0"
tagline: Simple, database-free blockchain explorer
description: >-
  BTC RPC Explorer is a full-featured, self-hosted explorer for the
  Bitcoin blockchain. With this explorer, you can explore not just the
  blockchain database, but also explore the functional capabilities of your
  Umbrel.

  It comes with a network summary dashboard, detailed view of blocks, transactions, addresses, along with analysis tools for viewing stats on miner activity, mempool summary, with fee, size, and age breakdowns. You can also search by transaction ID, block hash/height, and addresses.

  It's time to appreciate the "fullness" of your node.
releaseNotes: >-
  Dark mode is finally here! Easily switch between your preferred mode
  in one click.

  This version also includes lots of minor styling improvements, better
  error handling, and several bugfixes.
developer: Dan Janosik
website: https://explorer.btc21.org
dependencies:
  - bitcoin
  - electrs
repo: https://github.com/janoside/btc-rpc-explorer
support: https://github.com/janoside/btc-rpc-explorer/discussions
port: 3002
gallery:
  - 1.jpg
  - 2.jpg
  - 3.jpg
path: ""
defaultUsername: ""
defaultPassword: ""
submitter: Umbrel
submission: https://github.com/getumbrel/umbrel/pull/334
```
