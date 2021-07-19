# biospec
## Abstract
In this project, we experimented with deep learning networks (like the Siamese Network) to learn novel dense and compressed fixed-size representations of peptide mass spectra. We then analyze these representations qualitatively and quantitatively to gain insights into what is being learnt. We examine the results and try to provide understanding of how learning a good embedding of the spectrum can help us with various downstream tasks along with a substantial reduction in memory requirements (our embeddings are only 256 dimensional). In this project, we also compare and contrast the results of the embeddings with that of the raw spectral information using measures such as Cosine Similarity.

## Introduction
In this era of big data where we have enormous amounts of data to work with, deep learning provides immense opportunities to exploit the scale and learn effective dense embedding representations of peptide spectra. These dense representations can then be used as a proxy for other learning tasks such as similarity scoring, ranking and clustering of spectrum. It also entails sequence generation tasks, from spectrum to peptide, also called denovo sequencing. The aim of this project is to explore the embedding hyperspace and analyze the properties of the dense representations.

## Dataset
The dataset used for the project is the MSV000083508, 29 tissues proteome map[3]. It consists of 397,513 peptides identified with at least 10 spectra each. We use the ProteoSAFe-MAESTRO-d5f87289-identified spectra dataset file from the maestro server. It consists of 1491919 rows   22 columns. For stage 1 analysis, we had
used 5 mzML files of the Stomach Tissue dataset to train the model. To further increase the data and compare the results on training and testing, we then increased the data to 15 mzML files of the Stomach Tissue.

## Data Processing
In order to conduct our analysis, we first extracted and built a standardized data. It contains values where the x axis comprises an m/z array while the
y axis is an intensity array. Each spectrum in the mzML file has a variable dimension since it only represents the non-zero m/z values. This is problematic
for a neural network representation, where we need a fixed size input. So, we transform the spectrum into a 2051 dimension sparse array. We clipped the spectrum in range [50,2050], since this range explains most of the peaks. To get each index in the sparse array, we perform integer rounding of
the m/z values and store the maximum peak at each integer m/z. Thus, the binning process converts the m/z continuous array into individual coordinates.
Initially in Stage 1, we applied L1 normalization of the intensities. After analysing the results, we resorted to L2 normalization. This is because it constraints the values to a unit circle radius and provides better scale normalisation. This data is stored in the Compressed Sparse Row (CSR) format to save space. We use the scan ID from the spectrum meta information and merge this data with peptide information found from the identified spectra data. This process is repeated for each mzML file.



