---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# <span class="badge badge-primary">Github CI</span>
#<span class="badge badge-secondary">Web Service</span>
#<span class="badge badge-success">Open Source</span>
#<span class="badge badge-danger">Paid Service</span>
#<span class="badge badge-info">Free Service</span>

title: "Going In For Testing"
layout: single

---

## Finding a Cert House

When looking for a company that can perform the tests you need, there's a number of things you should be considering:

- Are they capable of performing the tests I need? For example, do they have anecoic chambers on site? Do they state on their website that they're capable of issueing CE DoCs and FCC SDoCs?
- Are they capable of determing the exact standards and tests necessary in order for your device to be compliant?
- Where are they? You should very likely be present for testing, espeically if it's your first time. Is it close enough to drive there every day? Will you have to travel?

Once you've found a few options, it's time to request a quote! Many cert houses have an online form, or just an email address where you can contact them. When you reach out, your email should contain:

- A bit about your company. Who are you and what are you making?
- What is your device? What does it do, what are its features? If it has a datasheet or product page, be sure to include that.
- Where are you looking to sell your device?
- Are there any active antenna on your device? Any Bluetooth or Wifi? And if so, are the antennas part of a pre-certified module?
- Your best guess of what class the device is, and what types of tests are needed.
- Your availability for when testing can happen.
- Any questions about tests and certifications are necessary. It's their job to tell you what you need to be compliant!
- A request for a quote.

Many certification houses are also happy to hop on the phone and have a quick discussion about your product if there's some more complicated requirements.

## Reviewing a Quote

Once you receive your quote, it should contain a list of all the tests they deem necessary in order to be compliant.

It's important that the quote also contains a formal test report, and the Declaration of Conformity documents or any filing with the FCC necessary for compliance. These documents are what the government organizations actually care about, so having these at the conclusion of testing is paramount.

In general, it's good to have a few quotes from a few different certification houses.

**You should get a quote before even designing your product.** When desigining your device, you should know exactly which directives you need to comply with. Don't let yourself be surprised by a test that you need to pass that you didn't consider during the design phase.

## Should you do Pre-Testing?

Because it's so expensive to book testing time, many folks will do "pre-testing," or a slightly less accurate test that still gives you a good idea about how well you'll perform in the actual test. This lets you try a number of things at a much lower cost, and when you have high confidence that you'll pass the real thing, then you pay for the expensive chamber time.

Whether or not this is useful is largely dependent on the cost of the pre-testing, and the likelihood that you'll fail.

## Preparing for Testing

When performing testing, the device will need to be able to perform its "worst-case continuous mode of operation" autonomously. For example, a blender would be left running on "HIGH" in the chamber during testing, and a 3D printer might just run a print using the highest temperature material it supports.

Sometimes this mode is just part of how the device works normally like in the case of a blender, or other times this needs to be a dedicated mode or script to simulate the worst case. If this is true for your device, you'll need to write a "test mode" operation for your device to do this. For example, this mode might refresh the display at the highest frame rate, move all motors at their maximum current, and send data across any communication busses at the highest rate possible during normal operation.

You should also come with a few backups of your device. Many of the tests that are likely to be performed can be destructive, so don't allow failing one test prevent you from running all the other tests you're scheduled for. If your device is large or prohibitavely expensive to provide a few, bring many spare parts instead, and prepare for a hot-swap.

It can also be good to bring:

- Multimeter or even a oscilloscope if it might be helpful for debugging issues with your device
- Clampable ferrite beads to test different values
- Soldering iron and spare components of different values if a component hot-swap on a PCB is necessary
- Mobile electrical tool set
- Many extra power supplies, IEC cables
- Aluminum tape and Aluminum foil (used for testing shielding certain parts of the device during RE to determine what is kicking out interference)
- Electrical tape
- Anything needed to update the functionality of your device (eg router as an access point for a wireless device, monitor and keyboard for changing configuration, programming cable for flashing different versions of firmware)

## Testing

Actually doing the testing is both a stressful and boring experience. It's the definition of the phrase "hurry up and wait." It's comprised of long periods of waiting, punctuated by brief stressful moments of intense work and disappointment.

In general, tests will be run in order of least likely to damage the device, to most likely. This is done so the most tests can be performed before potentially breaking the device.

## Solving Issues

It's incredibly likely that you'll fail your first time getting a device tested. Passing is very hard to do, and approximately half of the time, a device requires at least a second test.

Solving the issue that caused your device to fail is greatly dependent on which test it is. Ask your technician what they think would be helpful to solve the problem, as they see hundreds of similar devices pass and fail, so they're well attuned to what about your device is likely causing the issue. They should be your main source of information when addressing an issue.
