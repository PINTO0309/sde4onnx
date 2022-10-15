# sde4onnx
**S**imple **D**oc_string **E**raser for **O**NNX.

https://github.com/PINTO0309/simple-onnx-processing-tools

[![Downloads](https://static.pepy.tech/personalized-badge/sge4onnx?period=total&units=none&left_color=grey&right_color=brightgreen&left_text=Downloads)](https://pepy.tech/project/sge4onnx) ![GitHub](https://img.shields.io/github/license/PINTO0309/sge4onnx?color=2BAF2B) [![PyPI](https://img.shields.io/pypi/v/sge4onnx?color=2BAF2B)](https://pypi.org/project/sge4onnx/) [![CodeQL](https://github.com/PINTO0309/sge4onnx/workflows/CodeQL/badge.svg)](https://github.com/PINTO0309/sge4onnx/actions?query=workflow%3ACodeQL)

# Key concept

- [x] doc_string eraser for ONNX. e.g. Hagging Face Stable Diffusion ONNX.

## 1. Setup
### 1-1. HostPC
```bash
### option
$ echo export PATH="~/.local/bin:$PATH" >> ~/.bashrc \
&& source ~/.bashrc

### run
$ pip install -U onnx \
&& python3 -m pip install -U onnx_graphsurgeon --index-url https://pypi.ngc.nvidia.com \
&& pip install -U sge4onnx
```
### 1-2. Docker
https://github.com/PINTO0309/simple-onnx-processing-tools#docker

## 2. CLI Usage
```
$ sge4onnx -h

usage:
  sge4onnx [-h]
  -if INPUT_ONNX_FILE_PATH
  [-of OUTPUT_ONNX_FILE_PATH]
  [-n]

optional arguments:
  -h, --help
      show this help message and exit.

  -if INPUT_ONNX_FILE_PATH, --input_onnx_file_path INPUT_ONNX_FILE_PATH
      Input onnx file path.

  -of OUTPUT_ONNX_FILE_PATH, --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
      Output onnx file path.

  -n, --non_verbose
      Do not show all information logs. Only error logs are displayed.
```

## 3. In-script Usage
```python
>>> from sge4onnx import erase
>>> help(erase)

Help on function erase in module sge4onnx.onnx_opname_generator:

erase(
    input_onnx_file_path: Union[str, NoneType] = '',
    onnx_graph: Union[onnx.onnx_ml_pb2.ModelProto, NoneType] = None,
    output_onnx_file_path: Union[str, NoneType] = '',
    non_verbose: Union[bool, NoneType] = False
) -> onnx.onnx_ml_pb2.ModelProto

    Parameters
    ----------
    input_onnx_file_path: Optional[str]
        Input onnx file path.
        Either input_onnx_file_path or onnx_graph must be specified.
        Default: ''

    onnx_graph: Optional[onnx.ModelProto]
        onnx.ModelProto.
        Either input_onnx_file_path or onnx_graph must be specified.
        onnx_graph If specified, ignore input_onnx_file_path and process onnx_graph.

    output_onnx_file_path: Optional[str]
        Output onnx file path. If not specified, no ONNX file is output.
        Default: ''

    non_verbose: Optional[bool]
        Do not show all information logs. Only error logs are displayed.
        Default: False

    Returns
    -------
    renamed_graph: onnx.ModelProto
        Renamed onnx ModelProto.
```

## 4. CLI Execution
```bash
$ sge4onnx \
--input_onnx_file_path vae_encoder.onnx \
--output_onnx_file_path vae_encoder_erased.onnx
```

## 5. In-script Execution
```python
from sge4onnx import erase

onnx_graph = erase(
  input_onnx_file_path="vae_encoder.onnx",
  output_onnx_file_path="vae_encoder_erased.onnx",
)
```

## 6. Sample
https://huggingface.co/bes-dev/stable-diffusion-v1-4-onnx/resolve/main/vae_encoder.onnx
### Before
![image](https://user-images.githubusercontent.com/33194443/195969983-904da5ec-7fbb-48dc-b74d-3a9891192598.png)

### After
![image](https://user-images.githubusercontent.com/33194443/195969996-be2aa669-3625-4e8f-8fa1-3beee30c4df3.png)

## 7. Reference
1. https://github.com/onnx/onnx/blob/main/docs/Operators.md
2. https://docs.nvidia.com/deeplearning/tensorrt/onnx-graphsurgeon/docs/index.html
3. https://github.com/NVIDIA/TensorRT/tree/main/tools/onnx-graphsurgeon
4. https://github.com/PINTO0309/simple-onnx-processing-tools
5. https://github.com/PINTO0309/PINTO_model_zoo

## 8. Issues
https://github.com/PINTO0309/simple-onnx-processing-tools/issues
