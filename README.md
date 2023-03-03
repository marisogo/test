<br>
<img src="https://github.com/marisogo/test/blob/main/icone.png" alt="Taipy Logo" style="margin-top:20px" width="250" height="250" ></img>

#  🐍 Welcome to Taipy 🐍
<br>
Turns Data and AI algorithms into full web apps in no time. How? Taipy GUI with Taipy Core pops out as a 360° platform to build production-ready web apps.
** open source, 10000% python **

<br>
<br>

#  🔚 We make both **ends** meet 🔚
##  TAIPY GUI - the frond end
<img src="https://github.com/marisogo/test/blob/main/GUI.gif" alt="Taipy Logo" style="margin-top:20px" width="300" height="300" ></img>
## TAIPY CORE - the back end
<img src="https://github.com/marisogo/test/blob/main/CORE.png" alt="Taipy Logo" style="margin-top:20px" width="300" height="300" ></img>

## Installation

Open a terminal and run:

```bash
$ pip install taipy
```

You're all set! All aboard the Taipy journey 🚂

<br>

## Ready, Set, GUI

### Tiny Taipy GUI Demo

Create a new file `taipy.py` with the following code:
```python
from taipy import Gui

my_app="""
#Demo
##Getting started with Taipy GUI

<|{'WELCOME TO TAIPY'}|text|>
"""

Gui(page=my_app).run()
```
Press RUN/CTRL+F5

🎊 TADA! 🎊
<img src="https://user-images.githubusercontent.com/7164864/215172915-cf087c56-e7ae-449a-83a4-b5fa0328d954.gif" width=300 alt="Little example"></img>
### Ready for more
Check out all our [getting started and documentation](https://docs.taipy.io/en/latest/)

<br>

## EN-CORE?

### Tiny Taipy CORE Demo

<br>


## Usage
  - [Taipy](#taipy)
  - [License](#license)
  - [Usage](#usage)
  - [What is Taipy](#what-is-taipy)
  - [Installation](#installation)
  - [Contributing](#contributing)
  - [Code of conduct](#code-of-conduct)
  - [Directory Structure](#directory-structure)


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
