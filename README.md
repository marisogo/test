<br>
<br>

<img align="left" src="https://github.com/marisogo/test/blob/main/logo_borders.png" alt="Taipy Logo" width="150" height="150" ></img>
<br>
#  Welcome to Taipy 
<p align="left">
    <a href="https://pypi.python.org/pypi/taipy/" alt="PyPI version">
        <img alt="PyPI" src="https://img.shields.io/pypi/v/taipy?color=ff462b&labelColor=283282"></a>
    <a href="https://pepy.tech/badge/taipy/" alt="Downloads">
        <img src="https://img.shields.io/pypi/dm/taipy?color=ff462b&labelColor=283282" /></a>
    <a href="https://www.youtube.com/@taipy8009" alt="YouTube">
        <img src="https://img.shields.io/badge/youtube-click_to_watch_videos-red.svg?color=ff462b&labelColor=283282&logo=youtube" /></a>
     <a href="https://twitter.com/Taipy_io" alt="Twitter">
        <img src="https://img.shields.io/badge/twitter-click_for_tweets-red.svg?color=ff462b&labelColor=283282&logo=twitter" /></a>
</p> 

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
    
| TAIPY GUI - the frond end  | TAIPY CORE - the back end |
| --------  | -------- |
|<img src="https://github.com/marisogo/test/blob/main/taipyGUI.gif" alt="Taipy Logo"  width="400" height="300"/> | <img src="https://github.com/marisogo/test/blob/main/taipyCORE.gif" alt="Taipy Logo"  width="400" height="300"/>

    
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

Create a new file `taipy.py` with the following code:
```python
from taipy import Gui

my_app="""
# Welcome to Taipy
## Getting started with Taipy GUI

### How excited are you to try TAIPY?

<|{my_param}|slider|min=1|max=100|>

My excitement level: <|{my_param}|text|>
"""

my_param=100

Gui(page=my_app).run()
```
*Press RUN/CTRL+F5*  

<div align="center"><img src="https://github.com/marisogo/test/blob/main/taipyGUIdemo.gif" width=600 height=400 alt="GUI demo"></img></div>
<div align="center">🎊 TADA! 🎊</div>  

<br>
<br>

### <div align="center">*GUImme more*</div>
*<div align="center">Check out our [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-gui/) and [documentation](https://docs.taipy.io/en/latest/manuals/gui/)</div>*

<br>
<br>

## EN-CORE?

#### <div align="center">Let's create a quick pipeline that filters movie data based on the genre you choose. The output will be the 7 most popular movies for that genre</div>  
##### Here is our filter function
```python
def filter_genre(initial_dataset: pd.DataFrame, selected_value):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_value)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data
```
<br>

### Taipy Studio - The easy peasy way
*You can use Taipy Studio to configure your pipeline easily in VSCode.* 

<div align="center"><img src="https://github.com/marisogo/test/blob/main/movie_app_studio.gif" width=600 height=400 alt="GUI demo"></img></div> 

<br>

*Now, let's load this configuration and run it*
```python
import pandas as pd
import taipy as tp
from taipy import Config

# Filter function for task
def filter_genre(initial_dataset: pd.DataFrame, selected_value):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_value)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data

# Loading the configuration
Config.load('config.toml')
scenario_cfg = Config.scenarios['scenario']

# Run of the Taipy Core service
tp.Core().run()

# Create a scenario for "Fantasy" genre
scenario = tp.create_scenario(scenario_cfg)
# Configure "Fantasy" in the selected_value_node
scenario.selected_value_node.write('Fantasy')
# Submit scenario
tp.submit(scenario)
# Get the best 7 picks for "Fantasy" genre 
top_7 = scenario.filtered_data.read()
print("Top 7 picks for Fantasy genre", top_7[['Title', 'Popularity %']])

```
<br>

<div align="center">🎊 TADA! 🎊</div> 

*LOTR fan here so not suprised!* 

### <div align="center">*Want to be Studio-us?*</div>
*<div align="center">Check out our [documentation](https://docs.taipy.io/en/latest/manuals/studio/)
and [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) </div>*

<br>

### Taipy CORE - a walk on the code side
*If you prefer coding your configurations, Taipy's got you 🫵 Check out the movie genre selector pipeline creation HERE [movie selector demo](https://docs.taipy.io/en/latest/manuals/studio/)*

<br>

### <div align="center">*Gimme Core*</div>
*<div align="center">Check out our [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) and [documentation](https://docs.taipy.io/en/latest/manuals/core/) </div>*

<br>

## GUI + CORE = 🎉FULL APP🎉
#### <div align="center">Let's add some GUI to our previous code and create a full web application</div>  


```python
import taipy as tp
import pandas as pd
from taipy import Config, Scope, Gui

# Create a Taipy App that will output the 7 best movies for a genre

# Callback definition
def modify_df(state):
    scenario.selected_value_node.write(state.selected_value)
    tp.submit(scenario)
    state.df = scenario.filtered_data.read()    
# Filter function for Task
def filter_genre(initial_dataset: pd.DataFrame, selected_value):
    filtered_dataset = initial_dataset[initial_dataset['genres'].str.contains(selected_value)]
    filtered_data = filtered_dataset.nlargest(7, 'Popularity %')
    return filtered_data

# Loading the configuration
Config.load('config.toml')
scenario_cfg = Config.scenarios['scenario']

# Run of the Taipy Core service
tp.Core().run()

# Create a scenario for "Fantasy" genre
scenario = tp.create_scenario(scenario_cfg)

# Get list of genres
dataset = scenario.initial_dataset.read()
list_genres = list(dataset['genres'].str.split('|').explode().unique())

# Initialization of variables
df = pd.DataFrame(columns=['Title', 'Popularity %'])
selected_value = None

# My page
my_page = """
# Film recommendation

## Choose your favorite genre
<|{selected_value}|selector|lov={list_genres}|on_change=modify_df|dropdown|>

## Here are the top 7 picks
<|{df}|chart|x=Title|y=Popularity %|type=bar|title=Film Popularity|>
"""

Gui(page=my_page).run()
```
<br>

<div align="center">🎊 TADA! 🎊</div> 
<div align="center"><img src="https://github.com/marisogo/test/blob/main/movie_genre_selector_app.gif" width=700 height=400 alt="GUI demo"></img></div> 

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
