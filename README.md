latex2edx_xserver
=================

latex2edx conversion xserver

22-Jan-13: updated to produce XML consistent with new edX course format; 
22-Jan-13: don't use edXsequential anymore; edXsection compiles into `<sequential>` now, by default.

For examples, run DOTEST

This command:

    python latex2edx.py -prefix "49_" test3.tex

should produce this content for 1.00x/course.xml:

    <?xml version="1.0"?>
    <course number="1.00x" url_name="1.00x Fall 2012">
      <chapter url_name="Unit 1">
        <sequential display_name="Introduction">
          <problem url_name="49_Problem_1"/>
          <problem url_name="49_Problem_2"/>
          <problem url_name="49_Problem_3"/>
          <vertical display_name="A sample vertical - multiple problems in one day">
            <problem url_name="49_Problem_3.5"/>
            <problem url_name="49_Problem_4"/>
          </vertical>
          <problem url_name="49_Problem_4"/>
        </sequential>
      </chapter>
    </course>

For images, make sure the directory path "static/html" exists.

Here is how the process of getting from LaTeX to edXxml proceeds, in block diagram form:

```
             edXpsl.py
             render/*.zpts
                  |
                  |
                  \/
             ______________                      ____________
            |              |                    |            |
  .tex ---->|    plasTeX   |-----> .xhtml ----->|  latex2edx |------> .xml (edX)
            |______________|                    |____________|
                                                  [images,            [images (bitmap)]
                                                   chapters,
                                                   math]
```

PlasTeX uses edXpsl.py and the contents of the render folder to process your LaTeX source into the xhtml format.  The latex2edx.py script then processes the xhtml, operating on the images, chapters, sections, and math to produce the xml course files in the edX format.  It is intended to also convert and place the image files in the right locations to be served up properly by edX.

NOTE: If you are using celieber's fork of the latex2edx.py processor, you need to also download latex2edx.js and include it in your static directory on github --- this enables the javascript new windows for figure and equation reference links.
