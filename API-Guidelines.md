# Building connected digital services: API Guidelines

## Introduction

### About this guide
This guide is for anyone working to develop digital services for a public service, whether as part of the Ontario Public Service, a government agency, or beyond.

These guidelines are meant to be a roadmap, not a roadblock. They aim to help streamline digital service development for a more consistent and robust product for both developers and end users.

### What APIs can do
Application Programming Interfaces (APIs) let applications talk to each other in structured ways. Software developers create APIs to share some functionality or data from an application they've developed with anyone who might want to work with it.

For example, when you look at the weather app on your phone, the information you see is coming from an API built by your local weather service. Their API takes weather prediction data and converts it into a format that other app developers can use. This lets developers focus on building a user-friendly interface (for example, your phone's weather app) without having to worry about the science behind the data.

APIs can do more than share data; they can be the connective tissue between multiple related but independent systems. An agency—such as the Ministry of Transportation Ontario—that issues driver's licenses could build an API that takes a license number and checks whether it has expired. This API would be very useful for a car rental company that wants to verify that a customer has a valid license.

### Why you should care about APIs
APIs allow you to build reusable components and develop a platform, so that you don't have to reinvent the wheel every time. They are, in essence, the building blocks to a digital ecosystem. Understanding the value of APIs will help you shift your thinking into a digital first approach.

Sharing data and processes through APIs:

* reduces duplicated work
* encourages communication and learning between teams
* makes future application development more efficient

Following this guide will help ensure that your services are:

* interoperable with other platforms and services
* less likely to be locked in to a particular vendor or technology
* are more future proof and easier to update and test

For teams in the Ontario Public Service, APIs also make it easier for agencies to meet Ontario's [Open Data Directive](https://www.ontario.ca/page/ontarios-open-data-directive), which requires all government data to be made public, unless it is specifically exempt.

### Who this guide is for
You should read these guidelines if you are a:

* **executives**, **directors** and **managers** looking to deliver interoperable digital services
* **software developer** or **systems architect** looking for technical guidance
* **product manager** on an API product who needs to understand the context
* **business analyst** considering whether an API is a good solution for your problem
* **policy advisor** on a digital service looking to better understand how APIs can help fulfill policy goals
* **content designer**, **experience designer**, or a practitioner of any **other relevant discipline** who wants to familiarize themselves with the principles outlined here so they can add their perspective

### Standing on the shoulders of giants
We've adapted these guidelines for the Ontario Public Service from the excellent work of other digital governments, including:

* [Government of Canada](https://www.canada.ca/en/government/system/digital-government/modern-emerging-technologies/government-canada-standards-apis.html)
* [UK Digital Service](https://www.gov.uk/guidance/gds-api-technical-and-data-standards)
* [18F (the United States General Services Administration)](https://github.com/18F/api-standards)
* [Government of New Zealand](https://snapshot.ict.govt.nz/guidance-and-resources/standards-compliance/api-standard-and-guidelines/index.html)
* [Government of the State of Victoria, Australia](https://github.com/VictorianGovernment/api-design-standards)

## Business and process considerations
If you are building an API for the Ontario Public Service, you must follow the Government of Ontario's [Digital Service Standard](https://www.ontario.ca/page/digital-service-standard) (DSS). Even if you're not in the OPS, we still encourage you to become familiar with the DSS, which outlines 14 key principles for building good, user-centered services.

### Consume what you build
The best way to make sure your API design is good is to use it yourself within a production application. In the tech industry this is known as "eating your own dog food".

Always try to build your APIs in parallel with an internal use case that will integrate with the API before you publish it for external use. The internal use case can serve as a low-profile pilot project that you can use to validate your assumptions about how to design the API, and will allow you to pivot and adjust your design as necessary. It also forces you to think from the perspective of the user and their needs.

Make sure that the design of your API takes into account the different ways it might be used by your audience, including:

* internal OPS systems
* trusted partners
* the public

If you need to restrict an audience's access to certain components, build in user management capabilities instead of building multiple APIs. This approach will also highlight potential security issues from the beginning, when they can be addressed proactively.

### Talk to your users ([DSS #1](https://www.ontario.ca/page/digital-service-standard#section-1))
Work with the people who will be using the API to make sure that your architecture and design meet their needs. Engage user experience design experts to conduct research with:

* technical users
* business and program areas

APIs should be built to meet specific business requirements to solve concrete problems. If you don't know what user need the API is meeting, or you are simply building the API to expose data without knowing what it'll be used for, that's a good sign that the API may not be the right solution.

### Use open standards ([DSS #9](https://www.ontario.ca/page/digital-service-standard#section-9))
Wherever possible, build your API using open source tools, frameworks and standards. The open source communities that develop these tools work through collaboration and consensus-building, and participants range from individual contributors working in their free time to large technology companies. The diversity of voices ensures that tools aim for interoperability, security, reliability and accessibility. Plus, because these tools aren't tied to a particular vendor or system, you're sure not to exclude users from outside the OPS.

### Iterate frequently ([DSS #8](https://www.ontario.ca/page/digital-service-standard#section-8))
The Ontario Digital Service Standard includes [an agile approach to development](https://www.ontario.ca/page/digital-service-standard#section-8). This means building your application in "iterations" that improve one set of features at a time so you can:

* quickly test your service with real users
* prove or disprove your assumptions
* react faster to changing requirements, policy or technology

The easier it is to iterate on your API, the easier it will be for other developers to use.

### Practice privacy by design ([DSS #10](https://www.ontario.ca/page/digital-service-standard#section-10))
While it's important to minimize barriers to access to government programs, it's also important to secure any sensitive data and minimize the potential for data breaches.

Assess the data that will be shared through the API. When working with:

* non-sensitive data, build APIs that can be publicly used with minimal barriers
* sensitive data, put appropriate legal, privacy and security measures in place so data is not misused

Refer to the [seven principles of privacy by design](https://www.ryerson.ca/pbdce/certification/seven-foundational-principles-of-privacy-by-design/) for more guidance.

### Broadcast your intentions ([DSS #5](https://www.ontario.ca/page/digital-service-standard#section-5))
Keep your users updated on your plans for the API. Work with them to understand the impact of any major planned changes.

When releasing updates to an API that will break [backwards compatibility](#use-semantic-versioning) and require your developer partners to update their code, make sure to define and communicate clear deprecation timelines. This lets developers migrate to the new version before the old version they're using is taken offline, and avoids disrupting their work.

Make sure that every API has at least one designated point of contact for the teams using it:

* all APIs need a published support email account
* high-criticality APIs also need a published phone number
* ideally, publish a status page where users can find planned and unplanned outages and the latest information about the API's availability and status

### Make sure you actually need an API
APIs are one of many ways to integrate data and functions between systems, but they are not always the best or only solution. If you need to archive a large amount of complex data relationships once a year, you might prefer a [bulk data transfer system](https://en.wikipedia.org/wiki/File_transfer). On the other hand, if the client application and the server are unlikely to be online at the same time and they need to communicate asynchronously, a [messaging queue](https://aws.amazon.com/message-queue/) might be a better solution. APIs are most useful if you're supporting real-time system interactions and data access.

## Technical considerations
### Design stateless APIs
Every call to the API must contain all the information required to fulfill that request, without expecting the server to remember anything about any previous requests or contexts. This is known as stateless design.

Do not store information about session states on the API server. Any sort of state management—for example, in the form of cookies or session IDs—must be maintained by the client sending the request. This makes it easier for your API to detect and recover from errors, as each error is contained within a single request and does not involve the entire state of the server.

Stateless API design also improves the scalability of your server, since processing resources can be quickly freed up for each request, without needing to maintain a cache of incomplete transactions.

### Be RESTful if possible
For the vast majority of use cases, we recommend [RESTful](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) API design. Representational State Transfer (REST) is the leading standard for integration with cloud services, and is also the standard set by the majority of other Governments with mature API programs. Follow industry [ best practices](https://restfulapi.net/) when designing and developing your RESTful API. In particular:

#### Represent resources as URLs
Each URL endpoint in a RESTful API design should represent an entity, resource, or business object. For example, a ServiceOntario (SO) API could provide endpoints to see information about a single SO location:

* **DO**: `api.ontario.ca/offices/location/college-park`

Do not use endpoints to perform operations on those entities or objects. This also means that your URL patterns should be composed of nouns, not verbs.

* **DON'T**: `api.ontario.ca/getOpeningHours/college-park`

#### Use URIs to identify resources
If response data includes references to other resources in the API, include a full URL to the endpoint for that resource. This will allow the user to follow data references for future operations with minimal effort.

If data is returned as a part of a response, use Uniform Resource Identifiers (URIs) to uniquely identify each data resource. This will allow the client or consuming system to directly refer to that data for future operations with minimal rework.

For example, an endpoint that provides information about ServiceOntario locations close to a specific address should link directly to endpoints for each of those locations, instead of just listing the names.

* **DO**:
```
{
  nearby: [{
    name: "University Avenue",
    url: "api.ontario.ca/location/university-ave"
   }]
  }
```

* **DON'T**:
```
{
  nearby: ["University Avenue"]
}
```

#### Return data as JSON
Use JavaScript Object Notation ([JSON](https://www.json.org/)) and other JSON-based representations (such as [JSON-LD](https://json-ld.org/)) to transmit data between a client and a server. Responses that the API sends to the client should be formed as objects, and not as arrays. Arrays are not robust enough for including adequate metadata about the result object and can make it more difficult to iterate on the data design.

For example, an endpoint that lists all ServiceOntario locations should include information about how many there are.

* **DO:**
```
{
  total: 234
  locations: [ ... ]
}
```

* **DONT:**
```
[
  { id: university-ave ... },
  { id: college-park ... }
]
```

Make sure the design of your data objects is predictable and easy to use. Follow a consistent grammar case for naming object keys, and do not use live data to create dynamic object keys.

#### Do not overload HTTP request methods
Each [HTTP request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) (also known as an *HTTP verb*) should represent a *single* operation on a given resource or list of resources. Don't use request parameters to define additional operations; for example, don't use GET to do anything other than retrieving data. The following are idiomatic uses of HTTP verbs in the context of a RESTful API:

* `GET` – get a resource
* `POST` – create a new resource
* `PUT` – update or replace an existing resource
* `DELETE` – remove a resource

You may also hear these referred to as `CRUD` (Create, Read, Update, Delete) operations.

#### Use standard acceptance headers
Any negotiation between the client and the server about what kind of data is being requested must be performed using [HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). ACCEPT and CONTENT-TYPE request headers are mandatory, and AUTHORIZATION headers are mandatory for secured APIs. API keys must be passed in the header instead of in the request URL.

If your API supports multiple languages, the ACCEPT-LANGUAGE header must be sent by the client, and the server must return content in the requested language. If a language header is not set for a multilingual system, content in all supported languages should be returned. Different languages should be nested under [BCP-47 language codes](https://tools.ietf.org/html/bcp47) (e.g. "en", "fr") as object keys. The returned response data must, at a minimum, contain the CONTENT-TYPE header.

#### Use standardized error codes
Use standard [ HTTP status codes](https://restfulapi.net/http-status-codes/) when building RESTful APIs. Conform to [ SOAP 1.2 faults](http://www.w3.org/TR/soap12-part1/#soapfault) when building SOAP APIs. Avoid building custom error codes and data schemes, which require more work by the client to parse.

#### Alternatives to REST
RESTful APIs will not be the best solution for every business problem, especially if there are technical constraints on either the provider or consumer sides. Here are some examples of alternative API architectures you can consider:

##### SOAP
[Simple Object Access Protocol (SOAP)](https://en.wikipedia.org/wiki/SOAP) is a protocol for exchanging structured information over a network, most typically [Extensible Markup Language (XML)](https://en.wikipedia.org/wiki/XML) over HTTP. The standards are more stringent and have more implementation overhead than RESTful systems. This could be beneficial if you have compliance requirements. SOAP implementations should follow [ SOAP 1.2 specifications](http://www.w3.org/TR/soap12-part1/) and be [ WS-I Basic Profile 2.0](http://ws-i.org/profiles/BasicProfile-2.0-2010-11-09.html) compliant.

More guidance for using SOAP in the OPS is available in [GO-ITS 24.0: Omnibus Web Services Standard](https://www.ontario.ca/document/go-its-240-omnibus-web-services-standard).

##### GraphQL
[GraphQL](https://en.wikipedia.org/wiki/GraphQL) is a query language for building APIs designed to operate over a single endpoint. GraphQL requires the consumer to define the structure of the data that they want from the provider, which provides more granular control over data formats and more detailed analytics. GraphQL implementations should follow [industry best practices](https://graphql.org/learn/best-practices/).

##### RPC
[Remote Procedure Call (RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call) is a style of API design that focuses on operations (i.e. procedures) rather than resources. The consumer accesses endpoints that directly invoke a given function on the provider's server. This style of API design is best used if more complex interactions beyond CRUD (create, read, update, delete) are required. It is frequently used in conjunction with RESTful API design, though this is not strictly necessary.

##### gRPC
[gRPC](https://grpc.io/) is an open source RPC system initially developed by Google. It uses a different serialization protocol than most HTTP APIs which improves the communication speed of requests. It generally is used internally between microservices, as it requires a defined contract (a .proto file) between services.

### Design meaningful data structures
The design of the data structures that power the backend of the API can be just as important as the design of the software architecture of the API itself. Be thoughtful about how to structure the data that the API returns to the client. Consistent metadata and encoding ensure that APIs are interoperable both within and across organizations, and clearly structured response data is easier for the client to manipulate.

#### Use descriptive data schemas
Do not use generic data structures such as key-value pairs or generic fields. The constraints of a given data object should be apparent when reading the schema definition for that object type. Refer to [Schema.org](https://schema.org/) to see examples of well-designed data schemas.

#### Use industry-standard information models for your discipline
Avoid defining your own information model wherever possible. Instead, consider your business needs and see what information models other practitioners in your industry are using; for example, you might use [HL7](https://www.hl7.org/) for health data, or [GTFS](https://developers.google.com/transit/gtfs/) for transit data. If you *must* define your own information model, create a model that doesn't rely on a particular technology or platform and avoid getting locked into any particular vendor.

If you're a developer within the Ontario Public Service, you can also refer to the following internal resources on information architecture:

* [Standards for Developing Architecture](https://intra.ontario.ca/iit/standards-for-developing-architecture)
* [Common Elements Data Model - Party LDM](https://intra.ontario.ca/wordpress/uploads/2017/05/CDEM-Party-LDM-v2.5.pdf)
* [Common Data Elements - Address LDM](https://intra.ontario.ca/wordpress/uploads/2017/08/CDEM-Address-LDM-v2.3.pdf)
* [GO-ITS 56.3 Information Modelling Standards Handbook](http://www.ontario.ca/government/go-its-563-information-modeling-handbook-imh-appendices)

#### Abstract your raw data structures
Do not expose raw data from your backend systems to end users. All data should go through a transformation phase so that unnecessary details are abstracted away and the resulting data object is designed for that business case. Exposing raw data structures can expose information about your internal operations and create security vulnerabilities. If you must expose raw data, *only* do so for open data, reporting and statistical APIs.

For example, a transactional API that tracks purchase orders might sit on top of a database with confidential information about vendors. This information should be stripped out along with any other unnecessary data, so that the user only sees the order number and status.

#### Omit debugging data
All response data should be meaningful to the client, and should not expose any technical details that the developer might need for debugging. Do not include internal technical errors, thread dumps, process identifiers, or error messages within response data, even if the API call is unsuccessful. Exposing this information in a production environment can have major security implications. Instead, invest in a robust [logging system](#log-activity-and-performance).

#### Be clear about your data encoding
Use Unicode Transformation Format-8 ([UTF-8](http://unicode.org/faq/utf_bom.html#utf8-1)) as the standard encoding type for all text and textual representations of data through APIs. If technical or business constraints require the use of an encoding standard other than UTF-8, clearly identify the standard in the charset response header and API documentation.

#### Use consistent date-time format
Follow the international standard [ISO 8601](https://www.iso.org/standard/40874.html) in Coordinated Universal Time ([UTC](https://www.timeanddate.com/time/aboututc.html)) for standard datetime fields in data returned by the API. The date format is `<yyyy-mm-dd>`, and the timestamp format is `<yyyy-mm-dd>T<hh:mm:ss>Z` in 24-hour time. This allows for the same date representation in both official languages. Any other representation of time in the source data must be converted to this format by the API.

### Iterate thoughtfully
Take care to minimize the impact of your agile and iterative development on users so that they don't experience unnecessary or unexpected disruptions.

#### Use semantic versioning
Every released update to an API, no matter how small, must be tagged with a new version number in your version control system. Follow the [semantic versioning standard](https://semver.org/) to clearly signal the scope of each release and whether it is likely to break backwards compatibility. Each release should be tagged with `v<major>.<minor>.<patch>` (for example, `v2.3.1`). Major releases are the *only* releases that should introduce significant changes that may break backwards compatibility. Minor releases should indicate new backwards-compatible functionality or optional attributes, whereas patches should only be bug fixes or optimizations that do not impact how the API functions.

#### Indicate major version in URL
The major version of your API should be indicated in the URL of RESTful APIs, for example, api.ontario.ca/v3/endpoint. This makes it easier to support legacy versions of an API concurrently with the most recent version when releasing a major change that will break backwards compatibility. Do not pass versions as parameters or request headers.

#### Deprecate gracefully
Support at least one previous major version during a transition period to ensure that your users have enough notice to migrate their work, and communicate your development roadmaps with your users. For example, in a RESTful system, you can use the HTTP [Warning header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) to announce upcoming changes.

#### Test continuously
You should adopt Continuous Integration and Delivery (CI/CD) supported by automation tools and integrated security testing. This creates a safety net that enables fast iteration, and is the first step on a pathway towards [DevOps automation](https://aws.amazon.com/devops/what-is-devops/). DevOps is an organizational philosophy and culture that tightly integrates deployment, operations, and security with day-to-day development for maximum efficiency and quality.

Make sure your testing suite includes unit tests, integration tests and end-to-end tests. These should measure performance under a condition of average load while also identifying performance thresholds beyond which the API becomes unstable. Don't just test under ideal conditions.

For example, if you're testing multiple components that talk to each other, make sure your end-to-end test is taking place in a live environment to get the most accurate latency information. Watch "[Avoiding Microservice Megadisasters - Jimmy Bogard](https://www.youtube.com/watch?v=gfh-VCTwMw8)" to see why this is a worthwhile practice.

### Practice security by design
Even if your API does not expose protected or privileged data, it is still important to consider how to embed secure architecture design into your system. Not only is this good practice, it will also future-proof your API for future development. The following guidelines should be considered a *baseline* of security controls. Additional controls (for example, message-level encryption, mutual authentication and digital signatures) may also be required based on the sensitivity level of the data.

Refer to the [ten principles of security by design](https://www.owasp.org/index.php/Security_by_Design_Principles) laid out by the Open Web Application Security Project for further guidance.

#### Enforce secure communication
Never send or store sensitive data in plaintext. Avoid using insecure or unencrypted connection wherever possible, even with non-sensitive data.

* Sensitive data must be sent over TLS version 1.2 or later, and all certificates must be SHA-256 with a minimum key length of 2048.
* Insecure traffic sent over HTTP should be rejected instead of automatically redirecting to HTTPS. Follow the cybersecurity standards from the [Government of Ontario Information Technology Standards (GO-ITS)](https://www.ontario.ca/page/information-technology-standards#section-6) where relevant, or consult the [Canadian Centre for Cyber Security](https://cyber.gc.ca/en/directives).

#### Do not put sensitive data in request URLs
Never accept sensitive data in URL or query strings, including API keys. The client must send this information via HTTP header or a JSON message payload so it can be properly encrypted. Even with transport encryption, URL strings can be tracked and compromised.

#### Have a clearly-defined access policy
Always authenticate, authorize, and validate any incoming request. With the exception of public open data APIs, all APIs should implement key-based authorization controls. APIs must only permit access for valid API keys and restrict access otherwise. You may need to consider other approaches to manage abuse, including rate limiting by IP address.

Disable any unused HTTP verbs, and reject invalid requests to these endpoints. If relevant, use industry standards such as [ OpenID Connect](http://openid.net/connect/) and Open Authorization 2.0 ([OAuth 2.0](https://oauth.net/2/)) as an authentication protocol for RESTful APIs. Use Security Assertion Markup Language 2.0 ([SAML 2.0](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)) for SOAP APIs.

#### Implement token management
We strongly recommend token-based authentication. Ideally, use an open industry-standard token.

* [JSON Web Token (JWT)](https://jwt.io/) for RESTful APIs
* [WS-Security SAML Token Profile](http://docs.oasis-open.org/wss-m/wss/v1.1.1/wss-SAMLTokenProfile-v1.1.1.html) for SOAP APIs

Avoid vendor proprietary token schemes, and do not attempt to create a custom token scheme from scratch. All tokens must expire within a reasonable amount of time, depending on security requirements. For example, token used for rate limiting may have a longer expiry time than tokens used for authentication. In the case of SAML, the assertion expiry must control the validity of the entire authentication and authorization session.

#### Build internal security expertise around potential threat vectors
There are many different ways of attacking and compromising an API. These are known as threat vectors. As it is impossible to cover all of them in this guide, it is important for each development team to develop an internal intuition and expertise around potential threats, and to design your API to be resilient for your specific needs.

Some of the most common API attacks include:

* [Injection attacks](https://cheatsheetseries.owasp.org/cheatsheets/Injection_Prevention_Cheat_Sheet.html#introduction) involve attackers sending malformed input to the API with the intention of exposing security flaws. Some of the most prominent forms of this attack include SQL injection and XPath requests against XML. These can be partially mitigated with input validation.
* [Replay attacks](https://auth0.com/docs/security/common-threats#replay-attacks) involve attackers copying a valid user request and masquerading as that user. Depending on the level of access the user had, this could result in attackers viewing and destroying private data. These can be partially mitigated with short token expiry times, blacklisting used tokens, and one-time passwords.

### Validate user input
Any user input should be validated as soon as it is received, so that only properly formed and sanitized data is processed by your API. This will make your API more secure and also mitigate errors from malformed requests.

#### Define clear request parameters
Define what an appropriate request to your API looks like, including request size limit, content type, and range and format of any specific fields. If you are accepting string inputs, consider constraining these (for example, using regular expressions).

#### Restrict open queries
Dynamic and open queries not only constitute a dangerous threat vector, but they can also overly consume processing resources. Invest effort upfront to identify all the valid query uses cases and design the API to specifically meet them. If you must allow users to inject open query strings or objects into an API, these should be limited to open data, reporting, and statistical API only. Never permit open queries into an API with master data or with transactional APIs or business APIs. GraphQL can be used for statistical, analytics, and reporting purposes, but should not be used to support business transactions.

#### Be cautious about wildcard characters
Wildcards in APIs can be dangerous from a performance perspective. If wildcard characters are allowed, ensure there are restrictions on which and how many parameters can have wildcard input to prevent large data query sizes. Err on the side of rejecting a query with too many wildcards rather than risk timing out your database on the backend.

#### Don't over-validate
Before validating input, make sure the assumptions you're making about your user data are universally true. For example:

* Names are not always "First M Last": [Falsehoods programmers believe about names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)
* Days aren't always exactly 24 hours: [Falsehoods programmers believe about time](https://infiniteundo.com/post/25326999628/falsehoods-programmers-believe-about-time)
* Email addresses can have surprising characters: [I Knew How To Validate An Email Address Until I Read The RFC](https://haacked.com/archive/2007/08/21/i-knew-how-to-validate-an-email-address-until-i.aspx/)

### Log activity and performance
Good metrics form the basis of good evidence-based decision-making. Logs can provide information about attempted attacks, aid in post-mortem analyses, assess system performance, and suggest areas of product or feature improvement.

#### Define performance measurements
Different applications have different definitions of success. Rather than using the same benchmarks for every API, identify your key performance indicators prior to launch, and design measurement instruments that target those indicators specifically. Latency and response time will tell you different things about your API than user growth.

#### Maintain meaningful logs
All access to APIs should be tracked using industry logging standards (such as [common event format](https://help.deepsecurity.trendmicro.com/Events-Alerts/syslog-parsing.html)). If relevant, follow the logging requirements in [GO-ITS 25.0 General Security Requirements](https://www.ontario.ca/page/go-its-250-general-security-requirements) (3.4.2 and 3.4.3) and [GO-ITS 25.13 Security Requirements for Web Applications](https://www.ontario.ca/page/go-its-2513-security-requirements-web-applications) (section 2.9). These logs should be integrated centrally, and must include as a minimum both system and individual identifiers of the requesting client, as well as the timestamp. Ensure you don't inadvertently log confidential information (e.g. passwords).

#### Review logs regularly
API logs should be reviewed on a regular basis to monitor for suspicious usage or access patterns, such as after-hours requests, an unusually large volume of requests, or repeated input validation failures. Suspicious events must be sent to the Cyber Security Operations Centre, Cyber Security Division, Ministry of Government and Consumer Services.

#### Audit sensitive access
If your API provides personal or sensitive data, you must log when the data was accessed and by whom. This is needed in order to respond to data subject access requests, and will also help detect fraud or misuse. Consult your legal department for requirements on data retention and data custody policies.

### Optimize performance
To ensure that your API can serve the needs of all users, carefully consider the size of each payload and the rate of responses. API performance should be benchmarked periodically to ensure you are continually meeting existing and projected business needs.

#### Monitor and test performance
It is important for your API to return results quickly and consistently. While speed is not the only metric that matters, [user experience research](https://www.nngroup.com/articles/powers-of-10-time-scales-in-ux/) suggests that a response time of 0.1 second (100ms) make users to feel like they're directly interacting with the system, while response times greater than 1 second are perceived as a noticeable slowdown. We recommend that you aim for a response time of at least 200ms, preferably 50ms.

To achieve this, you should monitor ongoing performance and run regular performance tests to determine the response time and throughput. See section [Test continuously](#test-continuously).

#### Rate limit user access where appropriate
[Rate limiting](https://apisyouwonthate.com/blog/what-is-api-rate-limiting-all-about) is a good way of managing the amount of computing resources that an API requires. If widespread adoption of an API is expected or server costs are a concern, consider rate limiting each user based on how frequently they can call to the API, how much data they can request at once, or how many connections can live at once.

Rate limiting also provides increases security by preventing a malicious actor from overloading the API with too many requests through a denial-of-service attack while making sure the system is kept available to all users. If the limit is exceeded, a standard HTTP 429 error can be returned.

#### Implement pagination and data segmentation
APIs exposing large datasets must support some form of data segmentation, both for the sake of optimizing the performance of the API and for a better user experience. The following are some common patterns for pagination along with appropriate use cases:

* `page` and `per_page` are most appropriate when the dataset does not update frequently and the same set of data is likely to be returned given the same page reference over time, e.g. historical or reference data.
* `offset` and `limit` are most appropriate for frequently updated data where users are likely to want to see data points older than (*offset* by) a given reference point, e.g. skipping past new articles you've already read.
* `since` and `limit` are most appropriate for frequently updated data where users are likely to want to see new data points added *since*a given reference point, e.g. seeing all new content since your last visit.

#### Apply special cases for bulk data sets
There will be scenarios where APIs will need to be involved in making bulk datasets available between systems or to the public. In those scenarios, consider the following:

* Smaller datasets should be returned in low overhead formats (e.g., CSV or JSON) rather than XML. Compressed file attachments should be avoided, especially when consuming external APIs, as they may conceal malicious content.
* Trigger APIs initiate ("trigger") resource-heavy actions that are then carried out by a different system. They can start or stop events such as managed file transfers, which is more efficient than using the API to transfer the entire dataset.
* Search-and-link APIs are best used to index existing file servers. These APIs return links to specific files, rather than the contents of those files.

#### Define a caching policy
If your API serves up data that is frequently requested but infrequently changed, consider implementing a response cache that stores the response to a GET request on a unique resource for quick retrieval.

Caching best practices:

* Consider using [key-based cache expiration](https://signalvnoise.com/posts/3113-how-key-based-cache-expiration-works) to avoid serving stale objects
* Ensure that the cache is monitored to keep stale objects at a minimum
* Ensure that the server has sufficient memory to handle caching loads
* Be careful when caching non-public data to avoid inadvertently serving it to unauthorized users

### Documentation
Each API must be accompanied by concise and up-to-date documentation on how to consume that API. The following practices help ensure APIs are documented appropriately without incurring the excess burden of managing companion documentation.

#### Document both API specs and use cases
Your documentation should include:

* the technical specifications or contract of the API
* how developers can use your API, including configuration, [authentication](#have-a-clearly-defined-access-policy) and [rate-limiting](#rate-limit-user-access-where-appropriate)
* information about API availability, [versioning](#use-semantic-versioning), and incident management
* [point of contact](#broadcast-your-intentions-dss-5) and a way for users to stay up-to-date with planned changes

One effective way to help users get started quickly with your API is to publish code that makes use of it, such as test cases and validation data. See section on [testing continuously](#test-continuously). Example source code can be released on the [OPS Github Account](https://github.com/ongov).

#### Use OpenAPI for RESTful APIs
Use the [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification) for RESTful APIs, which will create a machine-readable interface specification. There are open source tools (e.g., [Swagger](https://swagger.io/solutions/api-documentation/)) which can then generate human-readable documentation from this specification, which avoids the need to create and maintain separate documentation.

#### WSDLs for SOAP
Each SOAP API must be accompanied with a Web Services Description Language ([WSDL](http://www.w3.org/TR/2007/REC-wsdl20-primer-20070626/)) contract. The WSDL is a machine-readable specification which allows the API consumer developer to generate the consumer code.

#### Don't over-document
Following the "[eat your own dog food](#consume-what-you-build)" principle, you should document the API to the degree that the documentation helps you and others build on the API, but not to the degree that the documentation is likely to become obtuse and obsolete.

## Future considerations
One of the underlying principles of agile development is not to let the perfect become the enemy of the good. It is important to empower teams to deliver a solid minimum-viable service that is secure, robust, and scalable, without getting overly ambitious about nice-to-have features that delay launch and prevent real users from testing your service. Here are some additional things you should consider as you iterate your API and develop new features.

### Use an API Catalogue
All APIs should be published to some sort of catalogue or inventory. Such an inventory can be a central repository of metadata and documentation, a lifecycle management point of contact for developers, and a portal for discovery for new users. This catalogue can also be integrated with a full-featured API gateway that directly manages the flow of traffic of the API, providing additional user management capabilities and security controls. Refer to the [API Store of the Federal Government of Canada](https://api.canada.ca/en/homepage/) or the [NASA API Portal](https://api.nasa.gov/) for examples of how this might look.

Contact the Ontario Digital Service for more information on the status of an API catalogue for the Ontario Public Service.

### Define a Service Level Agreement
Ideally, each API should be accompanied by a clearly defined Service Level Agreement (SLA), defining the following features:

* Support hours (e.g., 24/7, 9/5, coast to coast business hours)
* Service availability (e.g., 99%)
* Support response time (e.g., within the hour, 24 hours, best effort)
* Scheduled outages (e.g., nightly, weekly, every 2nd Sunday evening)
* Throughput limit (e.g., 100 requests per second per consumer)
* Message size limit (e.g., <1Mb per request)

### Publish source code and tests
Publishing the source code for your API as open source has many benefits:

* Allows a wider community of developers to spot potential problems with the code
* Improves government transparency and accountability
* Empowers other government departments to solve similar problems without reinventing the wheel
* Contributes back to the open source community whose labour the government is benefiting from
* Signals the technical expertise of the public service, which helps attract talent

Even if you never intend on open sourcing your code, it is good practice to develop as though it will be scrutinized by the public. This can often provide an easy high-level overview of whether there are any gaping security holes.
