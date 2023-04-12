<br>
<br>

<img align="left" src="https://github.com/marisogo/test/blob/main/logo_borders.png" alt="Taipy Logo" width="150" height="150" ></img>
<br>
#  Welcome to Taipy 
<p align="left">
    <a href="https://pypi.python.org/pypi/taipy/" alt="Python version">
        <img alt="PyPI" src="https://img.shields.io/pypi/v/taipy.svg?label=pip&logo=PyPI&color=ff462b&labelColor=283282"></a>
    <a href="https://pypi.org/project/taipy" alt="pip version">
        <img alt="PyPI" src="https://img.shields.io/pypi/pyversions/taipy?color=ff462b&labelColor=283282"></a>
    <a href="https://www.youtube.com/@taipy8009" alt="YouTube">
        <img src="https://img.shields.io/badge/youtube-click_to_watch_videos-red.svg?color=ff462b&labelColor=283282&logo=youtube" /></a>
     <a href="https://twitter.com/Taipy_io" alt="Twitter">
        <img src="https://img.shields.io/badge/twitter-click_for_tweets-red.svg?color=ff462b&labelColor=283282&logo=twitter" /></a>
    <a href="https://github.com/Avaiga/taipy/actions/workflows/tests.yml" alt="tests">
        <img alt="PyPI" src="https://github.com/Avaiga/taipy/actions/workflows/tests.yml/badge.svg"></a>


<br>

###  <div align="left">Turns Data and AI algorithms into full web apps in no time. 
###  How? Taipy GUI with Taipy Core pops out as a 360° platform to build production-ready web apps</div>  

 

<br>
<br>

###  <div align="left">*Open Source, 100% Python*</div>


<br>
<br>
<br>

#  <div align="center"> 📊 We make both ends meet ⚙️ </div>  
<br>
 <div align="center">
    
| TAIPY GUI - the frond end  | TAIPY Core - the back end |
| --------  | -------- |
|<img src="https://github.com/marisogo/test/blob/main/gui_intro_readme.gif" alt="Taipy Logo"  width="350" height="300"/> | <img src="https://github.com/marisogo/test/blob/main/core_intro_readme.gif" alt="Taipy Logo"  width="350" height="300"/>

    
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

## Ready, Set, GUI

### Tiny Taipy GUI Demo

```python
excitement_page="""
# Welcome to Taipy
## Getting started with Taipy GUI
### How excited are you to try Taipy?

<|{excitement}|slider|min=1|max=100|>

My excitement level: <|{excitement}|text|>
"""
excitement=100

Gui(page=my_page).run()
```
*RUN*🏃🏽‍♀️  

<div align="center"><img src="https://github.com/marisogo/test/blob/main/gui_app_readme.gif" width=600 height=400 alt="GUI demo"></img></div>
<div align="center">🎊 TADA! 🎊</div>  

<br>
<br>

### <div align="center">*GUImme more*</div>
*<div align="center">Check out our [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-gui/) and [Documentation](https://docs.taipy.io/en/latest/manuals/gui/)</div>*

<br>
<br>

## EN-CORE?

#### <div align="center">Let's create a back-end execution, also called scenario using Taipy Core. Our scenario will filter movie data based on the genre you choose. This scenario will be submitted (i.e., executed) each time the genre selection changes and output the seven most popular movies of that genre. </div>  
<br>

*Here is our filter function: it's a standard python function that will constitute our unique task in the scenario*
```python
def filtering_genre(initial_dataset: pd.DataFrame, selected_genre):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_genre)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data
```

*This is the execution graph of the scenario we will be implemeting*

<div align="center"><img src="https://github.com/marisogo/test/blob/main/readme_exec_g.png" alt="Taipy Logo"  width="400" height="200"/></div> 


### Taipy Studio - The easy peasy way
*You can use the Taipy Studio extension in VSCode to configure your pipeline easily* 

<div align="center"><img src="https://github.com/marisogo/test/blob/main/studio_readme.gif" width=600 height=400 alt="GUI demo"></img></div> 

*Your configuration is automatically saved as a toml file* 

<br>
<br>

### <div align="center">*Want to be Studio-us?*</div>
*<div align="center">Check out our [Documentation](https://docs.taipy.io/en/latest/manuals/studio/)
and [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) </div>*

<br>
<br>

*Now, let's load this configuration and add a GUI on top for a 🎉FULL APPLICATION🎉*
```python
import taipy as tp
import pandas as pd
from taipy import Config, Scope, Gui

# TAIPY Core

# Filtering function - task
def filtering_genre(initial_dataset: pd.DataFrame, selected_genre):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_genre)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data

# Load the configuration made with Taipy Studio
Config.load('config.toml')
scenario_cfg = Config.scenarios['scenario']

# Start Taipy Core service
tp.Core().run()

# Create a scenario
scenario = tp.create_scenario(scenario_cfg)


# TAIPY GUI
# Let's add Taipy GUI to our Taipy Core for a full application

# Callback definition - submits scenario with genre selection
def modify_genre(state):
    scenario.selected_genre_node.write(state.selected_genre)
    tp.submit(scenario)
    state.df = scenario.filtered_data.read()  

# Get list of genres
list_genres = ['Action', 'Adventure', 'Animation', 'Children', 'Comedy', 'Fantasy', 'IMAX', 'Romance',
               'Sci-FI', 'Western', 'Crime', 'Mystery', 'Drama', 'Horror', 'Thriller', 'Film-Noir',
               'War', 'Musical', 'Documentary']

# Initialization of variables
df = pd.DataFrame(columns=['Title', 'Popularity %'])
selected_genre = None

# My page
my_page = """
# Film recommendation

## Choose your favorite genre
<|{selected_genre}|selector|lov={list_genres}|on_change=modify_genre|dropdown|>

## Here are the top 7 picks by popularity
<|{df}|chart|x=Title|y=Popularity %|type=bar|title=Film Popularity|>
"""

Gui(page=my_page).run(port=5002)

```
*RUN*🏃🏽‍♀️ 

<br>

<div align="center">🎊TADA!🎊</div>  
<br>
<div align="center"><img src="https://github.com/marisogo/test/blob/main/app_readme.gif" width=700 height=400 alt="GUI demo"></img></div> 

<br>

<br>

<br>
<br>

### Taipy CORE - a walk on the code side
<div align="left">If you prefer coding your configurations instead of using Taipy Studio, Taipy's got you 🫵 </div>   

*<div align="left">Check out the Movie Genre Filter scenario creation with this [Demo](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) </div>*

<br>

### <div align="center">*Gimme Core*</div>
*<div align="center">Check out our [Getting Started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) and [Documentation](https://docs.taipy.io/en/latest/manuals/core/) </div>*

<br>
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
