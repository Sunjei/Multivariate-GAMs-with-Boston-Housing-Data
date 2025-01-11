# Multivariate-GAMs-with-Boston-Housing-Data

```

install.packages(mgcv)
install.packages("ggpubr")
install.packages(ggplot2)(ggpubr)
install.packages(egg)
install.packages(moonBook)
install.packages(ztable)
install.packages(ggGAM)
install.packages("MASS")  # Boston DataSet
data("Boston")  
head(Boston)    

require(mgcv)
require(ggplot2)
require(ggpubr)
require(egg)
require(moonBook)
require(ztable)
require(ggGAM)

```

```
gam_model <- gam(medv ~ s(lstat) + s(rm) + s(dis) + s(nox) + s(crim),
data = Boston,
method = "REML")
summary(gam_model)
par(mfrow = c(2, 3))  # Arrange plots in a grid
plot(gam_model, se = TRUE, shade = TRUE)

```



![스크린샷 2025-01-11 05-40-25](https://github.com/user-attachments/assets/5f6b951a-ac65-4877-b11d-9cf1a1945cc0)

```
plot(gam_model$residuals, ylab = "Residuals")
abline(h = 0, col = "red")
```

![스크린샷 2025-01-11 05-40-30](https://github.com/user-attachments/assets/fa0ee1b6-3037-4151-ba36-4982e6a00cdc)


![스크린샷 2025-01-11 05-40-34](https://github.com/user-attachments/assets/cb2e7a8f-c860-4701-a892-6e46b6802c58)


![스크린샷 2025-01-11 05-40-40](https://github.com/user-attachments/assets/53b9bab6-ebf5-49d0-b0d7-630afbbd65e8)




![스크린샷 2025-01-11 05-40-50](https://github.com/user-attachments/assets/767710e5-9dfd-42e1-959d-1f015f5176e3)




![스크린샷 2025-01-11 05-40-58](https://github.com/user-attachments/assets/8d869e00-41e2-4de5-974d-7b76a7034829)



![스크린샷 2025-01-11 05-41-04](https://github.com/user-attachments/assets/fdb34007-8ddf-4a74-8a71-6624395edb3a)


