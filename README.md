# pdf2img-lambda-friendly

This is a nodejs module for converting pdf into image files.

This fork was made to change this library to be AWS Lambda friendly.

Original package can be found at https://github.com/fitraditya/node-pdf2img

Currently (07-03-2018) AWS Lambda has a preinstalled ghostscript v8.70 (ancient!). In order to make pdf to img conversion work you need a newer ghostscript version.

## Installation

`npm i pdf2img-lambda-friendly`

Download the compiled version of Ghostscript from [lambda-ghostscript](https://github.com/sina-masnadi/lambda-ghostscript).

Ghostscript executable must be accessible by following this path `lambda-ghostscript/bin/./gs`


## Usage

```javascript
var fs      = require('fs');
var path    = require('path');
var pdf2img = require('pdf2img');

var input   = __dirname + '/test.pdf';

pdf2img.setOptions({
  type: 'png',                                // png or jpg, default jpg
  density: 600,                               // default 600
  outputdir: __dirname + path.sep + 'output', // output folder, default null (if null given, then it will create folder name same as file name)
  outputname: 'test',                         // output file name, dafault null (if null given, then it will create image name same as input name)
});

pdf2img.convert(input, function(err, info) {
  if (err) console.log(err)
  else console.log(info);
});
```

It will return array of splitted and converted image files.

```javascript
{ result: 'success',
  message:
   [ { page: 1,
       name: 'test_1.jpg',
       size: 17.275,
       path: '/output/test_1.jpg' },
     { page: 2,
       name: 'test_2.jpg',
       size: 24.518,
       path: '/output/test_2.jpg' },
     { page: 3,
       name: 'test_3.jpg',
       size: 24.055,
       path: '/output/test_3.jpg' } ] }
```

## License
MIT
