---
layout: post
title: "Lack of price discovery in the Healthcare Market"
date: 2013-01-15
original_url: "https://thebayesianobserver.wordpress.com/2013/01/15/lack-of-price-discovery-in-the-healthcare-market/"
categories: ["machine-learning"]
---
[Price discovery](http://en.wikipedia.org/wiki/Price_discovery) is

> … the process of determining the price of an asset in the marketplace through the interactions of buyers and sellers.

Buyers and sellers of a good or service set the price by expressing how much they are willing to buy or sell for. When a very large number of buyers and sellers interact in this way, the final price of the good or service settles to one that incorporates all this information. However, in the healthcare market, this mechanism is absent.

When you are sick and you visit a doctor, you do not get to ask up front what you will be charged for seeing the doctor! Instead, you present your health insurance card to the receptionist, thereby disclosing information about your ability to pay, and creating information assymetry. The other party (i.e. the healthcare provider) can now select a price , taking into account the information you have just disclosed, and that too, *after* you have made use of their services, rather than before. This is akin to getting to know the price of a haircut in a barber shop, *after* you have had the haircut. There is no price discovery mechanism in the healthcare industry in US. I recommend:

1. Providers should not be allowed to see the insurance coverage a patient has. Each patient should simply be treated. Claims and payments should be handled by a third party, such as a government agency, that acts as a mediator between the hospital and the patient.
2. Providers should be mandated to disclose a menu of charges, like a restaurant or a barber.
3. Providers should charge the same fee, irrespective of whether a patient has insurance or not, or how much insurance coverage she has.

Ostensibly, providers check a patient’s insurance card in order to make sure that the patient can pay for the services she is about to purchase. Instead, this function should be done by a ‘lookup’ over the internet on a server run by a government agency: Input = ‘name of the medical procedure’, Output = ‘Covered or not’. This will prevent the provider from learning about the extent of coverages available to the patient. Not learning about this will force providers to more honestly assess fees, and compete with each other more realistically, bringing down costs borne by the patients. I think this will also prevent providers from passing on large unnecessary fees to insurance companies.

A formal mechanism design formulation of the problem would be interesting to tackle. 4 players: patients, providers, insurance companies, government.
