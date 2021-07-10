Automatically Parse any Document
================================

Train Detectron2 based Custom Models for Document Layout Parsing
----------------------------------------------------------------

[![Nasheed Yasin](https://miro.medium.com/fit/c/56/56/0*IYbXMKhDeXCa3mPn)](https://medium.com/@nasheed.ny?source=post_page-----5d72e81b0be9--------------------------------)[

Nasheed Yasin

](https://medium.com/@nasheed.ny?source=post_page-----5d72e81b0be9--------------------------------)[

Jul 1·5 min read

](https://medium.com/auto-parse-and-understand-any-document-5d72e81b0be9?source=post_page-----5d72e81b0be9--------------------------------)

![A depiction of various layouts one encounters in everyday and sometimes not so everyday life, with the code to parse such layouts using the layoutparser library, superimposed on top of it.](https://miro.medium.com/max/2000/1*dc63KJapDFxivyeoksWEDg.png)Image by [Layout Parser](https://layout-parser.github.io/) on [GitHub](https://github.com/Layout-Parser/layout-parser/blob/master/.github/example.png)

Documents have been ubiquitous ever since humans first developed the written script. Magazines, agreements, historical archives, pamphlets at the local store, tax forms, property deeds, college application forms and so on. Processing these documents has been a rather manual task thus far, with automation only beginning to take over in the last few decades. This automation journey has largely been impeded by a crucial pitfall- Computers can’t understand layouts as intuitively as humans.

With the advent of modern Computer Vision all this changed. We now have [models](https://github.com/Layout-Parser/layout-parser/blob/master/docs/notes/modelzoo.md) that can accurately locate, represent and understand components of a document’s layout. But these models are rather abstract to the average automation enthusiast, usually requiring comprehensive knowledge in Python to even contemplate an attempt at understanding the documentation let alone use it in a project.

![The Layout Parser logo.](https://miro.medium.com/max/544/1*TJrHkouC2GvocDgVPhokdQ.png)Credits: [Layout Parser](https://layout-parser.github.io/)

To that extent, [Layout Parser](https://pypi.org/project/layoutparser/), as explained in their really cool [paper](https://arxiv.org/pdf/2103.15348.pdf), alleviates this complexity with a clean API that allows and enables complete end to end layout detection, parsing and understanding in just a few (and I mean really few, like 5) lines of code. They have a bunch of [models](https://github.com/Layout-Parser/layout-parser/blob/master/docs/notes/modelzoo.md) that can be used straight out of the box. All in all a super cool tool.

**Now, how can one use this tool to understand and work on custom layouts beyond the capabilities of the pre-trained models?**
==============================================================================================================================

<img alt="Images of two scientific papers with their layout components marked." class="et fh fd ms v" src="https://miro.medium.com/max/1000/1\*1vMzOHtusP88Wzz0L5F2tw.png" width="500" height="311" srcSet="https://miro.medium.com/max/552/1\*1vMzOHtusP88Wzz0L5F2tw.png 276w, https://miro.medium.com/max/1000/1\*1vMzOHtusP88Wzz0L5F2tw.png 500w" sizes="500px"/>

Image by author

> The obvious thought would be to fine tune an existing layout model on your custom layouts.

And you are right, it is the best way to go, especially given that not all of us have access to the hardware firepower required to train such models from scratch.

While the finetuning process is a tad more technically involved than just using a pre-trained model, a handy [repository](https://github.com/Layout-Parser/layout-model-training) created by the authors of [Layout Parser](https://pypi.org/project/layoutparser/), helps alleviate some of these issues by largely handling the untenable bits of the training/ finetuning activity.

<img alt="A rather unique arrange of gears shaped pretty similar to that of a human brain, signifying intelligent design." class="et fh fd ms v" src="https://miro.medium.com/max/982/1\*c5cS72gecmtJSNUD3QfoFA.gif" width="491" height="270" srcSet="https://miro.medium.com/max/552/1\*c5cS72gecmtJSNUD3QfoFA.gif 276w, https://miro.medium.com/max/982/1\*c5cS72gecmtJSNUD3QfoFA.gif 491w" sizes="491px"/>

GIF by [Gareth Fowler](http://www.garethfowler.com/) on [Tumblr](https://gifsofprocesses.tumblr.com/post/160274145124/nautilus-gears)

**In the following sections we go through a comprehensive tutorial on using** [**this repository**](https://github.com/Layout-Parser/layout-model-training) **to train your own custom models.**

Prerequisites
=============

![A checklist animation, where the boxes are being checked sequenctially](https://miro.medium.com/max/1000/1*86SnJ0zzd3QNQHMLE4gqcg.gif)Image by [Navanshu Agarwal](https://www.linkedin.com/in/navanshu-agarwal/)

1.  Python ≥ 3.6
2.  [Detectron2](https://github.com/facebookresearch/detectron2) forked or cloned from the [master branch](https://github.com/facebookresearch/detectron2).\*
3.  Latest version of [Layout Parser](https://pypi.org/project/layoutparser/) and it’s dependencies.
4.  Pytorch (Linux: 1.6+ or Windows: 1.6)\*\*
5.  CUDA toolkit: 10+ (As compatible with Pytorch)\*\*\*
6.  Dataset: Annotated in [COCO](https://cocodataset.org/#home) format.

Caveats
-------

\*[Detectron2](https://github.com/facebookresearch/detectron2) is not easily installed on Windows systems, please refer to this [fantastic post](https://ivanpp.cc/detectron2-walkthrough-windows/#step3installdetectron2) by _ivanapp_ for guidance on the Windows based installation process.

\*\*Though 1.8 is recommended in the [official docs](https://detectron2.readthedocs.io/tutorials/install.html), Windows users should stick to 1.6.

\*\*\*CUDA is not mandatory and one could theoretically train on CPU as well. Although, such a training attempt would be painfully slow.

Step 1: Basic Setup
===================

*   Clone or fork the [layout-model-training](https://github.com/Layout-Parser/layout-model-training) repository to your system.
*   Open up a command/anaconda prompt and activate the environment, where [Layout Parser](https://pypi.org/project/layoutparser/) and [Detectron2](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjx2tnXp7zxAhXVvp4KHQYJAbgQFjAJegQIBRAD&url=https%3A%2F%2Fai.facebook.com%2Fblog%2F-detectron2-a-pytorch-based-modular-object-detection-library-%2F&usg=AOvVaw1LG6fe39i41xY1II3rd3GJ) is installed.
*   Change the working directory to the location where the [layout-model-training](https://github.com/Layout-Parser/layout-model-training) repo was saved.

Step 2: Splitting the Dataset (Optional)
========================================

*   Packaged in the [layout-model-training](https://github.com/Layout-Parser/layout-model-training) repo is an inbuilt script (`utils\cocosplit.py`) to perform dataset splitting into test and train subsets.
*   The script ensures that in the event of images without tagged regions being present in the dataset, the ratio of tagged to untagged images in the train and test subsets will be equal.
*   Use the below command to split your dataset (Assuming the working directory is as instructed in the previous step).

_Note that the above command is on a Windows 10 based system, alter the path separators according to the Operating System._

Argument Explanation
--------------------

*   _annotation\_path_: The path to where the consolidated dataset lies.
*   _train_ and _test_: The path to where the train/ test dataset should be saved.
*   _split-ratio_: The fraction of the consolidated dataset to be allocated for training.

Step 3: Download the Pretrained Model
=====================================

*   Download a pre-trained model and its related config file from Layout Parser’s [**model zoo**](https://github.com/Layout-Parser/layout-parser/blob/master/docs/notes/modelzoo.md).
*   The download consists of two files:

1.  _model\_final.pth_: This is the pre-trained model’s weights.
2.  _config.yaml_: This is the pre-trained model’s configuration. For information about the configuration file, refer the [_Detectron2 Docs_](https://detectron2.readthedocs.io/en/latest/modules/config.html#config-references)_._

Step 4: Training the Model
==========================

Now that the dataset is split and the pretrained model weights are downloaded, let’s get to the juicy part: **_model training_** (or rather finetuning).

*   The training is done using the training script at `tools\train_net.py`
*   Use the command below to train the model.

_Note that the above command is on a Windows 10 based system, alter the path separators according to the Operating System._

Argument Explanation
--------------------

*   _dataset\_name_: The name of the custom dataset (One can name it as one pleases).
*   _json\_annotation\_train_: The path to the training annotations.
*   _json\_annotation\_val_: The path to the testing annotations.
*   _image\_path\_train_: The path to the training images.
*   _image\_path\_val_: The path to the testing images.
*   _config-file_: The path to the model configuration file downloaded in Step 3.

_Note that the rest of the argument-value pairs are actually config modifications and are specific to the use case (sometimes). For clarity on how to use and set them, refer the_ [_Detectron2 Docs_](https://detectron2.readthedocs.io/en/latest/modules/config.html#config-references)_._

*   The finetuned model along with its config file, training metrics and logs will be saved in the output path as indicated by the `OUTPUT_DIR` in the command above.

Step 5: Inference
=================

With the finetuned model, it is a straightforward task to use it to parse documents.

*   Replace the model initialization with the below code in [Layout Parser](https://pypi.org/project/layoutparser/)’s demo.

_Note that the above paths are based on a Windows 10 based system, alter the path separators according to the Operating System._

*   `custom_label_map` is the `int_label -> text_label` mapping. This mapping is made in accordance to the `'categories'` field present in the training data’s [COCO Json](https://cocodataset.org/#home) in the following way: `{'id': 'name'}` for each `category`. For instance:

`custom_label_map = {0: "layout_class_1", 1: "layout_class_2"}`

Conclusion
==========

All in all, custom models on any dataset can easily be trained using the [layout-model-training](https://github.com/Layout-Parser/layout-model-training) repo. Such models can be used to parse and understand a wide variety of documents with relative ease post training.

References
==========

\[1\] Y. Wu, A. Kirillov, F. Massa, W. Y. Lo and R. Girshick, [Detectron2](https://ai.facebook.com/blog/-detectron2-a-pytorch-based-modular-object-detection-library-/): Facebook AI Research’s next generation library that provides state-of-the-art detection and segmentation algorithms (2019), [GitHub Repo](https://github.com/facebookresearch/detectron2)

\[2\] Z. Shen, R. Zhang, M. Dell, B. C. G. Lee, J. Carlson and W. Li, [LayoutParser: A Unified Toolkit for Deep Learning Based Document Image Analysis](https://arxiv.org/pdf/2103.15348.pdf) (2021), arXiv preprint arXiv:2103.15348

\[3\] T. S. Lin, M. Maire, S. Belongie, L. Bourdev, R. Girshick, J. Hays, P. Perona, D. Ramanan, C. L. Zitnick and P. Dollár, [Microsoft COCO: Common Objects in Context](https://arxiv.org/abs/1405.0312) (2015), arXiv preprint arXiv:1405.0312v3
