
<img align="left" src="https://github.com/marisogo/test/blob/main/icone.png" alt="Taipy Logo" width="350" height="350" ></img>
<br>
<br>
#  Welcome to Taipy 
###  Turns Data and AI algorithms into full web apps in no time.
###  How? Taipy GUI with Taipy Core pops out as a 360° platform to build production-ready web apps</div>  
  
<br>

###  <div align="center">*Open Source, 100% Python*</div>


<br>
<br>
<br>

#  <div align="center">🔚 We make both **ends** meet 🔚</div>  
<br>

| TAIPY GUI - the frond end  | TAIPY CORE - the back end |
| --------  | -------- |
|<img src="https://github.com/marisogo/test/blob/main/taipyGUI.gif" alt="Taipy Logo" style="margin-top:20px" width="470" height="350"/> | <img src="https://github.com/marisogo/test/blob/main/taipyCORE.gif" alt="Taipy Logo" style="margin-top:20px" width="470" height="350"/>


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
#Welcome to Taipy
##Getting started with Taipy GUI

<|{'How excited are you to try TAIPY?'}|text|>

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

## <div align="center">*Gimme more*</div>
*<div align="center">Check out all our [getting started and documentation](https://docs.taipy.io/en/latest/)</div>*

<br>
<br>

## EN-CORE?

#### <div align="center">Let's create a quick pipeline that doubles our input number 43</div>  
<br>

### Taipy Studio - The easy peasy way
*You can use the CORE editor called Taipy Studio in VSCode.* 

<div align="center"><img src="https://github.com/marisogo/test/blob/main/taipySTUDIOdemo.gif" width=600 height=400 alt="GUI demo"></img></div>  

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
input_data_node_cfg = Config.configure_data_node("input", default_data=input_data)
output_data_node_cfg = Config.configure_data_node("output")

# Configuration of task
task_cfg = Config.configure_task("double",
                                 double,
                                 input_data_node_cfg,
                                 output_data_node_cfg)

# Configuration of the pipeline and scenario
pipeline_cfg = Config.configure_pipeline("my_pipeline", [task_cfg])
scenario_cfg = Config.configure_scenario("my_scenario", [pipeline_cfg])

# my_scenario is the id of the scenario configured
scenario_cfg = Config.scenarios['my_scenario']

tp.Core().run()

# Creation of the scenario and execution
scenario = tp.create_scenario(scenario_cfg)
tp.submit(scenario)

print("Value at the end of task", scenario.output.read())
```
<br>
<div align="center"><img src="https://github.com/marisogo/test/blob/main/taipyCOREdemo.gif" width=600 height=400 alt="CORE demo"></img></div>    

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


## Directory Structure

- `taipy`:
    - `_run.py`: The python module exposing the method `run` to use to start a Taipy application.
- `CODE_OF_CONDUCT.md`: Code of conduct for members and contributors of _taipy_.
- `CONTRIBUTING.md`: Instructions to contribute to _taipy_.
- `INSTALLATION.md`: Instructions to install _taipy_.
- `LICENSE`: The Apache 2.0 License.
- `README.md`: Current file.
- `setup.py`: The setup script managing building, distributing, and installing _taipy_.
