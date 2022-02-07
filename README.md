# SimpleDBSCAN
A head only [DBSCAN](https://en.wikipedia.org/wiki/DBSCAN) implementation which supports N-dimentional data space. (optional kdtree requires one cpp for boosting)

This is a C++ implementation of DBSCAN (Density-based spatial clustering of applications with noise) algorithm.
It has been tested and used in enterprise-level project.
Easy to use, light-weight to include.

![DBSCAN](https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/DBSCAN-density-data.svg/330px-DBSCAN-density-data.svg.png)

All you must write is really simple:
```cpp
#include "dbscan.h"
#include <vector>

struct vec4f {
    float data[4];
    float operator[](int idx) const { return data[idx]; }
};

int main() {

    auto dbscan = DBSCAN<vec4f, float>();

    auto data = std::vector<vec4f>{
        vec4f{ 0.f, 0.f, 1.f, 1.f }
        , vec4f{ 0.f, 0.f, 1.f, 0.9f }
        , vec4f{ 0.f, 0.f, 0.9f, 0.9f }
        , vec4f{ 0.f, 0.f, 0.f, 0.9f }
        , vec4f{ 0.f, 0.f, 0.f, 0.8f }
        , vec4f{ 0.f, 0.f, 0.1f, 0.8f }
    };



    /** 
    * @describe: Run DBSCAN clustering alogrithm
    * @param: V {std::vector<T>} : data
    * @param: dim {unsigned int} : dimension of T (a vector-like struct)
    * @param: eps {Float} : epsilon or in other words, radian
    * @param: min {unsigned int} : minimal number of points in epsilon radian, then the point is cluster core point
    * @param: disfunc {DistanceFunc} :!!!! only used in bruteforce mode.  Distance function recall. Euclidian distance is recommanded, but you can replace it by any metric measurement function
    * @usage: Object.Run() and get the cluster and noise indices from this->Clusters & this->Noise.
    * @pitfall: If you set big eps(search range) and huge density V, then kdtree will be a bottleneck of performance
    * @pitfall: You MUST ensure the data's identicality (TVector* V) during Run(), because DBSCAN just use the reference of data passed in.
    * @TODO: customize kdtree algorithm or rewrite it ,stop further searching when minimal number which indicates cluster core point condition is satisfied
    */
    // int Run(TVector* V, const uint dim, const Float eps, const uint min, const DistanceFunc& disfunc = [](const T& t1, const T& t2)->Float { return 0; });
    dbscan.Run(&data, 4, 0.2f, 2);
    auto noise = dbscan.Noise;
    auto clusters = dbscan.Clusters;

    return 0;

}
```

[1] https://en.wikipedia.org/wiki/DBSCAN

[2] https://scikit-learn.org/stable/auto_examples/cluster/plot_dbscan.html#sphx-glr-auto-examples-cluster-plot-dbscan-py


## License

MIT: https://rem.mit-license.org
