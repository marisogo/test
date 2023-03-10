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

## <div align="center">*GUImme more*</div>
*<div align="center">Check out our [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-gui/) and [documentation](https://docs.taipy.io/en/latest/manuals/gui/)</div>*

<br>
<br>

## EN-CORE?

#### <div align="center">Let's create a quick pipeline that doubles our input number 43</div>  
<br>

### Taipy Studio - The easy peasy way
*You can use the CORE editor called Taipy Studio in VSCode.* 

<div align="center"><img src="https://github.com/marisogo/test/blob/main/taipySTUDIOdemo.gif" width=600 height=400 alt="GUI demo"></img></div> 

## <div align="center">*Want to be Studio-us?*</div>
*<div align="center">Check out our [documentation]([https://docs.taipy.io/en/latest/](https://docs.taipy.io/en/latest/manuals/studio/)
and [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) </div>*

<br>

### Taipy CORE - a walk on the code side
*Low Code your DAGs* 

```python
import taipy as tp
from taipy import Config

#function
def double(nb):
    return nb * 2

input_data=43

#datanodes
input_data_node_cfg = Config.configure_data_node(id="input", default_data=input_data)
output_data_node_cfg = Config.configure_data_node(id="output")

#Configuration of task
task_cfg = Config.configure_task(id="double",
                                 function=double,
                                 input=input_data_node_cfg,
                                 output=output_data_node_cfg)

#Configuration of the pipeline and scenario
pipeline_cfg = Config.configure_pipeline("my_pipeline", [task_cfg])
scenario_cfg = Config.configure_scenario("my_scenario", [pipeline_cfg])

#my_scenario is the id of the scenario configured
scenario_cfg = Config.scenarios['my_scenario']

tp.Core().run()

# Creation of the scenario and execution
scenario = tp.create_scenario(scenario_cfg)
tp.submit(scenario)

print("Value at the end of task", scenario.output.read())
```
<br>

## <div align="center">*Gimme Core*</div>
*<div align="center">Check out our [getting started](https://docs.taipy.io/en/latest/getting_started/getting-started-core/) and [documentation](https://docs.taipy.io/en/latest/manuals/core/) </div>*

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
