# FAQ for General Troubleshooting

*Based on debugging done during the labs*

## Installation Issues

> *Q: When trying to pip install the `transformers` or `tokenizers` library, I get an error in building the `bdist_wheel` of `tokenizers`*

A: Try to install the Rust compiler using the command `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`, reopen a different shell session and try the installation again. If it doesn't work, you can try to [install from source](https://huggingface.co/docs/tokenizers/python/latest/installation/main.html).

## Runtime errors

> *Q: When I try to load a `pipeline` or a `transformer`, the loading stops and I get an error `AttributeError: 'FloatProgress' object has no attribute 'style'`.

A: Try to update your pip and ipywidgets versions: `pip install --upgrade pip ipywidgets`