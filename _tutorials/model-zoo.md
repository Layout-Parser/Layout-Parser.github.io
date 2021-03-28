---
layout: post
description: The full list of layout models currently available in Layout Parser
date: 2021-03-28 11:59:59
title: Layout Model Zoo
category: starter
external_link: https://layout-parser.readthedocs.io/en/latest/notes/modelzoo.html
show_nav: false
featured: true
---


|                                                           Dataset | Base Model | Large Model | Notes                                                      |
|------------------------------------------------------------------:|:----------:|:-----------:|------------------------------------------------------------|
|             [PubLayNet](https://github.com/ibm-aur-nlp/PubLayNet) |    F / M   |      M      | Layouts of modern scientific documents                     |
|                   [PRImA](https://www.primaresearch.org/dataset/) |      M     |      -      | Layouts of scanned modern magazines and scientific reports |
| [Newspaper Navigator](https://news-navigator.labs.loc.gov/search) |      F     |      -      | Layouts of scanned US newspapers from 20th century         |
|            [TableBank](https://github.com/doc-analysis/TableBank) |      F     |      F      | Table region on modern scientific and business document    |
|   [HJDataset](https://dell-research-harvard.github.io/HJDataset/) |  F / M / R |      -      | Layouts of history Japanese documents                      |

▲ *For each dataset, we provide models with different architectures like Faster RCNN (F), Mask RCNN (M), or Retina Net(R).*