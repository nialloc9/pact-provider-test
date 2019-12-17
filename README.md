# pact-provider

<p align="center">
  <img src="/logo.png" width="700" title="Pact provider logo">
</p>

An abstraction over pact.io's provider tests to hide away any complexities with integrating pact into your pipeline. 

To help with the buy in from other teams and to get them to integrate contract testing it is important to make it as easy as possible. To do this I have created a reusable abstraction over the provider tests to allow data sources to run just 1 function inside their pipeline to run against our consumer contracts in the broker. 

This function can be published as an npm package and ran inside their pipeline making it easy to to integrate. Also this allows us to update the contract versions without having the data source update their code. Instead we can just ask them to update their version of the package (or have them always install latest).

    // my-pact-provider-tests.js
    const { onRunPactTests } = require("@nialloc9/pact-provider");

    onRunPactTests();

## Usage

    $ PACT_BROKER_CONTRACT_NAME=NameOfContract PACT_BROKER_TOKEN=OdvzZqCuWQEHa8zVJsmmJg PACT_BROKER_URL=https://MY_BROKER.pact.dius.com.au/ mocha -t 10000 my-pact-provider-tests.js

The global variables are required.

### Config

A config object can also be passed to the pact tests.

    // my-pact-provider-tests.js
    const { onRunPactTests } = require("@nialloc9/pact-provider");
    
    const config = {};

    onRunPactTests(config);

<details><summary>Config Options</summary>

| Parameter                   | Required | Type             | Description                                                                                                                                                                                                                                      |
| --------------------------- | :------: | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `applicationUrl`           |   false   | string           | Running API provider host endpoint.                                                                                                                                                                                                    |
| `contractName`                  |   false   | string           | Name of the provider contract. Overrides global variable PACT_BROKER_CONTRACT_NAME.                 
| `pactBrokerUrl`             |  false   | string           | URL of the Pact Broker to retrieve pacts from. Required if not using pactUrls.                                                                                                                                                                   |
| `contractTags`                      |  false   | array of strings | Array of tags, used to filter pacts from the Broker.                                                                                                                               |
| `pactBrokerToken`           |  false   | string           | Bearer token for Pact Broker authentication. If using Pactflow, you likely need this option.                                                                                                                                                     |
| `publishVerificationResult` |  false   | boolean          | Publish verification result to Broker                                                                                                                                                                                                            | boolean |
| `contractVersion`           |  false   | string           | Provider version, required to publish verification results to a broker         

</details>


