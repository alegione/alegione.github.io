---
layout: page
title: Shiny apps
description: Shiny apps written by Alistair Legione
---

I have tried my hand at making some Shiny apps, you can access and run them from here

## [PCR assistant](https://alegione.shinyapps.io/PCR-assistant/)
The PCR assistant will help you to set up your conventional PCRs (Polymerase Chain Reactions)
and the occasional qPCR too, depending on your required materials. Just plug in the concentrations
of your working stock, and your desired reaction concentrations, and it will tell you how much of
each reagent to add to your mastermix.
You can then print the resulting table to paste in your lab books
There is also some tabs for primer dilution calculations and dNTP dilution calculations

## [Titration calculations](https://alegione.shinyapps.io/Virus_Titration_Calculators/)
I made this Shiny app for calculation of viral titres. It takes input in the form of
plaque forming units and a dilution factor, and can calculate your original concentration per millilitre
You can also calculate median infectious doses (e.g. EID<sub>50</sub> or TCID<sub>50</sub>)

## [Nanodrop plots](https://alegione.shinyapps.io/NanoDropPlotter/)
A work in progress. This tool allows comparison of multiple Nanodrop '.ndv' files on the one plot. This allows easy comparison between samples
analysed during different time periods. Ideally the finished product will allow the user to download both a plot
of the results and a table of the various metrics. In a perfect world there will also be 'warnings' for high values and details about
potential causes

## [Univariable data analysis](https://alegione.shinyapps.io/Univariable-Test/)
The aim of this tool will be for a user to upload a dataset, and be able to produce simple binary logistic regression
univariable output, with odds ratios and forest plots for easy visualisation of significant results. Currently all it does
is provide a 2x2 table calculator.

## [Veterinarian calculations](https://alegione.shinyapps.io/Vet_Help/)
This Shiny App is for calculations that veterinarians and vet nurses have to do in their workdays.
The aim was to make the process simpler. The item currently published is a feed requirement calculator
for recovering cats. It allows the user to select the food type, and input the cat's weight, and
the output provides the quantity of feed to supply the recovering cat depending on how many days
have passed. This value is based on the resting energy requirement of the cat and the
metabolisable energy in the selected food
