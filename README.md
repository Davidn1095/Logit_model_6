# Logit_model_6

This script involves reading data, fitting logistic regression models (including a stepwise approach), creating a contingency table, converting variables into factors, and fitting a weighted logistic regression model on the contingency table data.

### Reading Data from a Text File:

- `Coronarios <- read.table("Coronarios.txt", header = T, sep = "")`: This command reads data from a text file named "Coronarios.txt" into a DataFrame called Coronarios. The `header = T` indicates that the first row of the file contains column headers. The `sep = ""` suggests that the data might be space-separated or have another non-standard separator.

### Fitting Logistic Regression Models:

- `Ajuste.Coronarios0 <- glm(cbind(EC1, EC0) ~ 1, family = binomial, data = Coronarios)`: Fits a logistic regression model to the Coronarios data with only an intercept (no predictors). The response variable is a two-column matrix `cbind(EC1, EC0)`, which is typical for binomial outcomes.
- `Ajuste.Coronarios.All <- glm(cbind(EC1, EC0) ~ Ciga + Compor + Psang, family = binomial, data = Coronarios)`: Fits a logistic regression model with the predictors `Ciga`, `Compor`, and `Psang`.

### Stepwise Model Selection:

- `Ajuste.Coronarios.Step <- step(Ajuste.Coronarios0, scope = list(lower = cbind(EC1, EC0) ~ 1, upper = cbind(EC1, EC0) ~ Ciga + Compor + Psang), direction = "both")`: Performs stepwise model selection starting from the null model `Ajuste.Coronarios0`. The function iteratively adds or removes predictors to find an optimal model.

### Creating a New Data Frame:

- The next block of code creates vectors `Ec`, `Ciga`, `Tipo`, `Presion`, and `Freq`, and then combines them into a new DataFrame called `Coronarios.Tabla`.
- The `as.factor()` function is used to convert `Ciga`, `Tipo`, `Presion`, and `Ec` columns into factor variables, which is appropriate for categorical data in logistic regression.

### Checking Factor Levels:

- `levels(Coronarios.Tabla$Ciga)`, `levels(Coronarios.Tabla$Tipo)`, `levels(Coronarios.Tabla$Presion)`, `levels(Coronarios.Tabla$Ec)`: These commands display the levels of the factor variables in the `Coronarios.Tabla` DataFrame.

### Fitting Logistic Regression Model to the New Data Frame:

- `Ajuste.Coronarios.Tabla <- glm(Ec ~ Ciga + Tipo + Presion, weights = Freq, data = Coronarios.Tabla, family = binomial)`: Fits a logistic regression model to the `Coronarios.Tabla` data with `Ec` as the response variable and `Ciga`, `Tipo`, and `Presion` as predictors. The `weights = Freq` argument uses the `Freq` column as weights for the logistic regression, which is common in analyses of contingency tables.

### Displaying the Fitted Model:

- `Ajuste.Coronarios.Tabla`: This command simply displays the fitted logistic regression model `Ajuste.Coronarios.Tabla`.






