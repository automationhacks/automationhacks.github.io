---
id: 46
title: "Pycon India 2018: What i learned?"
date: 2018-10-11T16:59:17+00:00
author: Gaurav
layout: post
permalink: /2018/10/11/pycon-india-2018-what-i-learned/
publicize_twitter_user:
  - __gaurav_singh
publicize_linkedin_url:
  - null
categories:
  - "Talks &amp; Conferences"
---

![Pycon india website](/assets/images/wp-content/uploads/2018/10/24e58-0qa2jeiwzh_ivzp25.png)

Hi folks, recently I had the pleasure of attending 2-day Pycon conference in hyderabad, India. It
was also the 10th year of pycon being organized in india. Pretty sweet achievement if you ask me. 😃
There was little bit of something for everyone and I become aware of and learned few new things in
and around the python ecosystem.

> Disclaimer: This blog in no way covers all the sessions that happened but just the ones which i
> attended.

---

### Day 1:

There were many excellent talks to choose from and I did attend most of them.

<a href="https://in.pycon.org/2018/#" title="Keynote 1" target="_blank"><strong>Keynote
1</strong></a>  
_By Armin Ronacher_

The Conference was kicked off by the creator of
flask/<a href="http://lucumr.pocoo.org/" target="_blank">jinja</a>
<a href="https://medium.com/u/d38a80b1d039" target="_blank">Armin Ronacher</a> and his key note was
mostly about how python community can learn a lot from how Rust lang’s community is operating in the
light of Guido van rossums decision to step down as BDFL. It was quite interesting and he
highlighted few areas of potential improvements which python core devs can take going forward.

<a href="https://in.pycon.org/cfp/2018/proposals/python-project-workflows-continuous-deployment-friendly~bq8ya/" title="Python Project Workflows - Continuous Deployment Friendly" target="_blank"><strong>Python
Project Workflows — Continuous Deployment Friendly</strong></a>  
_By Abhijit Gadgil_

This talk illustrated how
<a href="https://pipenv.readthedocs.io/en/latest/" target="_blank">Pipenv</a> is actually a natural
evolution over pip and virtualenv created by none other than creator of requests module in python
(kennethreitz) Also how to setup pylint with a
<a href="https://github.com/PyCQA/pylint" target="_blank">pylintrc</a> file to get awesome linting
for python code and also leveraging a pre-commit git hook to ensure no code which violates code
quality is committed was interesting.

<a href="https://in.pycon.org/cfp/2018/proposals/inside-the-worlds-largest-python-course-on-coursera~bomYe/" title="Inside the World" target="_blank"><strong>Inside
the World’s Largest Python Course on Coursera</strong></a>

_By Charles Severance._

There was an interesting talk by <a href="https://medium.com/u/81da374cca2f" target="_blank">Chuck
Severance</a> on \_\_his open courses for python learning. It was quite amazing to see how he was
able to evolve from creating LMS (learning management systems) since the 90s to actually one of the
most popular courses on coursera for <a href="https://www.py4e.com/" target="_blank">Python for
everybody</a>. He is planning to follow this up with
<a href="https://www.dj4e.com/" target="_blank">Django for everybody</a> based on testing this
course out with his students in his university classes. Looks quite interesting.

<a href="https://in.pycon.org/cfp/2018/proposals/metaclasses-and-decorators-a-match-made-in-space~ervpe/" title="Metaclasses and decorators: a match made in space" target="_blank"><strong>Metaclasses
and decorators: a match made in space</strong></a>  
_By Ishan Srivastava_

This was an interesting talk by 3rd-year undergrad student on how metaclasses work in python and how
they form the basis for many behind the wraps implementations in django and other projects.
<a href="https://realpython.com/python-metaclasses/" target="_blank">Real Python</a> has an very
good article explaining how metaclasses work.

<a href="https://in.pycon.org/2018/#" title="Community Talk" target="_blank"><strong>Community
Talk</strong></a>  
_By&nbsp;  
Kushal Das,_ **_PSF_**_&nbsp;  
Mario Behling,_ **_FOSSASIA_**

Next up there was a talk about the <a href="https://www.python.org/psf/" target="_blank">Python
software foundation</a> that supports the development of the language we love the most and how we
can also contribute.

Also, Mario behling gave an introduction for people who want to contribute to FOSS (Free and open
source software) from <a href="https://fossasia.org/" target="_blank">fossasia,</a> also they are
planning to have a <a href="http://pslab.io/" target="_blank">Pocket size hardware device</a> as an
open source project which looked super 🆒. There were mentions of some interesting programs that
people can participate in like _Code heat, Google code in, GSOC, Summer internship program, Advanced
developer,_ details of which can be checked out in fossasia website.

<a href="https://in.pycon.org/2018/#" title="Keynote 2" target="_blank"><strong>Keynote
2</strong></a>  
_By Sidu Ponnapa_

The day ended with an awesome keynote by
<a href="https://medium.com/u/e2e244e6c6b3" target="_blank">Sidu Ponnappa</a> about how scaling an
engineering org is similar to how a tech product is scaled. Lots of nice tips and practical advices
to be taken from this. What stood out for me was two basic ideas:

- Engineers (devs) become best managers since they really understand all the challenges and mostly
  are able to reason logically (just like in code)
- CRY principle (Continuous repeat yourself) when you are trying to communicate since any form of
  communication between two individuals always has some elements of ambiquity.

---

### Day 2:

<a href="https://in.pycon.org/cfp/2018/proposals/testing-micro-services-made-easy~axm3b/" title="Testing micro-services made easy" target="_blank"><strong>Testing
micro-services made easy</strong></a>  
_By Devi A S L_

This talk was more around how **contract testing** can be an easier alternative to end to end tests
and really assists in finding issues in a microservices architecture. Devi showed some practical
python code using <a href="https://docs.pact.io/" target="_blank">PACT</a> framework.

<a href="https://in.pycon.org/cfp/2018/proposals/cleaning-data-with-python~azzma/" title="Cleaning data with Python" target="_blank"><strong>Cleaning
data with Python</strong></a>  
_By Anand S_

Really loved this talk by anand, he is such a clear orator and was able to basically explain the
techniques that go behind cleaning data using python libs like pandas (🐼). He took a practical
example of how data can be extracted from PDF and then cleaned to feed into ML algorithms.

Some key libs:

- <a href="https://github.com/jamesturk/jellyfish" target="_blank">Jelly Fish</a> for doing fuzzy
  matching of strings (Fingerprinting)

<a href="https://in.pycon.org/cfp/2018/proposals/alexa-enabled-smart-home-programming-with-python~dy5nd/" title="Alexa enabled smart home programming with Python" target="_blank"><strong>Alexa
enabled smart home programming with Python</strong></a>  
_By Sonal Raj_

This talk was really awesome, the speaker had used python flask to basically expose certain
endpoints hosted in AWS which could be invoked with certain
<a href="https://developer.amazon.com/alexa-skills-kit" target="_blank">Alexa skills</a> to control
his smart home. As an example he showed how its possible to control
<a href="https://www.belkin.com/us/Products/smarthome-iot/c/wemo/" target="_blank">wemo devices</a>
using
<a href="https://media.readthedocs.org/pdf/fauxmo/latest/fauxmo.pdf" target="_blank">fauxmo</a>

Some new python libs/modules that I came to know during this talk:

- <a href="https://plot.ly/products/dash/" target="_blank">Dash</a>,
  <a href="https://cherrypy.org/" target="_blank">Cherry pie</a> are some other python frameworks
  for making UI interfaces apart from the more popular Django project.
- <a href="https://ngrok.com/" target="_blank">Ngrok</a>&nbsp;: Can be used to expose local web
  server using public URLs
- <a href="https://ifttt.com/" target="_blank">IFTTS</a>: Allows devices to talk to each other

<a href="https://in.pycon.org/cfp/2018/proposals/experience-with-python-type-hints~dwl1e/" title="Experience with Python type hints" target="_blank"><strong>Experience
with Python type hints</strong></a>  
_By Kracekumar Ramaraju_

This talk was more around how type hints can be incorporated in python via
<a href="https://docs.python.org/3/library/typing.html" target="_blank">typing</a> module and how it
makes sense more for having a layer of security on your app boundaries.

Some new libs that i heard about in this talk.

- <a href="http://mypy-lang.org/" target="_blank">mypy</a>
- <a href="https://github.com/Instagram/MonkeyType" target="_blank">monkey type</a> by instagram
- <a href="https://pyre-check.org/" target="_blank">pyre</a>
- <a href="https://github.com/spulec/freezegun" target="_blank">Freeze gun</a>: module to basically
  allow mocking of datetime module to allow for more reliable tests

<a href="https://in.pycon.org/2018/#" title="Keynote 4" target="_blank"><strong>Keynote
4</strong></a>  
_By Carol Willing_

This talk was a perfect end to pycon where
<a href="https://medium.com/u/cebb27c32786" target="_blank">Carol Willing</a> who is Cpython core
dev and part of Jupytyr project explained what options are being discussed on the governance model
for python with Guidos step down and also what values we can imbibe and follow to ensure the lang
evolves further. Her slides are now made public on
<a href="https://speakerdeck.com/willingc/the-future-of-python" target="_blank">speakerdeck</a>

### Lightning talks&nbsp;⛈:

These are usually the best part of any conferences since you get to know so many new ideas as
quickly as possible.

I really liked this one talk by a student called biswaz about how during recent Kerela floods in
India OSS community created a Django website to aid in relief and rescue efforts. Read more about it
in this
<a href="https://medium.com/@biswaz/at-the-eye-of-the-flood-5ddec61a87b8" target="_blank">blog</a>

Also, there was a person who was able to use python code to recognize possible patterns in a
minesweeper to design the ultimate script to beat minesweeper every time. 🤷‍♂

Thats all folks. For more details you can check out
<a href="https://in.pycon.org/2018/" target="_blank">pycon website</a>. The talks recording might
come out. Be sure to check it out when it comes.

If you liked this, why not share with your friends or more. 😏
