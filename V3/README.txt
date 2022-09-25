En la version 2.0 ,se obtuvo que con K Means hast 20 clusters no se presentaba cluster distinguibles  y robustos.

En V3.0, se corrio Clustering Jeraquico,  y se obtuvo a tra ves de diatancia euclidiana y linkage = ward ; 42 clusters. Se vlvio a correr KMEAN con 42 cluster y el diagrama de silueote , muestra una topologia de cluster mas balanceada.


Intente correr DBSCAN pero los resulatdos son muy contradictorios. Creo que este algoritmo por su esencia no es aplicable en este conesto de negocio. Sin embargo, intente buscar el mejor epsilon usando el criterio de cantidad de outliers y me dio un epsilon 20 y esto me arroja un cluster  y el resto outliers (5%)

Intente usar epsilon =3.5808 que fe el que resulta del kneelocator y esto me arroja todos outliers . Aqui ya vuelvo a intuir que quizas PCA podria funcionar para serlos ma concentricos.