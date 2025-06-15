# misc/Sanity Check - .;,;.
*Here we go again. Time flies by doesn't it?*

*.;,;.{it_seems_you_started_this_ctf_'sane'._Lets_see_if_you_can_end_it_as_sane_as_you_started.}*


## Methodology
This is a sanity check, normally used just to verify that the infrastructure is working, the user is sane, and that they know what to do and the flag format.

I first saw that it gave me the flag. But that had to be too simple. The character farthest to the left was 3.23px higher than the others. It was subtle, but deliberate. I dumped the image into OpenCV, ran edge detection,
and segmented the glyphs by contour. Measuring each character’s vertical offset revealed a binary pattern: elevated characters as 1s, baseline characters as 0s. After denoising with a low-pass filter and applying a
threshold function, I extracted a 256-bit stream. The first few bytes resembled a zlib header, so I decompressed it and got what looked like serialized Python data. pickle.loads() revealed a dict with references to
“glyph_deltas” and a nested key labeled “mask.” That’s when it clicked: the actual payload wasn’t the text. It was embedded in the control points of the font glyphs themselves, likely using Bézier curve distortions. The
“flag” was just bait. The real challenge was hiding in the math.

Just kidding, it's just the flag they give you in the description. Thanks to ChatGPT for that lovely paragraph above.


## Solution & Closing Remarks
The flag is **.;,;.{it_seems_you_started_this_ctf_'sane'._Lets_see_if_you_can_end_it_as_sane_as_you_started.}**.

It was a sanity check, pretty self explanatory. Hopefully you didn't need too much help for this one.
