<br>
<br>

<img align="left" src="readme_img/readme_logo.png" alt="Taipy Logo" width="20%" ></img>
<br>
#  Welcome to Taipy
<p align="left">
    <a href="https://pypi.python.org/pypi/taipy/" alt="Taipy version">
        <img alt="PyPI" src="https://img.shields.io/pypi/v/taipy.svg?label=pip&logo=PyPI&color=ff462b&labelColor=283282"></a>
    <a href="https://pypi.org/project/taipy" alt="Python version">
        <img alt="PyPI" src="https://img.shields.io/pypi/pyversions/taipy?color=ff462b&labelColor=283282"></a>
    <a href="https://www.youtube.com/@taipy8009" alt="YouTube">
        <img src="https://img.shields.io/badge/youtube-click_to_watch_videos-red.svg?color=ff462b&labelColor=283282&logo=youtube" /></a>
     <a href="https://twitter.com/Taipy_io" alt="Twitter">
        <img src="https://img.shields.io/badge/twitter-click_for_tweets-red.svg?color=ff462b&labelColor=283282&logo=twitter" /></a>


<br>

###  <div align="left"> Your Web Application Builder. Pure Python. 
###  <div align="left"> How? Taipy pops out as a 360° platform to build production-ready web applications 
### <div align="center"> Open Source, 100% Python</div>

<br>

#  <div align="center"> 📊 We make both ends meet ⚙️ </div>
<br>
 <div align="center">

| TAIPY - the frond-end  | TAIPY - the back-end | Taipy Cloud - the host |
| --------  | -------- |-------- |
|<img src="readme_img/readme_gui_intro.gif" alt="Taipy FE Animation"  width="100%"/> | <img src="readme_img/readme_core_intro.gif" alt="Taipy BE Animation"  width="100%"/> | <img src="readme_img/readme_taipy_cloud.gif" alt="Taipy BE Animation"  width="100%"/>


</div>

<br>
<br>

## Installation

Open a terminal and run:

```bash
$ pip install taipy
```

*You're all set! All aboard the Taipy journey 🚂*

<br>

## Community

Join our [Discord](https://discord.gg/XcFhrJZru3) to give us feedback, share your creations or just to have a chat with us.

<br>

## Ready, Set, GUI

**Tiny Taipy Front-End Demo**

```python
from taipy import Gui

excitement_page = """
# Welcome to Taipy
## Getting started with Taipy
### How excited are you to try Taipy?

<|{excitement}|slider|min=1|max=100|>

My excitement level: <|{excitement}|text|>
"""
excitement = 100

Gui(page=excitement_page).run()
```
*RUN*🏃🏽‍♀️
<div align="center">🎊 TA-DA! 🎊</div>
<br>
<div align="center"><img src="readme_img/readme_fe_app.gif" width="50%" alt="GUI demo"></img></div>

<br>
<br>

***<div align="center">Find out more</div>***
*<div align="center">Check out our [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-gui/) and [Documentation](https://docs.taipy.io/en/latest/manuals/gui/)</div>*

<br>
<br>

## Taipy Back-End ⚙️

**<div align="left">Let's create a back-end execution, also called *scenario*, using Taipy backend. Our scenario will filter movie data based on the genre you choose. This scenario will be submitted (i.e., executed) each time the genre selection changes and output the seven most popular movies of that genre. </div>**

<br>

<div align="center"> ⚠️ Here, the backend involves the execution of a very simple pipeline (made of a single task). Note that Taipy is designed to build much more complex pipelines 🚀 (with many tasks!) </div>

<br>
<br>

*Here is our filter function: a standard Python function that is used by the unique task in the scenario*
```python
def filter_genre(initial_dataset: pd.DataFrame, selected_genre):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_genre)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data
```

*This is the execution graph of the scenario we are implementing*

<div align="center"><img src="readme_img/diag_2.png" alt="Taipy Core Graph"  width="40%"/></div>

### Taipy Studio - The easy-peasy way
*You can use the Taipy Studio extension in VSCode to configure your sequence with no code*

<div align="center"><img src="readme_img/readme_demo_studio.gif" width="60%" alt="GUI demo"></img></div>

*Your configuration is automatically saved as a TOML file*

<br>
<br>

***<div align="center">Find out more</div>***
*<div align="center">Check out our [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) and [Documentation](https://docs.taipy.io/en/latest/manuals/studio/) </div>*

<br>
<br>
<br>
<br>

### Taipy Back-End - a walk on the code side
<div align="left">For more advanced use cases or if you prefer coding your configurations instead of using Taipy Studio, Taipy has your back! </div>

*<div align="left">Check out the movie genre demo scenario creation with this [Demo](https://www.taipy.io/project/movie-genre-selector/) </div>*

<br>
<br>
<br>

***<div align="center">Find out more</div>***
*<div align="center">Check out our [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) and [Documentation](https://docs.taipy.io/en/latest/manuals/core/) </div>*

<br>
<br>
<br>


## Front-end ➕ Back-end
*Now, let's load this configuration and add a user interface on top for a 🎉FULL APPLICATION🎉*
```python
import taipy as tp
import pandas as pd
from taipy import Config, Scope, Gui


# TAIPY Back-end
=======
# Create a Taipy App that will output the 7 best movies for a genre


# Filter function for Task
def filtering_genre(initial_dataset: pd.DataFrame, selected_genre):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_genre)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data

# Taipy- Back-End definition

# Load the configuration made with Taipy Studio
Config.load('config.toml')
scenario_cfg = Config.scenarios['scenario']

# Run of the Taipy Back-End service
tp.Core().run()

# Creation of my scenario
scenario = tp.create_scenario(scenario_cfg)


# Taipy -Front-End definition

# Callback definition
def modify_df(state):
    scenario.selected_genre_node.write(state.selected_genre)
    tp.submit(scenario)
    state.df = scenario.filtered_data.read()    

# Get list of genres
list_genres = ['Action', 'Adventure', 'Animation', 'Children', 'Comedy', 'Fantasy', 'IMAX', 'Romance',
               'Sci-FI', 'Western', 'Crime', 'Mystery', 'Drama', 'Horror', 'Thriller', 'Film-Noir',
               'War', 'Musical', 'Documentary']

# Initialization of variables
df = pd.DataFrame(columns=['Title', 'Popularity %'])
selected_genre = 'Action'

## Set initial value to Action
def on_init(state):
    modify_df(state)

# movie_genre_app
movie_genre_app = """
# Film recommendation

## Choose your favorite genre
<|{selected_genre}|selector|lov={list_genres}|on_change=modify_df|dropdown|>

## Here are the top 7 picks
<|{df}|chart|x=Title|y=Popularity %|type=bar|title=Film Popularity|>
"""

# run the app
Gui(page=movie_genre_app).run()
```
*RUN*🏃🏽‍♀️

<br>

<div align="center">🎊TA-DA!🎊</div>
<br>
<div align="center"><img src="readme_img/readme_app.gif" width="80%" alt="GUI demo"></img></div>

<br>

<br>

## Taipy Cloud - Elevate your Taipy application to the cloud ☁️
Taipy greatly eases your web application deployment. It provides the most suitable cloud tool to host, deploy, and share your Taipy applications easily. In addition, this platform provides the ability to manage, store, and maintain the various states of your backend.

***<div align="center"> Click [here](https://www.taipy.io/taipy-cloud/) to get started for free </div>***

<br>
<br>

## Contributing ⚒⚒

Want to help build _Taipy_? Check out our [`CONTRIBUTING.md`](CONTRIBUTING.md) file.

## Code of conduct

Want to be part of the _Taipy_ community? Check out our [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) file.

## License
Copyright 2023 Avaiga Private Limited

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with
the License. You may obtain a copy of the License at
[http://www.apache.org/licenses/LICENSE-2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on
an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the
specific language governing permissions and limitations under the License.

