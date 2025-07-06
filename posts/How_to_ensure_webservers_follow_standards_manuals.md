**"Quirks mode" is still a problem. What to do: how to ensure [webservers](https://www.wmtips.com/technologies/web-servers/) follow reference manuals (plus [conform to accessible browsers](https://moderncss.dev/css-only-accessible-dropdown-navigation-menu/)).**

# Intro
\[[This post](https://swudususuwu.substack.com/p/quirks-mode-is-still-a-problem-what) allows [all uses](https://creativecommons.org/licenses/by/2.0/). For the most new; [*GitHub*’s `preview` branch](https://github.com/SwuduSusuwu/SusuPosts/blob/preview/posts/How_to_ensure_webservers_follow_standards_manuals.md).\]

\[This post interchanges "reference manuals" with "standards manuals". The reason is: the phrase "reference manuals" is most used for this, but the word "standards" is most used for this.\]

Not [“quirks mode” as in “missing DOCTYPE”](https://stackoverflow.com/questions/1695787/what-is-quirks-mode/1695790#1695790), but as the mode which is analogous to [Error correction mode](https://en.wikipedia.org/wiki/Error_correction_mode) for web browsers.
- The mode used if `<script>` is used without `</script>`, `text/html` causes browsers to fallback to [undefined behaviour](https://langdev.stackexchange.com/questions/481/why-would-a-language-have-a-concept-of-undefined-behavior-instead-of-raising-an) (“guessing” as to what such source code is “supposed to do” (which increases the risk of [phishing](https://en.wikipedia.org/wiki/Phishing) attacks, since such “guessing” results in execution of different amounts of *JavaScript* (**JS**) in different browsers; some browsers will disable **JS**, some browsers will use the **JS** parser to execute posts from random users)).
- Searches have not found what else to call this, but [*Grok-2* says to call this “quirks mode”](https://poe.com/s/cGXGFE3He8XfXYiKp4t3) (notice: [all “**AI**" answers are dubious](./Warning_AI_is_not_good_for_humans_to_use.md) but *Grok-2*’s somewhat less so).

[From the top *StackOverflow* answer to this](https://stackoverflow.com/questions/1695787/what-is-quirks-mode/1695790#1695790):
>- Quirks mode is not, however, a standard. The rendering of any page in quirks mode in different browsers may be different. Whenever possible, it is better to adhere to the W3C standards and try and avoid depending on any past or present browser quirks.
>- Generally, quirks mode is turned on when there is no correct `DOCTYPE` declaration, and turned off when there is a `DOCTYPE` definition. However, invalid HTML - with respect to the chosen `DOCTYPE` - can also cause the browser to switch to quirks mode.

`application/xhtml+xml` (**XML** or **XHTML2**) [allows the browser to abort (on such pages which do not follow standards manuals), plus give helpful error messages about which row of source code the tag (which the *webdev* forgot to close) starts on](https://www.w3schools.com/Html/html_xhtml.asp), which helps the web to improve.

The purpose is similar to how schools who give notices students who submit/publish documents which have malformed human languages.

Imagine a world with schools which did not give notices to students who submit/publish documents which do not follow human language rules:
- Those students will all guess different interpretations of human language rules.
- Once those students turn into graduate students, the documents which those publish will not follow human language rules, with the result that those documents will not have use.

The solution is that documents published which do not follow human (or computer) language rules must result in notices as to the positions of the text which does not follow those rules, plus the reason that the text does not follow those rules, such as:
- “This sentence (at row 6, column 2) does not end with ‘.’, ‘;’, ‘:’, ‘!’, nor ‘?’, thus is ambiguous.”
- “This `<script>` tag (at row 6, column 2) is not matched with `</script>`, thus causes [undefined behaviour](https://langdev.stackexchange.com/questions/481/why-would-a-language-have-a-concept-of-undefined-behavior-instead-of-raising-an) if executed.”

This image (fair-use attribution: <https://umm.sourceforge.net/About.html>) shows one of those notices (which XML browsers give you):
![One of those **XML** error notices](https://substack-post-media.s3.amazonaws.com/public/images/a487223b-f57d-4526-89cc-8f494bf60534_619x337.png)

The purpose of those notices is not to keep documents in such abortive modes, but to give clues to webmasters / web-developers (*webdevs*) on what to improve. The alternative (what **HTML** does) is to fallback to browser-specific [undefined behaviour](https://langdev.stackexchange.com/questions/481/why-would-a-language-have-a-concept-of-undefined-behavior-instead-of-raising-an) (which, when scripts are involved, can cause [accidental crashing](https://stackoverflow.com/questions/2346806/what-is-a-segmentation-fault), or enable [phishing](https://en.wikipedia.org/wiki/Phishing) and similar attacks), which is not good for computers (nor for humans).

## Howto
**XML** is almost a [superset](https://mathmonks.com/sets/superset) of **HTML**, but does not have as much duplicate syntax (thus is more simple to parse; less ambiguous).

Since **XHTML** is the [subset](https://mathworld.wolfram.com/Subset.html) of **XML** which most overlaps with **HTML**, the [changes to document source code are miniscule](https://www.w3schools.com/Html/html_xhtml.asp#:~:text=Important%20Differences); most source code which follows the [**HTML4** reference manuals](https://www.w3.org/TR/1998/REC-html40-19980424/html40.pdf) also follows the [`application/xhtml+xml` reference manuals](https://www.rfc-editor.org/rfc/rfc3236).

To ensure that browsers enforce the standards of those manuals, all you have to do is set the "**MIME** type" (`content-type`) to `application/xhtml+xml`:
- [*Abyss Web Server*](https://aprelium.com/data/doc/2/abyssws-win-doc-html/servergeneral.html#%3A~%3Atext%3Dmime)[ documents how to](https://aprelium.com/data/doc/2/abyssws-win-doc-html/servergeneral.html#%3A~%3Atext%3Dmime).
- [*lighttpd2*](https://doc.lighttpd.net/lighttpd2/all.html#plugin_core__option_mime_types)[ also documents how to](https://doc.lighttpd.net/lighttpd2/all.html#plugin_core__option_mime_types).
- [*Apache Web Server*](https://httpd.apache.org/docs/current/mod/mod_mime.html)[ also documents how to](https://httpd.apache.org/docs/current/mod/mod_mime.html).
- [_**PHP** Preprocessor_](https://www.php.net/manual/en/function.header.php#%3A~%3Atext%3DContent-type)[ also documents how to](https://www.php.net/manual/en/function.header.php#%3A~%3Atext%3DContent-type). Was more difficult to have the server use **MySQL** + **PHP** (but this is also [simple to do](https://www.digitalocean.com/community/tutorials/how-to-install-lamp-stack-on-ubuntu)).


## Counterarguments
Common reasons posted to not switch:
### “But you must use **HTML5** to have cool graphics, which is all our consumers value”

The first premise of that reason is not true:

In 2009 (as a child), was able to do the conversion of a huge **HTML4** server (to the **XHTML** subset of **XML**) alone. The result looked similar in *Mozilla Firefox* plus *Internet Explorer*, before and after the conversion to **XML**. Those webpages were also accessible to [browsers for disabled users](https://moderncss.dev/css-only-accessible-dropdown-navigation-menu/), plus to [pure console browsers](https://itsfoss.com/terminal-web-browsers/).

Most of the features of **HTML4** were in use, so know **XML** is not some “*draconian*” imposition which limits *webdevs* to simple pages.
Used **CSS** versions of all concepts which most *webdevs* used **JS** for, since **CSS** was/is more accessible/secure. For all data/info suitable to tables/charts, used **CSS** to give contrast to odd rows (don’t remember if used the [`nth-of-type`](https://www.thoughtco.com/zebra-striped-table-in-css3-3466982) or [`nth-child`](https://tutorialsarena.com/web/html/html-table-styling) "[selector](https://www.w3schools.com/CSS/css_selectors.asp)"), with additional **CSS** for [mouseover colors on tables with long rows](https://stackoverflow.com/questions/5492900/changing-background-colour-of-tr-element-on-mouseover). All the pages had [pure-**CSS** (mouseover hide/show) dropdown menus](https://www.w3schools.com/Css/css_dropdowns.asp).

Other webmasters asked to use some of the **XML** **API**s which were published through this server (and at no cost were allowed to; the purpose of the server was just to have the web improve); since **XML** is so simple to use, [one row of *PHP Preprocessor* source code](https://www.php.net/manual/en/function.simplexml-load-file.php) was sufficient to use those.

Was so impressed with the *World Web Consortium* for the release of an **XML** version of the web (plus for the [source code validation tools](https://validator.w3.org/)), plus proud to go around as one of the first *webdevs* who did whole conversion to **XML**, plus eager for more *webdevs* to switch to **XML**.

Once **XHTML2** was announced, trusted that the web would continue to improve on its own, so became a systems developer (*sysdev*). This post was published out of confusion at the results of searches on the web's progress; the results suggested that:
- most webservers still have not switched to `application/xhtml+xml`, so this post was published to inform *webdevs* on numerous reasons to do so.
- more webservers still do not serve source code which is accessible to browsers for disabled users (nor with pure console browsers), which this post is also supposed to encourage *webdevs* to do.

### “But you must use **HTML5** to have [**WYSIWYG** editors](https://itsfoss.com/open-source-wysiwyg-editors/), which is all consumers will publish through”
- The first premise of that reason is not true: `application/xhtml+xml` also allows those *JavaScript* editors.
- The second premise is debatable: although some syntaxes for text-mode editors (such as [*BBcode*](https://xenforo.com/docs/xf2/bbcode/)) require symbols (such as `[` `]`) which are difficult to use on mobile devices (such as smartphones),
numerous web services (such as *GitHub*) have switched to [*Markdown*](https://github.github.com/gfm/) (which just uses symbols which most smartphones have).

## Unnatural origin of problem
Since [undefined behaviour](https://langdev.stackexchange.com/questions/481/why-would-a-language-have-a-concept-of-undefined-behavior-instead-of-raising-an) is the worst possible error for computers (which is analogous to statuses which can cause [multiple organ failure](https://journals.lww.com/jtrauma/fulltext/2024/12000/multiple_organ_failure__what_you_need_to_know.1.aspx) for humans),

some have argued that external ([*Russian*](https://www.radware.com/cyberpedia/ddos-attacks/fancy-bear-apt28-threat-actor/)) influences manipulated browser developers into including “*Error correction modes*” which encourage such:

> This problem started when Russian spies pushed insecure browsers which execute all input (regardless of whether or not the page source follows the standards manuals). The Russian spies produced large amounts of posts (with attractive avatars) saying that this browser was "Cool" since it "Magically fixes broken pages for you", until users started demanding browser developers to all include [en.wikipedia.org/wiki/Error_correction_mode](https://en.wikipedia.org/wiki/Error_correction_mode), to make the Western web more "messy" (more vulnerable to phishing and similar attacks); for HTML the operation was successful. XML is immune

