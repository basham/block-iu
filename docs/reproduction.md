# Reproduction

In this exercise, the [official Block IU monogram art](../prior-art/README.md)
is going to be examined for areas of improvement and reproduced in a way that
follows certain [design principles](principles.md) while remaining faithful
to the original art.

## Designed for print

Upon opening [`iu_tab.eps`](../prior-art/iu_tab.eps), it's apparent for two reasons
that this was designed for print, with little consideration of the web medium.
First, the color mode is set as [CMYK](http://en.wikipedia.org/wiki/CMYK_color_model),
not [RGB](http://en.wikipedia.org/wiki/RGB_color_model). Second, the document
unit is set as [points](http://en.wikipedia.org/wiki/Point_(typography)), not
[pixels](http://en.wikipedia.org/wiki/Pixel).

![iu_tab.eps opened in Adobe Illustrator](images/illustrator-cmyk-pt.png)

## Anchor points

Another concern is that the coordinates for all 34 anchor points of the Block IU
contain decimal numbers, rather than whole numbers. Given the hard right or
45-degree angles of the Block IU, there's no reason why the anchor points
shouldn't snap to whole numbers. Since a monitor can't physically render
anything smaller than a pixel, it fakes these sub-pixels by applying a blurring
technique known as
[anti-aliasing](http://en.wikipedia.org/wiki/Spatial_anti-aliasing).

If `iu_tab.eps` is to the be vector source file from which raster files are to
be generated, it will be impossible to generate crisp edges at the current,
a smaller, or larger scale. By not correcting these misplaced anchor points,
the vector art counteracts the bold strength the logo is trying to convey.

In order to best illustrate the severity of these decimal anchor points,
an [SVG version](../prior-art/iu_tab.svg) of the original
[EPS file](../prior-art/iu_tab.eps) was generated.

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<!-- Generator: Adobe Illustrator 16.0.4, SVG Export Plug-In . SVG Version: 6.00 Build 0)  -->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
   width="164.840332px" height="191.9111328px" viewBox="0 0 164.840332 191.9111328"
   style="enable-background:new 0 0 164.840332 191.9111328;" xml:space="preserve">
<rect y="-0.2783203" style="fill:#A41F35;" width="164.1489258" height="191.9111328"/>
<polygon style="fill:#FFFFFF;" points="100.3500977,45.8730469 100.3500977,56.0742188 107.4008789,56.0742188
  107.4008789,112.8710938 92.4799805,112.8710938 92.4799805,38.0664062 100.4086914,38.0664062 100.4086914,27.8686523
  63.1948242,27.8686523 63.1948242,38.0664062 71.1274414,38.0664062 71.1274414,112.8710938 56.0385742,112.8710938
  56.0385742,56.0742188 63.0893555,56.0742188 63.0893555,45.8730469 28.081543,45.8730469 28.081543,56.0742188
  35.9907227,56.0742188 35.9907227,121.8457031 48.8588867,134.9775391 71.1274414,134.9775391 71.1274414,150.1386719
  63.2250977,150.1386719 63.2250977,163.2705078 100.3842773,163.2705078 100.3842773,150.1386719 92.4799805,150.1386719
  92.4799805,134.9775391 114.5805664,134.9775391 127.449707,121.8457031 127.449707,56.0742188 135.3754883,56.0742188
  135.3754883,45.8730469 "/>
</svg>
```

## Analysis

If the coordinates of the anchor points should change, then perhaps it's best to
first examine the dimensions of the monogram. Because the `<polygon/>` SVG tag
doesn't explicitly contain that information, it can be garnered from Illustrator.

![Block IU dimensions in Illustrator](images/illustrator-dimensions.png)

If the dimensions of `107.294pt` wide by `135.402pt` high is tweaked, perhaps
it can be reimagined as a more reasonable aspect ratio. That ratio, combined
with the logo's symmetrical and repetitive geometry will guide most of the
art's reconstruction.

The most stable aspect of the logo is the three vertical stems,
dividing the logo's width into three equal columns. Therefore, if the width of
the art is divisible by three, then there's a higher likelihood of retaining
crisp edges.

![Three columns of the logo](images/guide-02.png)

By examining closer, we can get a better sense for the intended inner dimensions
of the logo. Assuming the width of one edge of the
[serif](http://en.wikipedia.org/wiki/Serif) is one unit wide, then the potential
width of the [vertical bar](http://en.wikipedia.org/wiki/Typeface_anatomy) is
either two or three serif-widths wide. However, if the 45-degree raise of the
`U` is to align properly, then three serif-widths wide is the most reasonable
option.

![Columns either 4 or 5 units wide](images/guide-03.png)

Therefore, if the logo is to have any chance of working along a horizontal
dimension, then the minimal width of the logo must be `15 units`.

```
serif-width = 1 unit
vertical-bar-width = 3 units
stem-width = serif-width + vertical-bar-width + serif-width = 5 units
logo-width = stem-width * 3 = 15 units
```

With a known width of `15 units`, then a possible height can be derived.

```
original-ratio = 107.294 / 135.402
original-ratio = 15 / height
height = 15 / original-ratio = 18.929576677 ~= 19
```

With a height of `19 units` determined, a series of assumptions can guide the
remaining to be discovered.

Assume all four serifs share the same dimension of `5 × 2 units`.

![Serifs](images/guide-04.png)

Assume the lower segment of the `I` connecting to the base of the `U` is the
same `2 unit` height of the serifs.

![I connector](images/guide-05.png)

Assume the height of the `U` horizontal bar is the same as the `3 unit` width
of the two `U` vertical bars.

![U horizontal bar](images/guide-06.png)

Based on the aforementioned assumptions, the remaining heights of the `U`
vertical bar should be `7 units`.

![U vertical bar](images/guide-07.png)

By following these assumptions, the Block IU should be reconstructed in full,
at `15 × 19 units`.

![Reconstructed monogram](images/guide-08.png)
