In this folder, the convergence curves for all 24 functions can be found.

The convergence curves illustrate the behavior of the refined mutation strategies during the optimization process across the 24 functions of the BBOB benchmark in the 40-dimensional case. Compared to the baseline mutation, the refined mutations show clear improvements in convergence, reflected in a faster decrease in fitness and lower final values across a larger portion of the benchmark.

These results confirm that the refinement process introduces structural modifications that strengthen the reference operator and enhance its search dynamics. In particular, the mutation refined using GPT-5 mini demonstrates the most competitive performance among the evaluated variants. This strategy achieves the best results in 12 out of the 24 functions, showing a consistent improvement over the baseline operator.

For lower-complexity functions, the refined mutations converge rapidly toward the global optimum, requiring fewer evaluations to reach high-quality solutions. For more challenging landscapes, including ill-conditioned and multimodal functions, the operators maintain a stable improvement trend, avoid premature convergence, and achieve more accurate final fitness values compared to the baseline.

Overall, these results highlight the effectiveness of the performance-based refinement scheme and identify GPT-5 mini as the most effective model for generating improved mutation operators within the Differential Evolution framework.
