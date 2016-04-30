##4. Assertion Strength

###4.1. Assertion categories

As mentioned earlier, an assertion contains a set of claims or statements about an authenticated subscriber. Based on the statements contained within it, an authentication assertion will fall into one of two categories: *bearer* and *holder-of-key* assertions.

####4.1.1 Holder-of-Key Assertions

A holder-of-key assertion contains a reference to a symmetric key or a public key (corresponding to a private key) possessed by the Subscriber. The RP may require the Subscriber to prove possession of the secret that is referenced in the assertion. In proving possession of the Subscriber’s secret, the Subscriber also proves with a certain degree of assurance that he or she is the rightful owner of the assertion. It is therefore difficult for an Attacker to use a holder-of-key assertion issued to a Subscriber, since the former cannot prove possession of the secret referenced within the assertion. [ ** This is also a kind of parallel authentication since the user needs to authenticate with a key as well as possession of the associated assertion. Think of using OIDC to log in and get identity information but FIDO at the RP to step-up the transaction. ** ]

####4.1.2. Bearer Assertions

A bearer assertion does not provide a mechanism for the Claimant to prove that he or she is the rightful owner of the assertion. The RP has to assume that the assertion was issued to the Subscriber who presents the assertion or the corresponding assertion reference to the RP. If a bearer assertion (in the direct model) or assertion reference (in the indirect model)   belonging to a Subscriber is captured, copied, or manufactured by an Attacker, the latter can impersonate the rightful Subscriber to obtain services from the RP. Bearer assertions can be made secure only if some part of the assertion or assertion reference, sent to the Subscriber by the Verifier, is unpredictable to an Attacker and can reliably be kept secret. [ ** The indirect model can require other controls that protect it from this, making it not quite the same as a bearer assertion. ** ]

There are cases in which the RP should be anonymous to the Verifier for the purpose of privacy. The direct model is more suitable for the “anonymous RP” scenario since there is no requirement for the RP to authenticate to the Verifier as in the indirect model. However, it is possible to devise authentication schemes (e.g., using key hierarchies within a group or federation) that allow the use of the indirect model to support the “anonymous RP” scenario. [ ** This isn't really true since a good assertion protocol will have audience restricted assertions, otherwise you're open to injection and replay attacks. I think this whole paragraph is bad advice and sounds like justification for the setup of an existing system. ** ]

There are other cases where privacy concerns require that the Claimant’s identity/account at the Verifier and RP not be linked through use of a common identifier/account name. In such scenarios, pseudonymous identifiers are used within the assertions generated by the Verifier for the RP.

It should be noted that the two models described above are abstractions. There may be other interactions between the three players preceding or interspersed with the interactions described in the model. For example, the Claimant may initiate a connection with an RP of his or her choice, at which point, the latter would redirect the Claimant to an appropriate Verifier to be authenticated using the direct model, resulting in an assertion being sent to the RP. Alternately, the Claimant may first authenticate to a Verifier of his or her choice and then select one or more RPs to obtain further services. The direct model is used to generate assertions for each of these RPs. Parallel scenarios may be constructed for the indirect model as well.

#### 4.2. Threat Resistance per Authentication Assurance Level

Table 1 lists the requirements for assertions (both in the direct and indirect models) and assertion references (in the indirect model) at each assurance level in terms of resistance to the threats listed above.

***Obviously this table and the sections that follow need to be refactored for the 3 AALs rather than 4 LOAs.***

Table 1 – Threat Resistance per Authentication Assurance Level


| **Threat** | **Level 1** | **Level 2** | **Level 3** | **Level 4** |
|------------|:-----------:|:-----------:|:-----------:|:-----------:|
  Assertion manufacture/modification | Yes | Yes | Yes | Yes |
  Assertion disclosure | No | Yes | Yes | Yes |
  Assertion repudiation by Verifier | No | No | Yes<sup>[32](#note32)</sup> | Yes<sup>[32](#note32)</sup> |
  Assertion repudiation by Subscriber | No | No | No | Yes<sup>[32](#note32)</sup> |
  Assertion redirect | No | Yes | Yes | Yes |
  Assertion reuse | Yes | Yes | Yes | Yes |
  Secondary authenticator manufacture | Yes | Yes | Yes | Yes |
  Secondary authenticator capture | No | Yes | Yes | Yes |
  Assertion substitution | No | Yes | Yes | Yes |


The following sections summarize the requirements for assertions at each
assurance level.

All assertions recognized within this guideline shall indicate the
assurance level of the initial authentication of the Claimant to the
Verifier. The assurance level indication within the assertion may be
implicit (e.g., through the identity of the Verifier implicitly
indicating the resulting assurance level) or explicit (e.g., through an
explicit field within the assertion).

### 4.2.1. Level 1

At Level 1, it must be impractical for an Attacker to manufacture an
assertion or assertion reference that can be used to impersonate the
Subscriber. If the direct model is used, the assertion which is used
shall be signed by the Verifier or integrity protected using a secret
key shared by the Verifier and RP, and if the indirect model is used,
the assertion reference which is used shall have a minimum of 64 bits of
entropy. Bearer assertions shall be specific to a single
transaction.<sup>[33](#note33)</sup> Also, if assertion references are used, they shall be
freshly generated whenever a new assertion is created by the Verifier.
In other words, bearer assertions and assertion references are generated
for one-time use. [ ** This conflicts with all the advice and normal usage about cookies, above. ** ]

Furthermore, in order to protect assertions against modification in the
indirect model, all assertions sent from the Verifier to the RP shall
either be signed by the Verifier, or transmitted from an authenticated
Verifier via a protected session. [ ** should be both, right? ** ] In either case, a strong mechanism
must be in place which allows the RP to establish a binding between the
assertion reference and its corresponding assertion, based on integrity
protected (or signed) communications with the authenticated Verifier.

To lessen the impact of captured assertions and assertion references,
assertions that are consumed by an RP which is not part of the same
Internet domain as the Verifier shall expire if they are not used within
5 minutes of their creation. Assertions intended for use within a single
Internet domain, including assertions contained in or referenced by
cookies, however, may last as long as 12 hours without being used. [ ** This session timeout seems arbitrary, and what constitutes a "domain" in this practice? ** ]

##### 4.2.2. Level 2

If the underlying credential specifies that the subscriber name [ ** does this mean the display name? username? ** ] is a
pseudonym, this information must be conveyed in the assertion. Level 2
assertions shall be protected against manufacture/modification, capture,
redirect and reuse. Assertion references shall be protected against
manufacture, capture and reuse. Each assertion shall be targeted for a
single RP and the RP shall validate that it is the intended recipient of
the incoming assertion.

All stipulations from Level 1 apply. Additionally, assertions, assertion
references and any session cookies used by the Verifier or RP for
authentication purposes, shall be transmitted to the Subscriber through
a protected session which is linked to the primary authentication
process in such a way that session hijacking attacks are resisted (see
Section 8.2.2 for methods which may be used to protect against session
hijacking attacks). Assertions, assertion references and session cookies
shall not be subsequently transmitted over an unprotected session or to
an unauthenticated party while they remain valid. (To this end, any
session cookies used for authentication purposes shall be flagged as
secure, and redirects used to forward secondary authenticators from the
Subscriber to the RP shall specify a secure protocol such as HTTPS.)

To protect assertions against manufacture, modification, and disclosure,
assertions which are sent from the Verifier to the RP, whether directly
or through the Subscriber’s device, shall either be sent via a mutually
authenticated protected session between the Verifier and RP, or
equivalently shall be signed by the Verifier and encrypted for the RP. [ ** These requirements don't make much sense and provide very different kinds of protections. Signed by the Verifier and transmitted over server-validated TLS should be just fine here. ** ]

All assertion protocols used at Level 2 and above require the use of
Approved cryptographic techniques. As such, the use of Kerberos keys
derived from user generated passwords is not permitted at Level 2 or
above. [ ** Again, do we care about Kerb? ** ]

##### 9.3.2.3. Level 3

At Level 3, in addition to Level 2 requirements, assertions shall be
protected against repudiation by the Verifier; all assertions used at
Level 3 shall be signed. Level 3 assertions shall specify verified names
and not pseudonyms.

Kerberos uses symmetric key mechanisms to protect key management and
session data, and it does not protect against assertion repudiation.
However, based on the high degree of vetting conducted on the Kerberos
protocol and its wide deployment, Kerberos tickets are acceptable for
use as assertions at Level 3 as long as:

-   All Verifiers (Kerberos Authentication Servers and Ticket
    Granting Servers) are under the control of a single management
    authority that ensures the correct operation of the Kerberos
    protocol;

-   The Subscriber authenticates to the Verifier using a Level 3 token;

-   All Level 3 requirements unrelated to non-repudiation are satisfied.

Also, at Level 3, single-domain assertions (e.g., Web browser cookies)
shall expire if they are not used within 30 minutes. Cross-domain
assertions shall expire if not used within 5 minutes.

However, in order to deliver the effect of single sign on, the Verifier
may re-authenticate the Subscriber prior to delivering assertions to new
RPs, using a combination of long term and short term single domain
assertions provided that the following assurances are met:

-   The Subscriber has successfully authenticated to the Verifier within
    the last 12 hours.

-   The Subscriber can demonstrate that he or she was the party that
    authenticated to the Verifier. This could be demonstrated, for
    example, by the presence of a cookie set by the Verifier in the
    Subscriber’s browser. [ ** demonstrate to whom, the RP? ** ]

-   The Verifier can reliably determine whether the Subscriber has been
    in active communication with an RP since the last assertion was
    delivered by the Verifier. This means that the Verifier needs
    evidence that the Subscriber is actively using the services of the
    RP and has not been idle for more than 30 minutes. An authenticated
    assertion by the RP to this effect is considered sufficient evidence
    for this purpose. [ ** So this requires the RP to communicate back to the Verifier? I don't know of many protocols that do that. ** ]

#### 9.3.2.4. Level 4

At Level 4, bearer assertions (including cookies) shall not be used to
establish the identity of the Claimant to the RP. [ ** Establish, maybe no, but once the identity is established, what can we use to carry a session forward at level 4? These are separate questions. This also doesn't account for bearer assertions in the context of other information about the user. ** ] Assertions made by the
Verifier may however be used to bind keys or other attributes to an
identity. Holder-of-key assertions may be used, provided that all three
requirements below are met:

-   The Claimant authenticates to the Verifier using a Level 4 token (as
    described in Section 6) in a Level 4 authentication protocol (as
    described in Section 8).

-   The Verifier generates a holder-of-key assertion that references a
    key that is part of the Level 4 token (used to authenticate to
    the Verifier) or linked to it through a chain of trust, and;

-   The RP verifies that the Subscriber possesses the key that is
    referenced in the holder-of-key assertion using a Level 4 protocol
    (where the RP plays the role attributed to the Verifier by
    Section 8).

The RP should maintain records of the assertions it receives [ ** For how long? In what detail? This could be privacy leaking. ** ], so that if
a suspicious transaction occurs at the RP, the key asserted by the
Verifier may be compared to the value registered with the CSP. This
record keeping allows the RP to detect any attempt by the Verifier to
impersonate the Subscriber using fraudulent assertions and may also be
useful for preventing the Subscriber from repudiating various aspects of
the authentication process.

All Level 1-3 requirements for the protection of assertion data remain
in force at Level 4.
