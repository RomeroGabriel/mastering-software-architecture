# Foundations

Architecture styles, sometimes called architecture patterns, `define how components relate to each other and cover various architectural characteristics`. These style names are like shortcuts for experienced architects. For example, if an architect talks about a 'layered monolith,' it signals specific structural aspects, what works well (or not), common deployment models, data strategies, and more.

`An architecture style describes the structure and typical architectural characteristics`, both good and bad. `Architects should also understand the fundamental patterns often found within these styles`.

??? note "Fundamental Patterns"
    `Over time, some basic patterns keep showing up in software architecture. These patterns help us organize code and deployments`. For instance, the idea of separating different concerns based on functionality, into layers is an age-old concept in software. It's been around for a long time and still appears in various forms, even in modern architecture.

## Unitary Architecture

In the early days of software, `the computer and software were one`. But as technology evolved, they separated to handle more complex tasks. Mainframes, for instance, began as single systems but later split data into separate systems. Today, `unitary architectures are rare, except in specific situations like embedded systems`. Most software systems grow in complexity, so we separate them into different parts to keep them running smoothly.

## Client-Server

A fundamental style in architecture `separates technical functionality between frontend and backend`. This configuration is commonly referred to as a `two-tier or client/server architecture`. Over the years, this architectural approach has taken on various forms, adapting to different eras and advancements in computing technology.

### Desktop + Database Server

In the past, `desktop applications used to handle the user interface, while the data was stored in separate database servers accessible over networks`. This allowed desktops to handle user interfaces while heavy data processing happened on more powerful database servers.

### Browser + Web Server

In this setup, `users interact with a web server, which connects to a database server`. It's similar to the desktop architecture but with lighter clients (browsers), making it more accessible. Although the database is separate, it's still considered two-tier because the web and database servers run on one machine in the data center, while the user interface is in the user's browser.

### Three-tier

A popular architecture from the late 1990s is the three-tier architecture, `which adds more layers of separation`. `It includes a database tier with a powerful server, an application tier managed by an application server, and a frontend with HTML and JavaScript for user interfaces`.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
