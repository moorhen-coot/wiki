---
layout: post
title: "Creating Figures with Moorhen"
date: Fri 3 Nov 16:08:00 GMT 2023
---

## Introduction

This tutorial will explain how to make high-quality figures of molecular models, maps, and analysis/validation markup with Moorhen.
Load tutorial data 1 into Moorhen by:

Begin by clicking on the Moorhen burger icon and then 
 clicking on the "File" button and selecting "Load tutorial data" and then selecting tutorial 1 and clicking "OK". You should see something like this:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Initial-View.png)

This shows a cylinder representation of the model and a chickenwire representation of the electron density. 

Moorhen allows you to have finer control over what is drawn. For instance there are more representations available and we can turn them on or off from the "Models" and "Maps" dialogs.

We will begin by turning off the electron density map to allow us to see the model more clearly. To do this first click on "Maps" in the menu. You should see this:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Map-Dialog.png)

Turn off the maps by clicking on each of the eye icons. The slashes in the eyes will disappear and the maps will be hidden:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Maps-Hidden.png)

Click on the "X" in the top right of the "Maps" dialog to dismiss it.

### Switching representation style

Click on "Models" in the left-hand menu to show the "Models" dialog.

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Model-Dialog.png)

The "Bonds" button is highlighted to show that bonds are being drawn. CVlick on this to hide the bonds and then click on "Ribbons" to show ribbons.

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ribbon.png)

Try the "C-As", "Gauss.", "Surf." and "Spheres" buttons.

## Colour Schemes

The model representations shown so far have been coloured with a default colouring scheme: colour by chain mode. Moorhen allows you to change the colour scheme.

Click on the "colour bucket" icon ![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Colour-Bucket-55.png) to the right of the atom representations buttons. This will display the colour edit dialog showing the current colour rules.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Colour-Dialog.png)

The lower section shows the current colour rules. Each colour rule  supersedes the rules above it. To demonstrate this we will create a new colour rule. First change the "Rule type" from "By molecule" to "By atom selection". An "Atom selection" box appears, type "//A/87-298" into this box. Choose a new colour e.g. bright green from the colour picker to the right. Click "Add rule". The helical domain will turn bright green and your new colour rule appears at the bottom of the list of rules.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Colour-Rules.png)

(Clicking on the up arrow of this rule to make it go up the list will mean that is will be superseded by Rule 2 and the model will change back to previous appearance.)

## Additional Representations

## Ball and Stick Variants

Bond width options, etc.

## Symmetry

## Surfaces

Molecular, gaussian

## Maps and map masking

Style, colour, transparency, contour level, radius, 

## Validation and Analysis

## Lighting Effects

## Preferences

## Saving your image

## Video Recording
