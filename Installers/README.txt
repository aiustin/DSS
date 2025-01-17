﻿Welcome to DeepSkyStacker 5.1.1 Beta 1
======================================

Only 64 bit versions of Windows 10 and later are supported in this release.

Changes since 5.1.0

1. Possible bug fix - DeepSkyStacker terminated at startup when running on ARM version of Windows 11 in x64 emulation mode.  Unable to test.

2. Bug fix - A corrupt info.txt file caused an infinite loop.

3. Diagnostic added - Report processor architecture and processor type in trace file and to stderr at startup.

4. Bug fix - Stacked FITS images in SuperPixel mode were displayed only in the top left corner.

5. Bug fix - Resolve occasional odd problems when using edit stars mode.

6. Bug fix - DeepSkyStackerCL was only displaying the help text regardless of command line input.

7. Enhancement - Reinstate Image Properties as a Qt based dialogue to allow changing e.g. exposure for multiple images at once

8. Bug fix - Fields in the image list and the group tabs were not updated when switching to another language.

Welcome to DeepSkyStacker 5.1.0
===============================

This release is the start of the process of converting the code to Qt so that it can be ported to platforms other than Windows.

Here are the main changes that were made for DeepSkyStacker 5.1.0:

1. The bulk of the code for the "Stacking" panel has been converted to Qt.  This includes a completely reworked image display.

2. The image list can now be undocked from the bottom of the Stacking panel so that it operates as a separate window.  The "Explorer" bar (left panel) can also be undocked.

3. It is now possible to rename all groups with the exception of the initial group (Main Group).

4. Some fields in the image list (Type, ISO/Gain, and Exposure) can be double-clicked to change the values.

5. A large number of internal changes have been made with the intent of facilitating future enhancements and/or to improve processing.

6. SIMD (Single Instruction Multiple Data - also known as Advanced Vector Extensions or AVX) support for decoding raw images and for registration and stacking of RGGB images.  It *can* deliver dramatic reductions in processing times, but it depends on your processor and clock speed, so don't assume it will be faster.   As an example, Martin Toeltsch (who wrote the code) reports times to process 10 Nikon NEF files (on his computer):

	Without SIMD  52s
	Using SIMD    8s
	
   This also works for GBRG images so Canon CR2 files will benefit from this work as well.   
	
7. Some further tuning of the OpenMP (multi-processor support) has been done.

8. The "Stacking" panel image display now caches the last twenty images displayed, so you can use it as a "blink comparator"

9. The configured settings that are stored in the Windows registry are not compatible with earlier releases which stored them in the registry hive:

   HKCU\Software\DeepSkyStacker\DeepSkyStacker

   so now the settings are held in a separate registry hive:

   HKCU\Software\DeepSkyStacker\DeepSkyStacker5

10. The "Processing" panel is still running MFC code but has minor changes to allow it to work as a child of a Qt window.

11. The location for storing DeepSkyStacker settings files has changed from %ProgramData%\DeepSkyStacker (typically C:\ProgramData\DeepSkyStacker) to %AppData%\DeepSkyStacker\DeepSkyStacker5 (typically C:\Users\<username>\AppData\Roaming\DeepSkyStacker\DeepSkyStacker5).  You may wish to copy any old settings files to the new location.

12. A file association is now created during installation so that .dssfilelist files will be opened by DeepSkyStacker.

13. Add code to capture non C++ exceptions (e.g. SIGINT, SIGILL, SIGFPE, SIGSEGV, and SIGTERM) and write a debugging backtrace to stderr and to the trace file if active.

14. Change message for incompatible images to report the reason.

24. Registering and stacking now overlap processing with reading the images.   For n images where time to load each image is L and time to process each image is P, the total time will now typically be n*L + P (when L > P) or L + n*P.   Typically, the time to load the images will predominate on faster systems or those that use real disk drives.

15. Remove manual setting of "Set Black Point to Zero", this is now determined automatically.

16. Enable the Comet tab in Stacking Settings when it is invoked from Register Settings and Comet data is available.

17. Change LibRaw supported camera list so that "Olympus OM-1" is recognised as well as "OM Digital Solutions OM-1"

18. Update Libraw to 0.21.1

19. Bug fix - active tab jumped back to Main Group after drop of files when another group was active.
