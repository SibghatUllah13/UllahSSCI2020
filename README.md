[![DOI](https://zenodo.org/badge/404799810.svg)](https://zenodo.org/badge/latestdoi/404799810)



# Comparison of Dimensionality Reduction Techniques for High Dimensional Surrogate-Assisted Optimization
Contains the code for empirically comparing the porformance of four of the widely-utilized dimensionality reduction techniques, namely Autoencoders (AEs), Variational Autoencoders (VAEs), Principal Component Analysis (PCA), and (nonlinear) Kernel Principal Component Analysis (KPCA).
These techniques are compared with each other based on the performance of the low dimensional surrogate models, which
are originated by performing dimensionality reduction on the original Design of Experiment (DoE).

# Introduction
This code is based on our paper, titled [Exploring Dimensionality Reduction Techniques for Efficient Surrogate-Assisted Optimization](https://ieeexplore.ieee.org/abstract/document/9308465) (Ullah, Nguyen, Wang, Menzel, Sendhoff & Bäck, 2020), and can be used to reproduce
the experimental setup and results mentioned in the paper. The code is produced in Python 3.5.0. The main packages utilized in this code are presented in the next section which deals with technical requirements. 

The code is present in five directories, namely  `AES`, `Data Generation`, `KPCA`, `PCA` and `VAES` respectively.
As the nomenclature suggests, `Data Generation` contains the code for initial sampling plans and Design of Experiment (DoE), whereas
all the other directories carry the implementation of low dimensional surrogate models based on the particular choice of technique for performing dimensionality reduction.
Within the directory `Data Generation`, we have three further sub-directories, titled `50 D`, `100 D`, and `200 D` respectively.
Each of these sub-directories generates the data set for all test scenarios based on the choice of dimensionality (of the search space).

The structure of the other remaining directories, namely  `AES`, `KPCA`, `PCA` and `VAES` is the same.
Each of which has a further of two sub-directories, namely `Kriging`, and `Polynomials`.
These two sub-directories depict the choice of the modeling technique, and are similar in their structure as they contain three more
sub-directories, titled `100D`, `200D`, and `50D` respectively.
These three sub-directories define the choice of dimensionality (of the search space), and go one level deeper.
Inside these directories, we come across three more sub-directores, namely `0.1D`, `0.4D`, and `0.7D` respectively which define the size
of the low-dimensional surrogate model.
Having described the choice of dimensionality reduction technique, modeling technique, dimensionality (of the search space), and
the size of the low dimensional surrogate model, we finally come across three notebook files, which are named `Accuracy.ipynb`, `Hyper-Parameters.ipynb`, and `Optimality.ipynb` respectively.
The purpose of `Hyper-Parameters.ipynb` is to perform hyper parameter optimization for getting the best quality surrogate model, whereas .
`Accuracy.ipynb` and `Optimality.ipynb` assess the performance of the low dimensional surrogate model based on the criteria of modeling accuracy and the quality of
the optimal solution. 
In the following, we describe the technical requirements as well the instructions to run the code in a sequential manner.


# Requiremnts
In this code, we make use of four python packages (among others), which are presented below in the table.
In particular, `pyDOE` can be utilized for sampling plans and Design of Experiment (DoE).
We employ the so-called `Latin Hypercube Sampling` based on the `pyDOE` package.  
For the purpose of numerical optimization in the code, e.g., to maximize the acquisition function, we utilize the famous `L-BFGS` algorithm based on `SciPy` package.
For implementation AEs and VAEs, we utilize the `PyTorch` framework.
Finally, the main purpose of the `scikit-learn` package is to construct the Kriging surrogate, as well as data manipulation/wrangling in general 
All four required packages can be installed by executing `pip install -r requirements.txt` from the main directory via the command line.

| Package | Description |
| --- | --- |
| pyDOE | For sampling plans and Design of Experiment (DoE).  |
| SciPy | For numerical optimization based on L-BFGS-B algorithm. |
| PyTorch (cpu) | For implementing AEs and VAEs. |
| scikit-learn | For constructing the Kriging surrogate, as well as data manipulation. |

In the following, we describe how to reproduce the experimental setup and results mentioned in our paper.

## 1. Generating the initial Data Set
The first task in the experimental setup deals with the generation of initial data set. This refers to specifying the coordinates
of the sampling points to observe the functions responses. Since this task is dimensionality dependent (dimensionality describes the number of
sampling points), we first have to specify the sub-directory which specifies the dimensionality within the `Data Generation` directory.  
After specifying the correct sub-directory, we have to run the jupyter notebook, titled `Generate_Data_Sets.ipynb` which will generate the training and testing 
data sets. The testing data set will be later utilized to evaluate the modeling accuracy of the surrogate models. This notebook will also ensure that there 
are no replicates in the training and testing data sets.

## 2. Specifying the Test Scenario
After generating the initial data set, we are expected to choose the test scenario based on the combination of dimensionality reduction technique,
modeling technique, the dimensionality of the search space, and the size of the low dimensional surrogate model (represented in terms of the original dimensionality).
For this, we must traverse to the correct combination/order by specifying the (sub-)directories along the way.

## 3. Running the Experiments
Once we have traversed to the correct combination of sub-directories, we can utilize the files which are named `Hyper-Parameters.ipynb`, `Accuracy.ipynb`,  and `Optimality.ipynb` to perform hyper parameter optimization and assess the low dimensional surrogate models based on modeling accuracy and optimality
of the final solution.
Each of these files contains the necessary methods and routines to perform these tasks.
Note that to run these files, we may have to specify some paths to retrieve the training and testing data sets which were saved in the first step.
We may also have to specify the paths for the models, if they are saved on the hard disk.

# Citation
## Paper Reference
S. Ullah, D. A. Nguyen, H. Wang, S. Menzel, B. Sendhoff and T. Bäck, "Exploring Dimensionality Reduction Techniques for
Efficient Surrogate-Assisted optimization," 2020 IEEE Symposium Series on Computational Intelligence (SSCI), 2020, pp. 2965-2974.
## BibTex Reference
`@inproceedings{ullah2020exploring,`\
  `title={Exploring dimensionality reduction techniques for efficient surrogate-assisted optimization},`\
  `author={Ullah, Sibghat and Nguyen, Duc Anh and Wang, Hao and Menzel, Stefan and Sendhoff, Bernhard and B{\"a}ck, Thomas},`\
  `booktitle={2020 IEEE Symposium Series on Computational Intelligence (SSCI)},`\
  `pages={2965--2974},`\
  `year={2020},`\
  `organization={IEEE}`\
`}`

# Acknowledgements
This research has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement number 766186 (ECOLE).
