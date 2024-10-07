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
| `${APP_DATA_DIR}` | The app directory - the equivalent of `./` | example: `${APP_DATA_DIR}/foo:/foo` |
| `${APP_LIGHTNING_NODE_DATA_DIR}` |  LND's data directory |
| `${APP_BITCOIN_DATA_DIR}` |  Bitcoin Core's data directory |

## Variables
### System level environment variables
| Variables | Description |
| --- | --- |
| `$DEVICE_HOSTNAME` | Umbrel server device hostname (e.g. "umbrel") |
| `$DEVICE_DOMAIN_NAME` | A .local domain name for the Umbrel server (e.g. "umbrel.local") |

### Tor proxy environment variables
| Variables | Description |
| --- | --- |
| `$TOR_PROXY_IP` | Local IP of Tor proxy |
| `$TOR_PROXY_PORT` | Port of Tor proxy |

### App specific environment variables
| Variables | Description |
| --- | --- |
| `$APP_HIDDEN_SERVICE` | The address of the Tor hidden service your app will be exposed at |
| `$APP_PASSWORD` | Unique plain text password that can be used for authentication in your app, shown to the user in the Umbrel UI |
| `$APP_SEED` | Unique 256 bit long hex string (128 bits of entropy) deterministically derived from user's Umbrel seed and your app's ID |


## App manifest YAML

| Variables | Description |
| --- | --- |
| `manifestVersion` | There are currently two manifest versions: `1` and `1.1`. Version `1` is the basic version and is sufficient for most apps. However, if your app requires the use of hooks (scripts that are run at different stages of the app lifecycle), you need to use version `1.1`. Hooks allow you to perform custom actions at different stages of the app's lifecycle, such as before the app starts (pre-start), after the app installs (post-install), and more. If your app doesn't need to use hooks, you can stick with manifest version `1`. |
| `id` | `sparkles-hello-world` - This is the id defined in the `umbrel-app-store.yml` file + the application name |
| `category` | The app-store category in which the application should be displayed in (e.g. finance) |
| `name` | The name of the application (e.g. Hello World) |
| `version` | The version of the application (e.g. "3.3.0") |
| `tagline` | The tagline of the application (e.g. Simple hello-world application) |
| `description` | Description of the application |
| `releaseNotes` | The release notes of the last release |
| `developer` | The developer of the application (e.g. Umbrel) |
| `website` | The website of the application (e.g. umbrel.com) |
| `dependencies` | The dependencies section is a list of app IDs that must be already installed in order for the user to install the application and also function. |
| `repo` | The repository of the application (e.g. https://github.com/getumbrel/umbrel-community-app-store) |
| `support` | Link to where you can get support for the application (e.g. https://github.com/getumbrel/umbrel-community-app-store/issues) |
| `port` | The port of the application |
| `gallery` | The images that are going to be displayed in the app store |
| `path` | The path of the application |
| `defaultUsername` | If predefined by the application, the default username can be passed through |
| `defaultPassword` | If predefined by the application, the default password can be passed through  |
| `submitter` | The person who submitted the app (e.g. Umbrel) |
| `submission` | The link to the submission (e.g. https://github.com/getumbrel/umbrel/pull/334) |

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
