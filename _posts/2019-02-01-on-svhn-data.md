---
layout: post
title:  "Characteristics of Street View House Numbers Data"
date:   2019-02-01
---

Different general types of images:

* Blurry numbers on solid color/textured backgrounds (number taking up most of image) or in a shape in the image
* Small blurry numbers on architectural backgrounds (on framing, in windows, on garage doors) where number is really tiny in the image
* Numbers with decoration around them (like placards with the house number)
* Numbers partially hiding behind plants

Script to get heights/widths of all images:

```python
import glob
from PIL import Image

for filepath in glob.iglob('train/*.png'):
	im=Image.open(filepath)
	print(im.size[0]) # 0 is width, 1 is height
```

and then run:

```bash
python3 stats.py > stats.txt
```

Isolations:
* Geometric shapes
* Architectural patterns (brick, stone, etc)
* Different types of number forms (handwriting, different fonts, etc)
* Placards and other types of signs the numbers are on

Modifications (global):
* 3D transform
* Motion blur
* Brightness/contrast

Modifications (local):
* Shadows