# Let's make (super abstract) art!
Turn into Van Gogh with this amazing function!
All you have to do is choose a number to set the seed and ensure reproducibility, e.g.:

```
make_art(seed = 123 )
```

Then this beautiful function will generate a moving polygon with random colors and shapes or a colorful collection of tiles!
Either way, it will be unique to you. Some even say that the colors are chosen based on the mood you are in...


![preview](https://github.com/Quinky1998/make_art/assets/157707416/d26d2c9c-f2ac-47b7-b174-ae38c6fe83d0)




The following code must be run to get access to this box of endless creations:

```
make_art <- function(seed) {
  if (!is.numeric(seed)) {
    stop("Provide a number to set the seed.")
  } else {
    set.seed(seed)  
    }
  
  type = sample(c("poly", "tiles"), 1)
  
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
  } else if (type == "tiles") {
    num_tiles <- 1000
    
    tiles <- data.frame(
      x = runif(num_tiles, min = -10, max = 10),    
      y = runif(num_tiles, min = -10, max = 10),    
      color = sample(colors(), num_tiles, replace = TRUE)  
    )
    
    plot <- ggplot(tiles, aes(x = x, y = y, fill = color)) +
      geom_tile(width = 0.5, height = 0.5) +  
      theme_void() +  
      scale_fill_identity() +  
      theme(legend.position = "none") +
      transition_reveal(x)
  }
  return(plot)
}
```
