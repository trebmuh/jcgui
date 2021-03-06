jcgui
=====

A little host for jconvolver

Hello, 

Jc_Gui is a simple Host wrap around jconv/jconvolver


======================= Building Jc_Gui from source code

---- Build environment

Jc_Gui uses 'waf' for the build environment.
The simplest and fastest way to build Jc_Gui is given below:

  cd Jc_Gui_source_directory
  ./waf configure
  ./waf build
  sudo ./waf install

By default, this will install Jc_Gui and related files in
the /usr/local filesystem, e.g. /usr/local/bin.

The installation prefix can be provided at configure time, e.g.:

  ./waf configure --prefix=/usr
  ./waf build
  sudo ./waf install

Thus, Jc_Gui will be installed in /usr/bin.

---- Dependencies 

To compile and run properly Jc_Gui needs the following extra
packages (runtime binaries/libraries and development packages):

  GTK+-2.0 >= 2.12.0 
  libsndfile  >= 1.0.17
  JACK (jackd, libjack, and their development packages) >= 0.109.1

By the way, most package managers usually list development packages as 
'packagename-dev', e.g. libsndfile-dev.


==================== Startup options

---- From the command line

Jc_Gui provides a few user options at startup. They can be set in
two ways.  From the command line, Jc_Gui can be invoked with the
usual -h or --help option. The following help message is displayed:

  $ Jc_Gui --help

   Jc_Gui usage
   All parameters are optional. Examples:
          Jc_Gui
          Jc_Gui  -i system:capture_3 -i system:capture_2
          Jc_Gui -c -o system:playback_1 system:playback_2
  
    -h [ --help ]         Print this help
    -v [ --version ]      Print version string and exit
  
   JACK configuration options:
    -i [ --jack-input ] arg     Jc_Gui JACK input
    -o [ --jack-output ] arg    Jc_Gui JACK outputs
 
The options should be self explanatory but for the sake of clarity, a
few extra points are worth mentioning here.

JACK options: 
------------- 

By default, Jc_Gui will not auto-connect to any JACK system ports
unless the latter are explicitly provided from the command line.
If you started Jc_Gui as follows:

$ Jc_Gui

You can connect the Jc_Gui JACK ports to e.g.
system ports from Patchage (drobilla.net/software/patchage/) or the 
QJackCtl (qjackctl.sourceforge.net/) connection window.

In the following example system port names are given:

  $ Jc_Gui -i system:capture_1 -i system:capture_1 -o system:playback_1 system:playback_2

At startup Jc_Gui will autoconnect to these system ports


---- From SHELL variables 

Jc_Gui offers the possibility to make some of these options more
"permanent" thanks to SHELL variables. These variables are:

  Jc_Gui2JACK_INPUTS1
  Jc_Gui2JACK_INPUTS2
  Jc_Gui2JACK_OUTPUTS1
  Jc_Gui2JACK_OUTPUTS2
 

Those can be defined in your $HOME/.bashrc file. Here's a typical setup:

  export Jc_Gui2JACK_INPUTS1=system:capture_1 
  export Jc_Gui2JACK_INPUTS2=system:capture_1 
  export Jc_Gui2JACK_OUTPUTS1=system:playback_1
  export Jc_Gui2JACK_OUTPUTS2=system:playback_2
  

For (t)csh shells, the following can be placed in $HOME/.cshrc

  setenv Jc_Gui2JACK_INPUTS1  system:capture_1  
  setenv Jc_Gui2JACK_INPUTS2  system:capture_1  
  setenv Jc_Gui2JACK_OUTPUTS1  system:playback_1
  setenv Jc_Gui2JACK_OUTPUTS2  system:playback_2
  
You can connect Jc_Gui also over a integratet connection widget. 

==================== Keyboard shortcuts

Jc_Gui benefits from keyboard shortcuts for most of its operations.
At the moment (svn@200), the following keyboard shortcuts are available:

* Engine menu:
--------------
  - Audio engine play	: Space
  - Audio engine stop	: Space
  - Quit Jc_Gui		: Ctrl+Q

* Presets menu :
---------------

When Jc_Gui is launched, it will browse the $HOME/.Jc_Gui/Jc_Guiprerc 
file and store the found presets in its menu. The preset handling is quite
versatile and let you do some useful things:

  - Load a preset         : 1, 2, 3, ... (note (ii))  
  - Save a preset         : Ctrl+1, Ctrl+2, etc (note (ii))
  - Create a new preset   : Ctrl+P (insert a valid name, 
                                    spaces will be replaced by '-')
  - Recall main setting   : S      (see note (iii))
  - Save as main setting	: Ctrl+S (see note (iv))
  
  Submenu "More Preset Action" :
  - Cycle to next preset  : Page Down  (very useful)
  - Cycle to prev preset  : Page Up    (very useful)
  - Save active preset    : Alt+S
  - Rename active preset  : Alt+R
  - Delete active preset  : Delete
  - Delete ALL presets    : Ctrl+Shift+D (gives a warning)

Notes:

(ii)  If you have more than 9 presets, shortcuts will be disabled


* About menu:
-------------

  - About display		: Ctrl+A


==================== JACK startup when JACK isn't running

Jc_Gui will pop up a JACK start dialog window if it finds that jackd
is not running.

You can choose to activate JACK or exit Jc_Gui.  Note that the
supported methods for starting JACK are (by preference order):

1- QJackCtl --start
2- Use of $HOME/.jackdrc

Jc_Gui does not support jackdbus or any JACK start method other than
the two listed above.


=========== Extra information


=> jconv

Jc_Gui use the excellent jconv convolution engine developed by 
Fons Adriaensen, available here: 

	http://www.kokkinizita.net/linuxaudio/index.html 

Jconv can be configured from Jc_Gui. However, due to design
restrictions jconv can only be configured when not running. Despite
this restriction, it is possible to save particular jconv settings. 
The user can recall these presets from the
main Load Preset menu item.

Note: When trying to load an impulse response WAV file (aka an IR file), 
Jc_Gui will check for spaces in the filename and remove them if present.
You can also resample the file to the sample rate used by JACK. 


===========================================

THANKS:



Enjoy! :)

If you encounter problems building or running Jc_Gui, please inform us.

	 mason.green@gmail.com
     brummer-@web.de
