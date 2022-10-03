# NMTSloth

*NMTSloth* is designed to generate test samples to test efficiency degradation of neural machine translation (NMT) systems.  Specifically, *NMTSloth* perturbs the seed sentences with three types of perturbations, and the perturbed inputs will consume more computational resources.



## Design Overview
<div  align="center">    
 <img src="https://github.com/SeekingDream/NMTSloth/blob/main/fig/overview.png" width="800" height="300" alt="Design Overview"/><br/>
</div>    

*NMTSloth* is based on two observation: (i) NMT systems' generation process are Markov processes, the number of decoder calls are undetermined (ii) existing NMT systems usually set a large threshold to avoid incomplete translation.
With the above two observation, *NMTSloth* applies the gradient guided search to generate human unnoticeable perturbations.
The design overview of *NMTSloth* is shown in the above figure. 
At high level, *NMTSloth* includes three main steps: (i) find critical tokens, (ii) input muation, and (iii) efficiency degradation detection. For the detail desgin of each steps, we refer the readers to our paper.


## File Structure
* **src** -main source codes.
  * **./src/base_attack.py** - the wrapper calss for each testing methods.
  * **./src/TranslateAPI.py** - the basical translation api files.
  * **./src/TransRepair.py** -the method of TransRepair
  * **./src/baseline_attack.py** -the implementation of Seq2Sick and NoisyError.
  * **./src/my_attack.py** -the implementation of NMTSloth.
* **spider.py** -the script is used to study the NMT systemss' configurations in HuggingFace.
* **generate_adv.py** -the script is used for generating test samples.
* **measure_latency.py** -this script measures the latency/energy consumption of the generated adversarial examples.
* **measure_loops.py**   -this script measures the iteration numbers of the generated adversarial examples.
* **measure_senstive.py** -this script measures the hyperparameter senstivelity.
* **gpuXX.sh** -bash script to run experiments (**XX** are integer numbers).

## Setup

We recommend to use ``conda`` to manage the python libraries and the requirement libraries are listed in ``requirements.txt``. So run ``pip install -r requirements.txt``.

## How to run

We provide the bash script that generate adversarial examples and measure the efficiency in **gpu0.sh**. **gpu1.sh**, **gpu2.sh**,**gpu3.sh**, **gpu4.sh**. **gpu5.sh**, **gpu6.sh**, are implementing the similar functionality but for different gpus. 

So just run `bash gpu0.sh`.
 
 
## Generated Test Samples.

Seed Input:  **Death comes often to the soldiers and marines who are fighting in anbar province, which is roughly the size of louisiana and is the most intractable region in iraq.**

Test Input: **Death comes often to the soldiers and marines who are fighting in anbar province, which is roughly the (size of of louisiana and is the most intractable region in iraq.** 


## Relationship Between Output Length and Latency/Energy
<div  align="center">    
 <img src="https://github.com/SeekingDream/NMTSloth/blob/main/fig/study.png" width="1300" height="400" alt="cdf"/><br/>
</div>    

The above figure shows the relationship between output length and latency/energy of randomly selected seed inputs. From the results, we observe that there is a linear relationship between output length and latency/energy.


