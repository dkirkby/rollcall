# RollCall

Record attendance in a classroom environment.

## Installation

Install this package using:
```
git clone git@github.com:dkirkby/rollcall.git
cd rollcall
```

Build a suitable conda environment using:
```
conda env create -f environment.yml
```

## Usage

Activate the conda environment using:
```
conda activate rollcall
```

Build the rollcall handouts using, for example:
```
./rollcall template.pdf --num-copies 10
```
The output will be `template_rollcall.pdf` with 10 copies of `template.pdf`, each having a unique QR code on their last page. A list of the unique keys will also be written to `template_keys.txt`.

To see the full list of options, use:
```
./rollcall --help
```

## Dependencies

 - [numpy](http://www.numpy.org/) to generate random codes.
 - [PyPDF2](https://pythonhosted.org/PyPDF2/) to read, modify and write PDF files.
 - [qrcode](https://pypi.org/project/qrcode/) to generate QR codes.
 - [PIL](https://pillow.readthedocs.io/en/4.2.x/index.html) to decorate QR codes.
