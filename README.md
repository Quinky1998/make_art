# Let's make (super abstract) art!
Turn into Van Gogh with this amazing function!
All you have to do is choose a number to set the seed and ensure reproducibility, e.g.:

```
make_art(seed = 123 )
```

Then this beautiful function will generate a moving polygon with random colors and shapes or a pointillistic masterpiece!
Either way, it will be unique to you. Some even say that the colors are chosen based on the mood you are in...


![preview](https://github.com/Quinky1998/make_art/assets/157707416/d26d2c9c-f2ac-47b7-b174-ae38c6fe83d0)




The following code must be run to get access to this box of endless creations:

```
make_art <- function(seed = NULL) {
  if (!is.null(seed)) {
    set.seed(seed)
  } else {
    stop("Provide a number to set seed.")
  }
   type = sample(c("poly", "scatter"), 1)
  
  
   if (type == "poly") {
    
    x <- runif(4, min = 0, max = 100)
    y <- runif(4, min = 0, max = 100)
   
    color_1 <- rgb(runif(1), runif(1), runif(1))
    color_2 <- rgb(runif(1), runif(1), runif(1))
    
    plot <- ggplot(data = data.frame(x, y), mapping = aes(x, y)) +
      geom_polygon(color = color_1,
                   fill = color_2,
                   size = sample(1:5, 1)) +
      theme_void() +
      transition_reveal(x)
  } else if (type == "scatter") {
    
    plot_list <- list()
    
    for (i in 1:6) {
      points <- sample(10:100, 1)
      
      x <- runif(points)
      y <- runif(points)
      
      color <- rgb(runif(1), runif(1), runif(1))
      
      plot_i <- ggplot(data.frame(x, y), aes(x, y)) +
        geom_point(color = color, size = sample(1:5, 1)) +
        theme_void()
      
      plot_list[[i]] <- plot_i
    }
    plot <- gridExtra::grid.arrange(grobs = plot_list, ncol = 3)
  }
  return(plot)
}
```
