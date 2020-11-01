# Cere Decentralized Data Cloud (DDC) Service
## Project Description

Cere Decentralized Data Cloud is a blockchain-based storage solution that is optimized for capturing user/app interactions which are individually signed and encrypted, along with potential value transfers, to be stored in a tamper-proof and time-capsuled data scheme. This allows for the direct and secure decryption, validation, extraction, transformation, and utilization of such data by trusted or trustless parties, automated processes, and decentralized data marketplaces. 

DDC data operations are configured to work directly with Cere test/main networks or with any other Polkadot/Substrate blockchain network.

## Use Case Examples

### Optimizing For Automated AI/Data-Driven Consumer Interactions

Cere DCC’s captures and stores individually encrypted customer interaction data, along with value transactions to each user’s individual ledger and individual tamper-proof and time-capsuled data structures in IPFS clusters. This allows for AI/data-driven smart engagements and interaction to be automated by third-party vendors and partners. This fits into the critical needs of today’s consumer enterprises to digitize, automate, and become data-driven to strengthen their first-party data strategies.

Cere allows for:
* Capturing and storing all signed and validated user interaction events into a tamper-proof “customer journey” timeline, providing a source of truth of first-party data in raw form utilizing blockchain identity abstraction, data encryption, and time-capsuled consensus verifications. 
* Highly customized and granular extraction of user datasets upstream into virtual dataset such as indexes (ElasticSearch, SQL, AWS Athena, etc.), ETL’ing (Spark, Hadoop, Kafka Streams, etc.), which can then be directly and dynamically accessed by data services or used by existing product/services.
* Granular third-party access via permission keys such that AI, machine learning, and business intelligence processes can perform federated querying, modeling, and direct computations. Cere supports both federated access or data re-encryption use cases.
* Businesses, apps, partners, and even individual consumers can be permissioned to inspect a complete timeline of interactions for any user via apps and tools using Cere’s embedded wallet.
* Capturing key user events and interactions such as agreeing to terms or signing verifications along with the relevant material to be both on chain and within the DCC.

### Open Data Marketplace 

Cere follows the trend of Snowflake and its data marketplace which is gaining adoption and delivering value for businesses that are integrated into its proprietary ecosystem. Cere enhances this principle using an open and decentralized version of such a data marketplace, which is not locked into a single entity/vendor, but is fully open and interoperable, and powered by smart contracts designed to work within both Cere and Polkadot/Substrate chains.

Although the data marketplace itself is not part of this specific proposal, the following use cases work with DCC
* Unlocking the next level of efficiency through  data security/agility/interoperability to open up direct access of business datasets that are typically locked in by layers of SaaS agreements and inaccessible to the wider developers and data scientists communities.
* Business can use specific DDC tools to granularly (down to specific fields/attributes) decrypt, enrich, filter, and further anonymize data., This way, data is prepared for processing by  data experts who can sample/validate the data via staking CERE tokens and associated workflows.
* Smart contracts powering the marketplace works directly with the DDC to capture the granular steps of the workflow in terms of access and execution using Chainlink oracles for mapping to verifiable external processing. 
* Since every piece of consumer data is anonymized and multi-key encrypted with user and business keys during the onboarding into DCC, Cere marketplaces provide additional security and privacy measures such as federated data sampling/modeling/learning and differential privacy to facilitate secure remote computing/collaborations.
 
### NFT’s and Provenance

Cere Network will be supporting NFT’s (non-fungible tokens) that can represent unique or fractionalized ownership of real-world or digital assets for business and applications. The DDC offers a set of plug-and-play utilities that can be extended to any Substrate network as well. Key utility being:
* Capturing the critical event data relating to the issuance, transfers, and access of such tokens, ensuring that the state changes of the NFT are captured both on-chain and in the  DDC, both going through network consensus at the same time. This allows for fully automated verifications and value-transfer via smart contracts and workflow software to capture much more information and utility.

## Packages

### DDC Public Packages

```
├── Cere DDC SDK (toolset for interacting with Cere DDC)
    ├── Connectors and Tools to directly interact with Cere DDC
    ├── Info on how to extend this project or use with alternative data services
    ├── Cere Encryption API (encryption/decryption contracts)
    │   └── Data Encryption Module (Base Encryption API implementation)
    ├── DDC utility tools
    ├── Data and blocks viewer (public web service)
    ├── Examples and utilities
```

### Cere DDC Services

```
├── Cere Data Cloud
    ├── Cere CLS Service (content lookup service)
    ├── Cere Storage Service (write/read into/from IPFS, traverse data)
    └── Cere Blockchain Service (write/read into/from Cere Test/Mainnet)
```

### External Packages

```
├── Cere Embedded Wallet (user onboarding, sending events)
    └── Cere Custodial Service (user identity)
```

### Cere DDC operations

1. Sign user/app operation, store associated user-signed first-party unstructured data (_Cere DDC SDK_)
    * Associate wallet with associated IPFS data cluster(s), using Cere Testnet by default (_Cere CLS Service_)
    * Encrypt data (_Cere Encryption Module_)
    * Store data as individually signed & encrypted (_Cere Storage Service_)
    * Execute smart contract on the Cere Mainnet (_Cere Blockchain Service_)
        * pay data operation fees via CERE tokens
2. Extract data
    * Per user
        * Find the IPFS cluster with user data (_Cere CLS Service_)
        * Traverse data tree (_Cere Storage Service_)
        * Decrypt data (_Cere Encryption Module_)
    * Per application
        * Traverse user wallets of the application (_Cere CLS Service_)
        * Apply per user flow
3. Show data
    * Locate user data in clusters (_Cere CLS Service_)
    * Traverse IPFS data tree (_IPFS Service_)
    * Decrypt data (_Cere Encryption Module_)
    * Extract and display data (e.g can use the _Data Viewer tool packaged_)
4. Remove data
    * Tag for removing
    * Invalidate previous records

### Data Encryption module

This package provides the ready-to-use functionalities for encrypting and decrypting use data to/from Cere DDC. The default/standard user format represents meaningful user interaction events that have scopes of data and each scope is encrypted or decrypted with a separate key. It allows granular data sharing with third parties by providing them keys for specific scopes.

Encryption flow:
1. Split event data into scopes.
2. Encrypt each scope of data with its own key.
3. Merge encrypted scopes into one object.
4. Add event metadata (account public key, signature, event ID, timestamp).

Decryption flow:
1. Read event metadata, extract scopes, and read keys from the configuration.
2. Decrypt scoped data.
3. Merge decrypted data into one object.

Encryption and decryption operations here are explicitly and purposefully designed for raw user interaction data (e.g. JSON blobs). This package contains a high-level abstraction as well as a standard implementation using [Blake2](https://blake2.net/) for derivative keys and [XChaCha20-Poly1305](https://libsodium.gitbook.io/doc/secret-key_cryptography/aead/chacha20-poly1305/xchacha20-poly1305_construction) for granular data encryption.in the Cere Platform. It’s also possible to implement your own data encryption module with different techniques 

Cere provides Encryption Module API implementation as a service with internal validation so that data can be sent in a raw format with SDK. This service can be also used as a stand-alone service for encryption/decryption utilities.

### Data Utility and Testing Tools

* Dynamically indexing data upstream into schema registry (Based on Apache Avro). 
* This registry is designed to describe data that can be extracted upstream from DDC into other purposeful storages. . We have currently implemented some, other connectors are coming soon:
    * ElasticSearch
    * AWS Athena
    * Kafka
* ETL data with Spark, Hadoop ML, or Kafka Streams.
* Piping data for ML pipelines:
    * Spark ML
    * AWS SageMaker
    * Azure ML
    * Google TensorFlow
* Validate that all user sessions were signed and went through consensus.
* IPFS tools for reading and traversing a user's journey.

## Additional Project Details

* Who does this project help?
    * Application developers who are working with Cere or any other Substrate blockchain networks.
* How do they use it?
    * App developers can seamlessly connect to Cere DDC using either any Substrate non-custodial wallet or a custodial one such as Cere Identity SDK( [link]compatible with Substrate)
    * Developers can use pre-built Cere packages contained inside this project or building their own libraries to align with the OpenAPI specifications.
    * Cere packages are building blocks for custom applications. We provide abstractions and core implementations to enable encryption and signing functions, API communication, and IPFS data storage.
    * Seamlessly connect to DCC with (1) Cere wallet/network combo; or 2) support any Substrate network);
* How does DDC work with which blockchain network 
    * Developers can configure wallets to use them with Cere Network (main or test net) or any other Substrate network that is connected to DDC. Cere services and CLS (Content Location Service, similar to a DHT) can be dynamically used with any blockchain network. Besides that, Cere services provide call back functions to developers for more granular interaction with the data pipeline.
    * E.g. app/wallet can specify which Cere network (main/test or any private network part of Cere hub, and also how to add support for any other Substrate/Polkadot network), then  CLS and integrated blockchain services calls can directly work with that.
* How can I quickly try out and test the basic operations of this project?
    * Simple sandbox webpage with debug console with output from our services will be provided
    * Both runtime images and packaging tools(e.g. Docker compose files) with examples of data extraction/decryption/indexing test templates will be provided, as well as examples on how an app can use DDC data storage w/Cere testnet (or any other Substrate network)
    * Tools for viewing the transaction and data (on chain and on IPFS cluster)

## Ecosystem Fit
We aim to not only make the Cere DCC plug-and-play for enterprise partners integrating with Cere Network, but we are also making it accessible for all solutions that are being built on top of any Substate/Polkadot Network. 

## Team

### Team members TODO
* Name of team leader
* Names of team members

### Team Website
* https://cere.network

### Legal Structure TODO
Please provide the name and registered address of the legal entity executing the project. When applying via the General Grants program, these details can also be shared privately via the Google Form used for your application.

### Team's experience TODO
Please describe the team's relevant experience. If the project involves development work, then we'd appreciated if you can single out a few interesting code commits made by team members on their past projects. For research-related grants, references to past publications and projects in a related domain are helpful.

### Team Code Repos

* [https://github.com/Cerebellum-Network](https://github.com/Cerebellum-Network)
    * [Cere Identity/Custody SDK](https://github.com/Cerebellum-Network/Cere-Identity-Custody-SDK)
    * [Cere DDC SDK](https://github.com/Cerebellum-Network/Cere-DDC-SDK)
    * [Cere DCC API Interface](https://github.com/Cerebellum-Network/data-cloud-api)
    * [Cere Data Encryption Service API](https://github.com/Cerebellum-Network/crypto-service-api)
    * [Data Viewer](https://github.com/Cerebellum-Network/data-viewer)
    * [Data Cloud Examples](https://github.com/Cerebellum-Network/data-cloud-examples)

### Team LinkedIn Profiles TODO
* https://www.linkedin.com/<person_1>
* https://www.linkedin.com/<person_2>

## Development Roadmap

### Overview TODO
* Total Estimated Duration: Duration of the whole project
* Full-time equivalent (FTE): Workload of an employed person ([see](https://en.wikipedia.org/wiki/Full-time_equivalent))
* Total Costs: Amount of Payment for the whole project. The total amount of funding needs to be below $100k.

### Milestone 1 — Prepare and launch core modules and services

* Estimated Duration: 1 month
* FTE: 2.5
* Costs: $40,000

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
|0a.|License|MIT|
|0b.|Documentation and Packaging|We will add a clear structure of repositories with instructions for how to package, deploy, test, and extend the services in this project.|
|0c.|Testing Guide|The code will have a proper unit and integration test coverage to ensure functionality and robustness. In the guide, we will describe how to run these tests.|
|1.|Cere DDC API|We will create a service interface for interaction with Cere DDC and Cere Testnet, provide OpenAPI specification and Swagger UI for testing.|
|2.|Network Integrations|Integrate with Cere mainnet/testnet/subnets and validating of key utility use cases.|
|3.|Cere DDC SDK|We will create and package the DDC SDK for interacting with Cere DDC.|
|4.|Examples|We will create a repository with examples of usage of Cere DDC API.|
|5.|Binaries and Packaging tools|We will provide both Docker binaries and docker-compose files with configurable services for testing.|

### Milestone 2 — IPFS CLS/Data Service Integrations

* Estimated Duration: 1 month
* FTE: 2.5
* Costs: $40,000

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
|1.|API specification|We will create a specification for Cere CLS/Data Service API for internal use and external connections.|
|2.|Client Tools/Data structures|We will create the client-side SDK algorithms and data structure that will support traversing, search and delete operations to be used by client-side tools to interact with.|
|3.|Implementation|We will implement the main CLS and Data Service APIs.|

### Milestone 3 — Full End-to-End Testing w/ Utility Tools

* Estimated Duration: 1 month
* FTE: 2
* Costs: $30,000

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
|1.|Data Viewer and Block Viewer|We will create a public web-based tool and associated API for exploring stored data alongside blockchain transaction.|
|2.|Support of other Substrate Networks|We can first test internally [with Cere turnkey substrate network], then externally with other Polkadot ecosystem partners.|
|3.|Testing|Package and include fully functional end-to-end functional and load testing tools|

### Community engagement

We will be producing a series of articles/tutorials and publish them on Medium and our community channels to highlight each milestone.

### Future Plans

1. More data services (connectors) that can auto attach to data sets, can perform some logic, and then move data in/out.
2. ML/AI models and pipelines.
3. Ability to remove user’s data by request.

### Additional Information TODO

Any additional information that you think is relevant to this application that hasn't already been included.

Possible additional information to include:

* What work has been done so far?
* Are there are any teams who have already contributed (financially) to the project?
* Have you applied for other grants so far?
