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

Sometimes you may wish to add additional representations, e.g. to display only a subset of the atoms in a particular style. To do this, click
on the "+" button to the right of the main representation buttons. A new dialog will appear.
![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr.png)

In the new dialog you can select "Style" and "Residue selection" for the new representation.
Change "Selection" to "Spheres" and "Residue selection" to "Residue Range". A "Chain" selector and sequence viewer will appear.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Sequence.png)

The sequence viewer may be scrolled left and right by clicking on it and dragging. Move it around and then click on residue number 50 (R), then **shift-click** on residue number 65 (K). Two triangles connected by a line will appear - this represents the residue range selected.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Sequence-Selected.png)

Then click on the "Create" button at the bottom of the dialog. The new spheres will be drawn and a button labelled "Spheres //A/50-65"
which allows you to hide/show the spheres (like the main representations) will be shown in the "Models" dialog.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Spheres.png)

The new button also has "pen" and "dustbin" parts. The "pen" allows you to edit the atom selection/colouring/style;
the "dustbin" deletes the new representation. Click on the pen and then uncheck the "Apply general colours settings" button. You
will a new drop down menu, this will be set to "User defined colour":

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Custom-Colour.png)

Click on the green square to the right of this menu. A colour picker will appear. Pick a new colour (e.g. a shade of purple) 
and then click "Apply". Your spheres (and the representation hide/show button) will change colour.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Custom-Colour-Applied.png)

Now hide the new spheres and the default bond representations by clicking the appropriate buttons in the "Models" dialog. Then create a
new "Ribbons" representation coloured by temperate factor. First click on "+" again and then use the following settings:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Ribbon-BFactor-Settings.png)

Then click "Apply":

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Ribbon-BFactor.png)

## Ball and Stick Variants

There are many options to customize the drawing of both maps and models. We begin here by showing how to change some settings for
the drawing of "Bonds" model representations. Click on the gear wheel button ![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Model-Gear-Wheel.png) to the right of the atom representations buttons. A large dialog with many options will appear:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Model-Options.png)

The top slider ("Bond width") controls the thickness of the bond. The second slider ("Radius-Bond ratio") changes the relative size of
the sphere drawn at each atom position to the bond. Try changing these two sliders to about 0.2 and 2.0 respectively. Your "bonds" will
change to balls and sticks.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick.png)

The third slider in the settings dialog varies the smoothness of the cylinders drawing the bonds. The effect of this slider
will be most noticed in close up scenes. Zoom in closely and rotate the scene so that you can see a bond/sphere intersection
clearly:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick-Close.png)

Now change "Bond Smoothness" to smooth to produce a much rounder cylinder:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick-Close-Smooth.png)

## Symmetry

## Surfaces

Molecular, gaussian

## Maps and map masking

Style, colour, transparency, contour level, radius, 

## Validation and Analysis

## Clip, Fog and Lighting Effects

## Preferences

## Saving your image

## Video Recording
