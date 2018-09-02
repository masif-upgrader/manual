## What is Masif Upgrader?

*Masif* is a given name derived from the word *massive*
by the creator of **Masif Upgrader**.

*Masif Upgrader* stands obviously for *massive upgrader*.
It's a distributed update manager designed to simplify
updating packages on large amounts of hosts.

![A package store](./img/cover.jpg)

## Architecture

![Relation between Masif Upgrader components (1)](./img/architecture/1.svg)

Every host managed by Masif Upgrader runs the Masif Upgrader *[agent]*.
That agent monitors whether any new versions
of installed packages are available.

Once anything can be upgraded, the agents report all actions to be performed
to the *[master]*.
The master stores these actions in a MySQL database shared with the *[UI]*.

With all that data stored centrally the administrator of the managed hosts
can overview the actions to be performed by the package manager
across all hosts via the UI:

 Package, agents awaiting approval | Action    | Target version
 ----------------------------------|-----------|----------------
 perl, 23                          | Update    | 5.24.1-3+deb9u4
 []()                              | Configure | 5.24.1-3+deb9u4

![Relation between Masif Upgrader components (2)](./img/architecture/2.svg)

Actions the admin agrees with can be approved (across all hosts at once)
by just ticking the respective checkboxes
and clicking *Approve selection* in the UI.

The agents poll the master for approved actions and execute them once approved.

[agent]: https://github.com/masif-upgrader/agent
[master]: https://github.com/masif-upgrader/master
[UI]: https://github.com/masif-upgrader/icingaweb2-module-masifupgrader
