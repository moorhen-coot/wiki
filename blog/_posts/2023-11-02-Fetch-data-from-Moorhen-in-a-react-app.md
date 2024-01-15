---
layout: post
title: "Fetch data from Moorhen in your React app"
date: Thu 2 Nov 16:33:00 GMT 2023
---

## Background and requirements

This tutorial is part of a series that explains how to integrate Moorhen into a react app:

1. Build a simple Moorhen app, starting from `create-react-app` [tutorial 1](https://moorhen-coot.github.io/wiki/2023/07/06/Using-Moorhen-in-a-React-app.html)
2. Specialize that app to pull in structures and maps from an API (this tutorial) 
3. Provide dedicated UI elements to navigate around features of a structure within the Moorhen component [tutorial 3]()

This tutorial assumes you have completed the steps described in [tutorial 1](https://moorhen-coot.github.io/wiki/2023/07/06/Using-Moorhen-in-a-React-app.html).

## Creating a middleman between our App and Moorhen

After completing [tutorial 1](https://moorhen-coot.github.io/wiki/2023/07/06/Using-Moorhen-in-a-React-app.html), your `./src/App.js` file should look something like this:
```javascript
import { MoorhenReduxProvider, MoorhenContainer } from 'moorhen'

function App() {
  return (
    <MoorhenReduxProvider>
      <MoorhenContainer/>
    </MoorhenReduxProvider>
  );
}
```
As you can see, the component `MoorhenReduxProvider` sits on top of Moorhen's component tree and it's the component in charge of providing access to a redux store that holds all the states in Moorhen. All components rendered within this redux provider will have access to these states, which is the recommended way of fetching data from Moorhen. Let's write a component that has access to Moorhen's redux store and sits on top of the `MoorhenContainer`. We will use this component to control the interactions between our App and Moorhen. You can name this component whatever you want, so let's call it `MoorhenController` and let's write it in a separate file `./src/MoorhenController.js`
```javascript
import { MoorhenContainer } from 'moorhen'

export const MoorhenController = (props) => {

    return  <MoorhenContainer />
}
```
At the moment `MoorhenController` simply renders `MoorhenContainer`, we'll change that later. In `./src/App.js`, let's replace `MoorhenContainer` with our `MoorhenController`
```javascript
import { MoorhenController } from './MoorhenController'
import { MoorhenReduxProvider, MoorhenContainer } from 'moorhen'

function App() {
  return (
    <MoorhenReduxProvider>
      <MoorhenController/>
    </MoorhenReduxProvider>
  );
}
```
From now on all of our changes will focus on `MoorhenController`. This component will be the middleman between our App and Moorhen, and it will let us both fetch and set data from/into Moorhen.

## Fetching data from Moorhen using MoorhenController

Now, let's access data in Moorhen. To do this, we will retrieve data from Moorhen's redux store using `useSelector`. For instance, to access the molecules loaded in Moorhen we would use
```javascript
import { useSelector } from 'react-redux'

const molecules = useSelector((state) => state.molecules)
```
If we wanted our App to do something after a change in the molecules loaded in Moorhen, we could use React's `useEffect` hook to do so. Let's write such hook in our `MoorhenController`. Right after we define `collectedProps` and before we return `MoorhenContainer`, let's add the following:
```javascript
const molecules = useSelector((state) => state.molecules)

useEffect(() => {
    console.log('>>> Moorhen: Molecules have changed...')
    console.log('>>> Moorhen: Current no. of molecules: ', molecules.length)
    // Now we could do something useful...
}, [molecules])
```
In this case `molecules` is a list of [MoorhenMolecules](https://moorhen-coot.github.io/Moorhen/MoorhenMolecule.html). Similarly, to access a list of all loaded [MoorhenMaps](https://moorhen-coot.github.io/Moorhen/MoorhenMap.html) you could use:
```javascript
const maps = useSelector((state) => state.maps)
```
Or you could write a function that exports all molecules loaded in Moorhen in their current state using React's `useCallback` (for example if you want to do this after a button click)
```javascript
import { useCallback } from 'react'

const exportMolecules = useCallback(async () => {
    // A list of PDB strings
    const pdbStrings = await Promise.all(
        molecules.map(molecule => molecule.getAtoms())
    )
    // Now you can do something usefull...
}, [molecules])
```

## Using MoorhenController to set input data in Moorhen

We can also use `useDispatch` from redux in combination with a series of action creators shipped with Moorhen in order to dispatch changes to the app. For example, if we wanted to change the background colour of the canvas we could do the following 
```javascript
import { useDispatch } from 'react-redux'
import { setBackgroundColor } from 'moorhen';

const dispatch = useDispatch()

// Background colour is defined as a list of four floats [r, g, b, a]
dispatch( setBackgroundColor([0., 0., 0., 0.]) )
```
Again, we can combine this with a React's `useEffect` hook to achieve different results. For example if we want to set the colour on mount in our `MoorhenController` component, we could add this
```javascript
    const dispatch = useDispatch()

    useEffect(() => {
        console.log('>>> Moorhen: App has mounted, dispatch colour change...')
        dispatch( setBackgroundColor([0., 0., 0., 0.]) )
    }, [])
```
Similarly, we can use `dispatch` to set input molecules and maps. However this requires more sophisticated control that we will discuss in the next section.

## Fine control of Moorhen states

If we look back to our `MoorhenContainer`, you will see that at the moment we are not passing any variables in `props`. Let's change that. First, let's start by passing some references to `MoorhenContainer`. These react references are used internally in Moorhen to store data. All props are optional in `MoorhenContainer`, which means it is up to you to specify which variables you want access within your app. Here we are going to set the most commonly used ones, but bear in mind it's possible you will need some additional ones depending on what you want to do. The full list of variables that can be passed as `props` to `MoorhenContainer` can be found in our [dev documentation](https://moorhen-coot.github.io/Moorhen/global.html#MoorhenContainer).
```javascript
export const MoorhenController = () => {
    // In most cases you will want these refs defined within your app
    const glRef = useRef(null)
    const timeCapsuleRef = useRef(null)
    const commandCentre = useRef(null)
    const moleculesRef = useRef(null)
    const mapsRef = useRef(null)

    const collectedProps = {
        glRef, timeCapsuleRef, commandCentre, moleculesRef, mapsRef, 
    }

    return  <MoorhenContainer {...collectedProps}/>
  }
```
Now that we have access to Moorhen's internal references, we will use `glRef` and `commandCentre` to create and dispatch into Moorhen a new [MoorhenMolecule](https://moorhen-coot.github.io/Moorhen/MoorhenMolecule.html) using the `addMolecule` action creator shipped with Moorhen. Let's write a new function to do this, `loadMolecule`
```javascript
import { MoorhenMolecule, addMolecule } from 'moorhen'
import { useSelector, useDispatch } from 'react-redux';
    
const dispatch = useDispatch()
const defaultBondSmoothness = useSelector((state) => state.sceneSettings.defaultBondSmoothness)
const backgroundColor = useSelector((state) => state.canvasStates.backgroundColor)
    
const loadMolecule = async () => {        
    // Create a new molecule and assign user-defined defaults
    const newMolecule = new MoorhenMolecule(commandCentre, glRef)
    newMolecule.setBackgroundColour(backgroundColor)
    newMolecule.defaultBondOptions.smoothness = defaultBondSmoothness
        
    // Load molecule into coot instance and draw it using "bonds"
    await newMolecule.loadToCootFromURL('/file/path/uri', 'molecule-name')
    await newMolecule.fetchIfDirtyAndDraw('CBs')
        
    // Centre on the middle of the molecule with animation
    await newMolecule.centreOn('/*/*/*/*', true)
        
    // Dispatch the new molecule to Moorhen
    dispatch( addMolecule(newMolecule) )
}
```

Almost there! Now we just need to call `loadMolecule` within `MoorhenController`. However, we cannot simply create and dispatch a new molecule into Moorhen at any given point. This can only be done after the libcoot instance has booted up, which means we need wait for libcoot instance to initiate before we call `loadMolecule`. Luckily Moorhen's redux store contains a state named `cootInitialized` that indicates whether the libcoot instance has booted up already or not. Generally you want to wait until this happens before you start sending instructions to Moorhen. To achieve this, we need to again combine React's `useEffect` hook with Redux `useSelector`.

```javascript
    const cootInitialized = useSelector((state) => state.generalStates.cootInitialized)
    
    useEffect(() => {
        if (cootInitialized) {
            // This only happens after coot instance is created
            loadMolecule()
        }
    }, [cootInitialized])
```
And if we put it inside our `MoorhenController` it would look like this
```javascript
import { MoorhenMolecule, addMolecule } from 'moorhen'
import { useSelector, useDispatch } from 'react-redux'
import { useRef, useEffect } from 'react'

export const MoorhenController = () => {
    const glRef = useRef(null)
    const timeCapsuleRef = useRef(null)
    const commandCentre = useRef(null)
    const moleculesRef = useRef(null)
    const mapsRef = useRef(null)

    const dispatch = useDispatch()
    const cootInitialized = useSelector((state) => state.generalStates.cootInitialized)
    const defaultBondSmoothness = useSelector((state) => state.sceneSettings.defaultBondSmoothness)
    const backgroundColor = useSelector((state) => state.canvasStates.backgroundColor)

    const loadMolecule = async () => {        
        // Create a new molecule and assign user-defined defaults
        const newMolecule = new MoorhenMolecule(commandCentre, glRef)
        newMolecule.setBackgroundColour(backgroundColor)
        newMolecule.defaultBondOptions.smoothness = defaultBondSmoothness
        
        // Load molecule into coot instance and draw it using "bonds"
        await newMolecule.loadToCootFromURL('/file/path/uri', 'molecule-name')
        await newMolecule.fetchIfDirtyAndDraw('CBs')
        
        // Centre on the middle of the molecule with animation
        await newMolecule.centreOn('/*/*/*/*', true)
        
        // Dispatch the new molecule to Moorhen
        dispatch( addMolecule(newMolecule) )
    }

    useEffect(() => {
        if (cootInitialized) {
            loadMolecule()
        }
    }, [cootInitialized])


    const collectedProps = {
        glRef, timeCapsuleRef, commandCentre, moleculesRef, mapsRef, 
    }

    return  <MoorhenContainer {...collectedProps}/>
}
```
The same approach could be done to load a given map
```javascript
import { MoorhenMap, addMap } from 'moorhen'

export const MoorhenController = () => {
    
    // ...

    const loadMap = async () => {        
        // Create a new map and load a map file into the libcoot instance
        const newMap = new MoorhenMap(commandCentre, glRef)
        await newMap.loadToCootFromMapURL('/file/path/uri', 'map-name')
               
        // Centre on the middle of the map
        await newMolecule.centreOnMap()
        
        // Dispatch the new map to Moorhen
        dispatch( addMap(newMolecule) )
    }

    useEffect(() => {
        if (cootInitialized) {
            loadMolecule()
            loadMap()
        }
    }, [cootInitialized])

    // ...
}
```
That's it! Now you should be able to load molecules and maps into Moorhen from your host app and import them back into your app. Here's a full list of all the different states held in Moorhen's redux store and their types. Generally, action creators can be imported from `moorhen` module and are named with the convention `set<StateName>`, like for example `setBackgroundColor`. The only two exceptions are `molecules` and `maps`, which have action creators named `add<StatName>` and `remove<StateName>` like for example `addMolecule` and `removeMolecule`.
```javascript
    interface State {
        molecules: Molecule[];
        maps: Map[];
        mouseSettings: {
            contourWheelSensitivityFactor: number;
            zoomWheelSensitivityFactor: number;
            mouseSensitivity: number;
        };
        backupSettings: {
            enableTimeCapsule: boolean;
            makeBackups: boolean;
            maxBackupCount: number;
            modificationCountBackupThreshold: number;     
        };
        updatingMapScoresSettings: {
            defaultUpdatingScores: string[];
            showScoresToast: boolean;
        };
        shortcutSettings: {
            shortcutOnHoveredAtom: boolean;
            showShortcutToast: boolean;
            shortCuts: string;        
        };
        labelSettings: {
            atomLabelDepthMode: boolean;
            GLLabelsFontFamily: string;
            GLLabelsFontSize: number;
            availableFonts: string[];
        };
        sceneSettings: {
            defaultBackgroundColor: [number, number, number, number];
            drawCrosshairs: boolean; 
            drawAxes: boolean; 
            drawFPS: boolean; 
            drawMissingLoops: boolean; 
            drawInteractions: boolean; 
            doPerspectiveProjection: boolean; 
            useOffScreenBuffers: boolean; 
            depthBlurRadius: number; 
            depthBlurDepth: number; 
            ssaoBias: number; 
            ssaoRadius: number; 
            doShadowDepthDebug: boolean; 
            doShadow: boolean; 
            doSSAO: boolean; 
            doOutline: boolean; 
            doSpinTest: boolean;
            defaultBondSmoothness: number,
            resetClippingFogging: boolean; 
            clipCap: boolean;
            backgroundColor: [number, number, number, number];
            height: number;
            width: number;
            isDark: boolean;
        };
        miscAppSettings: {
            defaultExpandDisplayCards: boolean; 
            transparentModalsOnMouseOut: boolean; 
            enableRefineAfterMod: boolean; 
        };
        generalStates: {
            devMode: boolean; 
            userPreferencesMounted: boolean;
            appTitle: string;
            cootInitialized: boolean;
            notificationContent: JSX.Element;
            activeMap: Map;
            theme: string;
            residueSelection: ResidueSelection;
            isChangingRotamers: boolean;
            isDraggingAtoms: boolean;
            isRotatingAtoms: boolean;
            newCootCommandAlert: boolean;
            showResidueSelection: boolean;
        };
        hoveringStates: {
            enableAtomHovering: boolean;
            hoveredAtom: HoveredAtom;
            cursorStyle: string;
        };
        activeModals: {
            showModelsModal: boolean;
            showMapsModal: boolean;
            showCreateAcedrgLinkModal: boolean;
            showQuerySequenceModal: boolean;
            showScriptingModal: boolean;
            showControlsModal: boolean;
            showFitLigandModal: boolean;
            showRamaPlotModal: boolean;
            showDiffMapPeaksModal: boolean;
            showValidationPlotModal: boolean;
            showLigandValidationModal: boolean;
            showPepFlipsValidationModal: boolean;
            showFillPartialResValidationModal: boolean;
            showUnmodelledBlobsModal: boolean;
            showMmrrccModal: boolean;
            showWaterValidationModal: boolean;
            focusHierarchy: string[];
        };
        mapContourSettings: {
            visibleMaps: number[];
            contourLevels: { molNo: number; contourLevel: number }[];
            mapRadii: { molNo: number; radius: number }[];
            mapAlpha: { molNo: number; alpha: number }[];
            mapStyles: { molNo: number; style: "solid" | "lit-lines" | "lines" }[];
            defaultMapSamplingRate: number;
            defaultMapLitLines: boolean;
            mapLineWidth: number;
            defaultMapSurface: boolean;
            mapColours: { molNo: number; rgb: {r: number, g: number, b: number} }[];
            negativeMapColours: { molNo: number; rgb: {r: number, g: number, b: number} }[];
            positiveMapColours: { molNo: number; rgb: {r: number, g: number, b: number} }[];
        };
        moleculeRepresentations: {
            visibleMolecules: number[];
        };
    }
```