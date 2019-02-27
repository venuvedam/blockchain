# Seven Blockchain Pillars to Start With

> Note: We do know that blockchain and DLT are not synonymous. However, for the purpose of this document, we use the term ***blockchain*** to refer to all distributed ledger technologies whether they organise the transactions as blocks or not.

## What is this article all about?
This document attempts to provide some guidance on Blockchain Requirements Gathering – A Set of Questions to Help Start the Architectural Conversations

## Basic:


1.	How many organizations are part of the network?
2.	Is it a private network (All nodes are part of a single overarching Azure subscription (can be owned by an operator/custodian of consortium) and all participating orgs have nodes loaned to them) or a true consortium? (Each org with its own Azure subscription)
3.	Who owns the identity of the users? Who are the users? What is the identity management solution? 
4.	Key Management Solution in place? (Azure Key Vault for instance) – Is the key vault used only as key storage mechanism or is it used to sign the transactions as well?
5.	Transaction frequency/payload size/smart contract complexity
6.	Any off-chain workflow steps that need to be considered and maintained separately? (not part of the system we are designing – Manual verification requirements etc if any)

## Network Design

Generally, it is the ISVs/Partners who have good cloud devops skills – who are successful in managing the consortiums. The participant organizations mostly will not have these skills. 

1.	Network Administration (Who does the administration? How?) 
2.	Policies and voting criteria?
3.	Infrastructure Management – Taking care of the infra on which the ledger runs – patch management, minor/major version upgrades, high availability, BCDR requirements, RTO/RPO considerations etc, primary/DR regions
4.	Change Management – DevOps process for handling the lifecycle of the smart contracts.
5.	Security Requirements – (Application level, Infra level, Network isolation etc)

## Confidentiality

1.	Privacy vs Transparency – Striking a balance (Transactions between two orgs – visible only to those two? Or to the entire network?)
2.	What about IP stored on the DLT? How do you want to manage this?
3.	What is your off-chain data requirements? (Data insights, Crunching of the data, document/artefacts store etc)
4.	Process for hashing the documents.
5.	Data Encryption requirements – At rest, in transit, during compute.

## Scalability
1.	Throughput vs latency? What are your requirements?
2.	Which consensus model makes sense for your use case?
3.	What are your scalability requirements? Automating the process of joining a new node to the network. (There are PowerShell scripts available to do the org induction if the ledger is a managed ledger offering on Azure for instance.), Also keep in mind that increasing nodes on the network may increase the latency of the transaction – and we need to pay close attention to the consensus mechanism of choice. 
4.	Smart contract design – size of the contract – number of contracts – complexity of the smart contract.

## Compliance
1.	External and internal risks (Risks injected into the system due to external processes and systems; external data flowing into the system; non-deterministic processes etc)
2.	Actors – roles and responsibilities in the workflow
3.	Audit requirements – Extent of audit access – Transparency requirements. 
4.	GDPR requirements – What data resides on the ledger? PII?
5.	Landing zone compliance certifications required? – (To give you an example - Not relevant for this use case – but if it is a pharma/health consortium – GXP Compliance is mandatory for the infra component – Azure is fully compliant by the way)

## Ecosystem
1.	Solve ledger isolation – integration requirements with other LOB applications and patterns for integration. Events that trigger downstream actions; events that trigger state changes on the ledger etc.
2.	Minimize ledger dependence – (All business logic on chain vs minimum required etc – This will determine how dependent your network will be on the ledger technology)
3.	Landing zone – On-Prem/Cloud/Hybrid (Again, this is not relevant in this case because Intertek wants this all on Azure)
4.	Chain Interoperability

## Miscellaneous
1.	Performance benchmarking requirements of the network. 
2.	Improving throughput – (Discuss if relevant – increasing gas limit to max – eth – on all miners)
