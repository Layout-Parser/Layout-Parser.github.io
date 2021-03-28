---
layout: post
date: 2021-03-28 11:59:59
description: |
    A complete instruction for installing the main Layout Parser library and auxiliary components. 
title: Install LayoutParser
category: starter
show_nav: false
featured: true
---

## Install Python
LayoutParser is a Python package that requires Python >= 3.6. If you do not have Python 
installed on your computer, you might want to turn to [the official instruction](https://www.python.org/downloads/)
and download and install the appropriate version of Python. 

## Install layoutparser
Installing the LayoutParser library is very straightforward: you just need to run the following command: 

```bash
pip3 install layoutparser
```
## Install modeling utils
If you would like to use deep learning model detection, you need also install Detectron2 
on your computer. This could be done by running the following command: 

```bash
pip3 install 'git+https://github.com/facebookresearch/detectron2.git#egg=detectron2' 
```

This might take sometime as the command will *compile* the library. You might also install a Detectron2 version with
GPU supports or encounter some issues during the installation process. Please refer to the official Detectron2 
[installation instruction](https://github.com/facebookresearch/detectron2/blob/master/INSTALL.md) for detailed
information. 

## [Optional] Install OCR utils
LayoutParser also comes with supports for OCR functions. In order to use them, you need 
to install the OCR utils via: 

```bash
pip3 install layoutparser[ocr]
```

Additionally, if you want to use the Tesseract-OCR engine, you also need to install it on your computer. Please check the 
[official documentation](https://tesseract-ocr.github.io/tessdoc/Installation.html) for detailed installation instructions. 