# Cere Decentralized Data Cloud

## Project Description

Cere Decentralized Data Cloud allows enterprises to keep track of user interactions within the applications 
in a secure way. User data is encrypted and stored in a distributed decentralized 
persistence layer. Later, that data can be restored for ETL purposes, shared between partners, 
validated as a source of truth, or even deleted by user request. Any developer can onboard user data 
using embedded Cere SDK which is also compatible with other Substrate networks.
Decentralized Data Cloud is one of the key parts of the Cere SaaS, but we are interested in making it open
to other developers and Substrate community.

## Use cases examples
* Store customer journey in a decentralized network and use it as a source of truth.
* Extract historical data for indexing (ElasticSearch, Athena, etc.), ETL’ing (Spark, Hadoop, Kafka Streams, etc.), or Machine Learning for business intelligence or creating the new marketplace.
* User can look at the data collected for him using his private key or Cere Wallet.
* Validate that all user sessions were signed and went through consensus.
* Capture (time capsule) for the user’s agreeing on terms and conditions event.

### Project Details
 
#### Packages

* **Cere DDC API** - public API for connecting Cere SDK/Substrate wallets.
* **IPFS DHT Service** - associate/lookup wallets in IPFS clusters, part of the Cere SaaS.
* **IPFS Service** - write/read into/from IPFS, traverse data, part of the Cere SaaS.
* **Crypto Service** - encrypt/decrypt data, part of the Cere SaaS with public API.
* **Cere SDK** - user onboarding, sending events; public API with open sourced implementations for JavaScript, iOS and Android.
* **Cere Blockchain Service** - write/read into/from Cere Network, part of the Cere SaaS.
* **Data Viewer** - public web service where everyone who has private key can look at the decrypted data.
* **Examples** - ready to work solutions/embeddable services for data interaction (working with IPFS, building data pipelines, crypto functions, validation, etc.).

#### Cere DDC API operations
1. Sign user/app operation, store associated blob file (_Cere SDK_)
    * Associate wallet with an IPFS cluster, Cere Mainnet by default (_IPFS DHT Service_)
    * Encrypt data (_Crypto Service_)
    * Store data as individually signed & encrypted (_IPFS Service_)
    * Execute smart contract on the Cere Mainnet (_Cere Blockchain Service_)
        * Free/premium tiers
        * Count operations, pay fees
2. Extract data
    * Per user
        * Find IPFS cluster with user data (_IPFS DHT Service_)
        * Traverse data tree (_IPFS Service_)
        * Decrypt data (_Crypto Service_)
    * Per application
        * Traverse user wallets of the application (_IPFS DHT Service_)
        * Apply per user flow
3. Show data
    * Find IPFS cluster with user data (_IPFS DHT Service_)
    * Traverse data tree (_IPFS Service_)
    * Decrypt data (_Crypto Service_)
    * Show to user (_Data Viewer_)
4. Remove data
    * Tag for removing (_IPFS Service, IPFS DHT Service_)
    * Invalidate previous records

#### Cere SDK
Package with a high-level API for sending events to the events stream. 
Contains internal functions for signing and validation. 
This is a recommended way of sending events to the DDC. 
Cere provides SDK for Javascript (can be used on the server-side NodeJS as well), 
Swift (for iOS/iPad applications), and Kotlin (for Android applications). 
As a part of SaaS, Cere provides Sandbox for SDK where developers can send events using demo accounts.

#### Crypto module
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

### Ecosystem Fit 
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
* https://github.com/cere-io - private packages, Cere SaaS Paltform
* https://github.com/Cerebellum-Network - public packages

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
