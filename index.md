# Goal

The city of Santa Monica provides a public dataset describing the properties of
~35,000 trees in the city. Our goal is to provide a map interface that lets you
view, filter, and explore this dataset.

# Project Structure

The project is broken into two core repositories:

- [public-tree-map](https://github.com/Public-Tree-Map/public-tree-map)
- [public-tree-map-data-pipeline](https://github.com/Public-Tree-Map/public-tree-map-data-pipeline)

## public-tree-map
This repository manages the front-end web application. It uses CircleCI to
auto-publish itself to https://public-tree-map.surge.sh after every check-in to
master.

### Tech Stack

This is made in plain 'ol HTML, CSS, and JavaScript.

There is no traditional 'framework'.  
There is no build system.

Running the site is as easy as double-clicking the `index.html` file.

The site is structured using a class MVC/MVP pattern.

1. You write the UI in HTML and CSS.
1. You fetch some data.
1. You give that data to a "class" who is responsible for putting the data in
   that model into the HTML.

For more details, please see the specific repository's README.

## public-tree-map-data-pipeline

The data pipeline has one core goal: take data provided by the city and convert
it to something usable by the front-end.

This involves processing the data, fetching data from auxiliary sources, and
combining it into a set of common data structures that can be fetched by the
client.

It's called a 'pipeline' because it's structured as a series of scripts. Each
script expects some input, modifies that input, and then produces some output.
That output becomes another script's input, and thus the chain continues.

### Tech Stack

Most of the scripts are written in node.js, but some geodata processing is done
in python. The nice thing about setting it up as a pipeline is that you can
pretty much use any stack you want for each stage so long as you have a clear
contract between the scripts.

The end result of the pipeline is currently two types of JSON files.

1. `map.json`: All of the tree data necessary to view and filter the trees on
   the map.
1. `{tree_id}.json`: A set of JSON files (one for each tree) that contains all
   of the data specific to an individual tree that will be rendered in the info
   panel.

These files are stored and served in a Google Cloud Storage bucket.

For more information, see the specific repository's README.
