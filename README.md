# Cognitive Cascades -- Media Ecosystem Model

## Author: Nick Rabb 

#### Contact: nicholas.rabb@tufts.edu

<hr/>

## Project Overview

TO BE FILLED IN

## Experiment & Results Replication

### Using Netlogo Behaviorspace

TO BE FILLED IN

### Using data from Rabb & Cowen paper

#### Analysis of partition sizes (Table 3)

Our first major result, displayed in Table 3, was the distribution of polarized and nonpolarized results further partitioned by epsilon, gamma, h_G, and phi.

To prepare your Python environment for doing this analysis, you must first import the `data.py` file:

```py
from data import *
```

First, our result data must be downloaded, unzipped, and placed in a directory. Then, to get the data into a usable dataframe that aggregates results over simulation trials, run the following code:

```py
multidata = get_conditions_to_polarize_multidata(<YOUR_PATH>)
polarization_data = polarization_analysis(multidata)
```

`polarization_data` will then be dictionary containing severl `pandas` dataframes which you can use to see which results were classified as polarized and nonpolarized. These dataframes can be queried to measure partition sizes. For an example of this, see the function `polarizing_results_analysis()`. An example of code that would give the proportions of polarized data in Table 3 for the *epsilon* parameter is the following:

```py
polarized_df = polarization_data['polarizing']
epsilon_values = [0,1,2]
for epsilon in epsilon_values:
  partition = df.query(f'epsilon=="{epsilon}"')
  print(f'Portion for epsilon={epsilon}: {len(partition)/len(polarized_df)}')
```

One can imagine how a similar method could be used to, for example, retrieve the parition proportions for broadcast tactic, *phi*. 

#### Analysis of more fine-grained partition sizes (Table 4)

Our second result, that different media tactics polarize or do not based on the initial institution and citizen distributions, can be gathered using similar methods to the above section. If you follow the same steps to get `polarization_data`, you could arrive at the polarized portion of the table in the following manner:

```py
polarized_df = polarization_data['polarizing']
tactics = ['appeal-mean', 'appeal-median', 'broadcast']
distributions = ['uniform','normal','polarized']

for tactic in tactics:
  for i_dist in distributions:
    for c_dist in distributions:
      partition = polarized_df.query(f'tactic=={tactic} and media_dist=={i_dist} and citizen_dist=={c_dist}')
      print(f'Partition size for ({tactic},{i_dist},{c_dist}): {len(partition)}')
```

#### Generating visual charts

To generate charts based off of the experiment results, you should use the `process_polarizing_conditions_cognitive()` function, giving it the path of the downloaded data. This function has several variables within it that specify which parameter values to process. For example, if you wanted to generate diagrams for the cases where *gamma* (beta function translation factor) was 0, 1, and 2, you would set `cognitive_translate = [0,1,2]`.

**Note: The parameter values that you give the analysis function must have a corresponding directory where that data is stored from the NetLogo simulation. In other words, you must have gathered results for those parameter values. The parameter values that are contained in our results set are listed in Tables 1 and 2 in the paper.**