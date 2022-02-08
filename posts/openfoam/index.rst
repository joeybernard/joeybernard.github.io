.. title: OpenFOAM
.. slug: openfoam
.. date: 2022-02-07 22:00:57 UTC-04:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

To CFD, or not to CFD?

One area that chews up a lot of cycles on machines around the world is CFD. What is CFD? CFD is short for Computational Fluid Dynamics. The general idea is to model the flow of gases and liquids (or fluids) as they interact with solid surfaces. This type of modelling is used in designing aircraft, automobiles, submarines, and fan blades. Basically anything that travels through water or air. As you increase the complexity of the surfaces, or increase the complexity of the flow (such as going from subsonic to supersonic), the amount of computer time needed to model it goes up. One of the big packages available to do CFD is the suite of programs made by Ansys. Several groups here at my university use it. But, there is an open-source option available, OpenFOAM. This month, we'll look at what we can accomplish with OpenFOAM. The OpenFOAM project includes binary packages as deb files or RPM files. You can also download a source code package of files or even download directly from the git repository. 

OpenFOAM (Open Source Field Operation and Manipulation) is basically a set of C++ libraries that are used in the various processing steps. OpenFOAM, just like most other CFD packages, breaks down the work to be done into three separate steps. The first step is called pre-processing. In pre-processing, you define the problem you are trying to model. This involves defining the boundary conditions given by the solid objects in your model. You also describe the characteristics ofthe fluid that you are trying to model, including viscosity, density, and any other properties which are important for your model. The next step is called the solver step. This is where you actually solve the equations which describe your model. The third step is called post-processing. This is where you take a look at the results and visualize them so that you can see what happens in your model. An obvious consequence of this breakdown is that most of the computational work takes place during the solver phase. The pre- and post-processing steps can usually be done on a desktop, while the solver step can easily use up 50 or 100 processors. OpenFOAM includes several pre- and post-processing utilities, along with several solvers. But the real power comes from the fact that, since OpenFOAM is library based, you can build your own utilities or solvers by using OpenFOAM as a base. This is very useful in a research environment where you may be trying something no one else ever has.

A model in OpenFOAM is called a case. Cases are stored as a set of files within a case directory. Many other CFD packages use a single file instead. A directory allows you to separate the data from the control parameters from the properties. Case files can simply be edited using any text editor, such as emacs or vi. Pre-processing involves creating all of the files required for the case you are investigating. The first step is mesh generation. Your fluid (be it a liquid or a gas) is broken down into a collection of discrete cells, called a mesh. OpenFOAM includes a number of utilities which will generate a mesh based on a description of the geometry of your fluid. For example, the blockMesh utility generates simple meshes of blocks; the snappyHexMesh utility generates complex meshes of hexahedral or split-hexahedral cells. If you wanted to generate a basic block mesh, you would layout the details in a dictionary file, called blockMeshDict, in the subdirectory "constant/polyMesh" within your case subdirectory. The file starts with
```
   FoamFile
   {
      version     2.0;
      format      ascii;
      class       dictionary;
      object      blockMeshDict;
   }
```
Case files in general start with a header of this format, describing what each case file consists of. In this particular file, you can define sections containing vertices, blocks, edges, or patches. Once you have created this file, you can run the utility "blockMesh" to process this dictionary file and generate the actual mesh data that will be used in the computation. The next step is to set your initial conditions. This is done by creating a subdirectory called "0", and placing the relevant case files here. These case files would contain the initial values and boundary conditions for the fields of interest. If you were looking at a fluid flowing through a cavity, say, you may be interested in the pressure and velocity. So, you would have two files in the "0" subdirectory describing these two fields. You also need to set any important physical properties in files stored in the "Dictionaries" subdirectory. These files end with "Properties". This is where you would define items like viscosity. The last step in pre-processing is to setup the control file. This file is named "controlDict" and is located in the "system" subdirectory. As an example, let's say you wanted to start at t=0, run for 10 seconds with a timestep of 0.1 seconds. This section of the control file would look like
```
   startFrom     startTime;
   startTime     0;
   stopAt        stopTime;
   stopTime      10;
   deltaT        0.1;
```
You also set output parameters in this control file. You can set how often OpenFOAM writes output with the writeControl keyword. So let's say you wanted to write out the results every 10 timesteps. This section of the control file would look like
```
   writeControl        timeStep;
   writeInterval       10
```
This will tell OpenFOAM to write out results every 10 time steps into separate subdirectories for each write. These subdirectories would be labelled with the time step. You can also set the file format, the precision of results and file compression, among many other options. Before you actually start the solver step, it is probably a good idea to check the mesh to be sure that it looks right. There is a post-processing tool called "paraFoam" which you can use. If you are in your case directory, calling "paraFoam" will load it up. Or, you can specify another directory location with the command line argument "-case xxx" where xxx is the case directory you are interested in.

The next step is to run a solver on your model and see what you get. Solvers tend to be specialized, in order to solve one particular class of problem efficiently. So OpenFOAM comes with a rather large set of standard solvers out-of-the-box. If you are interested in solving a laminar flow problem for an incompressible fluid, you would likely use "icoFoam". Or, if you are interested in looking at cavitation, you could use "cavitatingFoam". Or you may want a solver for internal combustion engines ("engineFoam"). Take a look at the documentation and see what is available. Once you know which solver you are going to use, you can run it by simply executing the relevant binary from within your case directory, or you can use the "-case" command line argument to point to another case directory. 

The last step is the post-processing step, where you actually look at the results and see what happened inside your model. Here, you can use the supplied utility paraFoam. It can accept a "-case" command line argument, just like all of the other utilities we've looked at. You can then manipulate the data and look at various time slices. You can generate isosurface and contour plots, vector plots or streamline plots. You can even create animations, although not directly. You can get paraFoam to output image files representing movie frames. So they would be saved with file names of the form
```
   fileroot_imagenum.fileext
```
You can then take this sequence of images and run them through something like the convert utility from ImageMagick to bundle them together into a single movie file.

As a final comment, in both the pre- and post-processing steps, there are utilities that allow you to convert to and from file formats used by other CFD packages, including fluent, CFX, and gambit, to name just a few. This comes in handy if you are collaborating with other people who happen to be using one of these other packages. If you are working with someone who is using fluent, you would use "fluentMeshToFoam" in your pre-processing step and "foamMeshToFluent" in your post-processing step.

This very short article can't do anymore than give you a small taste of OpenFOAM. If you are interested in fluid dynamics, you should definitely take a look at OpenFOAM. The home page includes links to great documentation and several tutorials. The installation package also includes several example cases so you can see how standard problem sets are handled. You can usually use one of these examples as a jumping off point for your own problem. Go and check it out and see if it can help you in your work. 

Links
Homepage - http://www.openfoam.com
