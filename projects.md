[me](README.md)

# Personal Projects

A selection of my personal engineering projects. I'll leave out stuff like shimming tables. ;) The
bottom of the page is where you'll find recent projects. I'm leaving out many things, lots of physical 
one-off projects and of course my drug lab (that's a joke, I realize sarcasm doesn't do well in this medium).

## LEGO/Duplo

I guess the first kind of technical project I worked on was LEGO. By the age of ten, I enjoyed building
sculptures. I rarely used the instructions and preferred generic sets. I went so far as to win the Atlantic
Canadian official LEGO competition and competed nationally in 1991 (date?). LEGO fascinated me because it
was so abstract.

## Death Quest 1-3

When I became interested in computers, I discovered a program on my family PC that allowed me to write my
own programs. It was an interpreter, though I didn't understand this at the time. GW-BASIC empowered me
to build my first applications, as crude as they were. QBasic appeared shortly after, and in an effort to
make my programs distributable, I requested a copy of QuickBASIC for a holiday present.

With BASIC, a friend and I built two and a half text adventure games. I drove and navigated for the most
part, as I worked on it a lot in my spare time without my friend. The games were a series of complicated
conditionals and goto statements, and included coloured text and simple music.

`Death Quest` and `Death Quest 2` were games where you had to know one of the exact phrases required at
every juncture. Looking back I can see how difficult this would have been to play, but that's kind of the
appeal of text adventures. If you typed something wrong, you generally died. Hence the name. These games
were very linear.

`Death Quest 3` was a better game. It contained more state, a logical map (no graphics but you could navigate
with commands like `north`, `west`, etc. Character dialogue was colour-coded. It was a large undertaking for
for me at the time. This project was never completed, and I am unable to find the source.

## Graphics Experimentation

I outgrew BASIC in about a year, and poked around on some local [BBSes](https://en.wikipedia.org/wiki/Bulletin_board_system)
to learn that I needed to understand C and something called matrices if I wanted to make games with graphics
that would impress me. I procured some documentation about SVGA, and learned how to [unchain](http://www.brackeen.com/vga/unchain.html)
my hardware with a bit of assembly. This allowed me to have square aspect ratio pixels and buffering!

Unfortunately, matrix math eluded my 12 year-old mind and after developing some very nice looking
[rasterization](https://en.wikipedia.org/wiki/Rasterisation) methods that made an animated sine wave of
coloured tubes (I don't have this code anymore or I'd make a video) I abandoned graphics. I wasn't
interested in creating 2d games, I had played [wolf3d](https://en.wikipedia.org/wiki/Wolfenstein_3D)
and knew what was possible.

## *nix

My first experience with Linux was on another local BBS that basically gave you a login on a *nix machine. I
learned how to network through this host and others using modems to access some university systems outside my
locality.

I also received my first paid software gig on this server. I was given the task of making a multimedia demo
program that displayed a countdown timer until the next demonstration at a local college. When the teacher
realized how young I was, they gave me 150% the agreed compensation.

## Bulletin Board (The Pendulum)

Armed with C and my knowledge of other [BBS](https://en.wikipedia.org/wiki/Bulletin_board_system) software,
I set out to build my own Bulletin Board. I modelled it after another custom BBS that a local developer had
written, and the popular [Citadel](https://en.wikipedia.org/wiki/Citadel_(software)). I had to learn about
AT commands, ASCII and ANSI. It took me a while to figure out what a [null pointer exception](https://en.wikipedia.org/wiki/Null_pointer)
was, but eventually I made my BBS stable enough to support several daily users and even convinced my family
to let me install a secondary phone line for data (at 2400 baud).

## Reverse Engineering UFO: Enemy Unknown (XCOM)

While playing the game, I managed to level some attributes of my best characters beyond 255. The save game
format only had one octet allocated for these attributes, so when it wrapped I was left with characters weaker
than when I started playing the game. This was a frustrating experience, so I reverse engineered the save
games themselves to enable myself to play a level and edit my save, then repeat.

## 3D Modelling

I wanted to get back to my primary goal of making games, so I began investigating and using tools like
[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray) and [Moray](http://www.stmuc.com/moray/medown.html)
to understand the basics of the physics and simulation of [optics](https://en.wikipedia.org/wiki/Optics).

I crafted some of the typical things like chess pieces and planets. I made a logo for my software development
company, some procedurally generated trees, etc.

## Tracking

I also started making music using [Scream Tracker](https://en.wikipedia.org/wiki/Scream_Tracker) or
something that looks so much like Scream Tracker that I'm fooled.

## OS/Hardware Tweaking

In my late teens and early twenties I was writing software for university and didn't have many
extra-curricular projects on the go with the exception of a few cryptography and linux related endeavours.
Instead, I spent my time tweaking the look and feel of my OS by installing custom window managers and
creating my own themes and plugins.

I also spent time learning the limits of my hardware, overclocking safely, etc.

## Part-time Crypto

In university, I wanted to develop a hybrid factorization method for defeating [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
It involved a [sieve](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes),
the [Chinese Remainder Theorem](https://en.wikipedia.org/wiki/Chinese_remainder_theorem) and
[Pollard's Rho Algorithm](https://en.wikipedia.org/wiki/Pollard%27s_rho_algorithm).

It was probably pretty fast comparatively, but it obviously didn't work.

## Facebook

I began building a better `Myspace` and immersed myself in [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)),
but a few weeks later someone showed me [Facebook](https://en.wikipedia.org/wiki/Facebook). I stopped work.

## General Command Line Tool Abstraction

I worked a bit on creating a system to build a [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)
for command line tools in a generic way. Essentially, I observed a pretty standardized and parsable help
format in linux. I started work on generating an interface for [nemesis](https://troglobit.com/projects/nemesis/).

I didn't complete this and no longer have the code.

## Compiler farm

I bought some cheap used computers and set up a compiler farm when I was running [Gentoo](https://en.wikipedia.org/wiki/Gentoo_Linux).

## red/redrum

[Red](https://github.com/jasoncolburne/red) and [redrum](https://github.com/jasoncolburne/redrum) are a
low-level toolkit and build system I started developing after working at [Certicom](https://en.wikipedia.org/wiki/BlackBerry_Limited#Certicom).

`Red` is a platform abstraction that is designed to allow developers to achieve pace while creating secure
and portable code. It is incomplete.

`Redrum` is a Makefile system that supports multiple target configurations.

## Audio Engineering

I feel like I should mention this because it really is engineering. It is a highly complex job and requires
a good ear. I'm not the greatest but I get by.

## Electronics

It was always a plan of mine to build the pedal that Jimi Hendrix used most often - the [Fuzz Face](https://en.wikipedia.org/wiki/Fuzz_Face).
I began constructing various guitar pedals from scratch. I did everything except design the circuits. I:
1. designed the layouts
1. printed the circuits, using a laser printer, on magazine paper
1. transferred the toner to some copper clad with an iron
1. removed the magazine paper
1. used an etching agent to remove the copper unprotected by the toner
1. washed the pcbs
1. user acetone to remove the toner
1. cut the pcbs apart (this is actually difficult)
1. drilled hundreds of tiny holes using a drill press and many easily-broken bits
1. mounted the electronics components
1. soldered the components in place
1. drilled holes in the aluminum enclosures for potentiometers and jacks
1. applied rubberized coating to the interior of the enclosures
1. painted the enclosures
1. wired the true bypass switches
1. assembled
1. rocked out

## eyewarp

[This](https://github.com/jasoncolburne/eyewarp) is a project I wanted to complete since a young child. I
was into software demos like [Unreal](https://www.youtube.com/watch?v=VjYQeMExIwk) and
[Unreal \]\[](https://www.youtube.com/watch?v=17Bl4xf1BAg) and I liked playing around with
[fractint](https://en.wikipedia.org/wiki/Fractint) then, so when I had a bit
more skill I decided to try and implement one of my favourite effects from `fractint`.

It's called the diamond square algorithm and if you create a gradient, circular colour palette, you can cycle
the colours for some real nice plasma effects.

## jason-math

[This](https://github.com/jasoncolburne/jason-math) is a [Ruby](https://www.ruby-lang.org/en/) [gem](https://en.wikipedia.org/wiki/RubyGems)
that I created to help me complete coding challenges like [AdventOfCode](https://github.com/jasoncolburne/adventofcode),
[Project Euler](https://projecteuler.net/), [hackthebox](https://www.hackthebox.com/) and [cryptopals](https://github.com/jasoncolburne/cryptopals).
My favourite `hackthebox` challenge was called 'space', and my favourite `Project Euler` puzzle is #220.
I like them because they are tricky but not impossible. They are good learning challenges.

It features a lot of advanced [cryptography](https://en.wikipedia.org/wiki/Cryptography), notably:
- most modes of [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (including [GCM](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Galois/counter_(GCM)))
- [ECC](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) (don't trust the padding in the example code, I was in a rush)
- [NTRUPrime](https://ntruprime.cr.yp.to/) as a [KEM](https://en.wikipedia.org/wiki/Key_encapsulation_mechanism)
- [Argon2](https://en.wikipedia.org/wiki/Argon2) as a [Key Stretching](https://en.wikipedia.org/wiki/Key_stretching) algorithm
- All variants of [SHA](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms)
- [Blake2](https://en.wikipedia.org/wiki/BLAKE_(hash_function))

Additionally, it contains, as the name suggests, pure Ruby math routines. The most interesting bits outside cryptography are probably these:

- [Language Detector](https://github.com/jasoncolburne/jason-math/blob/main/lib/jason/math/utility/language_detector.rb) - crude but effective
- [Graph Algorithms](https://github.com/jasoncolburne/jason-math/blob/main/lib/jason/math/graph_theory/graph.rb) - Kruskal and Dijkstra
- [Number Theory](https://github.com/jasoncolburne/jason-math/blob/main/lib/jason/math/number_theory.rb) - the most magical branch of Mathematics, often defying intuition

There's also some pretty useful stuff in [utility](https://github.com/jasoncolburne/jason-math/blob/main/lib/jason/math/utility.rb).

## QuantumComputer.jl

I made a [Quantum Computer Simulator](https://github.com/jasoncolburne/QuantumComputer.jl) over the period of
a few weeks. I used Julia because it seemed to do the trick well, even though indicies start at 1 and it is
rumoured to not be dependable when correctness is required. I think for the purposes of Quantum Computing the
language holds up fairly well.

I will say that I don't yet fully understand measurement and my technique is surely flawed. I need to
understand projective measurements and global and local phase better to tackle this problem. The hilarious
thing is that many quantum algorithms still yield correct results.

Once I have my homelab set up (next project on this list), I want to build a distributed quantum computer simulator.
Measurement may not be parallelizable (this isn't a word, is it?) but circuit construction certainly is.

## homelab

[This](https://github.com/jasoncolburne/homelab) is one of my most ambitious projects to date. I built a secure
server with 18 network ports, 256gb of memory, and 24 cores. I plan to co-locate the required nodes of
[OpenStack](https://en.wikipedia.org/wiki/OpenStack) backed by Postgres and Kafka with apis served by nginx.
None of that is stock, and openstack is notoriously difficult to deploy. I am doing it from source, building
my own deployment scripts so that I can learn more about the OpenStack architecture. I'm going to write all
this up.

## ARAD

[ARAD](https://github.com/jasoncolburne/arad) is an attempt to create a reusable, permissively-licensed, teachable
distributed application. It is a work in progress. I started this project on June 26, 2022. I built it in my spare
time, and my pace has been furious. It features:

- Buzzword Tech Stack (asyncpg/aioredis/fastapi/openapi/react)
- [Refresh+JWTs](https://github.com/jasoncolburne/arad/blob/main/identity/identity/services/auth.py)
- [End-to-End Cypress Testing](https://github.com/jasoncolburne/arad/tree/main/front-end/cypress)
- [Documentation](https://github.com/jasoncolburne/arad/blob/main/documentation/README.md)
- [Scalable Architecture](https://github.com/jasoncolburne/arad/blob/main/documentation/design/README.md#overview)
- Production Deployment using [Hashicorp](https://www.hashicorp.com/) Tools (Nomad/Vault/Consul)
- OpenTelemetry (not yet integrated)
- Security Boundary around Identity Functionality

Not only is ARAD a reusable, documented kernel of a distributed application, the application that will be developed
on the stack is a useful tool. ARAD stands for Accessible Research Article Database. My friend and I have data from
junior university students, and can acquire more, that rates the difficulty and reading time of research papers to
provide an entrypoint to advanced topics for those without the foundation of a graduate student.

## howto [not started]

[Howto](https://github.com/jasoncolburne/howto) is an attempt to teach others what I know. I am going to
make guides for literally everything I know how to do.

## designs [not started]

My [designs](https://github.com/jasoncolburne/designs) of all kinds.