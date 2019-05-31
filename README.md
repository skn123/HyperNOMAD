*****
# Hyperparameter optimization of deep neural networks with HYPERNOMAD
*****

HYPERNOMAD is a C++ and Python package dedicated to the hyperparameter optimization of deep neural networks. The package contains a blackbox specifically designed for this problematic and provides a link with the NOMAD software used for the optimization. The blackbox takes as inputs a list of hyperparameters, builds a corresponding deep neural network in order to train, validate and test it on a specific data set before returning the test error as a mesure of performance. NOMAD is then used to minimize this error. The following appendix provides an overview of how to use the HYPERNOMAD package.

The following tutorial shows the different steps to take in order to run HYPERNOMAD on a first example. The complete functionalities of HYPERNOMAD are described in the [documentation](https://hypernomad.readthedocs.io/en/latest/).

## Prerequisites

In order to run HYPERNOMAD correctly, please make sure to have:

* A compiled version of [NOMAD](https://www.gerad.ca/nomad/).
* Python > 3.6
* [PyTorch](https://pytorch.org/)
* GCC > 3.8


## installation of HYPERNOMAD

First build the executable by running the following command.

```
make

    building HYPERNOMAD ...

    To be able to run the example
    the HYPERNOMAD_HOME environment variable
    must be set to path_to_home_directory_of_hypernomad
    
```

When the compilation is successful, a message appears asking to set an environment variable 'HYPERNOMAD_HOME'. This can be done by adding a line in the file .profile or .bashrc :


```
    export HYPERNOMAD_HOME=path_to_home_directory_of_hypernomad
```    

The executable hypernomad.exe is located in the bin directory. You can check that the installation is successful by trying to run the commad

```
    $HYPERNOMAD_HOME/bin/./hypernomad.exe -i
```    

which should return the following informations:

```
    --------------------------------------------------
      HyperNomad - version 1.0
    --------------------------------------------------
      Using Nomad version 3.9.0 - www.gerad.ca/nomad
    --------------------------------------------------

    Run           : hypernomad.exe hyperparameters_file
    Info          : hypernomad.exe -i
    Help          : hypernomad.exe -h
    Version       : hypernomad.exe -v
    Usage         : hypernomad.exe -u
    Neighboors    : hypernomad.exe -n hyperparameters_file
```

## Getting started

The next phase of to create a parameter file that contains the necessary informations to specify the classification problem, the search space and the initial starting point. Here is an example of a parameter file designed for the MNIST problem. The number of convolutional layers is fixed to 5, which means that this value will not change during the optimization, and it bounds are not changed from the default values. On the other hand, the dropout rate is allowed to vary between [0.3, 0.8] instead of the default range of [0, 1] and is initialized at 0.6


```
# Mandatory information
DATASET                 MNIST
MAX_BB_EVAL             100

# Optional information
NUM_CON_LAYERS          5  -  -  FIXED
KERNELS                 3
NUM_FC_LAYERS           6
ACTIVATION_FUNCTION     2
DROPOUT_RATE            0.6  0.3 0.8
```

More details are provided in the user guide section of the [documentation](https://hypernomad.readthedocs.io/en/latest/).


## Running an optimization

The optimization starts by executing the command:

```
$HYPERNOMAD_HOME/bin/./hypernomad.exe parameter_file.txt
```

Two examples of parameter files are provided in the folder examples. One uses CIFAR-10 starting from the default starting point and the second uses MNIST with the specifications detailed in the previous section.

To use this files, the cammand is:

```
$HYPERNOMAD_HOME/bin/./hypernomad.exe $HYPERNOMAD_HOME/examples/parameter_file_cifar10.txt
```
or 


```
$HYPERNOMAD_HOME/bin/./hypernomad.exe $HYPERNOMAD_HOME/examples/parameter_file_mnist.txt
```
