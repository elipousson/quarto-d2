# D2 Example

The [Quarto](https://quarto.org) extension that allows you to generate
[D2](https://d2lang.com) diagrams directly within your markdown
documents. You can specify various attributes to control the appearance
and layout of the diagrams.

This extension draws inspiration from
[`ram02z/d2-filter`](https://github.com/ram02z/d2-filter).

## Installing

Before you can use this extension, you’ll need to make sure you’ve
installed the d2 CLI utility.

Next, use the `quarto add` command to install the extension:

``` bash
quarto add data-intuitive/quarto-d2
```

This will install the extension under the `_extensions` subdirectory. If
you’re using version control, you will want to check in this directory.

## Example

Here is the source code for a [minimal example](example.qmd):

```` markdown
---
title: "D2 Example"
filters:
  - d2
---

```{.d2}
x -> y
```
````

With this setup, the `d2` filter will process any code blocks with the
`.d2` class, applying the attributes you specify.

That’s it! Now you know how to use the `d2` filter to generate diagrams
in your quarto documents.

## Usage

### Basic Use

To use the d2 filter, add the d2 class to your code blocks and write
your diagram code inside the code block. Here is a basic example:

```` markdown
```{.d2}
logs: {
  shape: page
  style.multiple: true
}
user: User {shape: person}
network: Network {
  tower: Cell Tower {
    satellites: {
      shape: stored_data
      style.multiple: true
    }

    satellites -> transmitter
    satellites -> transmitter
    satellites -> transmitter
    transmitter
  }
  processor: Data Processor {
    storage: Storage {
      shape: cylinder
      style.multiple: true
    }
  }
  portal: Online Portal {
    UI
  }

  tower.transmitter -> processor: phone logs
}
server: API Server

user -> network.tower: Make call
network.processor -> server
network.processor -> server
network.processor -> server

server -> logs
server -> logs
server -> logs: persist

server -> network.portal.UI: display
user -> network.portal.UI: access {
  style.stroke-dash: 3
}
```
````

![](./images/diagram-1.svg)

### Adding Attributes

You can specify additional attributes to control the appearance and
layout of the diagram.

- `theme`: Specifies the theme of the diagram. Default is
  `NeutralDefault`. Options are `NeutralDefault`, `NeutralGrey`,
  `FlagshipTerrastruct`, `CoolClassics`, `MixedBerryBlue`, `GrapeSoda`,
  `Aubergine`, `ColorblindClear`, `VanillaNitroCola`, `ShirelyTemple`,
  `EarthTones`, `EvergladeGreen`, `ButteredToast`, `DarkMauve`,
  `Terminal`, `TerminalGrayscale`, `Origami`.
- `layout`: Specifies the layout algorithm to use. Default is `elk`.
  Options are `dagre`, `elk`, `tala`.
- `format`: Specifies the format of the output image. Default is `svg`.
  Option are `svg`, `png`, `pdf`.
- `sketch`: Whether to use a “sketch” style for the diagram. Default is
  `false`.
- `pad`: Amount of padding around the diagram. Default is `100`.
- `caption`: Caption to add to the diagram.
- `folder`: Folder where the generated diagram will be saved. If not
  provided, the image will be embedded inline in the document (HTML
  only).
- `filename`: Name of the output file.

Here’s an example that uses multiple attributes:

```` markdown
```{.d2 theme="CoolClassics" layout="elk" pad=20 caption="This is a caption"}
x -> y -> z
```
````

![This is a caption](./images/diagram-2.svg)

### Setting Output Folder and File Name

You can specify a folder where the generated diagram will be saved using
the `folder` attribute. The `filename` attribute allows you to set a
custom name for the output file.

```` markdown
```{.d2 folder="./images" filename="my_diagram"}
x -> y -> z
```
````

![](./images/my_diagram.svg)

<div>

> **Note**
>
> If the `folder` attribute is not provided and the output format is
> HTML, the image will be embedded inline in the document.

</div>
