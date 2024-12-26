Palmer Penguins
================
Ishika Saha
2024-12-26

# R Markdown

This is an R Markdown document enlighting you about some of the basic
features of ggplot, which is an essential data visualization tool.
Markdown is a simple formatting syntax for authoring HTML, PDF, and MS
Word documents.

\##Setting up my environment

First we need to install the packages and here we are working with
Palmer penguins dataset:

``` r
#install.packages("ggplot2")
#install.packages("palmerpenguins")
```

Next we load the packages to our workspace:

``` r
library(ggplot2)
library(palmerpenguins)
```

In order to upload the dataframe and view it:

``` r
data(penguins)
View(penguins)
```

If we want to find a relationship between flipper length and body mass
of the penguins we run the following code:

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g))
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-2-1.png)<!-- --> The
**ggplot()** function creates a coordinate system that you can add
layers to. The first argument of the ggplot() function is the dataset to
use in the plot. In this case, it’s “penguins.”Then, you add a **+**
symbol to add a new layer to your plot. The **geom_point()** function
uses points to create **scatterplots**.Each geom function in ggplot2
takes a mapping argument. This defines how variables in your dataset are
mapped to visual properties. The mapping argument is always paired with
the aes() function. The x and y arguments of the aes() function specify
which variables to map to the x-axis and the y-axis of the coordinate
system. In this case, you want to map the variable
**“flipper_length_mm”** to the **x-axis**, and the variable
**“body_mass_g”** to the **y-axis**.

\##AESTHETICS

Now we are adding different *Aesthetic Features* like colour, shape,
size, alpha and many more:

``` r
ggplot(data=penguins) + geom_point(mapping = aes(x=bill_length_mm, y=bill_depth_mm, color = species))   #diff color is added for every different specie
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g, shape = species, color = species, size = species))   #diff shape is added to evry different specie
```

    ## Warning: Using size for a discrete variable is not advised.

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g, alpha = species)) #color density varies from one specie to another by alpha aes
```

    ## Warning: Using alpha for a discrete variable is not advised.

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

To add a colour or aesthetic to overall plot irrespective of any
particular variable we write that outside the parethesis of aes()

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g), colour = "red")
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

To create a trend line so that we can easily identify any trend if its
not normally visible we use geom_smooth()

``` r
ggplot(data = penguins) + geom_smooth(mapping = aes(x=flipper_length_mm,y=body_mass_g)) +
  geom_point(mapping = aes(x = flipper_length_mm,y=body_mass_g))
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-7-1.png)<!-- --> . A
*line type* aesthetic is added here to assign different line types to
every specie.

``` r
ggplot(data = penguins) + 
  geom_smooth(mapping = aes(x = flipper_length_mm,y=body_mass_g,linetype=species))
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

To view every data point clearly we use geom_jitter() which is just an
advanced scatterplot.

``` r
ggplot(data = penguins) + 
  geom_jitter(mapping = aes(x = flipper_length_mm,y=body_mass_g))
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

\##FACETS

The **facet_wrap** is a function separating and distributing the
independent data within the plot.

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,colour = species))+
  facet_wrap(~species)
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->
Here the independent data is species which is always written in the
right of tilde(~) operator.

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,colour = species))+
  facet_grid(sex~species)
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->
**facet_grid** can take 2 var as input with a (~) in between them. This
creates a grid like plot where sex is represented horizontally and
species vertically, just like a matrix. But it can also take one input
var then it will work the same as wrap.

\##ANNOTATIONS

It’s used to add labels(labs) that include title, subtitle, caption, and
also any additional information inside the plot. To add text inside the
plot we use annotate(), which further has the type of information we
want to include, the x coordinate(distance from the x-axis),y
coordinate, and the label i.e, the text, color, style, size, angle, etc.

``` r
ggplot(data = penguins) + geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, colour = species))+
  labs(title = "Palmer Penguins: Body Mass vs Flipper Length", subtitle = "Sample of three penguin species", caption = "Data collected by Dr. Kristen Gorman")+
  annotate("text", x=220,y=3500,label="The Gentoos are the largest",color="red",fontface="bold",size=3.5,angle=15)
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

\###Alternate way

``` r
p <- ggplot(data = penguins) + geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, colour = species))+
  labs(title = "Palmer Penguins: Body Mass vs Flipper Length", subtitle = "Sample of three penguin species", caption = "Data collected by Dr. Kristen Gorman")
p + annotate("text", x=220,y=3500,label="The Gentoos are the largest",color="red",fontface="bold",size=3.5,angle=15)
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](ggplot_markdown_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Now we can save the plot in form of .jpg or .png file:

``` r
ggsave('PalmerPennguin plot.jpg')
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).
