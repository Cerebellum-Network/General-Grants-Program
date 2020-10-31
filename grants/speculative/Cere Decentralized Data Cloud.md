# Cere Decentralized Data Cloud

## Project Description

Cere Decentralized Data Cloud is a blockchain based storage solution that is optimized for capturing user/app 
interactions which are individually signed and encrypted, along with potential value transfers, to be stored 
in a tamper-proof and time-capsuled data scheme. This allows for the direct and secure decryption, validation, 
extraction, transformation, and utilization of such data by trusted or trustless parties, or automated processes, 
or decentralized data marketplaces.

## Use Case Examples

### Optimizing For Automated AI/ML Driven Consumer Interactions

Only with Cere DCC’s individually encrypted, tamper-proof (and time capsuled) way of capturing customer interactions 
data, and storing it along with value transactions on to each user’s individual ledger, can AI/data driven smart 
engagements or interactions be automated by 3rd party vendors and partners. This fits into the critical needs 
for today’s consumer enterprises to digitize, automate, and become data-driven.

* Capturing and storing all signed and validated user interaction events into a tamper-proof timeline of 
“customer journey”, providing a source of truth of 1st party data in raw form. Utilizing blockchain identity 
abstraction, data encryption, and time-capsuled consensus verifications. 
* Allowing for highly customized and granular extraction of user(s) datasets upstream into virtual dataset such 
as indexes (ElasticSearch, SQL, AWS Athena, etc.), ETL’ing (Spark, Hadoop, Kafka Streams, etc.), which can then be 
directly and dynamically accessed by data services or used by existing product/services.
* Allowing for granular 3rd party access via permission keys such that AI, Machine Learning, and business intelligence 
processes can perform federated querying, modeling, and direct computations. Federated access or data re-encryption use 
cases can both be supported.
* Businesses/Apps/Partners and even individual consumers can be permissioned to inspect a complete timeline of 
interactions for any user(s) via apps and tool using Cere embedded wallet.
* Capturing key user events and interactions such as agreeing to terms or signing verifications along with the relevant 
material to be both on chain and within DCC.

### Open Data Marketplace (not part of this proposal, but relevant cases)

As Snowflake and its data marketplace are gaining adoption and delivering value for businesses that are integrated into 
its proprietary ecosystem, an open and decentralized version of such data marketplace which is not locked into a single 
entity/vendor, but is fully open and interoperable, and powered by smart contracts designed to work within both Cere and 
Polkadot/Substrate chains.

Although the data marketplace itself is not part of this specific proposal, the following use cases work with DCC

* Next level of efficiency, data security/agility/interoperability to open up direct access of business datasets that 
are typically locked in by layers of SaaS agreements and simply inaccessible to the wider developers and data scientists 
communities.
* Business can use specific DDC tools to granularly (down to specific fields/attributes) decrypt, enrich, filter, and 
further anonymized, and prepared for processing by the data expert who can sample/validate the data via staking CERE 
tokens and associated workflows..
* Smart contracts powering the marketplace works directly with DDC to capture the granular steps of the workflow in 
terms of access and execution, as well as chainlink oracles mapping to verifiable external processing. 
* Every pieces of consumer data is already anonymized and multi-key encrypted with user and business keys during the 
onboarding into DCC, Makreplace provides additional security and privacy measures such as federated data 
sampling/modeling/learning and differential privacy to facilitate secure remote computing/collaborations.

### NFT’s and Provenance
As Cere Network will be supporting NFT tokens, or non-fungible tokens that can represent unique or fractionalized 
ownership of real-world or digital assets for business and application, DDC offers a set of plug-and-play utility that 
can be extended to any Substrate network:

* Capture the critical event data relating to the issuance, transfers, and access of such tokens, ensuring that the 
state changes of the NFT are captured both on chain and also into DDC, going through network consensus at the same time:
    * TODO

## Project Details

* Who does this help?
    * Application developers who are working with Cere or Substrate networks.
* How do they use it?
    * Developers can seamlessly connect to Cere DDC using either Substrate wallet or Cere wallet (which is compatible 
    with Substrate)
    * Developers can use pre-built Cere packages like SDK and API clients. Or they can use Cere OpenAPI specifications 
    to build their own libraries.
    * Cere packages are building blocks for custom applications. We provide abstractions and implementations for encryption 
    and signing functions, API communication and working with IPFS data.
* How does DDC work with which network?
    * Developers can configure wallets to use them with Cere Network (main or test net) or any other Substrate network 
    that is connected to DDC. Cere services and DHT can be dynamically connected to any network. Besides that, Cere 
    services provide call back functions to developers for more granular interaction with data pipeline.
 
### Packages

#### High Level

* **Cere SDK** - user onboarding, sending events; public API with open sourced implementations for JavaScript, iOS and Android.
* **Cere DDC API** - public API for connecting Cere SDK/Substrate wallets.
* **Encryption Service** - encrypt/decrypt data, part of the Cere SaaS with public API.

#### Cere SaaS Services

* **IPFS DHT Service** - associate/lookup wallets in IPFS clusters, part of the Cere SaaS.
* **IPFS Service** - write/read into/from IPFS, traverse data, part of the Cere SaaS.
* **Cere Blockchain Service** - write/read into/from Cere Network, part of the Cere SaaS.

#### Standalone

* **Data Viewer** - public web service where everyone who has private key can look at the decrypted data.
* **Examples** - ready to work solutions/embeddable services for data interaction (working with IPFS, building data pipelines, crypto functions, validation, etc.).

#### Hierarchy and Interactions

* Cere SDK
    * _calls_ Cere DDC API
        * _calls_ IPFS DHT Service
        * _calls_ IPFS Service
            * _uses_ Encryption Service
        * _calls_ Blockchain Service
            * _uses_ Encryption Service
* Data Viewer
    * _uses_ Cere DDC API
    * _uses_ Encryption Service

### Cere DDC API Operations
1. Sign user/app operation, store associated blob file (_Cere SDK_)
    * Associate wallet with an IPFS cluster, Cere Mainnet by default (_IPFS DHT Service_)
    * Encrypt data (_Encryption Service_)
    * Store data as individually signed & encrypted (_IPFS Service_)
    * Execute smart contract on the Cere Mainnet (_Cere Blockchain Service_)
        * Free/premium tiers
        * Count operations, pay fees
2. Extract data
    * Per user
        * Find IPFS cluster with user data (_IPFS DHT Service_)
        * Traverse data tree (_IPFS Service_)
        * Decrypt data (_Encryption Service_)
    * Per application
        * Traverse user wallets of the application (_IPFS DHT Service_)
        * Apply per user flow
3. Show data
    * Find IPFS cluster with user data (_IPFS DHT Service_)
    * Traverse data tree (_IPFS Service_)
    * Decrypt data (_Encryption Service_)
    * Show to user (_Data Viewer_)
4. Remove data
    * Tag for removing (_IPFS Service, IPFS DHT Service_)
    * Invalidate previous records

### Cere SDK
Package with a high-level API for sending events to the events stream. 
Contains internal functions for signing and validation. 
This is a recommended way of sending events to the DDC. 
Cere provides SDK for Javascript (can be used on the server-side NodeJS as well), 
Swift (for iOS/iPad applications), and Kotlin (for Android applications). 
As a part of SaaS, Cere provides Sandbox for SDK where developers can send events using demo accounts.

### Encryption module
This package contains high-level functions for encrypting and decrypting events. 
Every event has scopes of data and each scope is encrypted or decrypted with a separate key. 
It allows sharing only the part of the data with third parties by providing them keys for specific scopes.

Encryption flow:
1. Split event data into scopes.
2. Encrypt each scope of data with its own key.
3. Merge encrypted scopes into one object.
4. Add event metadata (account public key, signature, event ID, timestamp).

Decryption flow:
1. Read event metadata, extract scopes, and read keys from the configuration.
2. Decrypt scoped data.
3. Merge decrypted data into one object.

For the partners who are using the Cere SaaS platform, encryption and decryption operations are explicit, 
they work with raw data as an input and output. 
If anyone else wants to connect to the Cere Platform, he can use the Crypto module package 
which contains a high-level abstraction for working with cryptography in the Cere Platform.
It’s also possible to implement your own crypto module. To be compatible with Cere Crypto, 
you must use [Blake2](https://blake2.net/) function to create a derived key for the field using the master key and [XChaCha20-Poly1305](https://libsodium.gitbook.io/doc/secret-key_cryptography/aead/chacha20-poly1305/xchacha20-poly1305_construction) for encryption.

## Ecosystem Fit 
Consider this project as a Decentralized Snowflake.

## Team

### Team members TODO
* Name of team leader
* Names of team members	

### Team Website	
* https://cere.network

### Legal Structure TODO
Please provide the name and registered address of the legal entity executing the project. When applying via the General Grants program, these details can also be shared privately via the Google Form used for your application.

### Team's experience TODO
Please describe the team's relevant experience.  If the project involves development work, then we'd appreciated if you can single out a few interesting code commits made by team members on their past projects. For research-related grants, references to past publications and projects in a related domain are helpful.  

### Team Code Repos
* https://github.com/Cerebellum-Network
    * [Cere Wallet API (SDK)](https://github.com/Cerebellum-Network/cere-wallet-api)
    * [Data Cloud API](https://github.com/Cerebellum-Network/data-cloud-api)
    * [Crypto Service API](https://github.com/Cerebellum-Network/crypto-service-api)
    * [Data Viewer](https://github.com/Cerebellum-Network/data-viewer)
    * [Data Cloud Examples](https://github.com/Cerebellum-Network/data-cloud-examples)

### Team LinkedIn Profiles TODO
* https://www.linkedin.com/<person_1>
* https://www.linkedin.com/<person_2>

## Development Roadmap 

### Overview TODO
* **Total Estimated Duration:** Duration of the whole project
* **Full-time equivalent (FTE):**  Workload of an employed person ([see](https://en.wikipedia.org/wiki/Full-time_equivalent)) 
* **Total Costs:** Amount of Payment for the whole project. The total amount of funding needs to be below $100k.

### Milestone 1 — Prepare and publish open source modules
* **Estimated Duration:** 1 month
* **FTE:**  1
* **Costs:** $5,000

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT |
| 0b. | Documentation | We will provide a README files inside repositories with instructions of how to build, run and use our services. |
| 0c. | Testing Guide | The code will have proper unit and integration test coverage to ensure functionality and robustness. In the guide we will describe how to run these tests. | 
| 1. | Cere DDC API | We will create a service for interaction with a Cere DDC, provide OpenAPI specification and Swagger UI for testing. |
| 2. | Data Viewer | We will create a public web service for exploring the data. |  
| 3. | Examples | We will create a repository with examples of usage if Cere DDC API. |
| 4. | Docker | We will provide docker-compose files with configured services for testing. |

### Milestone 2 — IPFS DHT
* **Estimated Duration:** 1 month
* **FTE:**  1
* **Costs:** $5,000

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 1. | API specification | We will create a specification for IPFS DHT API for internal use and external connections. |  
| 2. | Data structures | We will create a data structure that will support traversing, search and delete operations. |  
| 3. | Implementation | We will implement IPFS DHT API. |  

### Community engagement TODO

As part of the Program, we require that you produce an article/tutorial and publish it (for example on [Medium](https://medium.com/)). It should explain your work done as part of the grant. 

Normally, we ask you to submit the write-up upon the completion of your grant, although for larger projects it might make sense to publish multiple articles after the completion of different milestones.

## Future Plans
1. More data services (connectors) that can auto attach to data sets, can perform some logic, and then move data in/out.
2. ML/AI models and pipelines.
3. Ability to remove user’s data by request.

## Additional Information TODO
Any additional information that you think is relevant to this application that hasn't already been included.

Possible additional information to include:
* What work has been done so far?
* Are there are any teams who have already contributed (financially) to the project?
* Have you applied for other grants so far?
