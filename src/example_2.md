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
