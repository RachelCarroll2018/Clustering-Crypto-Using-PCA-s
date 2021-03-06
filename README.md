# The Power of the Cloud and Unsupervised Learning

## Clustering Crypto

### Background

You are a Senior Manager at the Advisory Services team on a [Big Four firm](https://en.wikipedia.org/wiki/Big_Four_accounting_firms). One of your most important clients, a prominent investment bank, is interested in offering a new cryptocurrencies investment portfolio for its customers, however, they are lost in the immense universe of cryptocurrencies. They ask you to help them make sense of it all by generating a report of what cryptocurrencies are available on the trading market and how they can be grouped using classification.

#### Data Preprocessing

1. Using the provided `CSV` file, create a `Path` object and read the file data directly into a DataFrame named `crypto_df` using `pd.read_csv()`.

With the data loaded into a Pandas DataFrame, continue with the following data preprocessing tasks.

2. Keep only the necessary columns: 'CoinName','Algorithm','IsTrading','ProofType','TotalCoinsMined','TotalCoinSupply'

3. Keep only the cryptocurrencies that are trading.

4. Keep only the cryptocurrencies with a working algorithm.

5. Remove the `IsTrading` column.

6. Remove all cryptocurrencies with at least one null value.

7. Remove all cryptocurrencies that have no coins mined.

8. Drop all rows where there are 'N/A' text values.

9. Store the names of all cryptocurrencies in a DataFrame named `coins_name`, use the `crypto_df.index` as the index for this new DataFrame.

10. Remove the `CoinName` column.

11. Create dummy variables for all the text features, and store the resulting data in a DataFrame named `X`.

12. Use the [`StandardScaler` from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) to standardize all the data of the `X` DataFrame. Remember, this is important prior to using PCA and K-Means algorithms.

#### Reducing Data Dimensions Using PCA

Use the [`PCA` algorithm from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html) to reduce the dimensions of the `X` DataFrame down to three principal components.

Once you have reduced the data dimensions, create a DataFrame named `pcs_df` using as columns names `"PC 1", "PC 2"` and `"PC 3"`; use the `crypto_df.index` as the index for this new DataFrame.

#### Clustering Cryptocurrencies Using K-Means

In this section, you will use the [`KMeans` algorithm from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) to cluster the cryptocurrencies using the PCA data.

Perform the following tasks:

1. Create an Elbow Curve to find the best value for `k` using the `pcs_df` DataFrame

![image](https://user-images.githubusercontent.com/98990090/172207752-bd4539f3-dd85-4e6b-91e2-29e91c4da549.png)


2. Once you define the best value for `k`, run the `Kmeans` algorithm to predict the `k` clusters for the cryptocurrencies data. Use the `pcs_df` to run the `KMeans` algorithm 
> The best value for "k" is 4

3. Create a new DataFrame named `clustered_df`, that includes the following columns `"Algorithm", "ProofType", "TotalCoinsMined", "TotalCoinSupply", "PC 1", "PC 2", "PC 3", "CoinName", "Class"`

![image](https://user-images.githubusercontent.com/98990090/172207972-83b27846-4276-46c5-9901-46669ae9467d.png)


#### Visualizing Results

In this section, you will create some data visualization to present the final results. Perform the following tasks:

1. Create a scatter plot using `hvplot.scatter`, to present the clustered data about cryptocurrencies having `x="TotalCoinsMined"` and `y="TotalCoinSupply"` to contrast the number of available coins versus the total number of mined coins. Use the `hover_cols=["CoinName"]` parameter to include the cryptocurrency name on each data point

![image](https://user-images.githubusercontent.com/98990090/172208049-f4f92864-89b2-42fb-af7a-540803e79b1f.png)
![image](https://user-images.githubusercontent.com/98990090/172208119-93cceb83-3e1d-457b-b318-20222941de55.png)


2. Use `hvplot.table` to create a data table with all the current tradable cryptocurrencies. The table should have the following columns: `"CoinName", "Algorithm", "ProofType", "TotalCoinSupply", "TotalCoinsMined", "Class"`

![image](https://user-images.githubusercontent.com/98990090/172208173-d30300a7-ea00-4a1e-b228-4c3459fffcf4.png)

