#JSONItem_MTC

This is a drop-in replacements for the native JSONItem. It emulates all its features but should perform certain functions faster.

To use it, search for "JSONItem" within your project and replace it with "JSONItem_MTC". Then drag the JSONItem_MTC class into your project.

##Differences

This class implements all the features and functions of its native twin and should be indistinguishable except for the following:

- You can add any object to JSONItem and it will raise an exception when you try to use ToString. This class will raise that exception when you try to add the bad object.

- This class has an extra enum property, EncodeUnicode. By default, it is EncodeType.JavascriptCompatible to emulate the native class. If set to EncodeType.All, it will encode all characters whose codepoints are greater than or equal to 127. In all cases (EncodeType.All, .JavascriptCompatible, .None), code points 0 - 31 will be encoded.

- Some error messages will be different within this class than the native class.

- The native class will raise an exception when loading a string that has an escaped character other than one of the "approved" characters. This class will accept any escaped character as long as Strict = False (see below).

- This class is more tolerant when loading values that aren't valid according to the specs. For example, the value `TRUE` is considered invalid according to the RFC as is the value `+1`, but both will be accepted by this class. As such, it should not be used as a validator unless Strict = True (see below). JSON string generation will meet always meet specs except as noted below.

- This class will accept `inf` and `nan` as doubles, and will output the same. This is the only case where the output will not strictly meet JSON guidelines when using ToString, unless Strict = True (see below).

- This class has a Strict property. When set to `True`, it will strictly interpret JSON string according to JSON specs (values like `TRUE` and `+1` will be rejected), and will raise an exception rather than outputting `inf` or `nan`.

- This class will properly handle characters with code points > &uFFFF when both encoding and decoding. The native class does not.

- This class will properly reject invalid hex in a "\uNNNN" structure. 

- The native class will load some badly formed JSON strings, e.g., "[true]]". This class will not.

- When loading a JSON string, this class will figure out its encoding and even strip any BOM that might prefix it.

- As of Xojo 2016r1, ToString and Load are significantly faster in this class than the native version.

##License

This class was created by Kem Tekinay, MacTechnologies Consulting (ktekinay@mactechnologies dot com). It is copyright ©2016 by Kem Tekinay, all rights reserved.

This project is distributed AS-IS and no warranty of fitness for any particular purpose is expressed or implied. The author disavows any responsibility for bad design, poor execution, or any other faults.

You may freely use or modify this project or any part within. You may distribute a modified version as long as this notice or any other legal notice is left undisturbed and all modifications are clearly documented and accredited. The author does not actively support this class, although comments and recommendations are welcome.

##Comments and Contributions

All contributions to this project will be gratefully considered. Fork this repo to your own, then submit your changes via a Pull Request.

All comments are also welcome.

##Who Did This?!?

This project was created by and is maintained by Kem Tekinay (ktekinay@mactechnologies dot com).
