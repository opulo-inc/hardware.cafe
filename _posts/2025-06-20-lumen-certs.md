---
title: "Taking the LumenPnP v4 Through Certification"
excerpt: "Taking the LumenPnP v4 Through Certification"
author: Stephen Hawes
header:
  overlay_image: /assets/blog-images/lumen-certs/lumen-chamber.png
  overlay_filter: 0.3 # same as adding an opacity of 0.5 to a black background
---

Last year we (Opulo) released a new version of the LumenPnP, with completely reworked electronics and cabling. And that means a new pass at certification.

![](https://cdn.shopify.com/s/files/1/0570/4256/7355/files/v4-iso-hero.png?v=1723749409)
*Used with permission from Opulo*

I brought the LumenPnP up to a testing house about an hour north of Pittsburgh called Keystone Compliance, and they were generous enough to let me film the process and interview a ton of people there. We were scheduled for four days of testing, and my awesome tech Jeremiah ran all the tests on the LumenPnP over those four days.

The two certifications we were going for in this process are FCC which covers the US, and CE which covers Europe. The point of these certifications is largely to check one thing: that the LumenPnP isn’t gonna mess with anything else electronic, and anything else electronic isn't gonna mess with the LumenPnP. We’re checking if it’s gonna play nice. Keystone determined which tests we needed to run in order to be compliant.

Again, this is a broad summary, but there are roughly four types of tests that we run, and they matrix pretty well. On one axis is Conducted (via physical contact), or Radiated (via electromagnetic waves). The other axis is the “direction” of the test, so is the LumenPnP affected by interference (called Immunity), or is the LumenPnP *making* interference (called Emissions). What’s getting messed up, and is it through waves or wires. Again, a huge simplification, and there’s a few that dont neatly fall into this, but that's the general idea.

{% mermaid %}
---
config:
  quadrantChart:
    chartWidth: 400
    chartHeight: 400
  themeVariables:
    quadrant1TextFill: "ff0000"
---
quadrantChart
  x-axis Radiated --> Conducted
  y-axis Emissions --> Immunity
  quadrant-1 Conducted Immunity
  quadrant-2 Radiated Immunity
  quadrant-3 Radiated Emissions
  quadrant-4 Conducted Emissions
  
{% endmermaid %}

Tests are run in the order of least likely to most likely to damage the device being tested, so we’re able to run the most tests possible without breaking something. The first test we ran is called Radiated Emissions, which (as you can tell from the chart above) is seeing what bad waves the LumenPnP is kicking out that could mess with other things.

In order to do this, we put the LumenPnP into one of the anechoic testing chambers at keystone, which is electromagnetically isolated from the outside world as much as possible. Full steel enclosure, with panels that are exceptionally good at absorbing electromagnetic waves all along the interior.

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/empty-chamber.png)
*An empty chamber waiting for a LumenPnP*

Then we have the LumenPnP run! I'm running a little script on it that goes through a simulated pick and place cycle, and this both shows us that things are working correctly and kicks out radiated and conducted emissions for testing.

For this radiated emissions test, we check to see what waves it kicks out with a huge antenna. It’s effectively listening to the Lumen, picking up what waves it’s kicking out. You can even think of it as a camera. It picks up what “color” of light the lumen is kicking out, and making sure none of it is too “bright.”

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/antenna.JPG)
*The antenna used for the 30MHz - 1GHz frequency range*

The signal is then processed by this thing, which costs literally $200k. Then it goes through a bunch of fancy filters, and then goes into their software which accounts for all the cables and calibration and such, then it spits out the actual reading. It actually talks to the computer outside the chamber using fiber optic cables so the wire doesnt interfere!

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/bulkhead.png)
*Signals are passed through this heavily shielded bulkhead*

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/desk.png)
*All the signal processing equipment is stored in an equally shielded chamber*

And because the Lumen could be kicking out waves in any direction or orientation, all of this moves! The pedestal rotates and the antenna switches from horizontal to vertical. And the whole antenna even moves up and down as well. And because motors would influence the signals the system used to move the antenna around is fully made of wood and pneumatically actuated.

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/pneumatic-rotation.JPG)
*Pneumatic mechanism for rotating the antenna*

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/pneumatic-winch.JPG)
*Pneumatic mechanism for raising and lowering the antenna*

So then we run the test. First, we do a quick scan of the signals that the antenna is reading. From that scan, we then pick the six highest peaks, called “quasipeaks,” then run a much more thorough test on just those frequencies at every orientation and rotation. If the highest signal from the quasipeak scan is under the red line here (which is the limit dictated by the standard we’re testing against), then we pass! If any one of them is above, then we fail. The quick scan takes around 15 minutes, and six quasipeaks takes just over an hour.

…and then that’s just *one* frequency band. This tie fighter antenna is only good for a certain range. For higher frequencies, we need to use a different antenna, or “horn” as this type is called, and do the same thing all over again. Radiated emissions *alone* took over a day and a half to complete. And it’s the hardest to pass. Electronics love spitting out EM radiation, and keeping it “quiet” enough to fit the standard is really tricky.

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/horn.png)
*This horn is used for much higher frequency bands*

But we did it! The Lumen didnt kick out anything disruptive, and we came in under the standard.

Ok, next up is Radiated Immunity! This is also with waves, but the other way around: we emit an electromagnetic field directed at the Lumen and see if it breaks anything. The setup is really similar, still in the chamber with an antenna, but instead of watching the graph, we watch the Lumen. There’s actually cameras in the chamber that let us watch the device under test, and see if it still maintains normal operation while we’re blasting it. It was really cool and deeply stressful watching the Lumen rotate around, holding my breath hoping that something didn't go wrong. And it didnt! Across all the frequency ranges, the Lumen kept operating as normal.

Next we moved on to conducted tests. These are actually run through touching the machine physically. The first one was conducted emissions. This one is pretty boring. We just hook the Lumen up to a fancy electrical outlet that listens to what electrical noise it kicks into the mains power line. If you’re using a good power supply which we do, this test is generally a non-issue. We also passed this without any trouble.

But the real spooky test is conducted immunity. In this one, we pump a ton of voltage and weird power patterns into the Lumen’s power supply and see if it breaks anything.

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/power-test.JPG)
*CI tests don't need to happen in the chamber*

And again, no issue! The Lumen took 2k volts repeatedly through mains with all kinds of weird power profiles no problem.

And then finally, there were two smaller miscellaneous tests left. Technically they’re radiated immunity and conducted immunity, but they happen on a different bench and are most likely to ruin something, so they’re done last.

The radiated immunity test is called magnetic field immunity, and it’s pretty much just putting the lumen on a table, running a ton of current through a coil around it, and checking to see if anything breaks. Again, no issue here, everything was fine. I was told  it's pretty rare for devices to fail this test.

And lastly is the scariest test of all: ElectroStatic Discharge, or ESD. This test is performed by literally zapping the Lumen with 8k volts with a Marvin the Martian pistol. 

![Image]({{ site.baseurl }}/assets/blog-images/lumen-certs/esd-gun.JPG)
*The scariest piece of equipment*

I was so nervous for this test the whole time I was at Keystone. We prepared for this test when designing all the machine's PCBs, but it was still terrifying. And thankfully, we passed this without issue as well.

And that's it! There were a few other tests that happened and I'm glossing over a lot about the testing procedure, but that’s the bulk of what happened. And we passed first try!

I was absolutely blown away. It’s incredibly rare for this to happen, for a product to pass first try. But the reason that we did is because of the LumenPnP community. Before we went for testing, I asked folks to help me look for potential issues with the machine before going in for testing, and we made a ton of changes to the design as a result of all the feedback. There is no world in which we would have passed first try without the LumenPnP dev community helping us refine the design.

How much did all this cost? Four days of testing and running the 13 tests that we needed cost us $9,250 from Keystone. The tests happened on a Thursday and Friday and then the following Monday and Tuesday for the last two days. Keystone is a bit of a hike from the Opulo office, so I got a hotel Thursday night and Monday night, $92.75 each night. Plus food and gas, the total was around $9,600. And this is just one cycle of testing, where everything went right first try. If you have a few pesky tests that you can't pass, or need to completely redo whole sections, this could easily run you up to $50k. Testing can be really expensive. It's possible to send your device to a testing house overseas that can do it much cheaper, but there come drawbacks with that approach as well.

We've had excellent luck with the certs process as an organization. The LumenPnP does not require a lot of difficult tests to be compliant, and we have an incredibly knowledgable community that helps us catch things early. We'll be sure to update with any new experiences we have with product certification.
