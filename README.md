### Introduction
Trying to illustrate how to implement a design to a mobile developer can be quite a challenge if you aren’t well-versed in programming for iOS or Android. Likewise, it’s challenging for a developer to adequately implement a design if he or she isn’t equally experienced with photoshop (or your design tool of choice). 

To bridge this gap at Two Toasters, designers are tasked with building out design specifications which detail the various colors, fonts, and assets throughout the app. Furthermore, to guarantee that our designs are translated perfectly, we’ve adopted a process of red-lining our mockups that details information about layout and styling. The guide that follows describes the intricacies of how to relay some of this information and creating a complete design spec as detailed below.
The Project
For the purposes of this guide, I’ve designed two screens for a fake Twitter iOS app called hootie.
Sidebar: http://invis.io/HKEL55BS
Tweet Feed: http://invis.io/AREL58WZ
Assets + Design Spec delivered to dev:

Resources Used
PSD: https://www.dropbox.com/s/6ys3lonkp1b7r9c/redline.psd
I’ve found it much easier to design all screens in a single PSD with a combinaton of smart objects and layer comps.
Photoshop Scripts
Measure and fill the dimensions from a marquee: https://gist.github.com/yorb/5112285
Measure the widest dimension and make a ruler from a marquee: https://gist.github.com/yorb/5042960
Github App
http://mac.github.com/

Fonts & Colors
Colors
It’s prudent to define variables for the colors that’ll be used throughout the application (these can translate directly with the color palette you use within the application). This allows you to easily tweak the colors throughout the application so that you maintain a consistent design language.

Fonts
Like colors, 
Slicing Assets
Simply put, assets are the images needed to programmatically build out a design. Typically, this includes things that can’t be easily drawn programmatically such as background textures, icons, and complicated visual elements such as tool tip overlays. Image assets can also be used in lieu of drawable UI elements, such as shadows to get a pixel-perfect implementation of a design.

When should you not slice an asset?
If you are not implementing a design through code yourself, answering this question will probably require communication with a developer. However, as a starting point, you can safely rely on the fact that if any part of your design just uses a solid color, it’s not necessary to slice it out. Moreover, if you’re using an icon font in your design (with no complex styling around them such as clipped gradients and inner shadows), its preferable to provide the font file to the developer in lieu of slicing out assets so they can be sharply rendered within the application.

How should I slice for different resolutions?

What file format should I save them in?
You should provide most of your assets as PNGs as it is a lossless format. This ensures that the visual quality of the asset is not tampered with through compression. That being said, I suggest you run your PNGs–especially the ones that have a large file size–through tinypng to really optimize them.

For larger assets–those that are dimensionally larger–such as backgrounds or screenshots that may not require transparency, it can be beneficial to save them as JPEGs instead. Much of the storage footprint of an application can be taken up by these larger images and the asset size can be easily compressed down by saving it them as JPEGs. When saving as a JPEG, it’s best to use your own judgement as to what quality level you should adjust to in order to get the best ratio of image size to quality. However, as a general rule of thumb, saving your asset as a JPEG at 70-80% quality will result in adequate savings with the size and not reduce the visual quality too much.

Stretching Assets
If your design elements have any part of them that can fluidly expand . Usually, you should employ stretchable assets for elements such as buttons, table cells, badges, and pop-over/tooltip backgrounds. For iOS, to communicate how an asset should stretch, you must define insets for the part of the element that should not be stretched programmatically. These insets should be provided in points and detailed as ([Top], [Left], [Bottom], [Right]). This works well with UI elements that only have portions that don’t need to be stretched on the edge, but for tooltips and popovers that have . For Android, google provides a detailed tutorial on how to use 9patching to create stretchable assets here.

Example: 
Badge background asset that can be stretched:
sidebar_badge.png
Stretch Insets: (3pt, 2pt, 5pt, 2pt)

Notice how the middle portion of this asset has a lot of visual information that repeats. As a result, the asset can be reduced in width so that we have a 1 point (2px) slice of the asset that we will stretch when the asset expands.

Tiling Assets
In the pursuit of further reducing the space your app takes, you should use a tileable asset where possible. If your background texture for the app

Example
sidebar_bg.png

The texture I used for the sidebar background tiles every 128 pixels. As a result, I was able to cut out just a 64x64pt slice of the background asset that I can instruct the developer to tile in that view.
Naming Assets
For iOS and Android projects, all assets go into a single folder. This can make navigating through the files to find any single asset a significant–yet avoidable–time sink. As a result, it’s advantageous to follow a consistent naming convention for assets that you share with developers to avoid any unnecessary overhead during development as well as when they need to be updated. 

Example Scheme
In our development process, I’ve found it helpful to follow the subsequent pattern:
[app name or UI element/feature]_[type of asset]_[specific identifier (optional)]_[state (optional)].png

Example:
For assets that can be used throughout the application, such as the app background, it should be named as:
hootie_bg.png

Example:
For assets specific to a screen, such as the normal and pressed states for the icons in the sidebar, they should be named as:
sidebar_ic_tweets_normal.png
sidebar_ic_tweets_pressed.png

Some helpful shorthands:
Icon: ic
Button: btn
Background: bg
Navigation Bar (iOS): navbar
Action Bar (Android): ab
Table: tbl
Divider: div
State Suffixes
If you are slicing buttons, cell backgrounds, or any other UI elements with different state its essential to also add a consistent for the suffix on the asset name:

When the user has not tapped something (element is static): normal
When a user taps down the element: pressed
(Optional) After a user taps on an element and it becomes active: active 
(Android) When a user uses a scroll wheel to focuse on an element: focused

Redlining

