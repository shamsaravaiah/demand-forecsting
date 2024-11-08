# Demand-Forecasting using Regression models

In this project, I developed a demand forecasting model using the Seoul Bike Sharing Dataset from Kaggle. The goal was to predict daily bike rental counts based on various environmental and seasonal factors, including temperature, humidity, wind speed, and holiday status.
I applied and evaluated multiple regression models, such as Linear Regression, Random Forest Regressor, and XGBoost Regressor, to identify the best-performing model. Each model’s performance was assessed using key metrics, including R² score, Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE).

After identifying the optimal model, I performed hyperparameter tuning, using both GridSearch and RandomSearch on the 2 models that had a R² score clost to 1, to further improve accuracy. The final model provides reliable bike rental predictions, which can be used to enhance resource allocation and improve operational efficiency for bike-sharing services.

This project demonstrates practical approaches to demand forecasting in the context of urban transportation.

DATASET obtained from Kaggle (https://www.kaggle.com/datasets/saurabhshahane/seoul-bike-sharing-demand-prediction)


## EDA

- Data Preparation: Loaded, cleaned, and checked for missing values and data types.
- Feature Exploration: Examined distributions and relationships for key features (e.g., Temperature, Humidity).
- Correlation Analysis: Identified strong correlations, e.g., between Temperature and Dew Point Temperature.
- Trend Analysis: Visualized seasonal trends and peak demand times across weekdays and months.



## _Data visualisations_

- [Pair plot](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/EDA_pairplot.png)
  
- [Correaltion Heat Map](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/correlation_heatmap.png)

- [Distribution Plot ](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/Displot.png)


- [Rented bike variable count by day](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/rented_bike_count_by_Day.png)

- [Rented bike variable count by Hour](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/rented_bike_count_by_Hour.png
)

- [Rented bike variable count by holiday](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/rented_bike_count_by_Holiday.png)

I plotted the count of the Rented bike feature against other features in the data set to see the distribution.


Below are the distrubution plots 
- [Displot](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/Displot.png)
- [Square root Displot](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/sqrt%20displot.png)


## _Feature Engineering_

Using VIF to remove variables with collinearity over 5

VIF = how other variables are explaining another variable, if VIF is high we remove that variable

High VIF Variables in my Data
* Temperature(°C): VIF = 87.57
* Humidity(%): VIF = 20.51
* Dew point temperature(°C): VIF = 115.71

### VIF Before Removing Dew Point

| Feature                     | VIF        |
|-----------------------------|------------|
| const                       | 397.715363 |
| Hour                        | 1.183686   |
| Temperature(°C)             | 87.112576  |
| Humidity(%)                 | 20.362259  |
| Wind speed (m/s)            | 1.276095   |
| Visibility (10m)            | 1.567300   |
| Dew point temperature(°C)   | 115.691025 |
| Solar Radiation (MJ/m2)     | 2.021193   |
| Rainfall(mm)                | 1.084427   |
| Snowfall (cm)               | 1.095396   |

### VIF After Removing Dew Point

| Feature                    | VIF        |
|----------------------------|------------|
| const                      | 53.654460  |
| Hour                       | 1.181468   |
| Temperature(°C)            | 1.623991   |
| Humidity(%)                | 2.534083   |
| Wind speed (m/s)           | 1.274067   |
| Visibility (10m)           | 1.556883   |
| Solar Radiation (MJ/m2)    | 1.924897   |
| Rainfall(mm)               | 1.070513   |
| Snowfall (cm)              | 1.090421   |




## _Model selection and Evaluation_:
| Model                | MSE         | MAE      | RMSE     | R² Score |
|----------------------|-------------|----------|----------|----------|
| Ridge                | 186567.569  | 330.2    | 431.935  | 0.543    |
| Lasso                | 187028.139  | 330.257  | 432.468  | 0.542    |
| Polynomial Regression| 117547.203  | 240.16   | 342.852  | 0.712    |
| SVR                  | 313071.334  | 381.349  | 559.528  | 0.233    |
| KNN                  | 100530.621  | 207.508  | 317.066  | 0.754    |
| Decision Tree        | 59212.449   | 133.789  | 243.336  | 0.855    |
| Random Forest        | 29387.62    | 97.937   | 171.428  | 0.928    |
| XGBoost              | 24164.912   | 95.454   | 155.451  | 0.941    |


Upon viewing the above table, the R² score for the regression models I have used one can observe that the lowest score is for the Support Vector Regressor model and the Random Forest and the XGBoost have highest scores closer to 1. 

I have plotted this prediction so it is easy to visualise

![SVR graph](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/%20SVR%20Truth%20vs%20Predicition.png)

![Random Forest graph](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/random%20forest%20Truth%20vs%20Predicition.png)

![XGBoost graph](https://github.com/shamsaravaiah/demand-forecsting/blob/main/images/xgboost%20Truth%20vs%20Predicition.png)

* SVR: Shows a poor fit with the lowest R² score, indicating that it may not be suitable for this dataset, potentially due to its limitations in capturing complex, non-linear patterns.
* Random Forest: Shows a good fit with a high R² score, effectively capturing data relationships, making it a reliable model for this task.
* XGBoost: Shows the best fit with the highest R² score, outperforming the other models in predictive accuracy. Its gradient boosting approach allows it to capture fine-grained patterns in the data.



## Fine tuning Random Forest and XGBoost models using Grid search and Random search



```sh
cd dillinger
npm i
node app
```

For production environments...

```sh
npm install --production
NODE_ENV=production node app
```

## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
