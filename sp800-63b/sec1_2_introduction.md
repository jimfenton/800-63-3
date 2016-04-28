## 1. Purpose

This recommendation and its companion documents, SP 800-63-3, SP 800-63A, and SP 800-63C, provide technical guidelines to credential service providers for the implementation of remote authentication.

##2. Introduction

Remote authentication is the process of establishing confidence in user identities electronically presented to an information system. E-authentication presents a technical challenge when this process involves the remote authentication of individual people over a network. 

The ongoing authentication of subscribers is central to this process. Subscriber authentication is performed by verifying that a claimant controls one or more *authenticators* (called *tokens* in earlier editions of SP 800-63) associated with a given subscriber. A successful authentication results in the assertion of an identifier, and optionally other identity information, to the relying party.

This document provides guidance on types of authentication processes, including choices of authenticators, that may be used at various Authenticator Assurance Levels. It also provides guidance on the lifecycle of authenticators, including revocation in the event of loss or theft.

These technical guidelines apply to remote authentication of human users to IT systems over a network. They do not primarily address the authentication of a person who is physically present, for example, for access to buildings, although some credentials that are used remotely may also be used in local authentication. These technical guidelines also establish requirements that Federal IT systems and service providers participating in authentication protocols be authenticated to subscribers. However, these guidelines do not specifically address machine-to-machine (such as router-to-router) authentication, or establish specific requirements for issuing authentication credentials to machines and servers when they are used in e-authentication protocols with people.

The strength of an authentication transaction is characterized by a categorization known as the *Authenticator Assurance Level* (AAL). A high-level summary of the technical requirements for each of the authenticator assurance levels is provided below; see [Section 4](sec4_aal.md/#AAL_SEC4) and [5](sec5_authenticators.md/#AAL_SEC5) of this document for specific normative requirements.

**Authenticator Assurance Level 1** - AAL 1 provides single factor authentication, giving some assurance that the same claimant who participated in previous transactions is accessing the protected transaction or data. AAL 1 allows a wide range of available authentication technologies to be employed and requires only a single authentication factor to be used. It also permits the use of any of the authentication methods of higher authenticator assurance levels, therefore allowing CSPs to allow users to use a higher AAL authenticator to be at AAL 1. Successful authentication requires that the claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.

**Authenticator Assurance Level 2** – AAL 2 provides higher assurance that the same claimant who participated in previous transactions is accessing the protected transaction or data. At least two different authentication factors SHALL be used. AAL 2 also permits any of the authentication methods of AAL 3 for the same reasons as AAL 1. AAL 2 authentication requires cryptographic mechanisms that protect the primary authenticator against compromise by the protocol threats for all threats at AAL 1 as well as verifier impersonation attacks. Approved cryptographic techniques SHALL be used at AAL 2 and above.

**Authentication Assurance Level 3** – AAL 3 is intended to provide the highest practical remote network authentication assurance. Authentication at AAL 3 is based on proof of possession of a key in a physical authenticator through a cryptographic protocol. AAL 3 is similar to AAL 2 except that only multifactor hardware cryptographic authenticators are allowed. The authenticator SHALL be a hardware cryptographic module validated at Federal Information Processing Standard (FIPS) 140 Level 2 or higher overall with at least FIPS 140 Level 3 physical security.

