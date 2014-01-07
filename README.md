Cobalt Fusion presents:

DebugView++
----------

DebugView++ is a viewer for Win32 OutputDebugString based logging in the style of
Sysinternals DebugView. DebugView++ features:

- single selfcontaining executable, setup is provided but not required
- runs without prerequisites on WinXPSP3, Vista and 7/8.x
- capture both Win32 and Global Win32 messages
- tabbed views
- resolve PID to process name
- filter by process or message
- advanced filtering, exclude, track, stop (ability to use regular expressions) 
- line and token highlighting (create your own syntax highlighting)
- minimal delay of the traced application, compared to debugview a factor of 10 better.
- fast and responsive user-interface, even with +50.000 incoming lines per second
- SAIT (search-as-I-type) token highlighting
- bookmarks
- statusbar shows detailed log/view/selection information
- open saved logs for post-mortum analysis
- memory compressed logbuffer using google snappy (-50% RAM consumed)


Download
--------
at http://debugviewpp.wordpress.com/

Screenshot
----------
![DebugView++ Screenshot](/art/syntax_high.png "DebugView++ Screenshot")

The screenshot demonstrates bookmarks and highlighting features:

Highlighted:
------------
- regex (token filter):     ``[^\s]*\\[\\\w+\.\s]+``    filenames in blue
- regex (token filter):     ``0x\w+``                   hexadecimal numbers in red
- regex (highlight filter): ``Unittest``                lines with the word 'Unittest' have a lightgreen background
- a doubleclick on 'bytes' causes all instances of 'bytes' to highlight in yellow

See http://www.cplusplus.com/reference/regex/ECMAScript/ for all options for supported regular expressions

![FilterDialog Screenshot](/art/filterdialog.png "FilterDialog Screenshot")

Filters:
--------

Filters can be defined per view, for example choose File -> New View, and the filter dialog will popup.
Pressing OK will open a new view without any filters. 

Different types of filters:

All filters support regular expressions, if you are not familliar with regular expressions you can
just type any word or part of a word to match.

- exclude: lines containing a matching expression will be excluded from the view
- highlight: lines containing a matching expression will be highlighted using the specified foreground and background colors
- token: only the matching expression will be highlighted using the specified foreground and background colors
- track: lines containing a matching expression will be focused and centered if possible. Note: auto scroll turns off if a track filter is matched 
- stop: if a matching expression is found autoscroll is turned off, all track filters will be disabled and the line is focused. Note: stop filters work only of autoscroll is on, think of a stop-filter as a one-shot track filter
- ignore: lines containing a matching expression will be ignored by the auto scroll feature. 

*Practical uses*:

Exclude and highlight filters are the most intuitive filters to use. Track, stop and ignore can be a little confusing, let me try to give examples of each filter.

**track**; use this filter to focus interesting lines that do not occur very often, but at a regular interval, for example, so you are monitoring a process that logs output every 30 seconds and you need to check the result. 

**stop**; this filter is good when some special event occurs (an exception?) and you want to inspect the context of the event in the log before continuing. A press of the 'end' button will resume auto scrolling.

**ignore**; this filter is usefull if you want to have auto scoll on, but some high frequeny messages are annoying you, but you cannot exclude them because they help you diagnose your problem when it occurs.

In this last case you can consider a different approach:

Use two views, one where the diagnostic messages are filtered and autoscroll is on, and one where the messages are included (and maybe highlighted), next turn on the 'link views' feature.



Other documentation:
--------------------

**Auto scroll**: scrolls down to new incoming lines automatically; autoscroll is turned on automatically when the last line in the view is selected.

**Bookmarks**: bookmarks are view specific and can be placed on a line by clicking left of the line number or Ctrl+F2, press F2 to move to the next bookmark. Bookmarks are temporary, so cannot be saved.

**ClockTime**: when enabled the time is displayed as provided by the system's real-time clock (RTC). Such a timestamp has a 16ms resolution. When disabled the time displayed as a relative time to the first message, however this timpstamp is obtained from the High-Performance Counter (HPC) which typically has a sub-microsecond resolution.

The resolution should not be confused with accuracy here, the recorded timestamp is not the actual time the message occured, it is the time the message was received by DebugView++. Also there is no quarantee that the time between occurance and reception of messages is constant, *however* in practive this is **pretty** constant :)


How to build
------------

This is a Visual Studio 2010 project with the following dependencies (download and install separately)
- boost 1.43 or later, tested with: http://sourceforge.net/projects/boost/files/boost/1.55.0/, choose boost_1_55_0.zip
- WTL 8.0 or later, tested with: http://sourceforge.net/projects/wtl/, choose WTL80_sf.exe
- zip.exe, http://gnuwin32.sourceforge.net/packages/zip.htm, choose [zip-3.0-setup.exe]

The libraries must be installed in /Libraries and zip.exe installed, add the binary directory to your path.

[zip-3.0-setup.exe]: http://downloads.sourceforge.net/gnuwin32/zip-3.0-setup.exe

-= Cobalt Fusion =-

Gert-Jan de Vos
mailto:boosttestui@on.nl

Jan Wilmans
mailto:janwilmans _at_ gmail.com
