# Generator Fuzzer

This Python script will automatically generate a test case for the Generator assignment.

## Requirements

- Python 3
- NumPy

## Usage

The main Python script is `fuzzer.py`. Run `python fuzzer.py -h` to see the following usage text and description:

```
usage: fuzzer.py [-h] [--seed SEED] config name [count]

Procedurally generate a Generator test case.

positional arguments:
  config       path to configuration file
  name         name of test case to generate (creates name.in, name.out)
  count        number of generators to make in the test case

optional arguments:
  -h, --help   show this help message and exit
  --seed SEED  random number generator seed
```

## Configuration

A default configuration file is provided as `config.json`.

The following is a break-down of each of the configurable options:

```
{
    "generation-options": {
        "max-expression-recursion-depth": 10,   // Maximum depth of recursion allowed in the generation of expressions
        "add-random-whitespace": false,         // Option to enable adding random whitespace to the input file
        "random-whitespace-density": 3          // Density of whitespace to add, if the above option is enabled
    },
    "properties": {
        "max-range-length": 256,                // Maximum length of a range
        "id-length": {
            "min": 1,                           // Minimum length of an ID
            "max": 20                           // Maximum length of an ID
        }
    },
    "expression-weights": {                     // Weights of different expressions. 
                                                // The higher the value, the more likely a particular type of expression will be generated.
                                                // The weights must be positive integers.
                                                // The weights do not need to sum to 100.
        "+": 30,                                // Generate an addition operation
        "-": 30,                                // Generate a subtraction operation
        "*": 30,                                // Generate a multiplication operation
        "/": 30,                                // Generate a division operation
        "%": 30,                                // Generate a remainder operation
        "^": 30,                                // Generate a power operation
        "()": 30,                               // Generate an expression enclosed in parenthesis
        "id": 100,                              // Generate an ID
        "int": 100                              // Generate an integer literal
        "max-int": 10,                          // Generate largest integer literal: 2147483647
        "min-int": 10                           // Generate smallest integer: (0 - 2147483647 - 1)
    }
}
```

Note that the above is a commented version of the default configuration used for explanatory purposes only. Configuration files do not support comments.