# ldtk_to_clr Readme

Updated 4/23/2026

LDtk to clr tool by RuDeE@thejankshop in collab with Copilot.

This folder contains an unpacked MTM2 .pod file for a basic working MTM2 track with textures from my Kryptik Mountains track...

PLUS! 

Two additional new tools for painting your track's textures using LDtk:

1. tex_to_tileset.py is a script for converting a .tex file from the data/ folder to a 4 columns by X rows .png tile set for use in LDtk (see kmtemp_tiles.png in the folder), and
2. ldtk_to_clr_v2.py for taking a .ldtk project of the appropriate shape (use the KMtemplate.ldtk as an example to follow) and converting it to a MTM2 .clr file (living in the data/ folder) for loading your LDtk painted map into Traxx or TrackED.

The included kmtemplate.ldtk project is already set up with some simple preset rules for painting rock, mud, and sand over the main grass ground texture (see below). The main LDtk setup is a single world with 16 levels arranged in a 4 by 4 square around the LDtk origin. Each level is 4096 by 4096, and this setup is required to mirror the MTM2 map size (a 256 by 256 grid of 64 by 64 tiles) following the LDtk editor's constraints. 

There are a couple of different layers in the example kmtemplate.ldtk (explained from bottom to top):

-The main tiles layer has a grid size of 64 pixels (required and matching the individual texture size of MTM2 textures) and is filled with the basic grass ground texture.

-the IntGrid_Baked layer has some examples I painted using the rules from the IntGrid layer above it.

-Finally, the IntGrid layer has the basic rules I set up for painting with rock, sand and dirt. After painting your own design, you must bake the IntGrid layer before running the ldk_to_clr* script.

Usage:

***tex_to_tileset.py***

Run python tex_to_tileset.py -h for the list of inputs.

To use tex_to_tileset.py, you need a MTM2 .tex file in the data/ folder giving a full list of the textures from the art/ folder that you want to use for your track; e.g. see kmtempla.tex in the data/ folder (just right click and open in notepad to view).

Just right click in the main KMtemplate folder and select Open in Terminal, then run 

python .\tex_to_tileset.py .\DATA\KMTEMPLA.tex art/ kmtemp_tiles.png

to generate kmtemp_tiles.png from .\DATA\KMTEMPLA.tex using textures from the art/ folder.

NB. The script assumes you have converted all of your MTM2 .raw textures to .png first. An easy way to do this is using dummiesman's triraw tool from https://4x4evolution.net/Downloads/Utilities/triraw/triraw.zip
Just select all of your .raw textures and drag and drop them onto triraw.exe to convert them.

***ldtk_to_clr_v2.py***

Run python ldtk_to_clr_vr.py -h for the list of inputs.

To use this script, you just need an LDtk project set up like kmtemplate.ldtk, as described above. The script writes the .clr from baked tiles layers and goes from bottom up as they are listed in LDtk; so any tiles layers at the top will overwrite layers below them if there is overlap. 

Just right click in the main KMtemplate folder and select Open in Terminal, then run 

python .\ldtk_to_clr_v2.py .\kmtemplate.ldtk .\kmtempla.clr

to generate kmtempla.clr from kmtemplate.ldtk. Replace the example filenames with your own. 

NB. MTM2 requires 8 character max file names, hence the truncation in kmtempla.clr. A .png of your textured map will also appear in the same directory as your script showing a color coded version of your painted map for a quick sanity check. 

Example: Loading up your track in Traxx:

Copy the newly generated .clr file over the one in the data/ directory. Copy the folders art/ data/ levels/ models/ and world/ into your Traxx folder. Open Traxx and select clone MTM2 track from the File menu, then select your .sit file (kmtempla.sit in the included example). See your textures painted with LDtk in the Traxx editor, and go from there!

