---
nav_title: Overview
title: Impart Security
---

Impart's API Protection and WAF platform delivers comprehensive protection for APIs, microservices, and serverless applications in cloud-native environments.

Use the Impart plugin to:
* Discover and catalog your API and web application Attack Surface.
* Protect your APIs and web applications from injection, enumeration, automated threats, and other attacks.
* Find and help you fix your API and web application vulnerabilities and misconfigurations with built in API testing.
* Reduce your API and web application risk profile.


## How it works

The Impart Kong plugin allows Impart to inspect your HTTP traffic within your own environment to detect threats, anomalies, and other interesting insights. These insights are used to protect your APIs in real time through an integration with Kong that introduces minimal additional latency, fails open to ensure reliability, and keeps sensitive data within your own environment to protect your privacy.


## How to install

Custom plugins can be installed via LuaRocks. A Lua plugin is distributed in `.rock` format, which is
a self-contained package that can be installed locally or from a remote server.

If you used one of the official {{site.base_gateway}} installation packages, the LuaRocks utility
should already be installed in your system.
Install the `.rock` in your LuaRocks tree, that is, the directory in which LuaRocks
installs Lua modules.

1. Install the Impart plugin:

    ```sh
    luarocks install kong-plugin-impart
    ```

2. Update your loaded plugins list in {{site.base_gateway}}.

    In your `kong.conf`, append `impart` to the `plugins` field. Make sure the field is not commented out.

    ```yaml
    plugins = bundled,impart                # Comma-separated list of plugins this node
                                            # should load. By default, only plugins
                                            # bundled in official distributions are
                                            # loaded via the `bundled` keyword.
    ```

3. Restart {{site.base_gateway}}:

    ```sh
    kong restart
    ```

## Using the plugin

This plugin requires having installed an Impart Inspector. Navigate to the Impart console for step-by-step [instructions](https://console.impartsecurity.net/orgs/_/integrations?q=kong).

### {{site.base_gateway}}

If you already configured an API, execute the command below after replacing `<YOUR_API>` with the name of your API and `<inspector_rpc_addr>` if different than the default.

```shell
curl -i -X POST http://localhost:8001/services/<YOUR_API>/plugins \
     -F "name=impart" \
     -F "config.inspector_rpc_addr=<inspector_rpc_addr>"
```

### {{site.konnect_product_name}}

If you are a {{site.konnect_short_name}} administrator, install the Impart plugin as a [custom plugin](/konnect/gateway-manager/plugins/add-custom-plugin/).

If the plugin has already been installed by an administrator, you can enable it through {{site.konnect_short_name}}:
1. Depending on where you want to enable Impart, select **Plugins**.
2. Click on **+ New Plugin**
3. On **Custom Plugins**, select **Kong Plugin Impart**.
4. Fill in the **`Inspector Rpc Addr`** field.
5. Click **Save**.

For further information, please check our [Impart Kong documentation page](https://docs.impartsecurity.net/docs/Quickstart/Integrations/Kong_lua).
