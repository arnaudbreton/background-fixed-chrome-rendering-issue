Chrome background-attachment:fixed rendering issue on high density display
=========

Chrome has rendering performance issues on Retina display when displaying a background fixed in a DIV (not a fixed block), making the overall scroll very laggy.

The issue is due to Chrome always re-painting the fixed background even when not displayed. You can see the issue by enabling the "Show paint rectangles" mode in the Dev tools (open them, press escape, go to rendering tab).

The issue can be solved by attaching the background in a positioned fixed DIV, hiding it on all the blocks with a background color (white in the example), except on one block (transparent background).
Displaying the background this way does not cause the paint waterfall of the 1st example. Attaching the background to a fixed DIV, with the `-webkit-transform: translateZ(0)` hack (see http://stackoverflow.com/questions/10814178/css-performance-relative-to-translatez0) let Chrome put it to it’s own composited layer.

This issue is not only visible on high pixel density display (like Apple Retina).

This solution is based on this blogpost (http://remysharp.com/2013/06/07/insights-into-rendering-performance/) by Remy Sharp (https://github.com/remy).

This issue is not present on Firefox.