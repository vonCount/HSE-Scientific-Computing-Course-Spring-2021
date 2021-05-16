Exercise: Write a simple RFC561-compliant e-mail.

Exercise: Send yourself an e-mail with non-ASCII characters. (E.g., "привет!") Download the raw message and open with a text editor. What are the contents? How is the message encoded, and where is the encoding specified? (Sometimes you need to select "view message source" or "view original message" to do this.)

Exercise: How are attachments handled? Refer to the Wikipedia article on MIME; send yourself an e-mail with a (very small!) attachment, and download the raw e-mail message and open with a text editor. What are the contents? Show and explain each MIME part. Can you recover the attachment from the raw message?

IRC

IRC is a chat system dating back to the late 1980s; it is the default chat system in the libre software and hacker communities. The protocol is open, and the core protocol can easily be implemented in a few days hacking.

IRC lacks many features some have come to expect from chat systems: history, images, formatting, etc, are all lacking. Read Drew DeVault's commentary for a counter-point.

Due to its openness and flexibility, IRC is a very popular place for bots; most major channels have at least one bot moderating them.

Exercise: Install an IRC client, log in to freenode.net, join #apertium and write a message "begiak: tell nlhowell hi". It will instruct the bot managing #apertium to forward me the message next time it sees me.

Exercise: Find a piece of software that you use which has an IRC channel for support. Ask a question there about the software. Include your conversation, and a brief description of your experiences.

Matrix

Matrix is a new messaging and communication system being developed to replace IRC. Many of the absent features of IRC are included in Matrix; generally, however, the protocols are very different.

Matrix is also an open protocol, and there are many different open-source clients and servers in development; there are also many projects to "bridge" with other chat systems. Matrix bridges exist for telegram, IRC, whatsapp, and others, allowing the Matrix user to connect to many different chat platforms.

Exercise: together with a friend, try out the Riot.im web client. How does it compare to IRC? To Telegram?

Exercise: Both Python and the Linux kernel have considered in the past moving from bugzilla- and e-mail-based systems to forges. Read both articles, and summarise the advantages and disadvantages of forge-based systems and e-mail, and the results of each.

Continuous integration

Modern large collaborative efforts usually involve many people working on different parts of the same project at the same time. Quality control tools are an essential part of ensuring that nobody forgets "best practices".

The simplest can be "syntax checking": you can request that the entire project is run through a "syntax checker" to make sure there are no errors in the programming syntax.

More sophisticated can be test suites which are developed in-concert with the project. Tests of small pieces of functionality are called "unit tests".

If these quality control tools are never run, or are run inconsistently, the mistakes of one contributor can have a disproportionate effect on the project. Continuous integration systems are unattended systems that run tests on all pull requests and commits, and notify the submitters/committers when changes "break" something.

Exercise: Suppose your project is not software. What kinds of quality control tests might you implement? Give examples for written articles, web sites, musical compositions, and graphics.

Documentation

Documentation comes in many forms, some more easily accessed or produced than others. Kinds you are probably already familiar with:

man pages
website documentation
project wikis
Other sources of documentation can be text files installed to /usr/share/docs, GNU info files (similar to man pages, run info <PROG> to view sometimes extensive documentation), or the source files themselves. Many projects include extensive documentation in PDF format (e.g. it is the standard in TeX).

Production of these documents all use different toolchains (though of course, all source files are plaintext), many very complicated. Luckily there is the [pandoc] tool, which can convert between many many different types of documents.

Exercise: install and run pandoc. (The dependencies are hefty.)
