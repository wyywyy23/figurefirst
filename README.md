# FigureFirst
FigureFirst is a python 3.5+ library to decorate and parse SVG files so they can serve as layout documents for matplotlib figures. In principle FigureFirst works on python 2.7, but it is not officially supported. 
* See our github page for readme and examples: http://flyranch.github.io/figurefirst/
* Read the docs: https://figurefirst.readthedocs.io/en/latest/index.html
* Read our Scipy 2017 proceedings: http://conference.scipy.org/proceedings/scipy2017/lindsay.html

If you use FigureFirst, please cite the above paper to help others find FigureFirst.

## Installation

```bash
pip install figurefirst
```

## Quickstart
*See http://flyranch.github.io/figurefirst/ for more detail*
1. Create your figure template in Inkscape. 
    a. Make a rectangle for each panel, tag the panel using `extensions > figurefirst > tagaxis`, e.g. `A` or `B`
    b. Group the rectangles (select all, `ctrl-g`), tag the group using `extensions > figurefirst > tagfigure`, e.g. `fig1`
    c. Save your template, e.g. `fifi_template.svg`
2. In Python use the following commands to load, plot, and save:
    a. `import figurefirst as fifi`
    b. `layout = figurefirst.svg_to_axes.FigureLayout('fifi_template.svg', autogenlayers=True, make_mplfigures=True, hide_layers=[])`
    c. For each axis, grab the axis handle using: `ax = layout.axes[('fig1', 'B')]`
    d. Plot on that axis using matplotlib as usual
    e. After you have plotted all panels, optionally update the aesthetics:
        * figurefirst.mpl_functions.adjust_spines(ax, ['left', 'bottom'])
        * figurefirst.mpl_functions.set_fontsize(ax, 6)
    f. Add your figure to the layout using `layout.append_figure_to_layer(layout.figures['fig1'], 'fig1', cleartarget=True)`
    g. Save your figure to the svg using `layout.write_svg('fifi_template.svg')`. Use a new name if you wish not to overwrite the template. 
3. Note that you can have multiple figurefirst "figures" in a single svg file. Each figure will appear as a new layer.  


## Use with Inkscape
FigureFirst is developed and tested with Inkscape. Some versions and settings of Inkscape are very slow. Try Inkscape 0.92: https://inkscape.org/en/release/0.92.3/

### Installing Inkscape 0.92 on Ubuntu
You can install Inkscape 0.92 using ppa:
* `sudo add-apt-repository ppa:inkscape.dev/stable`
* `sudo apt update`
* `sudo apt install inkscape`

### Optimizing Inkscape settings
Try increasing the Rendering Tile Multiplier:
* `Edit > Preference > Rending`
* `Rendering Tile Multiplier = 50`
Restart Inkscape

### Installing `figurefirst` extensions

This package includes a console script, `figurefirst_ext` to install inkscape extensions.
It tries to infer the default installation path for your OS (do `figurefirst_ext --help` to see what they are),
or you can pass a path in manually, e.g..

```bash
figurefirst_ext ~/.config/inkscape/extensions
```


## Development

- Clone this repo
- Test locally by running `pytest`
  - To keep the test output files for inspection, add the `--keep_files` option
  - To test against all supported python versions, run `tox`
- Enable your github account with travis for continuous integration
- Raise a pull request
