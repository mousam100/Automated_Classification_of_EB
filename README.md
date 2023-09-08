# Automated_Classification_of_EB
This is an automated technique to classify the Eclipsing Binaries into three primary classes which are Contact, Detached, and Semi-Detached. 

Introduction: We have created a single code that runs through the main directory(where the files are saved) and calculates chi_square values and normalized light curves using a sliding median function.

1. The sliding median technique and light curve generation technique are similar to Cruz et al. [2022]

2. We started by importing the necessary libraries. 

3. After reading the necessary file in the specified path we defined a sliding median function. Sliding Median function is inspired by [Cruz et al. 2022]. Which we have used to normalize the flux and later on to generate chi_square values and plots.

4. After that we used some basic data cleaning procedures like numeric value converter, dropping the null values, also we are using a standard deviation limit = STDV/5.

5. After that we have replaced the fluxes below stdv/5 by the median of their surrounding points.

6. Then we generated a window size that has 4 quarters and normalized the flux using the sliding median technique.
            
7. After that again we cleaned the normalized flux data generated from the sliding median technique.

8. Then, we defined a box/bin size and based on that we structured the chi_square_values using numpy function zero_like.

9. The chi-square formula is used which is a typical mathematical chi_square formula, which compares the median light curves and original light curves.

10. Then we saved the chi_square values in respective text files.

11. Now we are done with the chi_square values and moving towards light_curves generation. Chi_square values are saved in text files for future easy usage.

12. First we will read files in main directory which ends with '_res.txt'.

13. After following the steps from Cruz et al. [2022] we calculated tvar , phase , phase_000 and phase_025 variables.

14. Then we plot the light curves and chi_square vs Box plots in different plots.

# With this our Light Curve generation , chi_square vs Box plots and saving chi_square values in a text file is done. 

Now in the second part of the code we will use model fitting techniques to classify different chi_square plots.

15. We have used a damping function and polynomial function to classsify the binary classes.

16. he damping function we have used here is the most common damping function. Source : Wekipidia or any other Acoustics Physics book.

17. def damping(x, A, w, phi, decay):
    return A * np.exp(-decay*x) * np.sin(w * x + phi)    where , x = input values. A= Amplitude , decay = decay factor. w = frequency and phi= phase.

18. The second function is a polynomial function is a four degree polynomial and we know that four degree polynomial can explain more curved plots than three degree polynomials.

19. We have also used a baseline substratcion method to align the graph where We will be substracting the mean from the baseline to align everything around centre.

20. Initial parametric estimations. amplitude is accurate as I have used numpy max function. Rest are wild assumptions.

21. Generate predictions of fitting(function) using the optimized parameters.

22. we have also generated the fitting score / r2 score using python's sklearn.metrics . 

23. Based on the fitting values we have classified the binary systems in three categories, which are shown below. 

24. 
         Class "CONTACT":
	 R-squared > 0.8 for damping sinusoidal.
	 R-squared <= 0.2 for polynomial.
	 R-squared_damping_s > R-squared_polynomial.
	 
         Class "DETACHED":
	 R-squared > 0.8 for polynomial.
	 R-squared > 0.5 for damping sinusoidal.
 	 R-squared_p > R-squared_damping_s.
	
         Class "SEMI-DETACHED":
	 R-squared < 0.7 for damping sinusoidal.
         R-squared < 0.5 for polynomial.

25. Lastly the fitting plots are shown below.   



NOTE: I HAVE UPLOADED THREE FILES. ONE CONTAINS DETACHED BINARY DATA, ONE CONTAIN CONTACT AND ONE IS SEMI-DETACHED BINARY . YOU CAN CHECK THE FITTING RESULTS USING THOSE DATA. KEEP THE FOLDERS IN A SPECIFIC LOCATION AND RUN THE CODE. IT WILL AUTOMATICALLY GENERATE THE DESIRED OUTPUTS. 



XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXENDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
