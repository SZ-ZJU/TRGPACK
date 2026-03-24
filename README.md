# Trend--and-Reference-Guided-Hybrid-Modeling-of-Temperature-Dependent-Thermophysical-Properties
Models：
Heat capacity GC model：
█(C_p=∑_k▒〖N_k (A_K+B_K T)  〗#（1） )
N_k  represent the number of each groups, A_Kand B_K  is the parameters needed to be tuned.
Heat capacity GC_SⅠ model：
█(C_p=∑_k▒〖N_k (A_K+B_K T)+δ*(y_r2-y_r1)/(T_2-T_1 )*T 〗#（2） )
N_k  represent the number of each groups, A_Kand B_K  is the parameters needed to be tuned. T_1 and T_2 are the half-critical temperature and three-quarters of the critical temperature, respectively, and y_r1 and y_r2 are the corresponding heat capacity values at these temperatures. The critical temperature is predicted using a Gaussian process regression model with group contribution features as inputs. The heat capacity values at the two specific temperature points are predicted using Huber regression, also with group contribution features as inputs. δ is the coefficient to be regressed.
Heat of vaporization GC model：
█(H_i^vp=-R⁡((1.5*B_i^')/T^0.5 +〖C 〗_i^'*T+D_i^'*T^2 )#（2） )
█(B_i^'=∑_k▒〖N_K*(B_1K+M_i B_2K )+β(f_0+N_C *f_1 ) 〗#(3) )
█(C_i^'=∑_k▒〖N_K*(C_1K+M_i C_2K )+γ(f_0+N_C *f_1 ) 〗#（4） )
█(D_i^'=∑_k▒〖N_K*(D_1K+M_i D_2K )+δ(f_0+N_C *f_1 ) 〗#（5） )
R is the gas constant (8.3144 J/g mol K for H_i^vp in  J / gmol).Where N_k  is the number of groups k in the molecule; M_i  is the component molecular weight; B_1k,C_1k,D_1k,B_2k,C_2k,D_2kare group-contribution coefficients; f_0and f_1, β,γ" and"  δ are parameters obtained by regression of experimental data; k denotes the groups of component i; N_cis the total number of carbon atoms in the molecule. This specific implementation enhances the parameter prediction by integrating not only the counts of molecular groups but also supplemental molecular characteristics such as the total carbon count and molecular weight. These additional descriptors are incorporated alongside group contributions within the regression framework, with each feature assigned its own independently fitted coefficient.
Heat of vaporization GC_SⅠ model：
█(H_i^vp=-R⁡((1.5*B_i^')/T^0.5 +〖C 〗_i^'*T+D_i^'*T^2 )+δ_0*(y_r2-y_r1)/(T_2-T_1 )*T#（2） )
█(B_i^'=∑_k▒〖N_K*(B_1K+M_i B_2K )+β(f_0+N_C *f_1 ) 〗#(3) )
█(C_i^'=∑_k▒〖N_K*(C_1K+M_i C_2K )+γ(f_0+N_C *f_1 ) 〗#（4） )
█(D_i^'=∑_k▒〖N_K*(D_1K+M_i D_2K )+δ(f_0+N_C *f_1 ) 〗#（5） )
R is the gas constant (8.3144 J/g mol K for H_i^vp in  J / gmol).Where N_k  is the number of groups k in the molecule; M_i  is the component molecular weight; B_1k,C_1k,D_1k,B_2k,C_2k,D_2kare group-contribution coefficients; f_0and f_1, β,γ" and"  δ are parameters obtained by regression of experimental data; k denotes the groups of component i; N_cis the total number of carbon atoms in the molecule. This specific implementation enhances the parameter prediction by integrating not only the counts of molecular groups but also supplemental molecular characteristics such as the total carbon count and molecular weight. These additional descriptors are incorporated alongside group contributions within the regression framework, with each feature assigned its own independently fitted coefficient. T_1 and T_2 are the normal temperature and the boiling point, respectively, and y_r1 and y_r2 are the corresponding heat of vaporization at these temperatures. The boiling point is predicted using a Huber regression model with group contribution features as inputs. The heat of vaporization at the two specific temperature points are predicted using a random forest model, also with group contribution features as inputs. δ_0 is the coefficient to be regressed.
Vapor pressure GC model：
█(l n⁡〖P_i^vp 〗=A_i^'+(B_i^')/T+C_i^'∙lnT#(6) )
█(A_i^'=∑_k▒〖N_K∙(A_1K+M_i A_2K )+α(f_0+N_C ∙f_1 ) 〗+(s_0+N_cs∙s_1 )#(7) )
█(B_i^'=∑_k▒〖N_K∙(B_1K+M_i B_2K )+β(f_0+N_C ∙f_1 ) 〗#(8) )
█(C_i^'=∑_k▒〖N_K∙(C_1K+M_i C_2K ) 〗#（9） )
where N_K is the number of groups k in the molecule, M_i is the component molecular weight, N_cs is the number of carbons of the alcoholic part of methyl, ethyl, propyl and butyl esters (N_cs equals 1, 2, 3 and 4, respectively), N_C  is the total number of carbon atoms in the molecule. A_1k,B_1k,C_1k,D_1k,B_2k,C_2k,α,β,s_0,s_1, f_0 andf_1 are the parameters obtained by regression.
Vapor pressure GC_SⅠ model：
█(l n⁡〖P_i^vp 〗=A_i^'+(B_i^')/T+C_i^'∙lnT+δ_0*(y_r2-y_r1)/(T_2-T_1 )*T#(6) )
█(A_i^'=∑_k▒〖N_K∙(A_1K+M_i A_2K )+α(f_0+N_C ∙f_1 ) 〗+(s_0+N_cs∙s_1 )#(7) )
█(B_i^'=∑_k▒〖N_K∙(B_1K+M_i B_2K )+β(f_0+N_C ∙f_1 ) 〗#(8) )
█(C_i^'=∑_k▒〖N_K∙(C_1K+M_i C_2K ) 〗#（9） )
where N_K is the number of groups k in the molecule, M_i is the component molecular weight, N_cs is the number of carbons of the alcoholic part of methyl, ethyl, propyl and butyl esters (N_cs equals 1, 2, 3 and 4, respectively), N_C  is the total number of carbon atoms in the molecule. A_1k,B_1k,C_1k,D_1k,B_2k,C_2k,α,β,s_0,s_1, f_0 andf_1 are the parameters obtained by regression. T_1 and T_2 are the boiling point and the half-critical temperature, respectively, and y_r1 and y_r2 are the corresponding vapor pressures at these temperatures. The boiling point is predicted using a Huber regression model with group contribution features as inputs. The half-critical temperature is predicted using a gradient boosting decision tree model, also with group contribution features as inputs. The vapor pressure at the boiling point is taken as a fixed value (1 atm), while the vapor pressure at the half-critical temperature is predicted using an explicit expression with group contribution features and molecular weight as inputs. δ_0 is the coefficient to be regressed.
For all properties, the GBDT model uses functional group features and temperature as input features, with the regression model being a gradient boosting regression model.
For all properties, the GBDT_SⅡ model first constructs a linear model prior using group information and a reference point. The slope of the linear model is derived from group contributions, with T_1 and y_r1 representing a specific temperature point and its corresponding property value:
y ̂=y_r1+∑_K▒〖A_K N_K (T-T_1 ) 〗
Based on the predictions from this prior model, functional group features, temperature, and trend information are then used as input features for a gradient boosting regression model to predict the deviation between the baseline model and the experimental data, which is subsequently compensated.
For all features, the QSPR model uses two-dimensional structures downloaded from PubChem. After data cleaning, the top 25 most relevant descriptors are selected as input features, with the regression model being a random forest model.
For all features, the QSPR_SⅠ model, in addition to using the two-dimensional structures from PubChem and the top 25 most relevant descriptors after data cleaning, also incorporates the trend information (y_r2-y_r1)/(T_2-T_1 ) as an additional input feature. Details can be found in the open-source code.
