#Disclaimer

I am advising a [Blockchain/Distributed Ledger Technology (DLT) Healthcare project](http://grapevineworldtoken.io).

#Introduction

This article talks about interoperability and blockchain in the healthcare domain. 
There are two parts to this article. The first part explains how healthcare Information Technology achieves interoperability, and in the second part exposes some common pitfalls of blockchain use cases (IMHO) that I became aware of while attending some (strange) DLT-related events.

#Interoperability

The roots of IT system use within the healthcare domain go back to the 80s, with the advent of initiatives such as DICOM (->http://dicom.nema.org), and Health Level 7 (->http://hl7.org) which introduced an initial digitalisation step.

[ISO 27002](https://en.wikipedia.org/wiki/ISO/IEC_27002) defines the guidelines for IT system security as per CIA triad, Confidentiality, Integrity, and Availability. In particular, availability _[ensures that authorised users have access to information and associated assets when required](https://en.wikipedia.org/wiki/Availability)._

Now, let us imagine an emergency room. A patient arrives unconscious and the doctor needs to decide whether or not to treat the patient with a specific antibiotic. The doctor doesn't know about any potential allergies, so the doctor checks their local IT system for the patient's medical record (remember, since the 90s electronic medical records have been available and are the exclusive medical record format in some parts of the world). The emergency room client software uses HL7v3 and tries to access the central clinical document repository, which, in contrast, only understands HL7 FHIR,. There is no interoperability between the HL7v3 client system and the FHIR repository system (the lack or architecture is evident, and this is likely to lead to vendor lock-in). The patient's _safety_ is at risk, since the medical records are not _available._ Now, extend this to a global scale, for instance, the patient is travelling in a foreign country, and the doctor needs to fetch medical records from the patient's home country. Can you evaluate the risk of not having interoperability? Just imagine some of the elements to consider, including language barriers, medical disciplines, medicine types, dosage variance, electronic message types, security models, to name a few. This is an example where architecture would help.

#Standards are not enough

Interoperability is compelling, but how is interoperability achieved? [Bass et al.] identify interoperability as _the degree to which two or more systems can usefully exchange meaningful information via interfaces in a particular context._ On the bright side, a world working on a unique software infrastructure it’s a not a realistic scenario (see Section on EIF); thus different vendors around the globe must agree on a common rules for interoperability, but to which extent?

Interoperability has different levels. The most prominent worldwide healthcare IT society, HiMMS, further narrows the definition of interoperability, assigning it [three levels](https://www.himss.org/library/interoperability-standards/what-is):

_In healthcare, interoperability is the ability of different information technology systems and software applications to communicate, exchange data, and use the information that has been exchanged. Data exchange schema and standards should permit data to be shared across clinician, lab, hospital, pharmacy, and patient regardless of the application or application vendor._

#The HiMMS levels are: 

1. **Foundational** (at the level of message exchange),
2. **Structural** (the format of data exchange)
3. **Semantical** (at the level of the information exchanged). 

The EU e-SENS project introduced [5 more interoperability layers](http://wiki.ds.unipi.gr/display/ESENS) as shown in the picture below.

![# e-SENS Technical Levels](http://www.mascanc.net/tl.png "e-SENS Interoperability Levels")

The HiMMS definition stops at the second level, while e-SENS, is a project that aims to share healthcare data between different countries, has added both organisational and legal interoperability.

Vendors shall apply to common rules. Those rules are international data exchange standards. Still, Grace Lewis ([Bass et al.]) explicitly mention that "standards alone are not enough to guarantee interoperability". Andy Tanembaum once said ["The nice thing about standards is that you have so many to choose from"](https://en.wikiquote.org/wiki/Andrew_S._Tanenbaum) which is undoubtedly true.

Standards, without any governance, do not really achieve interoperability. Anyone can introduce a standard! But it shall be supported, implementable, testable, and _free_.

#The need for Enterprise Architectures

Enterprise Architectures come to the rescue. In fact, another architectural step has to be adopted, precisely the establishment of a governing structure over the precise selection of standards, to ensure a continuum of the economic and technical investments, such that a chosen technology will survive beyond the vendors proposing it and the possible deviations from the original intended standards. Having a so-called Vendor Neutral Architecture (VNA) provides an example of this. These concepts feed into to the definition of _enterprise architecture_. 

The two ground concepts in the architecture design process are the Reference Architecture and the Solution Architecture. 

1. A _Reference Architecture_ is the generic architecture that provides guidelines and options for the development of specific architectures and solution implementations. 
2. A _Solution Architecture_ describes the particular business operations/activities and how the information systems and technology support them. It typically applies to a single project/organisation.

Agilists may comment that architeture it's a BDUF, and YAGNI. That's a false fact, as the work of [Meyer] and [Babar et al.] describe.

[TOGAF](http://www.opengroup.org/subjectareas/enterprise/togaf), and [IHE](http://www.ihe.net) provide a methdological means to define the solution and reference architectures. In particular, IHE has been regulated by the EU commission with decision ​[**(EU) 2015/1302 of 28 July 2015**](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=OJ:JOL_2015_ 99_R_0011).

#Choosing a standard, or a single product, is a bad idea.

We, therefore, understand that we need interoperability to develop and choose sofwtware for healthcare. To achieve interoperability we need a standard, no, wait, we need a _organisation_ which supports and governs the standards, then we need to test, certify, oh my! Isn't it better to all select the same prodfuct and deploy it worldwide? No. Here the story of the European Interoperability Framework (EIF) and the Free Software Foundation comes into play.

At the beginning of the century, the EU commission made the right decision: to make interoperability mandatory amongst public services in Europe. A hypothetical IT employee within the EU would have said, "We know that a standard is not sufficient, so we bring in a Enterprise Architecture framework.". EIF quickly evolved to version 2.0 which raised a substantial political debate due to political lobbying from the Business Software Association (BSA). The Free Software Foundation produced a [statement](https://fsfe.org/activities/os/eifv2.en.html) as follows:

_Looking back to the consultation draft, it is obvious that during the development of EIFv2, the European Commission has abandoned the concept of Open Standards as a key enabler for interoperability. This is a central reason why the current draft would see the European Interoperability Framework become a shadow of its former self._

The basic idea of the Business Software Alliance lobbying was that software _homogeneity_ guarantees interoperability, while other approaches, well, probably not. BSA clearly wanted to achieve a vendor lock-in situation, disqualifying the continuum concept described above. The EIFv3 (or the New EIF) explicitly promotes open standards, and [Free Software has been indicated as one of the factors of enhanced interoperability](https://fsfe.org/activities/os/eif-v3.en.html).

#Part 2

##Blockchain and Interoperability

Blockchain is a distributed ledger, and is, in this text from now on referred to as a Distributed Ledger Technology (DLT). [Wattenhofer] defines the blockchain _as the longest path from the genesis block, i.e., root of the tree, to a leaf. The blockchain acts as a consistent transaction history on which all nodes eventually agree._ On each transaction some code can be executed in different ways and takes different names (e.g., Smart Contracts, Chaincode, etc). From this definition it should be clear what a blockchain is not: *an efficient database*. Storing unstructured data in a blockchain guarantees poor performance but still, depends on the blockchain deployment, whether public or private and on the consensus algorithm. [Here](https://blockchainatberkeley.blog/building-it-better-a-simple-guide-to- blockchain-use-cases-de494a8f5b60) and [here](https://eprint.iacr.org/2017/375.pdf) there are pretty famous blockchain papers on proper DLTs use.

Some projects, like Ethereum, store data in a public blockchain. However this introduces several problems in the healthcare domain:

1. Apart from storage costs, without a freely given informed consent you cannot disclose medical data
2. Data in the blockchain is publicly accessible

Some projects solve 1) and 2) by using encryption, but it is unwise to trust an encryption algorithm forever. The [NIST](https://csrc.nist.gov/Projects/Cryptographic-Standards-and-Guideline s) or [ENISA](https://www.enisa.europa.eu/topics/data-protection/security-of-perso nal-data/cryptographic-protocols-and-tools) update the list of useable algorithms every five years, on average.

Some other projects rely on Smart Contracts: however this introduces another IT security problem. Ethereum, writes a smart contract, "in stone". However, at the time of writing, Solidity is at version 0.4.xx, and [there are some rumors about its design flaws](https://news.ycombinator.com/item?id=14691212), and if a bug is introduced in the contract code it can't be simply corrected. Of course, smart contracts are audited, but the auditor performs static analysis checks using today's security knowledge, which can change in future, thereby introducing new issues and breaches. Moving between contracts version in Ethereum is an hard work (e.g., [via the proxy call](https://blog.zeppelinos.org/proxy-patterns/)). Other DLT (such as [Hyperledger](http://hyperledger.org)) allows the update of smart contract's code. But then, if few people can update a smart contract potentially holding economic value, we inherit the IT security problem of, who is entitled to change the contract? We loose the benefit of cryptography (the immutability of the smart contract), by rephrasing it as an IT Security problem (IA&A). Moreover, most of the auditors that I encountered, do not disclose the real persons behind the audit, and usually, audits are performed by creating some unit (e.g., with Truffle) tests, which is basically only defining a good test coverage, which is not a good indicator, [as this anecdote shows](https://dev.to/conectionist/why-code-coverage-is-not-a-reliable-metric -327l).

[EOS](https://eos.io) is a new and promising blockchain implementation, which uses the DPoS consensus algorithm. It also uses WASM as language to write smart contracts. On the negative side, the lack of adequate analysis on DPoS ([only one explanation exists](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this -missing-white-paper)) suggests careful evaluation of this technology in a real world. Mathematical proof of DPoS would be needed before medical data is injected into EOS. [Cardano](https://cardano.org) claims to have such mathematical proof. As an example, recently [De Angelis et al.] proved that the the Proof-of-Authority protocol for permissioned blockchain deployed over WANs experimenting Byzantine nodes, does not provide adequate consistency guarantees for scenarios where data integrity is essential. To my best knowledge no formal proof on DPoS has been done yet.

Again on the performance: the time of doctor is really precious. Time left waiting for a transaction to be processed in the blockchain is time left to the patient treatment: doctors can't simply wait minutes for a HL7 ADT to be processed by the blockchain. We cannot have blockchain stopping healthcare practicionners from admitting a patient.

##Is off-chain storage good?

Some DLT projects utilise pointers to data stored in a off-chain infrastructure. In particular, there are some using FHIR resources identifiers in the blockchain to guarantee a property (e.g., access control, patient-centric access to EHR, or data integrity). I don’t see blockchain acting as a market disruptor, but, in contrast, I see blockchain makes these projects more complicated, for two reasons:

1. If the blockchain deployment is public, and the blockchain uses code "written in stone", then the audit process is not sufficient to keep data secure forever. If the deployment is private, many regulations require the blockchain nodes that act as data controller to be operated under ISO 27002. Keeping many nodes utilising such operating model may be really expensive for hospitals, effectively opening an excellent marketing opportunity for Blockchain-as-a-Service.

2. The benefit of decentralisation is not entirely clear, since a centralised off-chain storage is anyway required (e.g., within a hospital information system).

The second point may have a corollary in the sense that if the goal is to achieve data integrity, and the blockchain implementation used is inefficient, an application including a database with properly signed data (e.g., using any aDES) is more suitable in terms of performance (although I don’t have done any tests).

##Marrying a single blockchain project

Other DLT initiatives propose visionary technologies and appealing solutions. However, as we already saw with the EIF story, homogeneity conflicts with interoperability, and lets adapters  proliferate.

#Conclusion

Healthcare can definitely exploit the DLTs for instance in patient matching, and resource consumption rewards. 

Patient matching involves the typical case when a patient, or even a doctor, has to be identified and authenticated. There are interesting ideas such as the concept of self-sovereign identities, clinical research, etc. [More information can be found here](https://healthcaresecprivacy.blogspot.com/2017/03/healthcare-blockc hain-use.html).

We see that a product with interfaces and algorithms supported by only one single vendor or organisation cannot be the ideal solution, since it goes against the concepts of the continuum (the software asset which survives to its creator), and produces vendor lock-in, elevating the risks of project failures and, most important, jeopardising patient safety. Also, storing data (even encrypted) in the blockchain is also a weak idea due to performance and security issues.

#Special Thanks

Special thanks to my colleagues and to the [FLUG](http://www.firenze.linux.it) for their help.

#References

[Bass et al] L. Bass, P. Clements, R. Kazman, _Software_ _Architecture in Practice,_ Third Edition, Addison-Wesley 2013

[Meyer] B. Meyer, _Agile! The Good, the Hype and the Ugly,_ Springer 2014

[Babar et al.] M. Babar, A. W. Brown, I. Mistrik, _Agile_ _Software Architecture: Aligning Agile Processes and Software Architectures,_ Morgan Kaufmann Publishers Inc. San Francisco, CA, USA 2013

[Wattenhofer] R. Wattenhofer, _The science of the blockchain,_ Inverted Forest Publishing, 2016

[De Angelis et al.] De Angelis, Stefano & Aniello, Leonardo & Baldoni, Roberto & Lombardi, Federico & Margheri, Andrea & Sassone, V., _PBFT vs proof-of-authority: applying the CAP theorem to permissioned blockchain._
