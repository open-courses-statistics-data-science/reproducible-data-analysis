# Nested logic and complex conditionals {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="|3-14"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines > 0) {
            if (indiv["age"] > threshold_age || indiv["isAtRisk"]) {
                if (indiv["hasFirstJab"]) {
                    inject_second_jab(indiv)
                    nvaccines <- nvaccines - 1
                } else {
                    inject_first_jab(indiv)
                }
            }
        } else {
            return("No more doses")
        }
    }
}
```

# If you can, return early {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="3,12-14"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines > 0) {
            if (indiv["age"] > threshold_age || indiv["isAtRisk"]) {
                if (indiv["hasFirstJab"]) {
                    inject_second_jab(indiv)
                    nvaccines <- nvaccines - 1
                } else {
                    inject_first_jab(indiv)
                }
            }
        } else {
            return("No more doses")
        }
    }
}
```

# If you can, return early {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="3|5-11"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
 
        if (indiv["age"] > threshold_age || indiv["isAtRisk"]) {
            if (indiv["hasFirstJab"]) {
                inject_second_jab(indiv)
                nvaccines <- nvaccines - 1
            } else {pp
                inject_first_jab(indiv)
            }
        }
}
```

# If you can, skip early {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="5"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
 
        if (indiv["age"] > threshold_age || indiv["isAtRisk"]) {
            if (indiv["hasFirstJab"]) {
                inject_second_jab(indiv)
                nvaccines <- nvaccines - 1
            } else {pp
                inject_first_jab(indiv)
            }
        }
}
```

# If you can, skip early {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="5|7-12"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
 
        if (indiv["age"] > threshold_age || indiv["isAtRisk"]) next
        
        if (indiv["hasFirstJab"]) {
            inject_second_jab(indiv)
            nvaccines <- nvaccines - 1
        } else {
            inject_first_jab(indiv)
        }
}

```
# Extract condition in function {data-auto-animate=""}

```{.R .numberLines data-id="nested-logic" data-line-numbers="5"}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
 
        if (indiv["age"] > threshold_age || indiv["isAtRisk"]) next
        
        if (indiv["hasFirstJab"]) {
            inject_second_jab(indiv)
            nvaccines <- nvaccines - 1
        } else {
            inject_first_jab(indiv)
        }
}
```

# Extract condition in function {data-auto-animate=""}

```{.R .numberLines data-line-numbers="1-4,10"}
eligible_to_vaccine <- function(individual, threshold_age) {
    in_target_age_group = indiv["age"] > threshold_age
    return(in_target_age_group || individual["isAtRisk"])
}

apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
        
        if (!eligible_to_vaccine(individual, threshold_age)) next
        
        if (indiv["hasFirstJab"]) {
            inject_second_jab(individual)
            nvaccines <- nvaccines - 1
        } else {
            inject_first_jab(individual)
        }
    }
```

# 

before
```{.R .numberLines data-id="nested-logic" data-line-numbers=""}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines > 0) {
            if (indiv["age"] > threshold_age || indiv["isAtRisk"]) {
                if (indiv["hasFirstJab"]) {
                    inject_second_jab(indiv)
                    nvaccines <- nvaccines - 1
                } else {
                    inject_first_jab(indiv)
                }
            }
        } else {
            return("No more doses")
        }
    }
}
```
after
```{.R .numberLines}
apply_vaccine_to_population <- function(population, nvaccines, threshold_age) {
    for (individual in population) {
        if (nvaccines == 0) { return("No more doses") }
        
        if (!eligible_to_vaccine(individual, threshold_age)) next
        
        if (indiv["hasFirstJab"]) {
            inject_second_jab(individual)
            nvaccines <- nvaccines - 1
        } else {
            inject_first_jab(individual)
        }
    }
}
```

# Recap on complex if/else constructs

- Return/continue early if you can.
- Extract complex conditions into a new function.
