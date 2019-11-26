## Regression - extra explanations





### Description vs prediction {#explanation-residuals}

(This section is related to [this class activity](#how-useful-are-the-lines)).

You **_should_** have found that the total length of the residuals for the
curved lines is _smaller_ than the residuals for the straight line. If this
isn't the case, check your measurements.

This is because a curved line will be better **description** of the data you had
when fitting it, but will be a poorer **predictor** of new data.

This is why fitting straight lines is such a common technique. We know that the
line doesn't describe the data we have perfectly, but we hope it will be a
better predictor of future events than anything else.

[If you like, there is more detail on this here](#explanation-worse-is-better)

### Worse is better {#explanation-worse-is-better}

You should have found that:

-   Curved lines have smaller residuals _for the original data_
-   Straight lines have smaller residuals _when you swap samples_

The reason for this is that there is a **_tradeoff_**:

-   If we draw a curved line, to get close to the original data points, then our
    lines reflect peculiarities in the sample. That is, our lines are drawn to
    accomodate **_random variation_** in this specific sample.

-   Because these random variations aren't repeated in new samples, the lines
    fit **_less well_** when we swap datasets.

In fact, because the straight line (mostly) ignores this sample variation it
_can be_ a better estimate of the real relationship in the population as a
whole^[It's not _always_ true, but it's a good rule of thumb.].

So worse is sometimes better: Because they were simpler, straight lines were a
worse fit for our original dataset. But they were a _better_ predictor in new
random samples.

This is an example of **_overfitting_**. By overfitting, we mean that a model
(in this case the line) is too closely matched to a particular sample, and so
might not be a good predictor of the population as a whole.

Overfitting is the reason we prefer simpler models (lines) to more complicated
ones.




### The shaded area when using `geom_smooth` {#explanation-shaded-area-geom-smooth}

If you use `geom_smoth` with `method=lm` you get a grey shaded area around the
line.


```r
mtcars %>%
  ggplot(aes(wt, mpg)) +
    geom_point() +
    geom_smooth(method=lm)
```

<img src="extras-regression_files/figure-html/unnamed-chunk-2-1.png" width="672" />

The shaded area shows the **_standard error_** of the line of best fit. This is
an estimate of how confident we are about the predictions the line makes. This
video explains it quite well: <https://www.youtube.com/watch?v=1oHe1a3JqHw>.
When he uses the greek letter \beta he just means "slope".

If you want to hide it, you can add: `se=FALSE`:


```r
mtcars %>%
  ggplot(aes(wt, mpg)) +
    geom_point() +
    geom_smooth(method=lm, se=FALSE)
```

<img src="extras-regression_files/figure-html/unnamed-chunk-3-1.png" width="672" />



### Checking your first predictions {#explanation-first-predictions}



You should get something like:
40.1, 54.0 and 72.4

Don't worry about rounding errors... within 1 point is fine.

We should be most confident about the prediction for 20 hours, because we have
more data in the sample which is close to that value. Our line was estimated
from data which didn't have many people who worked 5 or 40 hours, so we don't really
know about those extremes.



### Why don't we always use real data? {#explain-not-real-data}

Real data is often quite complicated, and it is sometimes easier to simulate
data which illustrates a particular teaching point as clearly as possible. It
also lets us create multiple examples quickly.

It _is_ important to use real data though, and this course includes a mix of
both simulated and real data.



### What is a formula? {#explain-formulae}

In R, **formulas** describe the relationship between variables.  They are used widely, e.g. in ggplot, functions like `t.test`, and especially in model-fitting functions like `lm`.

Formulas for regression will always describe the link between one *outcome* and one or more *predictor* variables.

The outcome goes on the left, and predictors go on the right. They are separated by the tilde symbol: the `~`.  When you read `~` you can say in your head *"is predicted by"*.

You can add multiple variables by separating them with a `+` symbol. So `outcome ~ age + gender` is a model where the outcome is predicted by age and gender. This doesn't add interaction terms.

If you want to include interaction terms (e.g. to let slopes vary for different groups) then you use a `*` symbol instead of a plus. So `outcome ~ age * gender` means the outcome is predicted by age, gender, and the interaction of age and gender.


There is a more technical explanation of all of the formula syntax here: <https://stat.ethz.ch/R-manual/R-devel/library/stats/html/formula.html>