---
layout: post
title:  "Improving Putty settings on Windows."
date:   2017-05-21 16:00:00 -0200
categories: software development putty
---

*Author: [Dag Wieers](https://twitter.com/dagwieers). Original article from  [Field Commander Wieers](http://dag.wiee.rs/blog/content/improving-putty-settings-on-windows)*

Since I started contract work for a new customer and have been offered a Windows Thinkpad to connect to the internal network, I have been looking at ways to make my life more comfortable. Putty is now my window to ~~the world~~ work so let's look at how I can make Putty nicer to work with by tweaking its configuration.

_PS: Some of these options work equally well for Putty on Linux, put there is little use for that combination._

* [Skip directly to Putty settings summary.](#settings-summary)

### Configure your Putty first, then make entries.
This is important advice. First configure your environment before you start using it. This is especially true for Putty, since you always start off from the default, it is important to configure the default entry before you create entries from these defaults. It will save you a lot of time afterwards to get things straight.

So before you make any changes, open the default template in **Category: Session** by selecting **Default Settings** and pressing the **Load** button.

### Make SSH the default.
If you have an older version of Putty, chances are that you have Telnet as the default protocol. Changing it to SSH will probably save you some time when you start Putty out-of-the-blue. For this go to **Category: Session** and select **SSH**.

### Keep windows around.
Putty cleverly exits when you leave a session, but I don't like that. I like to be able to still copy&paste from console even when one of my sessions times out or I closed one bash/session too many. Since I consider terminal output as possible interesting information I don't want to loose that by mistake (or inconsiderate intent). So you'd want to set in **Category: Session** the option **Close window on exit** to **Never**.

### Annoying PC bell.
Some systems have quite annoying (and loud) PC speaker bell sounds and since I am not fond of audible notifications (and I can imagine my colleagues even less when I frantically expand stuff in bash) I always enable visual bell in **Category: Terminal > Bell** and select **Visual bell**.

I also like to have taskbar notifications (when eg. putty is minimized or in the background) so I set **Taskbar/caption indication on bell** to **Flashing**.

### Increase scrollback buffer.
By default Putty buffers 200 lines of output, which is too little in lots of circumstances. And the moment you actually need this number increased, chances are you already lost some information you wanted. So it is wise to increase this number. What I do is go to **Category: Window** and increase **Lines of scrollback** to **20000**.

### Scrollback behavior
One thing I hate about terminal consoles is that if you are scrolling back output while the system is still producing output, the terminal jumps back to the bottom. I can see why this is the default, people might be confused if they are not aware that they are looking at the terminal buffer.

So in **Category: Window** I disable the **Reset scrollback on display activity** but I do enable **Reset scrollback on keypress**.

### Choose a good font.
The newer Putty binaries are able to make use of ClearType which drastically improves the font quality compared to Antialiased. Go to **Category: Window > Appearance**, choose **ClearType** and a nice font. I prefer **Lucida Console, 9-point**.

When you are there, you might want to change the **Gap between text and window edge** to **3** pixels.

### Use proper character encoding.
Nowadays all Linux systems are able to use Unicode (UTF-8) so to make sure that the output in Putty (especially everything non-ascii) looks fine, go to **Category: Window > Translation** and change the **character set** to **UTF-8**, make sure that also the line drawing characters use Unicode as well.

### Linux copy-and-pasting.
I prefer to do an implicit copy when selecting and using the middle mouse button for pasting. So I go to **Category: Window > Selection** and set the **Action of mouse buttons** to **xterm (Right extends, Middle pastes)**

When you are there, also enable the option **Paste to clipboard in RTF as well as plain text**, which is nice when you are copy-and-pasting to emails or text documents that allow fonts and colours. Your console output will look much the same as it does on your screen!

### Change dark colours on a black background.
One of the more annoying things with terminal applications (xterm has the same issue) is that by default dark-blue is too dark to be visible on a black background. Not only is this frustrating, it makes the experience for new users so bad that they prefer to disable colours (or hate the ls colour output or syntax highlighting in vim).

So if you are like me, go to **Category: Window > Colours** and select **ANSI Blue** in the **Select a colour to adjust** to **Red:74 Green:74 Blue:255**. I do the same for **ANSI Blue Bold** to **Red:140 Green:140 Blue:255**.

### Keeping idle sessions active.
Another frustrating problem is induced by the time-to-live of inactive or idle TCP sessions on firewall or switch configurations. At some companies this is put aggressively low so that TCP sessions that have no activity for 1 minute or even 30 seconds are being dropped. If you are using an SSH connection over such a network device, you have to take care to send keep-alive packets over your idle session. To do this go to **Category: Connection** and set **Seconds between keepalives (0 to turn off)** to **25**.

### Enable X11 forwarding.
Together with [Xming](http://www.straightrunning.com/XmingNotes/ "Xming X Server for Windows"), Putty allows you to run graphical Linux applications on your Windows system, so enabling X11 forwarding by default can be useful. To enable this, got to: **Connection > SSH > X11** and enable **Enable X11 forwarding**.

Also dynamic forwarding is very useful to connect to systems on a remote network, even when you do not know in advance having it enabled can be useful. This option however reserves a local port on the system so enabling it by default is not really practical. However you can still enable it from a running Putty by selecting **Change settings**.

### Finally, saving the default.
Now, don't forget to save the changes you just made to the default template. If you loaded the Default Settings at the start, return back to **Category: Session** and press the **Save** button. Now you are done !

## Putty settings summary. <a id="settings-summary"></a>

*Category:* Session
*Connection type:* SSH
*Close window on exit:* Never

*Category:* Terminal > Bell
*Action to happen when a bell occurs:* Visual bell (flash window)
*Taskbar/caption indication:* Flashing

*Category:* Window
*Lines of scrollback:* 20000
*Reset scrollback on keypress:* Checked
*Reset scrollback on display activity:* Unchecked

*Category:* Window > Appearance
*Font:* Lucida Console, 9-point
*Font quality:* ClearType
*Gap between text and window edge:* 3

*Category:* Window > Translation
*Character set:* UTF-8
*Handling of line drawing characters:* Unicode

*Category:* Window > Selection
*Action of mouse buttons:* xterm (Right extends, Middle pastes)
*Paste to clipboard in RTF as well as plain text:* enabled

*Category:* Window > Colours
*ANSI Blue:* Red:74 Green:74 Blue:255
*ANSI Blue Bold:* Red:140: Green:140 Blue:255

*Category:* Connection
*Seconds between keepalives (0 to turn off):* 25

*Category:* Connection > SSH > X11
*Enable X11 forwarding:* enabled