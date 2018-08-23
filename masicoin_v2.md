#Disclaimer

I am advising a [DLT Healthcare project](http://grapevineworldtoken.io).

#Introduction

This article talks about interoperability and blockchain in the healthcare domain. The article is divided in two parts. In the first it will explain how interoperability is achieved in healthcare IT, and in the second part it will spot some (IMHO) common pitfalls of blockchain use cases that I heard while attending some (strange) DLT-related events.

#Interoperability

The use of IT systems in the healthcare domain find its roots back in the 80s, with the advent of such initiatives as [DICOM](http://dicom.nema.org), and [Health Level 7](http://hl7.org) which brought an initial step for the digitalization.

[ISO 27002](https://en.wikipedia.org/wiki/ISO/IEC_27002) defines the guidelines for IT system security in terms of the CIA triad, Confidentiality, Integrity, and Availability. In particular, availability _[ensures that authorized users have access to information and associated assets when required](https://en.wikipedia.org/wiki/Availability)._

Now, let us imagine an emergency room. A patient arrives unconscious and the doctor needs to decide whether or not to treat him with a specific antibiotic. Doctor doesn't know about any potential allergies, so it checks in its IT system for the patient's medical record (remember, since the 90s the chance to have paper-based records is very low in some parts of the world). The client software on the emergency room tries to access via SOAP call the main clinical document repository, which, in contrast, understands only REST,. There is no interoperability amongst the systems: the _safety_ of the patient is at risk, since the documents are not _available._ Now, extend it to a global scale: for instance the patient is traveling in a foreign country, and the doctor needs to fetch medical records from patient's home country: can you evaluate the risk of not having interoperability? Just imagine the language barriers.

#Standards are not enough

Interoperability is compelling. But how to achieve it? [Bass et al.] identify interoperability as _the degree to which two or more systems can usefully exchange meaningful information via interfaces in a particular context._ Luckily, it is unrealistic to imagine a world sharing the same software globally (see Section on EIF later), thus different vendors around the globe shall agree on a common rules for interoperability. But to which extent?

Interoperability has different levels. The biggest healthcare IT society worldwide, HiMMS, further narrow the definition of interoperability, assigning it [3 levels](https://www.himss.org/library/interoperability-standards/what-is):

_In healthcare, interoperability is the ability of different information technology systems and software applications to communicate, exchange data, and use the information that has been exchanged. Data exchange schema and standards should permit data to be shared across clinician, lab, hospital, pharmacy, and patient regardless of the application or application vendor._

#Levels are: 

1. **Foundational** (at the level of message exchange),
2. **Structural** (the format of data exchange)
3. **Semantical** (at the level of the information exchanged). 

The EU e-SENS project introduced [5 more interoperability layers](http://wiki.ds.unipi.gr/display/ESENS) as shown in the picture below.

![# Technical level.png](Technical level.png)

The HiMMS definition stops at the second level, while e-SENS, being a project aiming at sharing healthcare data amongst different countries, it added both organizational and legal interoperability.

Vendors shall apply to common rules. Those rules are international standards. Still, Grace Lewis ([Bass et al.]) clearly mention that "standards alone are not enough to guarantee interoperability". Andy Tanembaum once said ["The nice thing about standards is that you have so many to choose from"](https://en.wikiquote.org/wiki/Andrew_S._Tanenbaum) which is undoubtedly true.

Standards, without any governance, are not really helping in achieving the interoperability. Anyone can introduce a standard! But it shall be supported, implementable, testable, and _free_.

#The need for Enterprise Architectures

Enterprise Architectures come to the rescue. In fact, another architectural step has to be adopted, precisely the establishment of a governing structure over the precise selection of standards, in order to ensure a continuum of the economic and technical investments, such that a chosen technology will survive upon the vendors proposing it and the possible deviations from the original intended standards. This is the benefit of having a so-called _Vendor Neutral Architecture_ (VNA). These concepts bring to the definition of _enterprise architecture_. 

The two ground concepts in the architecture design process are the Reference Architecture and the Solution Architecture. 

1. A _Reference Architecture_ is the generic architecture providing guidelines and options for the development of specific architectures and solution implementations. 
2. A _Solution Architecture_ describes the specific business operations/activities and the ways in which the information systems and technology support them. It typically applies to a single project/organisation.

Agilists may comment that architeture it's a BDUF, and YAGNI. That's a false fact, as the work of [Meyer] and [Babar et al.] describe.

[TOGAF](http://www.opengroup.org/subjectareas/enterprise/togaf), and [IHE](http://www.ihe.net) provide a methdological mean to define solution and reference architectures. In particular, IHE has been regulated by the EU commission with decision ​[**(EU) 2015/1302 of 28 July 2015**](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=OJ:JOL_2015_ 99_R_0011).

#Choosing a standard, or a single product, is a bad idea.

So we understood that while developing and choosing software for healthcare, we need interoperability. To achieve interoperability we need a standard, no, wait, we need a _organization_ which supports and governs the standards, then we need to test, certify, oh my! Isn't that easier if we all choose the same product and we deploy it worldwide? No. And here the story of the European Interoperability Framework (EIF) and the Free Software Foundation comes into play.

At the beginning of the century, the EU commission took a good decision: to make interoperability mandatory amongst public services in Europe. "We know that a standard is not sufficient, so we bring in a Enterprise Architecture framework.", an hypotethical IT employee at the EU would have said. EIF quickly evolved to version 2.0 which raised a huge political debate due to political lobbying from the Business Software Association (BSA). The Free Software Foundation raised a [statement](https://fsfe.org/activities/os/eifv2.en.html) with the following rationale:

_Looking back to the consultation draft, it is obvious that during the development of EIFv2, the European Commission has abandoned the concept of Open Standards as a key enabler for interoperability. This is a central reason why the current draft would see the European Interoperability Framework become a shadow of its former self._

Basic idea of the business software alliance lobbying was that software _homogeneity_ guarantees interoperability, while other approaches, well, probably not. BSA clearly wanted to achieve a vendor lock-in situation, disqualifying the continuum concept described above. This has not been adopted by the EU member states. The EIFv3 (or the New EIF) explicitly promotes open standards, and [Free Software has been indicated as one of the factors of enhanced interoperability](https://fsfe.org/activities/os/eif-v3.en.html).

#Part 2

##Blockchain and Interoperability

Blockchain is a distributed ledger, from now to now it will be referenced as a Distributed Ledger Technology (DLT). [Wattenhofer] defines the blockchain _as the longest path from the genesis block, i.e., root of the tree, to a leaf. The blockchain acts as a consistent transaction history on_


_which all nodes eventually agree._ On each transaction some code can be executed in different ways, and takes different names (e.g., Smart Contracts, Chaincode, etc). From this definition it should be clear what a blockchain it is not: an efficient database. Storing unstructured data in a blockchain guarantees poor performance but still, depends on the blockchain deployment, whether public or private, and on the consensus algorithm. In fact, not only the consensus has to run, but also the nodes shall be updated. [Here](https://blockchainatberkeley.blog/building-it-better-a-simple-guide-to- blockchain-use-cases-de494a8f5b60) and [here](https://eprint.iacr.org/2017/375.pdf) there are pretty famous blockchain papers on proper use of DLTs.

Some projects store data in a public blockchain like Ethereum. However this encounter several problems in the healthcare domain, i.e.:

1) Apart from storage costs, medical data cannot be disclosed without a freely given informed consent
2) Data in the blockchain is publicly accessible

Some projects solve 1) and 2) by using encryption, but it is unwise to trust an encryption algorithm forever. The [NIST](https://csrc.nist.gov/Projects/Cryptographic-Standards-and-Guideline s) or [ENISA](https://www.enisa.europa.eu/topics/data-protection/security-of-perso nal-data/cryptographic-protocols-and-tools) update the list of usable algorithms every 5 years, in average.

Some other projects rely on Smart Contracts, but there is another IT security problem here. As an example, in Ethereum, a smart contract is written on stone. However, at the time of writing, Solidity is at version 0.4.xx, [there are some rumors about its design](https://news.ycombinator.com/item?id=14691212), and a bug can't be simply corrected. Of course, smart contracts are audited, but the auditor performs static analysis checks using the security knowledge of today, which can change eventually in future, introducing new issues and breaches. Moving amongst contracts version is an hard work in Ethereum today (e.g., [via the proxy call](https://blog.zeppelinos.org/proxy-patterns/)). Other DLT (such as [Hyperledger](http://hyperledger.org)) allows the update of smart contract's code. But then, if few people can update a smart contract potentially holding economic value, we inherit the IT security problem of who is entitled to change the contract? We loose the value of cryptography (the immutability of the smart contract), rephrasing it as an IT Security problem (IA&A). Moreover, most of the auditors that I encountered, do not disclose the real persons behind the audit, and usually audits are performed by creating some unit (e.g., with Truffle) tests, which is basically only defining a good test coverage. But this is not a good indicator, [as this anecdote shows](https://dev.to/conectionist/why-code-coverage-is-not-a-reliable-metric -327l).

[EOS](https://eos.io) is a new and promising blockchain implementation, using the DPoS consensus algorithm. It also uses WASM as language to write smart contracts. However, the lack of adequate analysis on DPoS ([only one explanation exists](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this -missing-white-paper)) hinders cautious evaluation of this technology in a real-world. Mathematical proof of it would be needed before injecting medical data into EOS. [Cardano](https://cardano.org) claims to have one. As an example, recently [De Angelis et al.] proved that the the Proof-of-Authority protocol for permissioned blockchain deployed over WANs experimenting Byzantine nodes, does not provide adequate consistency guarantees for scenarios where data integrity is essential. To my best knowledge no formal proof on DPoS has been done yet.

##Is off-chain storage good?

Some DLT projects utilize pointers to data stored in a off-chain infrastructure. In particular, there are some using FHIR resources identifiers in the blockchain to guarantee a property (e.g., access control, patient-centric access to EHR, or data integrity). I don’t see blockchain acting as a market disruptor, but, in contrast, blockchain makes those projects more complex, for two reasons:

1. If the blockchain deployment is public, and the blockchain uses code written in stone, then the audit process is not sufficient to keep data secure forever. If the deployment is private, many regulations require the blockchain nodes acting as data controller to be operated under ISO 27002. Keeping many nodes under such operating model may be really expensive for hospitals, effectively opening a good marketing opportunity for Blockchain-as-a-Service.

2. The benefit of decentralization is not entirely clear, since a centralized off-chain storage is anyway required (e.g., a hospital information system).

The second point may have a corollary in the sense that if the goal is to achieve data integrity, and the blockchain implementation used is inefficient, an application including a database with properly signed data (e.g., using any aDES) is more suitable in terms of performance (although I don’t have done any tests).

##Marrying a single blockchain project

Other DLT initiatives propose visionary technologies and appealing solutions. However, as we already saw with the EIF story, homogeneity conflicts with interoperability, and let adapters to proliferate.

#Conclusion

Healthcare can definitely exploit the DLTs for instance in patient matching, and resource consumption rewards. 

Patient matching is the typical case when a patient, or even a doctor, has to be identified and authenticated. Here there are interesting ideas such as the concept of self-sovereign identities, clinical research, etc. [More information can be found here](https://healthcaresecprivacy.blogspot.com/2017/03/healthcare-blockc hain-use.html).

We saw that a product with interfaces and algorithms supported by only one single vendor or organization cannot be the ideal solution, since it goes against the concepts of the continuum (the software asset which survives to its creator), and vendor lock-in, elevating the risks of project failures and, most important, jeopardizing the patient safety. Also, storing data (even encrypted) in the blockchain is also a weak idea due to performance and security.

#References

[Bass et al] L. Bass, P. Clements, R. Kazman, _Software_ _Architecture in Practice,_ Third Edition, Addison-Wesley 2013

[Meyer] B. Meyer, _Agile! The Good, the Hype and the Ugly,_ Springer 2014

[Babar et al.] M. Babar, A. W. Brown, I. Mistrik, _Agile_ _Software Architecture: Aligning Agile Processes and Software Architectures,_ Morgan Kaufmann Publishers Inc. San Francisco, CA, USA 2013

[Wattenhofer] R. Wattenhofer, _The science of the blockchain,_ Inverted Forest Publishing, 2016

[De Angelis et al.] De Angelis, Stefano & Aniello, Leonardo & Baldoni, Roberto & Lombardi, Federico & Margheri, Andrea & Sassone, V., _PBFT vs proof-of-authority: applying the CAP theorem to permissioned blockchain._
