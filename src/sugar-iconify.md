# Sugar Iconify

## Description

Sugar uses entities for its SVG colors in order to match the icon
colors to the user colors.

The sugariconify.py script is used to convert SVGs into the format
required for Sugar icons, adding the necessary stroke and fill
entities. This is a Python script, and as such requires Python to run.
It creates Sugar-compatible SVG icons from an ```input.svg``` by
adding the appropriate stroke and fill entities. It can be used to
convert a single icon or run over a batch of icons at one time.

You can find the script in the [sugariconify repository](https://github.com/sugarlabs/sugariconify/blob/master/sugariconify.py).  You can find a web version at https://github.com/sugarlabs/iconify-web

For creating an SVG suitable for Sugar,
see the tutorial on [Making Sugar
Icons](http://wiki.sugarlabs.org/go/Development_Team/Almanac/Making_Icons).

In some cases, you may want to update a single icon or a subset of 
icons within a given SVG. To do so, pass a pattern to the
script with -p, and only those icons which match the pattern will be
exported.

### Usage

```
sugariconify.py [-ceghipv] [-s stroke_hex] [-f fill_hex] [-m | -o ] [-d directory] input.svg
```
Example usage: 

```
python sugariconify.py input.svg
```

Options
```
   -c    Apply default color entities (#666666, #FFFFFF) to output 
   -d    [directory] The preferred output directory 
   -e    Do not insert entities for strokes and fills 
   -f    [hex] Hex value to replace with fill entity 
   -g    Automatically accept guesses for stroke and fill entities 
   -h    Display this help message 
   -i    Insert "isolated stroke" entities 
   -m    Multiple export; export top level groups as separate icons 
   -o    Modify input file in place, overwriting it; overridden by -m 
   -p    [pattern] Only export icons whose name contains pattern 
   -s    [hex] Hex value to replace with stroke entity 
   -v    Verbose 
   -x    Create HTML preview files, for icon validation 
```
Note: A common problem encountered when using this script is when the
target SVG has more than two colors.

### Details
 
Below is an example of a simple input SVG:
 
```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:cc="http://creativecommons.org/ns#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   version="1.1"
   viewBox="0 0 55 55"
   height="55mm"
   width="55mm">
  <rect
      y="2.5"
      x="2.5"
      height="50"
      width="50"
      style="fill:#ffff00;fill-opacity:1;stroke:#ff0000;stroke-width:3.5;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
</svg>
```
 
The resulting output would look like this:
 
```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE svg  PUBLIC '-//W3C//DTD SVG 1.1//EN'
          'http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd' [
        <!ENTITY stroke_color "#666666">
        <!ENTITY fill_color "#ffffff">
]>
<svg
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:cc="http://creativecommons.org/ns#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   version="1.1"
   viewBox="0 0 55 55"
   height="55mm"
   width="55mm">
     <rect
  <rect
      y="2.5"
      x="2.5"
      height="50"
      width="50"
      style="fill:&fill_color;;fill-opacity:1;stroke:&stroke_color;;stroke-width:3.5;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1"/>
</svg>
```
## Instantiating SugarIconify

It is also possible to use SugarIconify in your own Python scripts.

``` 
   from sugariconify import SugarIconify
   icon = SugarIconify()
```

## Methods

#### #set_stroke_color():
It is equivalent to ```-s``` on the command line. It can be a hex value
(e.g #FFFF00) or an rgb percent value such as rgb(31%, 28%, 56%).

```
   icon.set_stroke_color('#FFFF00')
   icon.set_stroke_color('rgb(55%, 12%, 55%)')
```
#### #set_fill_color():
It is equivalent to ```-f``` on the command line. It can be a hex value
(e.g #FF0000) or an rgb percent value such as rgb(32%, 33%, 87%).

```
   icon.set_fill_color('#FFFFFF')
   icon.set_fill_color('rgb(55%, 12%, 55%)')
```
#### #set_confirm_guess():
It is equivalent to ```-g``` on the command line; automatically
accepts guesses for stroke and fill entities. It accepts only True or False values.

```
   icon.set_confirm_guess(True)
```
#### #set_use_default_colors():
It is equivalent to ```-c``` on the command line; uses default stroke and
fill entities (#666666, #FFFFFF) for sugar iconify. It accepts only True or False values.

```
   icon.set_use_default_colors(True)
```

#### #set_overwrite_input():
It is equivalent to ```-o``` on the command line; overwrites input file in
place. It accepts only True or False values.

```
   icon.set_overwrite_input(True)
```

#### #set_output_path():
It is equivalent to ```-d``` on the command line; sets the output path for the iconified file. It accepts only string values.

```
   icon.set_output_path('/home/user/Desktop')
```

#### #set_use_entity():
It is equivalent to ```-e``` on the command line; prevents insertion of stroke and fill entities. It accepts only True or False values.

```
   icon.set_use_entity(True)
```

#### #set_verbose():
It is equivalent to ```-v``` on the command line; outputs informational messages
to the console. It accepts only True or False values.

```
   icon.set_verbose(True)
```
#### #set_pattern():
It is equivalent to ```-p``` on the command line; exports only icons whose names
contain a specific pattern. It accepts only string values.

```
   icon.set_pattern('pattern')
```
#### #set_multiple():
It is equivalent to ```-m``` on the command line; exports top-level groups as 
separate icons. It accepts only True or False values.

```
   icon.set_multiple(True)
```
#### #set_output_examples():
It is equivalent to ```-x``` on the command line;
creates HTML preview files for icon validation. It accepts only True or False values.

```
   icon.set_output_examples(True)
```

#### #set_use_iso_strokes():
It is equivalent to ```-i``` on the command line; inserts 'isolated stroke'
entities. It accepts only True or False values.

```
   icon.set_use_iso_strokes(True)
```

## Example

```
   from sugariconify import SugarIconify
   icon = SugarIconify()
   icon.set_use_default_colors(True)
   icon.iconify('/home/user/Desktop/image.svg')
```
