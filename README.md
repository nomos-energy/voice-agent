## Clearing calls

### Context

At Nomos we're building a full-stack, AI-native power company, with one mission: to create
energy abundance in Europe. We build new energy products with Europe's leading technology
companies and installers, and embed energy as a cost-saving feature inside the things people
already buy: electric vehicles, heat pumps, battery storage and more. One of those partners,
Cloover, is also a partner in this hackathon.

To supply even a single household, we exchange a constant stream of regulated messages with the
rest of the German energy market: grid operators (Netzbetreiber), metering operators, and other
suppliers. We've already made ourselves autonomous in the two big layers, the machine-to-machine
one (EDIFACT) and the written one (email). They run themselves.

But the market isn't ready for end-to-end automation yet. A message bounces with a cryptic
error, or a grid operator simply never replies, and the rules push the case off the automated
rails and onto a phone call. The only thing that clears it then is a human: pick up the phone,
get to the right desk, explain the case, and push until there's an answer.

Your challenge: build the AI voice agent that makes that call, and bridges the gap until the
market itself can support full automation.

### Anatomy of a clearing call

A clearing call is short (about two minutes) and always in German. It runs the same beats:

1. An IVR menu answers first ("für Fragen zum Lieferantenwechsel drücken Sie die 1"). The agent
   navigates it before a human picks up.
2. The agent says who it is and why it's calling, and offers the case identifiers up front.
3. A light identity check: the clerk asks a couple of simple things (the delivery address, the
   market-location ID, when the registration was sent). No passwords, no security interrogation.
4. The clerk opens the system and tells you what's actually wrong.
5. The agent recognises the answer, reads any number back digit by digit to confirm it, and
   agrees the next step.

Worked example (a real Nomos call, lightly anonymized): we sent a registration for a customer in
Kastel, but it bounced with "Marktlokation nimmt nicht teil". On the phone, the clerk checks her
system: the meter behind that market location was a temporary construction-site meter
(Baustromzähler), removed on 18.05. The old market location is dead, and the connection needs a
brand-new setup. The win wasn't a ticket number; it was that diagnosis, plus the next step: go
back to the customer.

| Case | What's wrong | What "cleared" looks like |
|---|---|---|
| Reminder / Nachfassen | Registration sent, no reply, deadline passed | Confirmed it's in process + a reference number |
| Registration bounced | Rejected despite a valid market-location ID | The real reason + the next step |
| Wrong market-location ID | The ID doesn't match the address | The correct ID, read back to confirm |

### Task

Build an agent that Helga, 54, in a grid operator's back office, is happy to talk to and doesn't
hang up on in the first ten seconds. That sounds soft; it's the whole game. It means an agent
that's warm and genuinely human, and that can slow down and read a long number back cleanly,
digit by digit. That last part is where most voice agents fall apart.

And it has to actually clear the case: pull the key facts out of the conversation, store them,
and trigger the right next action. Two real examples:

* It gets the market-location ID from Helga, writes it into our system, and the customer's
  subscription continues automatically.
* It learns the meter is no longer active, because it was only ever there while the house was
  being built, flags that we need to reach out to the customer, and triggers our mail agent.

This is a hands-on exercise. We want to see how you make an agent sound human, how you get it to
listen and extract the right facts, and how you close the loop back into a system. There's no
single expected answer here, and we're as interested in the angle you take as in the result.

### What you'll get

* **ElevenLabs credits (free).** Claim them through the automated Discord redemption:
  1. Join the Discord: https://discord.com/invite/VnBvbbcdEC
  2. Open the `#🎟️│coupon-codes` channel
  3. Click **Start Redemption**
  4. Select this event and fill out the form with the email you registered with
  5. The bot sends you your unique coupon code

  Video walkthrough: https://youtu.be/S143_JtCtV8
* **Twilio.** Ask us in the Discord and a Nomos team member will set you up with a number.
* A **starter repo** with the outbound call wired up, so your first call is minutes away.
* **3–5 real, anonymized recordings and transcripts** so you can hear what good sounds like
  (`/recordings`).
* **Synthetic case files** to run against (`fixtures.json`): fake customers, market-location IDs
  and addresses. No real customer data.
* A one-page **market-communication cheat-sheet** (`CHEATSHEET.md`): every German term you'll
  hear, in plain English. You don't need to speak German or know the energy market.
* The number of our **clearing-desk agent**. Your agent only ever dials that number, never a real
  grid operator.

Two rules, non-negotiable: your agent says it's an AI as its first words to a human (EU AI Act),
and it uses synthetic data only.

### Expansion

The real prize is closing the loop. A great agent doesn't just report back, it acts: it writes
the corrected market-location ID into the system, or triggers the mail agent when the meter turns
out to be inactive. Go as far as you can: handle the harder cases where the clerk's record
disagrees with yours by a single digit, or where another supplier's registration is already in
progress on the same connection. The agent that listens, gets it right, and moves the case
forward, wins.
