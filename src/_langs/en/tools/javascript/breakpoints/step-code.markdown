---
rss: false
layout: tools-article
title: "How to Step Through the Code"
seotitle: "How to Step Through the Code Using Chrome DevTools Breakpoints"
description: "By executing code one line or one function at a time, you can observe changes in the data and in the page to understand exactly what is happening."
introduction: "By executing code one line or one function at a time, you can observe changes in the data and in the page to understand exactly what is happening. You can also modify data values used by the script, and you can even modify the script itself."
article:
  written_on: 2015-04-14
  updated_on: 2015-05-18
  order: 3
authors:
  - dgash
  - pbakaus
priority: 0
collection: breakpoints
key-takeaways:
  tldr:
    - Stepping through code allows you to observe issues before or while they happen.
    - Stepping is superior to console logging, as the data is already stale the moment it arrives in the console.
    - Stepping allows you to trial changes through live editing during a pause.
remember:
  note-tbd:
    - TBD note.
---
{% wrap content %}

*Why is this variable value 20 instead of 30? Why doesn't that line of code seem to have any effect? Why is this flag true when it should be false?* Every developer faces these questions, and steps through code to find out.

After [setting breakpoints](/web/tools/javascript/breakpoints/add-breakpoints), return to the page and use it normally until a breakpoint is reached. This pauses all JavaScript on the page, focus shifts to the DevTools Sources panel, and the breakpoint is highlighted. You can now selectively execute code and examine its data, step by step.

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.tldr %}

## Stepping in action

All step options are represented through clickable icons ![Breakpoints button bar](imgs/image_7.png){:.inline} in the sidebar, but can also be triggered via shortcut. Here's the rundown:

<table class="table-1">
  <thead>
    <tr>
      <th data-th="Icon/Button">Icon/Button</th>
      <th data-th="Action">Action</th>
      <th data-th="Description">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_8.png" alt="Resume" class="inline"></td>
      <td data-th="Action">Resume</td>
      <td data-th="Description">Resumes execution up to the next breakpoint. If no breakpoint is encountered, normal execution is resumed.</td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_9.png" alt="Long Resume" class="inline"></td>
      <td data-th="Action">Long Resume</td>
      <td data-th="Description">Resumes execution with breakpoints disabled for 500ms. Convenient for momentarily skipping breakpoints that would otherwise continually pause the code, e.g., a breakpoint inside a loop. <p><b>Click and hold <i>Resume</i> until expands to show the action.</b></p></td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_10.png" alt="Step Over" class="inline"></td>
      <td data-th="Action">Step Over</td>
      <td data-th="Description">Executes whatever happens on the next line and jumps to the next line.</td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_11.png" alt="Step Into" class="inline"></td>
      <td data-th="Action">Step Into</td>
      <td data-th="Description">If the next line contains a function call, <i>Step Into</i> will jump to and pause that function at its first line.</td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_12.png" alt="Step Out" class="inline"></td>
      <td data-th="Action">Step Out</td>
      <td data-th="Description">Executes the remainder of the current function and then pauses at the next statement after the function call.</td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_13.png" alt="Deactivate breakpoints" class="inline"></td>
      <td data-th="Action">Deactivate breakpoints</td>
      <td data-th="Description">Temporarily disables all breakpoints. Use to resume full execution without actually removing your breakpoints. Click it again to reactivate the breakpoints.</td>
    </tr>
    <tr>
      <td data-th="Icon/Button"><img src="imgs/image_14.png" alt="Pause on exceptions" class="inline"></td>
      <td data-th="Action">Pause on exceptions</td>
      <td data-th="Description">Automatically pauses the code when an exception occurs.</td>
    </tr>
  </tbody>
</table>

Use **step into** as your typical "one line at a time" action, as it ensures that only one statement gets executed, no matter what functions you step in and out of.

**Pause on exceptions** is useful when you suspect a non-fatal exception is causing a problem, but you don't know where it is. When this option is enabled, you can refine it by clicking the **Pause On Caught Exceptions** checkbox; in this case, execution is paused only when a specifically-handled exception occurs. 

## The call stack

Near the top of the sidebar is the **Call Stack** section. When the code is paused at a breakpoint, the call stack shows the execution path, in reverse chronological order, that brought the code to that breakpoint. This is helpful in understanding not just where the execution is *now*, but how it got there, an important factor in debugging.

#### Example

<p><img src="imgs/image_15.png" alt="Call stack" style="float: left;margin-right: 1em;margin-bottom: 1em;">An initial onclick event at line 50 in the <strong>index.html</strong> file called the <code>setone()</code> function at line 18 in the <strong>dgjs.js</strong> JavaScript file, which then called the <code>setall()</code> function at line 4 in the same file, where execution is paused at the current breakpoint.</p>

## Data manipulation

When code execution is paused, you can observe and modify the data it is processing. This is crucial when trying to track down a variable that seems to have the wrong value or a passed parameter that isn't received as expected.

Show the Console drawer by clicking **Show/Hide drawer** ![Show/Hide drawer](imgs/image_16.png){: .inline} or press <kbd class="kbd">ESC</kbd>. With the console open while stepping, you can now:

* Type the name of a variable to see its current value in the scope of the current function
* Type a JavaScript assignment statement to change the value

Try modifying values, then continue execution to see how it changes the outcome of your code and whether it behaves as you expect.

#### Example

<p class="clear"><img src="imgs/image_17.png" alt="Console Drawer" style="float: left;margin-right: 1em;margin-bottom: 1em;">We reveal that the value of the parameter `dow` is currently 2, but manually change it to 3 before resuming execution.</p>

## Live editing

Observing and pausing the executing code helps you locate errors, and live editing allows you to quickly preview changes without the need for reloading.

To live edit a script, simply click into the editor part of the Sources panel while stepping. Make your changes as you would do in your editor, then resume execution and interact with the page as usual; your modified script will execute in place of the original, and you can observe the effects of your changes.

#### Example

<p class="clear"><img src="imgs/image_18.png" alt="Live Editing" style="max-width:300px;float: left;margin-right: 1em;margin-bottom: 1em;">We suspect that the parameter <code>dow</code> is, in every case, off by +1 when it is passed to the function <code>setone()</code> – that is, the value of <code>dow</code>, as received, is 1 when it should be 0, 2 when it should be 1, etc. To quickly test whether decrementing the passed value confirms that this is the problem, we add line 17 at the beginning of the function and resume.</p>

{% include modules/nextarticle.liquid %}

{% endwrap %}
