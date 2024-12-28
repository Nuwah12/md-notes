* Informally, a decomposition is "lossless" if it preserves the connections between attributes within tuples

$R_1,R_2$ is a lossless join decomposition of R with respect to F iff at least one of the following dependencies is implied by F:
$$R_1\cap R_2\rightarrow(R_1-R_2)$$
or
$$R_1\cap R_2\rightarrow(R_2-R_1)$$
if either of these hold, the decomposition is lossless.