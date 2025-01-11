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
predictions <- predict(gam_model, newdata = Boston)
mse <- mean((Boston$medv - predictions)^2)
cat("Mean Squared Error: ", mse, "\n")
par(mfrow = c(1, 1))  # Single plot
plot(predict(gam_model), residuals(gam_model),
xlab = "Fitted Values",
ylab = "Residuals",
main = "Residuals vs Fitted Values")
abline(h = 0, col = "red")
library(lmtest)
shapiro.test(residuals(gam_model))

```

![스크린샷 2025-01-11 05-40-30](https://github.com/user-attachments/assets/fa0ee1b6-3037-4151-ba36-4982e6a00cdc)

```
install.packages("lmtest")
library(lmtest)
bptest(gam_model)
gam_model_log <- gam(log(medv) ~ s(lstat) + s(rm), data = Boston, method = "REML")
plot(predict(gam_model_log), residuals(gam_model_log),
xlab = "Fitted Values (Log Scale)",
ylab = "Residuals",
main = "Residuals vs Fitted Values (Log Transformed)")
abline(h = 0, col = "red")
bptest(gam_model_log)
concurvity(gam_model, full = FALSE)
concurvity(gam_model,full=TRUE)
shapiro.test(residuals(gam_model))
qqnorm(residuals(gam_model))
qqline(residuals(gam_model), col = "red")
plot(gam_model, resid = TRUE, pch = 20,
ylab = "Standardized Residuals",
main = "Scale-Location Plot")
gam_model_weighted <- gam(medv ~ s(lstat) + s(rm),
data = Boston,
weights = 1 / (fitted(gam_model)^2),
method = "REML")
summary(gam_model_weighted)

gam_model_log <- gam(log(medv) ~ s(lstat) + s(rm), data = Boston, method = "REML")
summary(gam_model_log)
AIC(gam_model, gam_model_weighted, gam_model_log)
BIC(gam_model, gam_model_weighted, gam_model_log)

```


![스크린샷 2025-01-11 05-40-34](https://github.com/user-attachments/assets/cb2e7a8f-c860-4701-a892-6e46b6802c58)

```
library(caret)
install.packages("caret")
install.packages(c("e1071", "lattice", "ggplot2"))
cv_control <- trainControl(method = "cv", number = 10)
gam_cv <- train(medv ~ lstat + rm, data = Boston, method = "gam", trControl = cv_control)
gam_cv


```

![스크린샷 2025-01-11 05-40-40](https://github.com/user-attachments/assets/53b9bab6-ebf5-49d0-b0d7-630afbbd65e8)

```
install.packages("performance")
library(performance)
check_model(gam_model)
hist(residuals(gam_model), breaks = 20, col = "skyblue", main = "Histogram of Residuals")


```


![스크린샷 2025-01-11 05-40-50](https://github.com/user-attachments/assets/767710e5-9dfd-42e1-959d-1f015f5176e3)




![스크린샷 2025-01-11 05-40-58](https://github.com/user-attachments/assets/8d869e00-41e2-4de5-974d-7b76a7034829)

check_model(gam_model)


![스크린샷 2025-01-11 05-41-04](https://github.com/user-attachments/assets/fdb34007-8ddf-4a74-8a71-6624395edb3a)


