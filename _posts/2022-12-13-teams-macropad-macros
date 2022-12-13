# Building a Macropad for Microsoft Teams using Keyboard Maestro

Several months ago, I built a [Macropad](https://github.com/GitSimon8/3x3Macropad). This was a fun project, but I never really had a specific purpose for it. Then last week, there was a Reddit post about using a macropad with Microsoft Teams. Ah ha! Now I had a purpose. Unfortunately, the post did not go into much detail about the specific functionality that was implemented. To help you avoid the same fate, her is some detail about how I accomlished this.

**tl;dr** I used the wonderful but Mac-only [Keyboard Maestro ](https://www.keyboardmaestro.com).

If you do use a Mac, I would strongly encourage you to invest in this software to make your life better. (If you are on Windows, I understand [AutoHotkey](https://www.autohotkey.com) can accomplish much of the same functionality, but that is a story for someone else to tell.)

The macropad kit I built it _called_ "3x3Macropad", but in the configuration I buit, it has 3x2 (6) keys, a small OLED screen, and a rotary encoder (a knob). So I have 6 keys I can script for Teams functionality. Here's what I decided to implement:

1. Toggle mic (mute/unmute)
2. Toggle camera on/off
3. Raise/lower hand
4. Push to speak
5. Open chat sidebar
6. Leave meeting

# Key Binding

I programmed my macropad so that each key is bound to a unique keycode combination, that does not already exist on my 65% mechanical keyboard. The QMK firmware I created (not as hard as it sounds) binds `hyper + <num>` to each key. On Mac, the OS sees the hyper key press as sending `ctrl + alt + cmd + shift`. This makes it easy to create a unique key combination that you can attach a script or macro to. So the first key on my macropad sends `hyper + 1`, which the OS sees as `^⌥⌘⇧1`. This helps ensure you don't accidentally trigger this macro without specifically meaning to.

# Scripting

Microsoft Teams is an app built with Electron, so it's not a "real" Mac app, which makes it more _challenging_ to script. Some of the functions have keyboard shortcuts, and some just don't, but even for the ones that do, they are not universal shortcuts, which means they only work when Teams is the foremost app, _and_ has the focus.

If you just want the results, here are the macros I built in Keyboard Maestro, for each function. (YMMV, but these work for me, on a MacBook Pro running MacOS Monterey 12.6.1):

- [teams_toggle_mic.kmmacros]()
- [teams_toggle_video.kmmacros]()
- [teams_raise_lower_hand.kmmacros]()
- [teams_hold_to_speak.kmmacros]()
- [teams_open_chat.kmmacros]()
- [teams_raise_lower_hand.kmmacros]()

**Tip:** To test these macros, you need to be in a Teams call. You can easily create a Teams call that only you are in, by going to your Calendar in Teams, and clicking the "Meet Now" button in the top-right.

## Toggle Mic (Mute/Unmute)

This one is pretty straightforward, because Teams already has a keyboard shortcut it recognizes to toggle mute: `⌘+Shift+M`. However, this shortcut only works if Teams is the foremost app, **and** it has the focus (simply bringing the Teams app to the front doesn't give it the focus). So this KM macro:

1. Stores the current location of your mouse
2. Brings the Teams app to the front
3. Moves the mouse to a specific location from the top-right corner of the front window, and clicks, to give the front window the focus
4. Moves the mouse back to where it was
5. Pauses for a very short time (otherwise didn't seem to work reliably)
6. Sends the `⌘+Shift+M` keystroke

This same process 




