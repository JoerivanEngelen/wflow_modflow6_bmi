# Installation
Coupling Modflow 6 with Wflow.jl requires both a Julia and a Python 
installation. This is not a trivial exercise, and I hope that I can guide you
through it. Most of this README will be me you pointing you to the right 
documentation, with some extra tips.

## The Python side of things
Unlike Julia, Python does not have its' own package manager, therefore
I advise to install [miniconda](https://docs.conda.io/en/latest/miniconda.html).
This will install the package manager conda. 
Unless you really know what you are doing, I can recommend [creating a seperate conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html). 

### pyjulia
[pyjulia](https://pyjulia.readthedocs.io/en/latest/) lets you run Julia commands from 
within Python. You can install it by calling `pip install julia`. The first time you
use pyjulia, you have to call the following lines of code in Python:

```
import julia
julia.install()
```


## The Julia side of things

### Wflow
[The Wflow installation guide](https://deltares.github.io/Wflow.jl/dev/quick-start/) provides a good start with installing
Julia as well as Wflow. It also has some basic tips on the usage of Julia as well as how Wflow works. I recommend starting here.

### PyCall
[PyCall](https://github.com/JuliaPy/PyCall.jl) is required to let 
Julia call Python functions, but also to do the opposite, which is 
what we are going to do. Installing PyCall by default installs 
an extra conda installation, which seemed to confuse my computer.
Therefore one can build PyCall against an existing Python environment.

For example for a Windows user named "harry" who wants to build PyCall against 
the environment "trybmi", "harry" can open up his Julia REPL and call the 
following lines of code:

```
using Pkg
ENV["PYTHON"] = c:\Users\harry\Miniconda3\envs\trybmi\python.exe
Pkg.build("PyCall")
```

### BMI
The Julia [BasicModelInterface](https://github.com/Deltares/BasicModelInterface.jl) is used to access variables in Wflow. It can be called from Python with the above steps.

# Modflow 6

## Memory addresses
Knowing which memory addresses are availalbe in Modflow 6 is hard to infer from the source
code, therefore to print all available memory addresses in Modflow6, add this option in 
your namfile:

```
begin options
  memory_print_option all
end options
```

This will print all available memory addresses in you list file.