# Supply Chain Transformation using Distributed Ledger Technology

One of the challenges faced by an enterprise that wishes to transform its supply chain using a distributed ledger technology (DLT) is to secure the buy-in for this paradigm from all its suppliers. Without the suppliers’ (Tier 1, Tier 2 at least) consent there is no value in investing in the transformation.

The first step, hence, for any enterprise is to prepare a comprehensive project report on the idea and discuss it with its main suppliers. Before embarking on this exercise, the enterprise must have completed a set of proof-of-concept (PoC) projects to ascertain the viability of the technology and the new paradigm specifically related to the use case that needs to be transformed. 

The goal should be to recruit at least two suppliers so that a minimum viable network can be established to demonstrate the value proposition of a decentralized and distributed immutable ledger that brings in transparency, speed and accuracy into the business transactions that happen on the supply chain network between these organizations.

This phase is generally called the “Pilot” phase of the business transformation. During this period and probably for sometime after this as well, the governance aspects of the network (Maintaining the network infrastructure, topology, recruiting new suppliers, handling the consensus process etc) is handled by the anchor enterprise itself in order to remove any barriers to entry for its suppliers. 

Obviously, this role of a business network operator requires considerable expertise in the technology platform of choice. The anchor enterprise may or may not have the manpower and the systems to handle this inhouse. Mostly, the organisation will invite a partner to deal with these aspects on its behalf. 

This may involve setting up the distributed network nodes for each organisation; making sure that the nodes can talk to each other and integrating the nodes with the downstream and upstream line of business applications that these organisations use. 

There is a lot of effort involved in setting this up. The anchor customer cannot expect the suppliers to take care of this expense without knowing whether the network would be beneficial to them. It may be necessary for the anchor customer to fund the pilot in its entirety or at least partly. Otherwise, the suppliers may not be willing to come onboard. This barrier to entry needs to be scrapped for the network to succeed. In some cases, it is seen that the anchor customer and the main partner both invest in the network together to get it going. 

In the distributed ledger world, some of the partners have expertise both in implementing the platform as well as acting as the governance operator of the network. However, most small/medium partners focus on either of them. So, the anchor enterprise in question may have to work with one partner for the implementation of the network and another for governing it. Also, the world is moving towards cloud computing. Enterprises are gradually moving their systems from on-premises datacentres to the cloud. In this case, the anchor enterprise will also be teaming up with a platform vendor in addition to the implementation partner and the governance operator. Some of the investment in the network may come from the platform vendor especially if the suppliers are going to be using the same platform for implementing their end of the network. 

Once the suppliers are onboarded, the anchor enterprise needs to demonstrate the value proposition of this network in such a way that it makes sense for all the parties involved. The network should be able to prove the value of participating in it. That means, it is not just the anchor customer who derives business value from this investment, the suppliers and other parties on the network should also benefit from it. Otherwise, the network is not going to be sustainable and successful. 

Hence, the first step is to use this pilot network to execute a real-life supply chain transaction end to end on the network between the two or three parties involved. Ideally, thanks to the underlying distributed ledger and the network consensus process, handoffs can be done automatically via purpose-built smart contracts that reside on the ledger. Since the data on the ledger is immutable and hence trusted by all the participants, the contracts can be settled automatically as well – cutting down on a number of manual verification steps that are a necessary evil in the conventional supply chain scenario.

The preferred outcome of this exercise is an order of magnitude reduction in the time to pay for the anchor customer’s suppliers. The results should speak for themselves. If not, it is time to go back to the drawing board and take a critical look at all the decision made so far in the journey. This includes both the technology decisions such as the choice of the DLT platform and the business workflow selected for this exercise.

If the pilot is successful, the scope of the exercise can be broadened to include more participants and create a minimum viable product (MVP). This is like the Minimum Marketable Product (MMP) concept found in a conventional product company roadmap. However, here the focus is more on the entire network rather than an isolated part of the implementation.

It is important to document the benefits of the network along with its structure as a shareable case study so that the seller teams are equipped properly when they reach out to potential suppliers of the supply chain network. 

# Go to Market Strategy for this network

1. Harness the power of all the sales organizations – Anchor customer, partners, pilot participants. In some cases, the underlying platform or DLT provider also joins the effort.

2. Create a focus list of suppliers to talk to. This comes mainly from the anchor customer though the partners can provide their inputs. 

3. Remove all entries to barrier (at least to start with) – Customers need to experience before they can invest in the network. 

4. Create a Network-as-a-Service offering with the partner. Any new customer wanting to test the waters, can be onboarded on to this network. They get a DLT Node-as-a-Service. If they are convinced, the partner can implement the node for them in their deployment zone of choice. (The customer is free, however, to choose an implementation partner of his/her choice)

5. Create a revenue model for the network governance operator. For the pilot, this is mainly funded by the anchor customer. However, it is important to define how the governance operators are compensated on the network. 

   > - Per transaction per organization – may not work in all cases as it does not deal with the actual business process. 
   > - Per User, per SKU
   > - T-shirt sizing of the SKUs tracked
   > - Annual fixed price contracts with each of the participants. (This can vary from participant to participant depending on their stake on the network and the value they derive from it)

6. How to compute the subscription costs or the Node-as-a-Service costs? 

   It is a function of the following parameters. (Not an exhaustive list)

   >a.    Platform costs (Compute, Storage, Bandwidth etc)
   >
   >b.    Implementation costs (Setting up the infra and the application)
   >
   >c.    Service and Support costs (Supporting the node, upgrades, patches etc)
   >
   >d.    Governance costs (Network governance operations)

Once you have these costs estimated, you must decide which pricing model makes sense for you and your network participants. You can keep the initial costs low to convince organizations to join your network and then charge a subscription fee. 

No matter which pricing model you choose, you must be prepared for a multi-year journey to recoup your investment on this project.

Finally, the distributed ledger protocol space is rapidly evolving. In the next couple of years, the market may see a rationalization or consolidation of the protocols in play. It is important to future proof any investment made in this area. Architecturally speaking, the solution should not be tightly coupled with the underlying ledger protocol. Ideally, an API layer should abstract the ledger so that the rest of your solution need not undergo an expensive re-engineering routine if circumstances dictate in future that the protocol technology should be swapped with another. 

Before I conclude this article, three architectural drivers to keep in mind when designing a supply chain network: (Or any network for that matter)

>1. Keep the network open. Anyone should be able to join from any platform.
>2. Keep it layered and sufficiently abstracted to weather “tech storms”.
>3. Be creative with governance and pricing models.