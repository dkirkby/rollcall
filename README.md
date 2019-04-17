# RollCall

Record attendance in a classroom environment.

## Installation

Install this package using:
```
git clone git@github.com:dkirkby/rollcall.git
cd rollcall
```
### Dependencies

 - [numpy](http://www.numpy.org/) to generate random codes.
 - [PyPDF2](https://pythonhosted.org/PyPDF2/) to read, modify and write PDF files.
 - [qrcode](https://pypi.org/project/qrcode/) to generate QR codes.
 - [PIL](https://pillow.readthedocs.io/en/4.2.x/index.html) to decorate QR codes.

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
You will normally want to set the `pattern` option to specify how each unique key is mapped to the QR data. For example:
```
./rollcall template.pdf --num-copies 10 --pattern 'https://me.com/register?id=STUDENTKEY'
```
will replace `STUDENTKEY` with each student's unique key in the QR code.

If you would like reproducible keys, specify the random seed to use with the `--seed` argument. Otherwise, each run will generate different unique keys.

### Google Form Integration

A convenient way to collect rollcall data if you do not have your own server is to use a google form. The basic steps are:
1. Create a new form [here](https://docs.google.com/forms).
2. Select "Get pre-filled link" from the menu and enter `STUDENTKEY` where the student should enter their unique code.
3. Click "GET LINK" then use "COPY LINK" and paste the result into the `--pattern` argument of your command line, surrounded by single quotes, for example (`-n` is a shortcut for `--num-copies`):
```
./rollcall template.pdf -n 10 --pattern 'https://docs.google.com/forms/...&entry.2097963549=STUDENTKEY'
```
Some recommended non-default settings when you create your form:
 - Set field where STUDENTKEY is entered to "Required".
 - Enable "Response validation" for the STUDENTKEY field, using "Regular expression" + "Matches" + [0-9]{8} (assuming the default keylen=8)
 - Disable "Show link to submit another response".
 - Disable the "Restrict to users in..." option, if present (since it requires a sign in ).
 - Disable the "Limit to 1 response" option (since it requires a sign in).
