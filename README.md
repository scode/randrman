# randrman

Tiny tool for automating xrandr invocations when monitors are
connected/disconnected. Given a list of displays in their preferred
order at the command line, it continuosly monitors, by polling xrandr,
for changes in the set of available displays and switches to the most
preferred display available (turning off all other displays).

For example, on my laptop I prefer a single display at a time, and I
always prefer the external HDMI port when a display is
connected. Hence, I run:

  randrman HDMI1 eDP1

It does exactly this, and nothing else. There is no configuration
file, no dependencies other than a vaguely recent Python and xrandr in
PATH. It's utterly stupid. But it's useful to me and why not share it.

Caveats:

- It simply polls by repeatedly running 'xrandr' with a sleep in between. It
  will thus consume CPU resources even when no display connects/disconnects
  take place.
- It does not understand the concept of "screens", and assumes there
  is just one. If running 'xrandr' on your host lists multiple screens,
  you're out of lock.
- It uses xrandr the tool, which is not meant for non-interactive use
  and it's possible output would change in the future.
- It only ever picks non-interlaced resolutions.
- It assumes the resolutions supported by a display cannot change while connected.
- It assumes xrandr displays the highest resolution available first.
- It assumes the user always wants the highest resolution possible.
