> **SYNTHETIC — INVENTED TEST DATA. This host, guest, company, and every quote below are fabricated for
> prompt testing. Never publish, never cite, never treat as real.**

# Fixture: Synthetic Episode Transcript

**Host (fabricated):** Jordan Calloway
**Guest (fabricated):** Theo Okonkwo, founder of Runway Kit
**Episode (fabricated):** "Building the Boring Parts First"

---

[00:00:15] **Jordan Calloway:** Welcome back to the show. I'm here with Theo Okonkwo, who's the founder
of Runway Kit, a logistics scheduling platform for small freight operators. Theo, thanks for doing this.

**Theo Okonkwo:** Happy to be here. Long time listener, first time being yelled at by you in person.

**Jordan Calloway:** We'll see how the hour goes. Let's start at the beginning. Where did Runway Kit come
from?

**Theo Okonkwo:** So back in 2021 I was doing freelance ops consulting for small trucking companies, the
kind with like five to fifteen trucks, no software budget to speak of. And I kept seeing the same problem
over and over: dispatchers were literally using whiteboards and group texts to figure out which driver
goes where. Not because they didn't want software, but because everything on the market was built for
fleets of five hundred trucks, not five. So I started building a scheduling tool for one client, just to
solve their problem. Then their competitor asked for it. Then I had four customers and a spreadsheet
invoice system, and at some point I looked up and realized I had a company.

**Jordan Calloway:** Did you set out to start a company, or did the company kind of happen to you?

**Theo Okonkwo:** Completely the second one. I didn't write a pitch deck until eighteen months in. I
wrote my first invoice template before I wrote any kind of business plan. Honestly the first "company"
artifact I created wasn't even the invoice template, it was a shared folder of screenshots of dispatch
whiteboards from four different customers, because I wanted to see what was actually common across them
before I built anything else.

**Jordan Calloway:** And you did this alone from the start?

**Theo Okonkwo:** Alone from the start, yeah. Partly by accident, honestly — I didn't know anyone else who
wanted to spend a year thinking about trucking dispatch software. It wasn't some grand philosophical
choice at first. It became one later.

**Jordan Calloway:** When did it become a philosophical choice instead of an accident?

**Theo Okonkwo:** Probably around customer number seven or eight. People kept asking if I had a co-founder
lined up, like it was assumed I'd need one eventually, and I remember sitting with that question and
realizing the honest answer was "not for any reason other than I've been told I should want one." Once I
noticed that, I stopped treating solo as a temporary state I was passing through.

---

[00:05:40] **Jordan Calloway:** Let's talk about a specific decision. You built your own dispatch engine
in-house instead of licensing one. Walk me through that.

**Theo Okonkwo:** Right, so in early 2022 we looked hard at licensing a routing engine from a company
called Fleetward — they had an API, reasonable docs, and it would have saved us probably four months of
work. We actually integrated it and ran it in a pilot with two customers for about six weeks. And it
technically worked, but it optimized for highway miles, not for the way small operators actually think,
which is: which driver is close to home tonight, and which driver hasn't had a rest day in two weeks.
Fleetward's engine didn't have a concept of "this driver needs to sleep in his own bed on Thursday." So we
ripped it out and built our own scheduling core from scratch, starting April 2022. Took us five months.
It was the single most expensive decision I made in the company's first two years, and it's also the
reason customers stay.

**Jordan Calloway:** Did you have anyone telling you that was a mistake at the time?

**Theo Okonkwo:** My advisor Priya Chen thought I was insane. She'd run ops at a much bigger logistics
company before advising early-stage founders, and her read was "you're a team of one, you do not have the
luxury of rebuilding infrastructure." She wasn't wrong that it was risky. She was wrong that it was the
wrong call. Both things can be true.

**Jordan Calloway:** Was there a moment during those five months where you thought she might actually be
right?

**Theo Okonkwo:** Month three. I'd burned through basically all of my runway buffer, I was building the
rest-day logic and it kept breaking in edge cases I hadn't anticipated — drivers with split shifts,
drivers who wanted the app in Spanish, drivers who worked two operators at once. I called Priya and said
I thought I'd made a huge mistake. She didn't tell me I was wrong. She just asked whether the Fleetward
pilot customers were happier or less happy with the new prototype so far, even broken. They were happier.
That was the only data point that mattered, so I kept going.

---

[00:11:20] **Jordan Calloway:** Tell me about a mistake. Not a strategic bet that paid off — an actual
mistake.

**Theo Okonkwo:** Okay, this one still makes me wince. Fall of 2022, I decided to change our pricing model
overnight, from a flat monthly fee to per-truck pricing, and I announced it with eleven days notice by
email. No call, no heads up, just an email that said "here's your new bill starting next month." Three
customers churned immediately, including our second-ever customer, who I'd had a genuinely good
relationship with. She called me, not to yell, just to say it felt like she'd been notified like a vendor
instead of talked to like a person. That one stuck with me more than the revenue we lost.

**Jordan Calloway:** What was going through your head when you decided eleven days was enough notice?

**Theo Okonkwo:** Honestly, I was optimizing for my own schedule, not theirs. I had a finance deadline of
my own coming up and I wanted the new pricing live before it hit, so I picked a date that worked for me
and worked backward. I never once modeled it from the customer's side, which in hindsight is a strange
thing for a solo founder to get wrong, because usually being solo means you're forced to model everything
from the customer's side. I just didn't, that one time.

**Jordan Calloway:** What did you change after that?

**Theo Okonkwo:** Every pricing change since then gets a 60-day notice and a personal call to every
customer above a certain size before the email ever goes out. It's slower. It's also never happened again.
I actually still have her name written on a sticky note on my monitor, not as a punishment exactly, more
as a reminder of what the note in the corner of my eye is for.

---

[00:16:05] **Jordan Calloway:** What do you tell other people building something like this alone?

**Theo Okonkwo:** The line I keep coming back to is: the moment I stopped hiring to fill loneliness and
started hiring to fill gaps, Runway Kit actually got better. I almost brought someone on in year one
purely because I wanted company, not because the role made sense. I'm glad I didn't. Our first real hire,
about fourteen months in, was a support lead, because I was answering 40 tickets a day by hand through a
tool called Threadline and it was eating every hour I had left for product work. That was a gap. Loneliness
isn't a gap you hire your way out of.

**Jordan Calloway:** That's a good line.

**Theo Okonkwo:** I've said it enough times it better be good by now.

**Jordan Calloway:** Any other advice you give people that you don't think gets said often enough?

**Theo Okonkwo:** Write down the boring decision the day you make it, not the exciting one. Nobody
forgets why they picked their logo color. Everybody forgets why they picked the payment processor, or why
they decided drivers get paid on the 1st and 15th instead of biweekly. Those boring decisions are the ones
that come back to bite you eighteen months later when someone asks "wait, why do we do it this way," and
if you don't have the answer written down you end up re-litigating decisions you already made correctly.

---

[00:21:30] **Jordan Calloway:** Let's close with rapid fire. Favorite part of the job?

**Theo Okonkwo:** Getting a text from a dispatcher at 6am saying the schedule just worked and they went
back to sleep.

**Jordan Calloway:** Least favorite?

**Theo Okonkwo:** Payroll paperwork. Every single time.

**Jordan Calloway:** One tool you couldn't run the company without?

**Theo Okonkwo:** Threadline, still, even after we hired support help. And embarrassingly, a very old
version of a whiteboard app, for my own brain, not the customers'.

**Jordan Calloway:** Book or resource you'd recommend to another solo founder?

**Theo Okonkwo:** Less a book, more a person — talk to Priya Chen if you ever get the chance, or find your
own version of her. Someone who's run ops at scale and will tell you the truth about your plan instead of
being encouraging.

**Jordan Calloway:** Last question. What's next for Runway Kit?

**Theo Okonkwo:** We're building a rest-day compliance module for 2026, so the "sleep in his own bed"
logic that started as a gut instinct becomes an actual auditable feature. Full circle, honestly.

**Jordan Calloway:** Theo Okonkwo, founder of Runway Kit. Thanks for coming on.

**Theo Okonkwo:** Thanks for having me. And for not asking about the whiteboard app sooner.

[END OF TRANSCRIPT]
