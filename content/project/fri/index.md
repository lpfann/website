+++
title = "Feature Relevance Analysis Tool"
date = 2019-05-02T14:03:32+02:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["feature-selection","relevance-determination","interactive","python","ordinal-regression","regression","classification"]

# Project summary to display on homepage.
summary = "Python tool to discover relevant features in machine learning problems."

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
url_pdf = "https://arxiv.org/pdf/1903.00719"
url_code = "https://github.com/lpfann/fri"
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
Feature selection is the task of finding relevant features used in a machine learning model. Often used for this task are models which produce a sparse subset of all input features by permitting the use of additional features (e.g. Lasso with L1 regularization). But these models are often tuned to filter out redundancies in the input set and produce only an unstable solution especially in the presence of higher dimensional data.

*FRI* calculates relevance bound values for all input features. These bounds give rise to intervals which we named ‘feature relevance intervals’ (FRI). A given interval symbolizes the allowed contribution each feature has, when it is allowed to be maximized and minimized independently from the others. This allows us to approximate the global solution instead of relying on the local solutions of the alternatives.

