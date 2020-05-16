# Gitea PlantUML external renderer

Very simple renderer for standalone PlantUML files. Basically just creates the image URL using provided PlantUML server address.

Markdown with PlantUML is already solved as explained in [Gitea documentation](https://docs.gitea.io/en-us/customizing-gitea/). This addresses rendering of "plain" PlantUML files.

It is uses parts from [python-plantuml](https://github.com/dougn/python-plantuml).

## Usage

```Bash
usage: gitea_puml_renderer [-h] [-u PLANTUML_URL] [-f PUML_FILE] [-s] [-i]

Gitea PlantUML renderer.

optional arguments:
  -h, --help            show this help message and exit
  -u PLANTUML_URL, --plantuml-url PLANTUML_URL
                        Plantuml server URL. Default is
                        http://www.plantuml.com/plantuml
  -f PUML_FILE, --file PUML_FILE
                        Use given file as input. Otherwise will use stdin
  -s, --svg             Use SVG (default is PNG)
  -i, --image-only      Generate only image URL (default the whole image HTML
                        tag)
```

## Gitea integration

Put somewhere `gitea_puml_renderer` (e.g. as `/usr/local/bin/gitea_puml_renderer`).
Add to your gitea config app.ini (usually in `/etc/gitea/app.ini`) something like (check/adjust at least path to the `gitea_puml_renderer`):

```ini
[markup.plantuml]
ENABLED = true
FILE_EXTENSIONS = .plantuml,.puml
RENDER_COMMAND = "/usr/local/bin/gitea_puml_renderer -u http://www.plantuml.com/plantuml"
IS_INPUT_FILE = false
```

Restart `gitea` (depends on the way how you run it), for example:

```Bash
systemctl restart gitea
```
