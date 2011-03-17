# Email Reply Parser

EmailReplyParser is a small library to parse plain text email content.
See the rocco-documented source code for specifics on how it works.

This is what GitHub uses to display comments that were created from
email replies.  This code is being open sourced in an effort to
crowdsource the quality of our email representation.

See more at http://help.github.com/code/email_reply_parser/

## Installation

Get it from [GitHub][github] or `gem install email_reply_parser`.  Run `rake` to run the tests.

[github]: https://github.com/github/email_reply_parser

## Contribute

If you'd like to hack on EmailReplyParser, start by forking the repo on GitHub:

https://github.com/github/email_reply_parser

The best way to get your changes merged back into core is as follows:

* Clone down your fork
* Create a thoughtfully named topic branch to contain your change
* Hack away
* Add tests and make sure everything still passes by running rake
* If you are adding new functionality, document it in the README
* Do not change the version number, I will do that on my end
* If necessary, rebase your commits into logical chunks, without errors
* Push the branch up to GitHub
* Send a pull request to the `github/email_reply_parser` project.

## Known Issues

### Quoted Headers

Quoted headers aren't picked up if there's an extra line break:

    On <date>, <author> wrote:

    > blah

Also, they're not picked up if the email client breaks it up into
multiple lines.  GMail breaks up any lines over 80 characters for you.

    On <date>, <author>
    wrote:
    > blah

Not to mention that we're search for "on" and "wrote".  It won't work
with other languages.

Possible solution: Remove "reply@reply.github.com" lines...

### Weird Signatures

Lines starting with `-` or `_` sometimes mark the beginning of
signatures:

    Hello

    -- 
    Rick

Not everyone follows this convention:

    Hello

    Mr Rick Olson
    Galactic President Superstar Mc Awesomeville
    GitHub

    **********************DISCLAIMER***********************************
    * Note: blah blah blah                                            *
    **********************DISCLAIMER***********************************



### Strange Quoting

Apparently, prefixing lines with `>` isn't universal either:

    Hello

    --
    Rick

    ________________________________________
    From: Bob [reply@reply.github.com]
    Sent: Monday, March 14, 2011 6:16 PM
    To: Rick
