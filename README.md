<div align="center">
  <h1>ibc-go</h1>
</div>

![banner](docs/static/img/IBC-go-cover.svg)

<div align="center">
  <a href="https://github.com/cosmos/ibc-go/releases/latest">
    <img alt="Version" src="https://img.shields.io/github/tag/cosmos/ibc-go.svg" />
  </a>
  <a href="https://github.com/cosmos/ibc-go/blob/main/LICENSE">
    <img alt="License: Apache-2.0" src="https://img.shields.io/github/license/cosmos/ibc-go.svg" />
  </a>
  <a href="https://pkg.go.dev/github.com/cosmos/ibc-go?tab=doc">
    <img alt="GoDoc" src="https://godoc.org/github.com/cosmos/ibc-go?status.svg" />
  </a>
  <a href="https://goreportcard.com/report/github.com/cosmos/ibc-go">
    <img alt="Go report card" src="https://goreportcard.com/badge/github.com/cosmos/ibc-go" />
  </a>
  <a href="https://sonarcloud.io/summary/overall?id=cosmos_ibc-go">
    <img alt="Code Coverage" src="https://sonarcloud.io/api/project_badges/measure?project=cosmos_ibc-go&metric=coverage" />
  </a>
</div>

The [Inter-Blockchain Communication protocol (IBC)](https://ibcprotocol.dev/) allows blockchains to talk to each other. This end-to-end, connection-oriented, stateful protocol provides reliable, ordered, and authenticated communication between heterogeneous blockchains. For a high-level explanation of what IBC is and how it works, please read [this blog post](https://medium.com/the-interchain-foundation/eli5-what-is-ibc-def44d7b5b4c).

This IBC implementation in Golang is built as a Cosmos SDK module. To understand more about how to use the `ibc-go` module as well as about the IBC protocol, please check out the Interchain Developer Academy [section on IBC](https://tutorials.cosmos.network/academy/3-ibc/), or [our docs](./docs/docs/01-ibc/01-overview.md).

## Light Clients

### ICS 14 Avalanche Light Client Integration

The Avalanche light-client is not part of the canonical IBC-go repository and must be implemented separately. Below are tailored instructions for versions below and above v0.50. Please ensure you follow these specific steps to correctly integrate the Avalanche light-client into your Cosmos SDK application.

#### Lower than v0.50
**Integrating the Avalanche Light-Client Module in Your Cosmos SDK Application**

Enhance your Cosmos SDK application by integrating the `light-clients/14-avalanche` module. Follow this step-by-step guide to easily import and register the Avalanche light-client in your project.

1. **Import the Avalanche Light-Client Module**
   
   First, ensure you import the Avalanche (`ava`) module into your Cosmos SDK application. Typically, this is done in the `app.go` file, where your application's modules are defined:
   ```go
   import (
     // other imports...
     ava "github.com/cosmos/ibc-go/v8/modules/light-clients/14-avalanche"
   )
   ```

2. **Register the Avalanche Module in the Module Manager**
   
   Next, add the `ava` module to your application’s `ModuleManager`. Locate the section where you initialize the `ModuleManager` and include the Avalanche light-client:
   ```go
   app.ModuleManager = module.NewManager(
     // other modules...
     ava.AppModuleBasic{},
   )
   ```

By following these steps, you'll successfully integrate the Avalanche light-client module into your Cosmos SDK application, enabling enhanced interoperability with Avalanche-based chains.

#### Higher than v0.50
**Integrating the Avalanche Light-Client Module in Your Cosmos SDK Application**

Enhance your Cosmos SDK application by integrating the `light-clients/14-avalanche` module. Follow this step-by-step guide to easily import and register the Avalanche light-client in your project.

1. **Import the Avalanche Light-Client Module**

   First, ensure you import the Avalanche (`ava`) module into your Cosmos SDK application. Typically, this is done in the `ibc.go` file, where your application's modules are defined:
   ```go
   import (
     // other imports...
     ava "github.com/cosmos/ibc-go/v8/modules/light-clients/14-avalanche"
   )
   ```

2. **Register the Avalanche Module in the Module Manager**

   Add the `ava` module to your application’s `ModuleManager`. Locate the section where you initialize the `ModuleManager` and include the Avalanche light-client:
   ```go
   app.ModuleManager = module.NewManager(
     // other modules...
     ava.AppModuleBasic{},
   )
   ```

3. **Add the Module to the RegisterIBC Function**

   Finally, register the Avalanche module in the `RegisterIBC` function of your application. This function is typically found in the `ibc.go` file:
   ```go
   func RegisterIBC(registry cdctypes.InterfaceRegistry) map[string]appmodule.AppModule {
       modules := map[string]appmodule.AppModule{
           // other modules...
           ava.ModuleName: ava.AppModuleBasic{},
       }
       ...
   }
   ```

By following these steps, you'll successfully integrate the Avalanche light-client module into your Cosmos SDK application, enabling enhanced interoperability with Avalanche-based chains.

---

For the complete list of light clients, refer to the following:

- [ICS 07 Tendermint](https://github.com/cosmos/ibc-go/tree/main/modules/light-clients/07-tendermint)
- [ICS 06 Solo Machine](https://github.com/cosmos/ibc-go/tree/main/modules/light-clients/06-solomachine)
- [ICS 09 Localhost](https://github.com/cosmos/ibc-go/tree/main/modules/light-clients/09-localhost)
- [ICS 14 Avalanche](https://github.com/cosmos/ibc-go/tree/main/modules/light-clients/14-avalanche)

---

### Official Landslide Documentation

For more detailed information on the Landslide network, refer to the [Landslide Docs](https://docs.landslide.network/).

---

## Ecosystem
Discover more applications and middleware in the [cosmos/ibc-apps repository](https://github.com/cosmos/ibc-apps#-bonus-content).

## Community
We have active, helpful communities on Discord and Telegram.

For questions and support, please use the `developers` channel in the [Cosmos Network Discord server](https://discord.com/channels/669268347736686612/1019978171367559208) or join the [Interchain Discord server](https://discord.com/invite/interchain). The issue list of this repo is exclusively for bug reports and feature requests.

To receive announcements of new releases or other technical updates, please join the [Telegram group that we administer](https://t.me/ibc_is_expansive).

We run biweekly community calls to update the community with our current direction and gather feedback on what to work on next. The community calls are also a platform for you to update everyone else with what you're working on, ask questions, and find opportunities to collaborate. Please join [this Google group](https://groups.google.com/g/ibc-community) to receive a calendar invitation for the meeting.

## Contributing
If you're interested in contributing to ibc-go, please take a look at the [contributing guidelines](./CONTRIBUTING.md). We welcome and appreciate community contributions!

This project adheres to ibc-go's [code of conduct](./CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

To help contributors understand which issues are good to pick up, we have the following two categories:

- Issues with the label [`good first issue`](https://github.com/cosmos/ibc-go/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) should be pretty well defined and are best suited for developers new to ibc-go.
- Issues with the label [`help wanted`](https://github.com/cosmos/ibc-go/issues?q=is%3Aopen+is%3Aissue+label%3A%22help+wanted%22) are a bit more involved and they usually require some familiarity already with the codebase.

If you are interested in working on an issue, please comment on it; then we will be able to assign it to you. We will be happy to answer any questions you may have and help you out while you work on the issue.

## Security
To report a security vulnerability, see our [Coordinated Vulnerability Disclosure Policy](./SECURITY.md).

## Audits
The following audits have been performed on the `ibc-go` source code:

- [ICS20 Fungible Token Transfer](https://github.com/informalsystems/audits/tree/dc8b503727adcbb8e29c3d3a25a9070e0bf1ec87/IBC-GO) by Informal Systems.
- [ICS20 Fungible Token Transfer V2](https://github.com/cosmos/ibc-go/blob/main/docs/audits/20-token-transfer/Atredis%20Partners%20-%20Interchain%20ICS20%20v2%20New%20Features%20Assessment%20-%20Report%20v1.0.pdf) by Atredis Partners.
- ICS27 Interchain Accounts by [Trail of Bits](https://github.com/cosmos/ibc-go/blob/main/docs/audits/27-interchain-accounts/Trail%20of%20Bits%20audit%20-%20Final%20Report.pdf) and [Informal Systems](https://github.com/cosmos/ibc-go/issues/631).
- [ICS08 Wasm Clients](https://github.com/cosmos/ibc-go/blob/main/docs/audits/08-wasm/Ethan%20Frey%20-%20Wasm%20Client%20Review.pdf) by Ethan Frey/Confio.
- [ICS04 Channel upgradability](https://github.com/cosmos/ibc-go/blob/main/docs/audits/04-channel-upgrades/Atredis%20Partners%20-%20Interchain%20Foundation%20IBC-Go%20Channel%20Upgrade%20Feature%20Assessment%20-%20Report%20v1.1.pdf) by Atredis Partners.

---
