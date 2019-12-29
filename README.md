**CausalSHAP (Causal SHApley Additive imPacts)** is a game theoretic approach to explain the causal impact of any variable in a machine learning model. It follows directly from the ideas in shap (https://github.com/slundberg/shap) from Lundberg et al.

Modification to SHAP (CausalSHAP™) that could give us member-level impact scores:

Assuming binary feature $i$:

 

Current SHAP (simplified) with current impact methodology
For each member $j$:
For each ordered subset of features $S$  excluding feature $i$, calculate the change in model score $m_{ijS}$ by adding feature $j$ with data value $v_{ij}$ to $S$ 
Take weighted average of $m_{ijS}$ over all $S$ (weighting based on some kernel, in practice this is sampled etc) ==> result is $Shap_{ij}$  (value of feature $i$ to member $j$)
Average $m_{ij}$ over all $j$ to get $m_i$, which is average shap value of feature $i$ over members, 
 

CausalSHAP™
For each member $j$ 
For each ordered subset of features $S$ excluding feature $i$,
calculate the change in model score $m_{ijS_0}$ by adding feature $i$ with data value $0$ to $S$ 
calculate the change in model score $m_{ijS_1}$ by adding feature $i$ with data value $1$ to $S$ 
calculate the impact value $m_{ijS} == m_{ijS_1} - m_{ijS_0}$
Take weighted average of $m_{ijS}$ over all $S$ (weighting based on some kernel, in practice this is sampled etc) ==> result is $CausalShapImpact_{ij}$ (impact of toggling feature $i$ to member $j$)
Impact Score: Average $CausalShapImpact_{ij}$ over all members $j$ to get $CausalShapImpact_i$
 

So basically instead of just finding the average impact of adding feature  as it exists in the data, find the average impact of it being 1 vs it being 0.

