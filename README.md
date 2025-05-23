# WhatIF Analyzer

A powerful Python package for analyzing functions by automatically generating and running "what-if" scenarios, with a focus on edge cases and robustness testing.

## Features

- 🔍 **Static Analysis**: Automatically infers parameter types and generates edge cases
- 🎯 **Edge Case Testing**: Tests with None, empty values, extreme numbers, and more
- 🧪 **Lightweight Fuzzing**: Optional fuzzing for additional test cases
- 📊 **Detailed Reports**: Human-readable summaries of test results
- 🛠️ **Multiple Interfaces**: Use as a decorator, CLI tool, or Python API
- 📝 **Comprehensive Documentation**: Clear examples and usage instructions

## Installation

```bash
pip install whatif-analyzer
```

## Quick Start

### Using the Decorator

```python
from whatif_analyzer import analyze

@analyze
def divide(a: float, b: float) -> float:
    return a / b

# The function will be automatically analyzed when called
result = divide(10, 2)
```

### Using the CLI

```bash
# Analyze a Python file
whatif analyze path/to/your/file.py

# Analyze a specific function
whatif analyze path/to/your/file.py:function_name
```

### Using the API

```python
from whatif_analyzer import WhatIfAnalyzer

def my_function(x: int, y: str) -> bool:
    return len(y) > x

analyzer = WhatIfAnalyzer()
report = analyzer.analyze_function(my_function)
print(report)
```

## Example Report

```python
from whatif_analyzer import analyze

@analyze
def process_data(data: list, threshold: int) -> float:
    if not data:
        return 0.0
    return sum(x for x in data if x > threshold) / len(data)

# The analysis will run automatically
result = process_data([1, 2, 3, 4, 5], 2)
```

Sample report output:
```
WhatIF Analysis Report
=====================

Function: process_data
Parameters:
  - data: list
  - threshold: int

Edge Cases Tested:
✓ Empty list
✓ None values
✓ Negative threshold
✓ Large threshold
✓ Mixed data types

Exceptions Found:
- TypeError: When data contains non-numeric values
- ZeroDivisionError: When data is empty and threshold is 0

Recommendations:
1. Add type checking for list elements
2. Handle empty list case explicitly
3. Consider adding input validation for threshold
```

## Advanced Usage

### Custom Edge Cases

```python
from whatif_analyzer import WhatIfAnalyzer, EdgeCase

analyzer = WhatIfAnalyzer()

# Define custom edge cases
custom_cases = [
    EdgeCase("special_value", lambda x: x == 42),
    EdgeCase("negative_list", lambda x: all(i < 0 for i in x))
]

# Analyze with custom cases
report = analyzer.analyze_function(
    my_function,
    edge_cases=custom_cases
)
```

### Configuration Options

```python
from whatif_analyzer import WhatIfAnalyzer

analyzer = WhatIfAnalyzer(
    enable_fuzzing=True,
    max_fuzz_cases=100,
    timeout_seconds=5,
    verbose=True
)
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Citation

If you use WhatIF Analyzer in your research, please cite:

```bibtex
@software{whatif_analyzer,
  author = {Your Name},
  title = {WhatIF Analyzer},
  year = {2024},
  url = {https://github.com/yourusername/whatif-analyzer}
}
``` 