---
layout: post
title: The unofficial Fujitsu Server Guide for Homelabs
---

So you live in the EU and want to have a server, but realized that Dell and HP can be quite expensive here? Then this is something for you!

Every once in a while you will find a Fujitsu server on ebay. There is not much information about them on this subreddit, that is why I, your friendly Gammel, created this page!

## Concerning Names

First of all let's decrypt the naming scheme. Often they are just called Fujitsu but sometimes you come across something like "FSC" this originates from their partnership with Siemens, I believe.

When there is an RX in the name it is a rack server. TX on the other hand means tower server. BXs are blades, CXs are node servers, SX are storage servers and MX micro servers. But you are mainly looking for TX and RX.

Then there usually is a three digit number. Something starting with a 1 is normally the smallest variant with just one processor. A 2 means dual processors most of the time and 3 is a tiered up dual processor server, like being able to have more RAM etc. And a 4 usually means, you guessed it, a 4 proc server. After that the last two digits give some more information about processor version (AMD/Intel) but are not too important. Every Fujitsu server I have come across had an Intel processor.

The name ends in a S followed by a number. You are looking for anything S"X" with "X" being larger or equal to 6! !However somehow Fujistu fucked it up a little. S6 with one server might mean be an LGA1156 system, with another system this might be an LGA1366 and on top of all that a S7 server can also have an LGA1156 CPU... So be careful with that!

Some examples of what we have learned:

* Fujitsu RX100 S6: 1U Rack Server with one LGA1156

* Fujitsu RX200 S6: 1U Rack Server with dual LGA1366

* Fujitsu RX300 S6: 2U Rack server with dual LGA1366

* Fujitsu TX150 S7: Tower Servr with single LGA1156

* Fujitsu TX200 S6: Tower Server with dual LGA1366


Anything older than S6 will most likely be DDR2 based, so just avoid those... (or look it up, if you want to know for sure ;))

## Concerning Noise

When it comes to noise they are quite diverse... My RX100 S6 was reasonably quiet. My RX300 quite loud (but hey it's a 2U power horse...) and again Tower Servers here are most likely quieter than their Rack counterparts. Just like always ;) The TX150 S7 for example is supposed to be really quiet! Something very interesting is the Low Noise Option for some models. The RX300 S7 for example offers this option, if there are only Xeon E5-26xxL CPUs, only one DIMM per channel and only one RAID card installed.

All Fujitsu S7+ servers do a daily fan test, it's set at midnight per default. This should be changed if in use at home as you really don't want sudden loud fan noise in the middle of the night. The disabling checkbox for that should be located in the iRMC under power management.

## Concerning Power

Power consumption ranges from astonishingly good to okish... My older RX100 S6 only pulled 45 Watts at medium load! Impressive for an LGA1156 system I would say. The RX300 S6 however was a little on the hungry side...

## Concerning Raid Cards

It is not different to the HP and Dell servers. They are usually shipped with something like a PERC6i and only support 3GBs. I have no clue about the different cards there are yet. But as far as I could see most of it was rebranded LSI stuff as well. The Riser cards are really good and sturdy, so no problems putting in a "real LSI".

## Concerning iRMC

The integrated Management module is called ServerView/iRMC and is always included. No additional modules required, it has a dedicated NIC out of the box. Features are enabled through License Keys. ~~Those can be had for quite cheap or you might be lucky finding some of them floating around... ~~(Apparently this was some time ago. It has become quite hard to find keys online when you don't want to stand in jail with one leg all the time... You have to be "lucky" and get a server with the advanced license installed.) There are different versions of iRMC (S1-SX), so keep that in mind! The remote console works really good. I had no problems viewing it in a modern browser, it does however require an advanced license, those are sometimes already installed...

## Concerning Build Quality

I would rank Fujitsu servers right between HP and Dell. They also use some plastic on the front, but that feals a lot more reassuring than that flimsy HP plastic... The hard drive caddies are on a par with Dell's.

## Concerning HDDs

Most servers can be had in different HDD configurations. It is probably best to look up the Illustrated Spares Catalog for the available configurations. Keep in mind that some configurations might be more common than others! An RX300 S6 for example can be had in a 8x/12x 2,5" or in a 6x 3,5" configuration. The 3,5" configuration however is a lot more expensive!

Some more examples:

* RX100 S6: normally 2x 3,5"

* RX200 S6: normally 6x 2,5"

* RX300 S6: normally 8x 2,5"

* TX150 S7: normally 4x 3,5"

## Concerning Caddies

The caddies can be used through the whole range! There were only done some front design changes from S5 to S6 but this doesn't limit you in any way. The 3,5" caddies are a little on the pricier side, but it always depends on what offer you find...

## Concerning Updates

Big shoutout to Fujitsu for that! You can dowload like EVERYTHING for free from their website [Support](http://support.ts.fujitsu.com) You just browse your server and you are directly presented with everything there is. You can even find their really old models there, so absolutely no problems with that! In addition to that I have found what they call an [illustrated spare catalog](http://manuals.ts.fujitsu.com/illustrated_spares/isc-portal-fts.php?filter=RX)! You again browse you product and you are then presented with multiple images of you server where you can just click on things on the image and you get a list of every spare part for that. This is helpful and cool times 10!

## Concerning Upgrades

Generally the spare parts are a lot cheaper. This does not include the rails however! Rails are freakin expensive! You should really try to find an offer where those are included!

**Some servers you should look out for:**

* RX300 S7 or S8 - These are amazing E5-26XX 2U servers. Great boxes, but a bit noisier than a R720. 2 of these currently on ebay UK for £240 and £300.

* RX100 S7 S7P S8 - Not that common tbh, but very great 1U E3 servers, with 3 PCI slots. The best E3 server I have used and have experience with Dell and HP ones, the Fujitsu is just easier to work with although it is a fair bit bigger than a R210 II.

* TX200 S7 - This is a E5-24XX tower. Its silent, as has 3 big 140mm fans. Can't carry tons of drives, doesn't have an internal USB, most commonly only comes with 1 PSU and no IPMI (the only Fuijitsu Xeon machine that does as far as I am aware). Also is the only Fujitsu machine I have come across thats picky about hardware. But its faults can be ignored as it uses little electricity and is completely silent. Can be rack mounted like all Fujitsu Towers.

* TX300 S7 or S8 - Possibly the Best E5 v1 or V2 server in existence. They are very very similar to HP 350p G8 and the G9 seemed to nick ideas from the TX300 S8. These Beasts are designed to run 2 NVidia Tesla Cards - as such they can carry 4 800W PSU's. They have 10 PCIE slots, and upto 12 3.5" drives. They are amazing. Only downside is some 4 CPU servers weigh less as a TX300 S8 fully loaded can be over 35KG, so rack mounting them is fun. Also they aren't that common, probably as they are that good people see no reason to get rid.


If you are lucky or search deep, you find these servers in the US for quite cheap as well. They are not as common as Dell and HP over there, so they often fall under the radar of the big resellers.
