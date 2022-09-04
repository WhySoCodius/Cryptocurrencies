# Cryptocurrencies

## Overview

The goal of this project is to use unsupervised machine learning to examine cryptocurrency data. Pandas is used for preprocessing the original [CryptoCompare](https://min-api.cryptocompare.com/data/all/coinlist) cryptocurrency data in order to fit Unsupervised Machine Learning models. Data is grouped using a clustering method, and the results are shared using hvPlot visualisation.

## Resources
### Data Source

The crypto_data.csv was retrieved from [CryptoCompare](https://min-api.cryptocompare.com/data/all/coinlist).

### Softwares

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-%233F4F75.svg?style=for-the-badge&logo=plotly&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

## Results

**[Elbow Curve](/Resources/Elbow_curve.png)**

![Elbow_curve](/Resources/Elbow_curve.png)

The ideal number of clusters (k=4) can be deduced from the elbow curve above. When initialising the K-means model, these data is utilised to specify the number of clusters (n clusters):

```python
model = KMeans(n_clusters=4, random_state=1)
```

**[3D plot](/Resources/3D_Scatter.png)**

![3D_plot](/Resources/3D_Scatter.png)

This 3D scatter plot with cluster is generated using the following code:

```python
fig = px.scatter_3d(
    clustered_df,
    x="PC 1",
    y="PC 2",
    z="PC 3",
    color="Class",
    symbol="Class",
    hover_name =  "CoinName",
    hover_data = ["Algorithm"],
    width=800,
)
fig.update_layout(legend=dict(x=0, y=1))
fig.show()
```

**[hvTable](/Resources/hvtable.png)**

![hvTable](/Resources/hvtable.png)

All of the cryptocurrencies that are currently tradable are shown in the hvTable above. Utilizing the hvplot.table() method, this table was made.

```python
clustered_df.hvplot.table(columns=['CoinName', 'Algorithm', 'ProofType', 'TotalCoinSupply', 'TotalCoinsMined', 'Class'], sortable=True, selectable=True)
```

**[hvPlot (Scatter)](/Resources/hvplot.png)**

![hvPlot (Scatter)](/Resources/hvplot.png)

The graph shown above is a scatter plot with classes. Utilizing hvplot.scatter, this was produced. View the code here:

```python
plot_df.hvplot.scatter(x="TotalCoinsMined",
                       y="TotalCoinSupply",
                       by="Class", 
                       hover_cols= ['CoinName', 'Class', 'TotalCoinSupply', 'TotalCoinsMined']
                       )
```