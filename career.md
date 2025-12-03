[me](README.md)

# Career

I'll now go into some high level details for all the projects I have worked on professionally. I'm omitting
some things, even though it may appear I am not.

Notable Professional Projects:
- [Secure-ish Boot](#secure-ish-boot-anti-cloning)
- [Secure Feature Enablement](#feature-enablement)
- [Low-Level Tooling and OS Abstraction](#tooling)
- [Secure Utility Infrastructure](#utility-infrastructure)
- [OpenGL ES on an RTOS](#mbx-on-vxworks-5x)
- [Data Aggregation and Warehousing](#core-product)
- [Application and Data Migration](#invoicing-migration)
- [Kafka](#kafka)
- [Other Duties](#other-duties)

## Independent

I didn't plan on taking jobs this young, but one came up.

### NSAC

This was a local college. A teacher in the technology department found me on a *nix BBS.

#### showtime

This was a project I worked on for the multimedia department of a local college. It was a simple C
program that displayed the time of the next show. The time moved around the screen and scaled itself
along the x and y axis so that it looked kind of 'alive'. Turns out the money bug didn't bite me,
I didn't really look for more paid software work for a long time.

## Mount Allison University

This was my university.

### Algebra Master

Algebra Master was an engine capable of determining if two equations in a ring were equivalent. The ring
needed not be commutative. This was a challenging project and we tackled it in C++. You could define a set of
relationships/equations and then ask about another equation given the constraints of the set.

## Gurza

I worked here fresh out of university, and got roped into too much effort for too little return.

### 3PL

Gurza was a customs brokerage warehouse that needed a system to provide logistics upon receipt. What this
means is that they needed to be able to account for their receipt of product, in an automated way. I built
a crude system that was able to scan bar codes using a Symbol scanner (at the time this brand was superior in
terms of scanning accuracy) and save them to a spreadsheet. I had no prior experience device hacking and
figuring out what to do with the scanner was a challenge for me. This would have been welcome, except that I
also agreed to be the IT manager at this company. This meant I was responsible for the computing experience
of the office workers, and it was not a smooth one. Back to the project - I used a ruby script to parse the
spreadsheet and verify against another list that came from the sender to look for discrepancies. One thing
I will say about this, was that the manufacturer was sending palettes of product with a printed page of
bar codes (one code per product) and this seems ridiculous. It would have made far more sense to scan one bar
code per palette.

## Certicom

Certicom was a leader in [ECC](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) technology. They
developed about a hundred patents before I arrived, surrounding efficient implementations on different types
of hardware and also cryptographic design. They were independent from Blackberry/RIM when I started, and this
is actually why I left. I refused to sign RIM's intellectual property agreement. It basically said that any
idea I had while employed was to be owned by them, regardless of where or when I had this idea. No thanks. I
was the only one who refused.

I worked on the Professional Services team designing and implementing solutions using ECC that required some
of the highest grades of security. Read on for details.

### Secure(-ish) Boot (Anti-Cloning)

I took over design and implementation of a very elaborate secure boot/device provisioning project when I
started at Certicom. It wasn't true security, but it was the best we could do given the constraints we were
provided. This is typical of a security solution. There are always tradeoffs and it basically boils down to
normalizing the factors (risk, cost/impact) of each attack vector and then multiplying them together. Then,
the client picks a price point that makes sense in their business model and we determine how much it will
take to implement everything that multiplies out to a cost higher than they are willing to pay. Sales and
lawyers are involved, and we mutually decide how to proceed. In this case, the client wanted to protect a
product (and more importantly its software) from being copied. Full disk encryption was employed in this solution.

To accomplish this, I had to:
- Hack the BIOS (this was pretty cool and I still have my Willem EPROM programmer - I believe my friend paid
for it =) ) and implement both AES (I forget the mode but probably one that only requires a single cipher 
method) and SHA256 in x86 Assembly, in a single block (512 bytes).
- Develop a method to easily provision/encrypt these devices with unique keys.
- Bring the system up from POST (at the time [bochs](https://bochs.sourceforge.io/) was the tool I used to
learn how to do this - but the VM scene has exploded since then, so you can take your pick now).
- Integrate with (reverse engineer) a real-mode full-disk encryption driver that wasn't producing correct
results (anyone who has worked in security understands this means it produced undebuggable garbage), in
assembly. I made a binary patch to fix it.
- Bootstrap the Windows kernel with a tiny Linux kernel.
- Reverse engineer NTFS (yes, they wanted to use Windows as a platform).
- Develop a secure challenge-response mechanism that allowed service techs to work on the product on-site,
without necessarily having network access.

This never went to market. It worked fine, though it would definitely have been broken. Anyone with an EPROM
reader could eventually figure out how I obfuscated keying data in the BIOS itself.

### Satellite Contributions

I put some code in a satellite though I can't recall at all what it did. I got a spec and was told to make it
fast, so I used bit magic in C to make it hella fast. I think it was a message authentication mechanism. This
code will likely live for a long time.

### Feature Enablement

This was a project that allowed a chipset to be endowed with varying degrees of feature capability, predicated
on a grant provided by the chipset manufacturer. For example, you may buy a CPU that is identical to your
friend's, but theirs can perform operations yours can't because they were issued a grant (they paid for an
upgrade) that allowed those operations to execute.

I needed to:
- Design and implement a client library to communicate with the server that was capable of requesting
signatures securely
- Assist in building and provisioning physical appliances
- Configure the operating system the server was deployed on
- Implement the server itself, which interacted with an [HSM](https://en.wikipedia.org/wiki/Hardware_security_module)
to store signing keys and create signatures
- Write tools to securely provision and manage the HSM (using N of M key splitting, hardware tokens and
multiple security officers)

This was pretty fun to execute. I remember demoing the otherwise clean server code with a tight loop in it. =)
This solution was deployed but I'm not sure the concept caught on.

### Tooling

I helped create a C abstraction that allowed professional services to move much faster. We build a toolkit
that abstracted pretty much everything the OS is responsible for in a consistent interface. [This](https://github.com/jasoncolburne/red)
is a taste of what that looks like.

I also built a system to generate RPC client/server code from YAML (I may not make that choice again). It
allowed us to define messages that were easy to evolve. Anyone who has written networking code in C
understands how much encoding and decoding goes on, it's all pointer addition here and offsets there. It's
fairly easy to make a mistake, and changes can be a nightmare. By generating libraries for both sides of the
communication, I was able to provide a superior developer experience and in the end we produced higher quality
code at a faster pace.

### Utility Infrastructure

This was a set of highly complex projects. I was jointly responsible for the overall system design and
implemented most of it with a partner. We got our initial design from the client, they had a strong engineer
that had thought a lot about their problem. The needed help with figuring out some of the ECC details
and we were able to provide tech that wasn't available from other vendors that significantly reduced their
power footprint.

We needed to provide confidentiality and integrity of data and control plane commands while validating the
identity of both sender and receiver.

Possible vectors of attack to consider:
- Injecting a command that appears to be from the control plane that say, causes rolling brownouts or shuts
down a hospital's power.
- Surveilling end user data to determine an appropriate time of day to mount a physical intrusion leveraging
information leakage due to inactivity (the attacker can infer when you are not home).
- There were more. I'd have to sit around and ponder to come up with them all again.

In these projects, I:

- Redesigned and improved the original security model through iteration
- Designed and implemented a signing solution similar to the feature enablement project, but this time
decoupled from the application domain. It was highly modular and horizontally scalable.
- Integrated the tooling developed above to prove its value
- Developed custom HSM software, an [FM](https://www.thalesdocs.com/gphsm/luna/7.4/docs/pci/Content/administration/fms/fms.htm)
that provided secure storage and custom ECC routines (then unavailable out of box). I believe I implemented
a crude version of TAR for the internal filesystem to manage the data produced by our libraries. I also had
to create tooling and provide a path for upgrading the FM software itself, in a trusted way. This was fun.
- Consulted with another developer working on the other half of the solution, a high speed encryption server
that could cipher data from every node of the mesh network using a per-node symmetric key.
- Wrote and debugged threaded code.
- Helped build some appliances.
- Helped solve a distributed consensus problem.

This solution is deployed around the world.

### Hostile Deployment of Secure, Trusted Boot

In this project, the goal was to secure a casino table against tampering/unfair observation by casino
customers and malicious operators.

In this solution, I was:
- Leveraging new TPM technology to provide trusted boot.

This project didn't last long, as RIM purchased Certicom as I was in New York at a client meeting for this
very project. They canned it and threw up a ton of red tape around any type of professional services work.
I'm glad I left. If you want to see how this should be implemented, [this](https://github.com/jasoncolburne/homelab/blob/main/switch.md)
is a start. I need to audit the permissions on the entire filesystem next, then I need to upgrade the
security where possible. As an example, I think I installed a 2048-bit RSA cert that is valid for 100 years
as my Machine Owner key. I can swap it easily I think, but I really just wanted to make it work. I will read
the manual later and see if ECDSA is supported ;).

## Nerdgames

This was a company I started with 3 other friends. We made mobile applications/games when the Apple App Store
was first a thing.

### Stuntcopter

Stuntcopter was our first project and it was a remake of a [classic game](https://en.wikipedia.org/wiki/Stunt_Copter)

In this project I:
- Implemented, from scratch, game logic and physical controls. Of note was the accelerometer-based helicopter
control, it was responsive and smoothed out some jerk.
- Integrated existing image and sound assets into the project.
- Learned the App Store submission process (this was a long time ago).

### Pow

This was a novelty app that used the accelerometer to sense a punching motion. It made sound effects similar
to the 1960s Batman television series, and had a soundtrack. When you used it, it would create a stylized
graphic on the screen that said 'Kapow!' or one of the other words ('Sock!', 'Biff!', etc) in random but
complementary colours.

In this project I:
- Designed and implemented the control logic.
- Integrated assets.
- Created music assets.

### iBubbly

This was an app that simulated pouring champagne out of a bottle by tipping the iphone. It was actually a
multi-user app, and you could pour from one phone into a glass on another.

In this project I:
- Designed and implemented the physics the simulated the bubbles and liquid.
- Wrote client/server code (I can't recall if we used wi-fi or bluetooth).
- Integrated with the accelerometer.
- Integrated assets.

### iTalkie

This was a radio application that allowed multiple people on the same channel to communicate with each other.
It was never completed. It worked, just not well. We used bluetooth and I found it to be a bit unreliable at
the time.

In this project I:
- Designed the solution.
- Integrated with bluetooth for discovery and communication.
- Integrated with the audio subsystem.

## Redbeard Enterprises

Redbeard is a company that I started to consult with.

### Webdiligence

Webdiligence was a client I interacted with occasionally for small jobs.

#### iSnipe

[iSnipe](https://apprecs.com/ios/297093432/isnipe) is an iPhone application that is meant to accompany a
recreational shooter.

I worked on some of the iOS code and took a look at the ballistics engine but didn't contribute in that
meaningful a way.

### ALT

ALT was a client of mine that specialized in embedded OpenGL drivers. I did a project and a half for them
before putting consulting on pause to try Amazon out.

#### MBX on VxWorks 5.x

I needed to make OpenGL ES work on the MBX chipset (used by one of the 3 model iPhones) on top of an RTOS
named VxWorks. The code ended up in an automobile.

To do this, I had to:

- Port a reference driver from Linux to VxWorks
- Make it compile.
- Make it behave correctly.
- Help the client integrate with the library.

This kind of development can be painful. The tooling was only available in Windows, and it's a bit like
security in that when things don't work, sometimes there is nothing to debug - there is just no output. I
recall spending a long time trying to figure out why nothing worked, only to realize that valloc() didn't
behave the same way on VxWorks as it did in Linux. This difference caused the VxWorks allocation not to be
page aligned, which caused the chipset to fail silently.

#### ATI 4850, PMC configuration on VxWorks 6.x running Xorg 

This was an ambitious project. I didn't have the experience to understand at that time, but it was probably
lucky that I went to Amazon during this project. I was leading it, and had two team members, and it would have
fallen on me to make sure we met our goals. I had estimated the project as if there would be three of me
working, and this isn't correct. This was going to go in a tank. Not sure if it ever made it there.

I had to:

- Port a reference driver from Linux to VxWorks 6.x.
- Port Xorg to VxWorks (!).
- Develop example code.

## Amazon

I worked at Amazon for about 9 months before deciding it was not for me. I wrote a ton of code but in the
end my personal life took precedence and I had to leave Seattle. I did various tasks but I'll describe the
one large project I worked on.

Amazon taught me what a complex software graph can look like, but that's about it.

### Delivery Experience Aggregator

I worked on the Prime team, and at the time we were responsible for the delivery experience. The aggregator
components I was responsible for were figuring out how to group and send order items.

I had to:

- Implement grouping logic.
- Implement mapping logic for input and output data.
- Complete various other tasks surrounding project setup and configuration.

## 900feet

900feet was a startup I founded with a couple friends that pivoted a few times until deciding to try and
empower small businesses with access to big data. We made a proof of concept that leveraged social media
data and stored it, spatially and temporally indexed. This meant we could answer questions like 'What happened
at some time in some area?' We planned to use this technology to infer valuable strategic information for
clients to make business decisions through prediction. We couldn't find anyone willing to adopt the tech,
though we did receive some funding that allowed us to continue this project for a few years.

### Core Product

I needed to:
- Bootstrap a distributed system.
- Engineer a way to query multiple data sources, constantly, while avoiding rate limiting.
- Provide an api for consumers (a colleague made a front end).
- Participate in and drive design.
- Provide directional input to other company stakeholders.

## Redbeard, Again

Same company, I'm just going chronologically. I did some Redbeard work after 900feet.

### Harbinger

Harbinger was a company that engaged me to produce various small scale applications integrated with social
media (things like facebook apps). They were pretty basic so I won't describe them here.

## Wave

At this job, I learned a lot about distributed computing at scale and I am
grateful for the opportunity I had. I touched nearly every product at the company and was in
a position where I helped guide the engineering organization's efforts to improve our craft.

### Invoicing Migration

You can actually read about this [here](https://medium.com/engineering-at-wave/wave-invoicing-migration-part-1-429ae414fe4f), [here](https://medium.com/engineering-at-wave/wave-invoicing-migration-part-2-8484a55845cc) and [here](https://medium.com/engineering-at-wave/wave-invoicing-migration-part-3-57171603c67).
**WARNING: These are medium links and may exhaust your credits.**

We needed to migrate an application and data from a monolith to a microservice (~1 billion records).

I had to:
- Help decide which entity from the service we would use to test our tooling.
- Integrate with our authentication and identity service to determine migration status (in future migrations
I take a cleaner approach).
- Implement the tooling for the initial entity.
- Devise a plan to migrate the rest of the entities.
- Integrate remaining entity migrations into tooling.
- Operate migration tooling.
- Programmatically resolve errors due to source data inconsistencies.
- Respond to any incidents related to the migration.

This project was a success, and I learned a lot about Django application architecture from this project. In
particular I got to see many things in the legacy codebase that caused problems, and what it looks like to
solve them in the new system.

### Onboarding Experimentation

I moved to the Onboarding Experience team as the invoicing migration was finishing. My primary goal there was
to help them set up long term storage for data gathered during the onboarding process.

Among many other things, I ended up:
- Using a short-lived token generated on behalf of the client by the server to authenticate with a protected
S3 bucket to write the data to, temporarily.
- Integrating a backend service with S3 to permit a better data flow.
- Refactoring to allow the onboarding client to connect to the service through our api.

In addition to this I made some great reusable front-end code.

### Kafka

I was the first person at Wave to implement an end-to-end Kafka solution. We had a few producing
applications, and someone hooked a consumer up to one, but no one wrote both a producer and consumer for
a purpose.

I utilized Kafka for resilient transport of data to facilitate a state change in another system. This can be
a bit dangerous, for instance, if the second system has the ability to refuse the state change. In that case,
we'd risk a global de-sync of data. In our case, however, we did not have the option of rolling back the
transaction on the producing side, so a synchronous call still didn't solve the problem. Given this
information, it made sense to use the most resilient transport available, and this was Kafka.

I:
- Implemented producing code and prepped the application for additional producers.
- Implemented consuming code in another system.
- Helped demonstrate a migration from one Kafka infrastructure to another.
- Helped establish some best practices and guides surrounding the use of Kafka at Wave.

### Covid Response

Just before Covid became a thing, I was working with the Payroll team. This was a Ruby team, and I don't know
if I've made my love for Ruby clear in my writing, but the fact that it is so guessable to me makes it a joy.

Payroll, however, was impacted quite heavily by Covid, since employers could hold back tax payments from the
government to take advantage of support policies. There were a bunch of policies and we needed to implement
solutions rather quickly.

I had to:
- Contribute to the design of a policy-agnostic solution
- Implement a policy
- Lead implementation of a dashboard for all policies

This was a successful and welcome addition to our product.

### Bills Migration

This was very similar to the invoicing migration, but we ended up needing to divert resources to other areas
of business before completing this. We only migrated part of the legacy application.

For this, I:
- Designed the solution and migration plan
- Led the project (created tickets, guided developers, maintained rituals)
- Implemented the back end of the new portion of code, thrice (I had to implement three different ways before
matching the performance of the original implementation due to framework constraints).
- Paired with colleagues to get the api and front-end layers worked out

### Other Duties

I:
- Led two working groups (`Reactive Systems` and `Resilience and Fault Tolerance`)
- Mentored other developers
- Was a member of the site-wide on-call rotation
- Assisted the DevOps team
- Assisted the Security team
- Promoteed best practices across the organization
- Developed onboarding materials

## goConfirm

goConfirm was a seed round startup that I co-founded. I was also the Principal Engineer. In this role, over three years, I built a highly tuned engineering organization with deep technical roots. We had to spin the product down because we only acquired 70,000 (consumer, unpaying) users in our last year of operation. During the AI revolution, this was not enough to whet the appetites of investors. Nonetheless, we produced a 5 star app and released features like secure messaging in under 4 months of developer time (less than 2 months with 2 devs).

The primary mission of goConfirm was to increase trust online, and allow individuals
to interact safely. We were attempting to deploy a new technology, Decentralized Identity, to accomplish this.

### Responsibilities

- Last word in all technical decisions (Our company had no CTO)
- Leading a team of 4-6 engineers
- Building everything
- Communicating with stakeholders
- Board meetings

### The Platform

goConfirm was primarily a Golang application. The thing that made it really interesting was the way we handled data. We used decentralized techniques from KERI (Key Event Receipt Infrastructure) to secure our datastore, and I noticed several other benefits after making this decision.

Intially, I wrote a rust library with the intent of deploying to both our backend and mobile app. We ended up using it to secure identifiers for users, in the backend, in a python service. Sounds wild given that we were a mobile shop with a Golang backend, but it fit at the time.

Application Features:
- Secure messaging
- Fraud Insurance (we successfully offered this, our setup allowed us to permanently ban bad actors)
- Endorsements
- Semi-anonymous connection

Security Features:
- ed25519 passphrase derived key based verification
- secp256r1 hardware key based verification
- hardware-signed requests
- registration/auth binding to IDV
- temper-evident data throughout
- aes-256-gcm encrypted messaging

Integrations:
- AWS
    - Aurora
    - Rekognition 
    - S3
    - SQS
- Persona (IDV)
- Stream (Messaging)
- Customer.io (Email/Push)
- Zendesk (Support)
- Slack (Company comms)
- Segment.io (Analytics)

## Certn

I've worked at Certn since only October 2025, but in that short time I've had an impact by
- making improvements to onboarding
- onboarding new hires
- releasing a broad API feature to retain a valuable customer and enable a new vertical market slice
- planning a migration to a decentralized world (this is why they hired me)