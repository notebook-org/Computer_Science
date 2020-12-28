- ==numpy.matrix== is matrix class that has a more convenient interface than ==numpy.ndarray== for matrix operations.
- scipy.linalg operations can be applied equally to numpy.matrix or to 2D numpy.ndarray objects.
#### Link
https://docs.scipy.org/doc/scipy/reference/tutorial/index.html

####Linear Algebra
	from scipy import linalg
	linalg.inv(A) # Inverse of the matrix
	linalg.det(A) # Finding determinant
	linalg.expm(A) # Matrix Exponent