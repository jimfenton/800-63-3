## 4. Authenticator Assurance Levels

As described in Section 2, this guideline defines three Authenticator Assurance Levels (AALs). In order to satisfy the requirements of a given AAL, a claimant SHALL authenticate themselves with at least a given level of strength to be recognized as a subscriber. The result of an authentication process is an identifier, that simply conveys a "handle" to that subscriber that will be used each time that subscriber authenticates to that relying party. Optionally, other attributes that identify the subscriber as a unique person may also be provided.

Detailed normative requirements for authenticators and verifiers at each AAL are provided in Section 5.

Throughout this document, references to FIPS 140-2 requirements may also be satisfied by subsequent versions of FIPS 140.

###4.1. Authenticator Assurance Level 1

Authenticator Assurance Level (AAL) 1 provides single factor remote network authentication, giving some assurance that the same Claimant who participated in previous transactions is accessing the protected transaction or data. AAL 1 allows a wide range of available authentication technologies to be employed and requires only a single authentication factor to be used. It also permits the use of any of the authentication methods of higher authenticator assurance levels. Successful authentication requires that the Claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.

####4.1.1. Permitted Authenticator Types

Authenticator Assurance Level 1 permits the use of any of the following authenticator types, defined in Section 5:

* Memorized Secret
* Look-up Secret
* Out of Band
* Single Factor OTP Device
* Multi-Factor OTP Device
* Single Factor Cryptographic Device
* Multi-Factor Software Cryptographic Authenticator
* Multi-Factor Cryptographic Device

####4.1.2. Authenticator Requirements

Hardware authenticators ("devices" from the list above) used at AAL1 SHOULD be designed to meet the requirements of FIPS 140-2 Level 1.

####4.1.3. Assertion Requirements

In order to be valid at AAL 1, authentication assertions SHALL meet the requirements defined in SP 800-63C.

####4.1.4. Reauthentication

At AAL 1, authentication of the subscriber SHALL be repeated at least once per 24 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following no more than 2 hours of user inactivity. It is permissible to prompt the user to cause activity just before the inactivity timeout, if desired.

###4.2. Authenticator Assurance Level 2

Authenticator Assurance Level (AAL) 2 provides higher assurance that the same Claimant who participated in previous transactions is accessing the protected transaction or data. At least two different authentication factors are required. Various types of authenticators, including multi-factor Software Cryptographic Authenticators, may be used as described below. AAL 2 also permits any of the authentication methods of AAL 3. AAL 2 authentication requires cryptographic mechanisms that protect the primary authenticator against compromise by the protocol threats for all threats at AAL 1 as well as against verifier impersonation attacks. Approved cryptographic techniques are required at AAL 2 and above.

####4.2.1. Permitted Authenticator Types

Two or more single-factor authenticators, or one or more multi-factor authenticators, are required at AAL2. Authenticator requirements are specified in Section 5.

If a combination of single-factor authenticators is used, it SHALL include a Memorized Secret authenticator and one possession-based ("something you have") authenticator from the following list:
* Look-up Secret
* Out of Band
* Single Factor OTP Device
* Single Factor Cryptographic Device

Alternatively, any of following multi-factor authenticators may be used:
* Multi-factor OTP Device
* Multi-Factor Software Cryptographic Authenticator
* Multi-Factor Cryptographic Device

####4.2.2. Authenticator Requirements

Single-factor hardware authenticators used at AAL 2 SHALL meet the requirements of FIPS 140-2 Level 1 and multi-factor hardware authenticators SHALL meet the requirements of FIPS 140-2 Level 2. Formal verification of compliance is not required.

####4.2.3. Assertion Requirements

In order to be valid at AAL 2, authentication assertions SHALL meet the requirements defined in SP 800-63C.

####4.2.4. Reauthentication

At AAL 2, authentication of the subscriber SHALL be repeated at least once per 12 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following a no more than 30 minutes of user inactivity. It is permissible to prompt the user to cause activity just before the inactivity timeout, if desired. Reauthentication requires the use of both authentication factors.

###4.3. Authenticator Assurance Level 3

Authentication Assurance Level (AAL) 3 is intended to provide the highest practical remote network authentication assurance. Authentication at AAL 3 is based on proof of possession of a key through a cryptographic protocol. AAL 3 is similar to AAL 2 except that only “hard” cryptographic authenticators are allowed. The authenticator is required to be a hardware cryptographic module validated at Federal Information Processing Standard (FIPS) 140-2 Level 2 or higher overall with at least FIPS 140-2 Level 3 physical security. Level 4 authenticator requirements can be met by using the PIV authentication key of a FIPS 201 compliant Personal Identity Verification (PIV) Card.

####4.3.1. Permitted Authenticator Types

Authentication Assurance Level 3 requires the use of one of two kinds of hardware devices:
* Multi-factor OTP Device
* Multi-Factor Cryptographic Device

####4.3.2. Authenticator Requirements

Multi-factor hardware authenticators at AAL 3 SHALL be verified to meet the requirements of FIPS 140-2 Level 2.

####4.3.3. Assertion Requirements
In order to be valid at AAL 3, authentication assertions SHALL meet the requirements of proof-of-possession assertions as defined in SP 800-63C.

####4.3.4. Reauthentication

At AAL 3, authentication of the subscriber SHALL be repeated at least once per 12 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following a period of no more than 15 minutes of user inactivity. It is permissible to prompt the user to cause activity just before the inactivity timeout, if desired.

###4.4. Summary of Requirements

*(Non-normative; refer to preceding sections for normative requirements)*

The following table summarizes the requirements for each of the authenticator assurance levels:

Requirement | AAL 1 | AAL 2 | AAL 3
------------|-------|-------|-------
**Authenticator types** | Memorized Secret<br />Look-up Secret<br />Out of Band<br />SF OTP Device<br />MF OTP Device<br />SF Cryptographic Device<br />MF Software Cryptographic Authenticator<br />MF Cryptographic Device | Memorized secret plus:<br />&nbsp;Look-up Secret<br />&nbsp;Out of Band<br />&nbsp;SF OTP Device<br />&nbsp;SF Cryptographic Device<br />or:<br />&nbsp;MF OTP Device<br />&nbsp;MF Software Cryptographic Authenticator<br />&nbsp;MF Cryptographic Device | MF OTP Device<br />MF Cryptographic Device
**FIPS 140 verification** | Designed to meet Level 1 | Level 1 (single factor),<br /> Level 2 (multi factor); self-asserted | Verified to meet Level 2
**Assertions** | Bearer or proof of possession | Bearer or proof of possession | Proof of possession only
**Reauthentication** | 24 hours or 2 hours inactivity | 12 hours or 30 minutes inactivity | 12 hours or 15 minutes inactivity



