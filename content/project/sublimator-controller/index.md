+++
title = "Sublimator Controller"
date = 2014-05-03T21:20:43+02:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["controller","sublimation machine", "study project","group work","raspberry pi", "python"]

# Project summary to display on homepage.
summary = "Program to control sublimation machine using Raspberry Pi."

# Slides (optional).
#   Associate this page with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Optional external URL for project (replaces project detail page).
external_link = ""

# Links (optional).
url_pdf = ""
url_code = "https://github.com/lpfann/sublimator-controller"
url_dataset = ""
url_slides = ""
url_video = ""
url_poster = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++
The overarching goal of this project was the development of a new machine used in biological experiments.
Biologists often utilize mass spectrometry to analyse samples.
To improve the analysis, it is necessary to use a homogeneous sample.
One can use the process of sublimation to turn solid substances into gas.
This gas then finally turns into a perfectly homogeneous solid again, when cooled down.
To automate this process one can built a **sublimaton** machine.

{{< figure src="sublimator_window.png" title="Control Interface" numbered="true">}}

In this project we used a Raspberry Pi microcomputer to control a heating element as well as vacuum pump to create a _Sublimator_.
Our contribution specifically was the implementation of the control software which enabled preprogrammed heating schedules as well as logging features.
The interface can be seen in Figure 1.

This project was a group effort. Also involved in the project were _Jens Schulz_ and _Dominik Gründing_.

### Example heating sequences
 {{< gallery album="sequences">}}