---
layout: post
title: "Everything Has Cracks"
tags:
  - raw
  - coding
created: 2023-01-25
date: 2023-01-25 08:36:00 -8000
---
Technology looks good until you look closely. You can only see the cracks when you look closely. I noticed GitHub Pages first potential issue.

### GitHub Pages and Ruby 2.7 EOL

As I tried to do [local testing for GitHub Pages]({% post_url 2023-01-25-local-github-pages %}), I looked into the dependencies. GitHub Pages still uses Ruby 2.7.4 and dependencies were last updated 2022-12-12. [GitHub itself updated to Ruby 2.7](https://github.blog/2020-08-25-upgrading-github-to-ruby-2-7/) (from 2.6) in 2020. Is this bad?

According to [Ruby's maintenance branches](https://www.ruby-lang.org/en/downloads/branches/), 2.7 was released in 2019-12-25 and is currently in `security maintenance`, meaning "only security fixes are backported to this branch". This is better than being marked as `eol`, but I don't think it'll be long before this happens. These are the details for the last few versions that have reached end-of-life:

| Version | Release Date | EOL |
| --- | --- | --- |
| 2.6 | 2018-12-25 | 2022-04-12 |
| 2.5 | 2017-12-25 | 2021-04-05 |
| 2.4 | 2016-12-25 | 2022-03-31 |

If I were a betting man and didn't have any more data points, I'd wager than 2.7 will have an end-of-life date of about late March or early April 2023 (about 3 months from now).

Since 2.7 to 3.x will be a major upgrade, I'd hope that the GitHub team has already started the process of upgrading. Their last minor version upgrade from 2.6 to 2.7 took "many months of work" and I'd expect a major version upgrade to take more time than that.

### How Bad Is It?

Technically, nothing happens if you miss this deadline. You don't get a zero on your homework or anything like that. But because the branch no longer is patched with security updates, you are potentially exposing your company to security vulnerabilities.

But if something bad happens, it has high potential to be *really* bad. Like "it will make headlines" level bad. Do you really want your business to fail because you didn't update versions?

Seeing delayed updates isn't really new to me though. Even a company like YouTube was putting off their Python 2.7 upgrade until very close to the 2020 EOL date. I wouldn't blame them. They have hundreds of employees working on an multi-billion dollar product. It's hard to prioritize upgrades like this, especially a major version upgrade, when you know it has the potential to also hurt your business. Done poorly, you could end up breaking all your systems. Done well, users don't notice anything.

You may get performance improvements, which yes, yes I know also has positive impact on revenue. But relative to a feature release, the perception of the product isn't improved greatly doing version upgrades.

### Everything Has Cracks

No matter how good something looks from the outside or at a high level, when you zoom in, there are always issues. Just a few examples:

* Working in FAANG sounds nice until you do it and you realize burnout is high and your work no longer feels meaningful.
* Owning a house sounds nice until you realize there is almost non-stop for home maintenance.
* Elon Musk seemed like a genius with Tesla until he lit $44 billion on fire.

Take anything that you value, you will always notice the flaws when you learn more about it. I can keep giving examples, but this exercise is best done on your own.

### Ignorance is Bliss

If you don't want your life to be miserable, maybe this is truly the way to go. Learn about stuff... but not too much.