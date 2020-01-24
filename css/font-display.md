## Font-display
Let's talk about the lifetime of a web font:

<img src="../assets/font-display-1.png" width="400" >

From the image you can see there are 3 periods with 3 different behaviours: 
- `block period`, the browser renders your text in an invisible font. This is why on a lot of webfont-heavy websites, during the first load of the page you will see no text or worse, phantom underlines.
- `swap period`, the browser renders your text in the fallback font (in the example in the diagram, that would be the default `serif` font.
- `failure period` means no font has been found, in which case the browser renders your text in the fallback font, as above.

With the font-display attribute, you can control the length of each of these periods, and what happens when one of them fails. There are 4 different values: `block`, `swap`, `fallback` and `optional`. There's also auto, which usually ends up being the same as block.


#### Sample
The font display is controlled per font-face:

```css
@font-face {
    font-family: 'my-font';
    font-display: optional;
    src: url(my-font.woff2) format('woff2');
}
```


#### Possible values and behaviours

##### font-display: block
The text blocks (is invisible) for a short period*. Then, if the custom font hasn't been downloaded yet, the browser swaps (renders the text in the fallback font), for however long it takes the custom font to be downloaded, and then re-renders the text in the custom font. You get a FOIT (flash of invisible text).

*The length of the block period depends on which browser you're using. Chrome, Firefox and (recently) Safari use 3s. IE uses 0s (effectively having no block period), and older Safari used no timeout, effectively having an inifinite block period.

##### font-display: swap
There is no block period (so no invisible text), and the text is shown immediately in the fallback font until the custom font loads, then it's swapped with the custom font. You get a FOUT (flash of unstyled text).

##### font-display: fallback
This is somewhere in between block and swap. The text is invisible for a short period of time (100ms). Then if the custom font hasn't downloaded, the text is shown in a fallback font (for about 3s), then swapped after the custom font loads.

##### font-display: optional
This behaves just like fallback, only the browser can decide to not use the custom font at all, based on the user's connection speed (if you're on a slow 3G or less, it will take forever to download the custom font and then swapping to it will be too late and extremely annoying)

<img src="../assets/font-display-2.png" width="400" >

    
#### Extra informations
https://font-display.glitch.me/