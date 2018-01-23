# JsonResume

JsonResume creates pretty versions of resume from a single JSON input file. Output formats are specifically customized to modern resume templates. Also, there are a ton of customizations to the templates possible, to make your own version of resume created easily and super quickly.

## Installation

    $ gem install json_resume

## Usage

### Create a sample JSON input file to start

    $ json_resume sample

A [sample](https://github.com/prat0318/json_resume/blob/master/examples/prateek_cv.json) `prateek_cv.json` is generated in the current working directory(cwd).

Modify it as per the needs, and remove or keep rest of the fields empty.

Note: YAML files are also supported. Try `$ json_resume sample --in=yaml`.

### Conversion

* Syntax

```
    json_resume convert [--template=/path/to/custom/template]
                        [--out=html|html_pdf|tex|tex_pdf|md]
                        [--locale=es|en|ge|fi|pt|zh_cn]
                        [--dest_dir=/path/to/put/output/files]
                        [--theme=default|classic] <json_input>

    <json_input> can be /path/to/json OR "{'json':'string'}" OR http://raw.json
```

    NEW: YAML files are also supported. Pass path/to/yaml file (must have .yaml or .yml).

* Default (HTML) version

```
    $ json_resume convert prateek_cv.json
```

A directory `resume/` will be generated in cwd, which can be put hosted on /var/www or on github pages. ([Sample](http://prat0318.github.io/json_resume/html_version/resume_with_icons/))


* HTML\* version

`html` version without icons can be generated by giving `icons` as `false` : ([Sample](http://prat0318.github.io/json_resume/html_version/resume_without_icons/))

```
     "settings": {
         "icons" : false
    },
```

* PDF version from HTML ([Sample](http://prat0318.github.io/json_resume/html_version/resume_with_icons/resume.pdf))

```
    $ json_resume convert --out=html_pdf prateek_cv.json
```

* LaTeX version ([Sample](https://www.writelatex.com/read/ynhgbrnmtrbw))

```
    $ json_resume convert --out=tex prateek_cv.json
```

  LaTex also includes a ``classic`` theme. Usage: ``--theme=classic`` ([Sample](https://www.writelatex.com/read/xscbhfpxwkqh)).

* PDF version from LaTeX ([Sample](https://www.writelatex.com/read/ynhgbrnmtrbw))

```
    $ json_resume convert --out=tex_pdf prateek_cv.json
```

* Markdown version ([Sample](https://gist.github.com/prat0318/9c6e36fdcfd6a854f1f9))

```
    $ json_resume convert --out=md prateek_cv.json
```

## i18n Support

Support for ``en``, ``ge``, ``es``, ``fi`` and ``pt`` right now. Pull requests for others are welcome.

```
    $ json_resume convert --locale=es prateek_cv.json
```

It is also possible to define a custom location for locale definitions.
Pass the option `--locale_dir=path/to/defs`.
In this location there should be the definitions available.
The default one is `en.yml`, others may be provided as well.
This is useful if you want to define new headings.

## Markup Language

JSON is parsed as per the `markdown` standards. This implies all this works-
- \*\* **bold** \*\*,
- \_ _italics_ \_,
- script&lt;sup&gt;<sup>sup</sup>&lt;sup/&gt;,
- script&lt;sub&gt;<sub>sub</sub>&lt;sub/&gt;,
- \[[href](#)\]\(#\),
- <<[http://github.com](http://github.com)>>

## Customization

#### Mustache Templates
* Output is created using mustache templates. They are located in `templates/`. These can be modified and given as `--template=/path/to/template` to `convert`.

#### Adding your own icons to json_resume
1. Download the svg(s) you would like to use from a site like [IcoMoon](https://icomoon.io/app/) or [IconFinder](https://www.iconfinder.com) and chose size as 16X16.
2. Download the official ``json_resume`` svgs from [the json_resume_icon repo zip](https://github.com/NoahHines/json_resume_icons/archive/master.zip). Unzip it, svgs are present in `/SVG`.
3. Drag all svgs (including yours) onto the [grumpicon](http://www.grumpicon.com/) and then "downlode it".
4. Drag all the files (``.css`` and ``.png``) from the ``grunticon`` folder into your local ``json_resume`` gem's folder ``json_resume-1.X.X/extras/resume_html/public/css/``, replacing existing files ([Read this](http://stackoverflow.com/questions/2827496/where-are-my-ruby-gems) to find your gem's location in your machine).
5. Modify your HTML [mustache template](#mustache-templates) to include your icons. Specifically, edit the ``div`` class in the template to include your new grunticon (```<div class="icon-user icon-square">```, where "user" is the SVG name). You can also check grunticon's generated ``preview.html`` file to verify the icon class name.
6. Run ``json_resume convert --template=/path/to/template <json>``, and you should be able to see the changes in the generated HTML. Also, steps 1-5 are to be done just once and the icons will be stored within your local gem.

## Changelog

### v1.0
* Glyphicons are now replaced by Font-Awesome icons.
* HTML version has a responsive design.
* Supports i18n. (Supporting ``es``, ``pt`` right now).
* New classic theme for latex format.

## Contributing

Many awesome formats can be created by writing new mustache templates. We :heart: **Pull Requests**.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
