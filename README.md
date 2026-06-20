# Clearing calls

## Context

At Nomos, we want to make energy abundant for European households. We are building a new kind of
power company from the ground up, with software and artificial intelligence at its core, and we
build the whole thing ourselves because that is the only way to do it properly. We create new
energy products together with Europe's leading technology companies and installers, and we turn
energy into a cost-saving feature inside the things people already own, like electric vehicles,
heat pumps and home batteries. One of those partners, Cloover, is also a partner in this
hackathon.

To supply even a single household, we exchange a constant stream of regulated messages with the
rest of the German energy market. That means the grid operators (called Netzbetreiber in German),
the metering operators, and the other electricity suppliers. We have already made two of these
channels run on their own. The first is the computer-to-computer one, where our systems and
theirs swap standardised electronic messages in a format the industry calls EDIFACT. The second
is plain email. Both of them now handle themselves.

But the market is not ready for full automation yet. Sometimes a message bounces back with an
error code nobody can read, or a grid operator simply never replies. When that happens, the rules
say the case has to be sorted out over the phone. Today the only thing that works is a person
picking up the phone, getting through to the right desk, explaining the case, and pushing until
there is an answer.

Your challenge is to build the voice agent that makes that call. It clears the case today, and it
bridges the gap until the market itself can support full automation.

## What a clearing call looks like

A clearing call is short, around two minutes, and always in German. It runs through the same few
steps every time.

First, an automated phone menu answers, not a person. It is the recorded voice that says
something like "for questions about switching supplier, press one." The agent has to notice that
it is talking to a menu, not a human, and press the right number on the keypad before anyone comes
on the line.

Then a clerk picks up. The agent says who it is and why it is calling, and offers the details of
the case straight away. The clerk asks a few simple things to find the case, like the address, the
market-location number (known in German as the MaLo), and when the registration was sent. There
is no password and no security check.

Then the clerk looks it up and says what is actually wrong. The agent listens, repeats any number
back one digit at a time to make sure it got it right, and agrees on the next step.

Here is a real Nomos call, with the details changed. We had sent a registration for a customer in
Mainz-Kastel, but it kept getting rejected with the message "this market location is not taking
part." On the phone, the clerk checks her system. The meter behind that connection had been a
temporary one, the kind used while a house is still being built (a Baustromzähler in German), and
it had already been removed. So the old market location is dead, and the connection has to be set
up again from scratch. The win was not a reference number. It was understanding the real reason,
and knowing the next step, which was to go back to the customer.

You will run into three kinds of case:

| Case | What is wrong | What a cleared case looks like |
|---|---|---|
| Chasing a silent registration | We sent it, nobody replied, the deadline has passed | Confirmation it is being worked on, plus a reference number |
| A registration that bounced | Rejected even though we have a valid market-location number | The real reason, plus the next step |
| The wrong market-location number | The number we have does not match the address | The correct number, read back to be sure |

## The goal

Build an agent that Helga, 54, sitting in a grid operator's back office, is happy to talk to and
does not hang up on in the first ten seconds. That sounds soft, but it is the whole game. It means
an agent that is warm and genuinely human, and that can slow down and read a long number back
cleanly, one digit at a time. That last part is where most voice agents fall apart.

It also has to actually clear the case. That means pulling the key facts out of the conversation,
saving them, and setting the right next action in motion. Two real examples:

* It gets the market-location number from Helga, writes it into our system, and the customer's
  sign-up carries on by itself.
* It learns the meter is no longer active, because it was only ever there while the house was being
  built, notes that we need to reach back out to the customer, and hands the case to our email
  agent.

This is a hands-on exercise. We want to see how you make an agent sound human, how you get it to
listen and pull out the right facts, and how you close the loop back into a system. There is no
single right answer, and we are just as interested in the angle you take as in where you land.

## What you get from us

* Free credits for ElevenLabs, the voice platform. You claim them yourself through a bot on our
  Discord server. Join the server at https://discord.com/invite/VnBvbbcdEC, open the channel called
  coupon-codes, click "Start Redemption," and fill in the short form with the email you registered
  with. The bot then sends you your own code. There is a short video that walks through it at
  https://youtu.be/S143_JtCtV8.
* A Twilio account, which is the service that places the actual phone call. If you need one, just
  reach out to us and we will take care of it.
* An example call, written out with the details changed, so you can hear what a good one sounds
  like. You will find it in the recordings folder.
* A set of made-up cases to practise on, in the file fixtures.json. The customers, numbers and
  addresses are all invented. None of it is real.
* A one-page cheat-sheet (the file CHEATSHEET.md) that explains every German term you will hear in
  plain English. You do not need to speak German or know anything about the energy market.
* The phone number of our practice clerk. Your agent only ever calls that number, never a real grid
  operator.

If you need anything else, just ask. We have more resources on hand, and someone from Nomos is
around all weekend to help you get set up.

Two rules you cannot break. Your agent has to say it is an artificial intelligence as its very first
words to a person, because European law (the EU AI Act) requires it. And it only ever uses the
made-up data we give you, never anyone's real details.

## Going further

The real prize is closing the loop. A great agent does not just report back, it acts. It writes the
corrected market-location number into the system, or it hands the case to our email agent when the
meter turns out to be gone. Push as far as you can. Try the harder calls, like the ones where the
clerk's record is off from yours by a single digit, or where another supplier has already started a
registration on the same connection. The agent that listens, gets it right, and moves the case
forward is the one that wins.
