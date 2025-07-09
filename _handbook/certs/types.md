---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# <span class="badge badge-primary">Github CI</span>
#<span class="badge badge-secondary">Web Service</span>
#<span class="badge badge-success">Open Source</span>
#<span class="badge badge-danger">Paid Service</span>
#<span class="badge badge-info">Free Service</span>

title: "Types of EMC Certs and Tests"
layout: single

---

This page is going to give you an overview of the main types of EMC certifications that you should be aware of that are required before marketing your product.

## FCC

The FCC (Federal Communications Commission) is the regulatory body for electronic device compliance in the United States. Being FCC compliant is required to market and sell a electronic device in the US.

FCC compliance comes in two types:

1. **Supplier's Declaration of Conformity** - This is what's called "self-declaration," where the manufacturer itself declares that the device is compliant, and there isn't a formal filing with the FCC. However, the manufacturer is still required to supply testing data that demonstrates that it's compliant; you can't just write up this document and assume you're set to go. This type of certification is acceptable for a large number of devices, generally ones that are less likely to cause issues. 
2. **FCC Certification** - This is the stricter type of certification where you're actually filing with the FCC. This type is *required* for "intentional radiators," or devices that have an antenna (think wifi, bluetooth, etc). These devices are issued an FCC ID which is a unique identification number for that device.

[(Source)](https://www.fcc.gov/general/equipment-authorization-procedures)

## CE
The CE marking indicates that a product has been assessed by the manufacturer and deemed to meet EU safety, health and environmental protection requirements. It is required for products manufactured anywhere in the world that are then marketed in the EU. [Trade.gov](https://www.trade.gov/ce-marking) [Europa.eu](https://europa.eu/youreurope/business/product-requirements/labels-markings/ce-marking/index_en.htm)

CE compliance has one type, which is called the **Declaration of Conformity** (DoC). This is a document that affirms the device is compliant with any required CE standards. It's very similar to the FCC's Supplier's Declaration of Conformity, in that you never end up filing any documents with any organization. When you mark your device with the CE mark and you provide DoC, you're claiming that your device is compliant. However, if a european regulatory body requests your Techinal Documents, you need to provide test data and any relevant information that proves you are compliant. You can't just mark your device and write this document and assume you're good; you **must** have the proof ready to share.

Since Brexit, products sold in Great Britain now require a UKCA mark.  It applies to most products where CE marking can also be used and at present has similar requirements/specifications.  Note for products sold in Northern Ireland a CE mark is still required - read more at [GOV.UK](https://www.gov.uk/guidance/using-the-ukca-marking). In general, most testing houses will consider these the same and test for both together, and issue DoCs together for both of these.

## UL
UL (Underwriter Laboratories) is not a regulatory body, but is actually a third-party organization that has become a ubiquitous certification for safety in most products on the global market. UL is anecdotally one of the hardest certifications to acquire.

Generally, UL is not required for devices that do not have mains power integrated into them. For this reason, many companies will opt for a separate power brick that has been UL certified, and not need to go through this expensive and time consuming process. [Bunnie Huang notes this](https://www.bunniestudios.com/blog/2016/formlabs-form-2-teardown/) about the difference between the Formlabs Form 1 and Form 2.

## EMC Tests

EMC (**E**lectro**m**agnetic **C**ompatibility) tests are roughly categorized into the following quadrant chart:

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

**Radiated** tests involve electromagnetic waves, and typically use an antenna.

**Conducted** tests involve physically touching a conductor in the device.

**Immunity** checks to see how robust the device is to interference.

**Emissions** checks to see how much interference the device itself kicks out.

So, the four quadrants are:

- **Radiated Immunity**
  - How robust is the device to an aggressive electromagnetic field being aimed at it? These tests usually involve an antenna pointed at the device, and "shooting" electromagnetic fields at it across varying frequencies, and checking for abnormal functionality. A pass is generally dictated by the device's ability to maintain operation, or even just recover normal operation in the case of abnormal behavior.
- **Conducted Immunity**
  - How robust is the device to conducted interference? These tests are conducted on any power inputs, but can also be conducted on any ports or interfaces exposed to the user (for example, a USB port).
- **Radiated Emissions**
  - How strong of electromagnetic waves does the device kick out? These tests are effectively checking to make sure the device isn't too noisy and won't affect other devices in the vicinity. These tests are typically the hardest to pass.
- **Conducted Emissions**
  - How strong of electrical noise does the device kick back into connected wires? This typically happens with power, where the mains power source that the device is connected to is checked for any interference caused by the device.

## Which Do I Need?

This is *not* something that can easily be answered on this site. The *only* way to know for sure what tests and agencies you must comply with is by getting the advice of a testing house. It's their job to figure out what you need to do in order to be compliant. Email a few testing houses and get quotes, ask questions, and see what type of testing they sign you up for.
