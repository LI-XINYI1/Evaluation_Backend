## EVALUTAION: a module for evaluating RL trading strategy

### Dataset
There are four sets of dataset with same format, representing market data and strategy in four different markets.
- BTCT
- BTCU: market with high winning rate
- ETH: volatile market
- GALA

In each dataset, there are several data files
| Data Name | Description | Source |
|:--------:|:--------:|:--------:|
|test.feather|Market data|Given|
|micro_action.npy| Actions, a representation of holding number | Given |
|df_label.feather| Market data labeled with index corresponding to different dynamics | Generated by Linear_Market_Dynamics_Model() with market data|
|valid/label_x/df_x.feather|Fragment of market data with label x| Generated by Linear_Market_Dynamics_Model() with market data|


### Results
The result of execution is stored under best_result/DATASET_name/data. 
|Result data name| Type| Description| Generated with|
|:----:|:----:|:----------:|:----:|
|metrics_dynamics_market.csv| number | Total return rate, Max drawdown, Calmar Ratio of market data in divided dynamics| analysis_along_dynamics()|
|metrics_dynamics_strategy.csv|number | Total return rate, Max drawdown, Calmar Ratio of strategy in divided dynamics| analysis_along_dynamics()|
|metrics_segment.csv|number | Value of indexes (Total return rate, Max drawdown, Calmar Ratio, etc.) for different segments divided by times|  analysis_along_time_dynamics()|
|phase_dynamic_amount_porportion.pdf|graph | Stacking bar graph shows the porportion of opening and closing amount among differnt dynamics| analysis_along_time_dynamics(), draw_stacking_graph()|
|phase_dynamic_count_porportion.pdf|graph | Stacking bar graph shows the porportion of opening and closing count among differnt dynamics| analysis_along_time_dynamics(), draw_stacking_graph()|
|return_rate_market&strat.pdf|graph |Line graphs of return rates for market and strategy |draw_PnL()|

### Script
The evaluation module can be easily run by scipts defined in script/script.sh </br>
The script will run the evaluaion on four datasets simutaneously. </br></br>
Sample of script: 
```python
CUDA_VISIBLE_DEVICE=2 nohup python comprehensive_evaluation/analyzer1027.py \
  --positions_loc best_result/BTCU/micro_action.npy --data_loc best_result/BTCU/test.feather --path best_result/BTCU/data --max_holding_number1 0.01 --commission_fee 0.00015 \
  >log/analysis_assert_error_BTCU.log 2>&1 &
```
The paremeters are predefined. Here are the descriptions about parameters. Please check and change parameters if needed before execution.
|Parameter name|Description|Type|
|:----:|:----:|:----------:|
|positions_loc|location of file micro_action.npy| string|
|data_loc|location of file test.feather|string|
|path|location to save results|string|
|max_holding_number|max holding number| float, >0|
|commission_fee|commission fee| float, >=0|


Commands to run the script: ```bash script/script.sh```

