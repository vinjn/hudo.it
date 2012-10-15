High-resolution information about how the normal vector is perturbed is stored in a two-dimensional array of three-dimensional vectors called a bump map or normal map.

Each vector in the bump map represents the direction in which the normal vector should point relative to the interpolated normal vector at a point inside the face of a triangle.

The vector <0,0,1> represents an unperturbed normal, whereas any other vector represents a modification to the normal that affects the result of the lighting formula.

The unperturbednormal vector <0,0,1> corresponds to the RGB color (1/2, 1/2, 1)

Normal map gives normal vector( bumpedNormalT ) in tangent space, since light direction( lightDirW ) is in world space, we need to transform normalT to world space ( bumpedNormalW ).

float3x3 TBN is the tansform matrix, the three components are
    - float3 N = normalize(input.NormalW);
    - float3 B = normalize(input.NormalW - dot(input.TangentW, N)*N);;
    - float3 T = cross(N, T);
    
Then
    float3 bumpedNormalW = mul(normalT, TBN);

Which is what we want to replace input.NormalW with.
