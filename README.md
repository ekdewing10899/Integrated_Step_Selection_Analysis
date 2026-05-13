#An Integrated Step Selection (ISSA) on GPS collared mountain lions in California's North Bay Area. 
#This code find how these mountain lions select/avoid burn severity, years since a burn occured, and vegetation in their habitats.

#ISSA is a spatial analysis method that is used to study the habitat preferences and movement patterns of tracked animals (Hoffman et. al, 2024). 
#To conduct the ISSA analysis, the amt (animal movement tools)  library was used, and I downloaded the outline of a basic ISSA code 
#from the Ecological Forecasting Initiative and the ESA Statistical Ecology Section’s code in GitHub. 
#I then edited the code to fit my parameters.

#Using the mountain lion GPS collar points from All-Hands Ecology and True Wild, I created “tracks” and “steps” 
#with functions within the amt package, which is essential for processing the movement of the lions. Using these steps, 
#I calculated the step length and turn angle of each group of consecutive three “steps” taken by the lions. 
#To understand the possible steps the lions could have taken instead of the steps they did take, 
#I created 20 random possible steps per actual step. An observed (real) step taken by the mountain lion, 
#paired with the associated random (theoretical) steps, form what is called a “strata”, which is used in the model below. 
#Using the composited rasters with the vegetation and burn severity of most recent burn combined with years since burn data, 
#I extracted the raster data (covariates) from the rasters and imported them into the random possible steps. 
#This would help to identify what burn severities, years since burn, and vegetation types the lions are and aren’t selecting for. 
#I filtered out any mountain lions that did not use every type of vegetation and burn severity categories, to avoid difficulties with the model. 
#This resulted in a total of 12 mountain lions. After preparing this data, I utilized the “fit_issf()” model from the amt package, 
#which is a wrapper for the “clogit()” function in the survival package. This model  is used to estimate a logistic regression model 
#by maximizing the conditional likelihood. Logistic regression will estimate the selection coefficients for the vegetation and  
#years since burn with burn severity. The formula for the model is as follows:
#m1 <- fit_issf(model_df, case_ ~ vegetation + age_burnsev + sl_ + log_sl_ + cos_ta_ + strata(step_id_),  model = TRUE)
