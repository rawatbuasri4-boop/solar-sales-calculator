# Solar Sales Calculator

A Thai-language solar sizing and package-selection tool developed by Rawat Buasri to support solar sales consultations. It turns a customer's appliance usage into a preliminary solar capacity estimate and a package comparison that can be discussed during the sale.

[Open the live application](https://sell-rawat.netlify.app/)

## Business context

Sales conversations involve understanding which appliances a customer uses, how many they have, and how long they operate during the day. This calculator captures those inputs in a consistent form and presents a preliminary recommendation to support product explanations and customer decisions.

The application connects customer needs, input requirements, calculation rules, and a usable sales-support interface. Its intended contribution is to make sales consultations easier and more consistent.

## Features

- Select single-phase or three-phase packages.
- Add multiple air conditioners with different capacities and quantities.
- Enable common appliances and adjust their quantities and operating hours.
- Add a custom appliance with a name, wattage, quantity, and hours of use.
- Estimate daily energy demand and the corresponding solar capacity.
- Display the selected package, panel count, inverter model, reference prices, estimated savings, and a simple payback estimate.
- Compare up to three matching packages from the embedded catalog.

## Sales workflow

```mermaid
flowchart LR
    A[Discuss customer needs] --> B[Choose phase and appliances]
    B --> C[Enter quantities and operating hours]
    C --> D[Estimate demand and capacity]
    D --> E[Match embedded solar packages]
    E --> F[Explain options to the customer]
```

## Run locally

Download this repository and open `index.html` in a modern browser. Internet access loads Bootstrap and the Sarabun font from their CDNs.

## Technology

- HTML for the form and result panels.
- CSS and Bootstrap 5.3.3 for the interface.
- Vanilla JavaScript for state, calculations, and catalog matching.
- Netlify for the existing live deployment.

## Calculation rules in this source

The current implementation uses the following rules and embedded assumptions.

| Item | Rule |
| --- | --- |
| Daily consumption | Sum of watts x quantity x operating hours for enabled appliances |
| Capacity estimate | Daily kWh / 4.5 peak-sun hours / 0.80 system factor |
| Package selection | Lowest `exvat` value among packages with capacity at least equal to the estimate |
| Monthly savings estimate | Rounded daily kWh x 30 x 5 baht |
| Simple payback estimate | Package `incvat` / monthly savings / 12, rounded up |

The displayed figures depend on the input assumptions and embedded package data.

## Review notes from source inspection

- The embedded catalog stores `exvat` values that are higher than `incvat` values. The tax labels and intended price values need confirmation before using the displayed prices for quotations.
- When demand exceeds every catalog package, `findPackage` returns the last catalog entry. The interface needs an explicit out-of-range result to make this situation clear.
- Appliance wattages, generation assumptions, electricity cost, and catalog prices are hardcoded reference values. They need review for a customer's actual installation and current sales catalog.

## Source provenance

`index.html` is a byte-for-byte copy of the public page retrieved from [the original deployment](https://sell-rawat.netlify.app/) on 26 November 2026. It also matches the author's local `solar_v3_pricelist.html` source file. This repository packages the existing application and documents its current behavior.

## Author

Rawat Buasri

[GitHub profile](https://github.com/rawatbuasri4-boop)
