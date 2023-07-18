
    !jupyter nbconvert --to markdown Credit_EDA_Assignment.ipynb --output README.md

------------

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
%matplotlib inline
```

### reading application.csv data


```python
application_data = pd.read_csv('application_data.csv')
application_data.head()
```





  <div id="df-b1a8dba8-5de3-474c-a1d5-fb576d90b783">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>CODE_GENDER</th>
      <th>FLAG_OWN_CAR</th>
      <th>FLAG_OWN_REALTY</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>...</th>
      <th>FLAG_DOCUMENT_18</th>
      <th>FLAG_DOCUMENT_19</th>
      <th>FLAG_DOCUMENT_20</th>
      <th>FLAG_DOCUMENT_21</th>
      <th>AMT_REQ_CREDIT_BUREAU_HOUR</th>
      <th>AMT_REQ_CREDIT_BUREAU_DAY</th>
      <th>AMT_REQ_CREDIT_BUREAU_WEEK</th>
      <th>AMT_REQ_CREDIT_BUREAU_MON</th>
      <th>AMT_REQ_CREDIT_BUREAU_QRT</th>
      <th>AMT_REQ_CREDIT_BUREAU_YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100002</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>202500.0</td>
      <td>406597.5</td>
      <td>24700.5</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100003</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>N</td>
      <td>0</td>
      <td>270000.0</td>
      <td>1293502.5</td>
      <td>35698.5</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100004</td>
      <td>0</td>
      <td>Revolving loans</td>
      <td>M</td>
      <td>Y</td>
      <td>Y</td>
      <td>0</td>
      <td>67500.0</td>
      <td>135000.0</td>
      <td>6750.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100006</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>135000.0</td>
      <td>312682.5</td>
      <td>29686.5</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100007</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>121500.0</td>
      <td>513000.0</td>
      <td>21865.5</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 122 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b1a8dba8-5de3-474c-a1d5-fb576d90b783')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b1a8dba8-5de3-474c-a1d5-fb576d90b783 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b1a8dba8-5de3-474c-a1d5-fb576d90b783');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### information about data


```python
application_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 307511 entries, 0 to 307510
    Columns: 122 entries, SK_ID_CURR to AMT_REQ_CREDIT_BUREAU_YEAR
    dtypes: float64(65), int64(41), object(16)
    memory usage: 286.2+ MB



```python
application_data.describe()
```





  <div id="df-24b192ff-33ce-412e-b70d-a52f91e9a982">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_DOCUMENT_18</th>
      <th>FLAG_DOCUMENT_19</th>
      <th>FLAG_DOCUMENT_20</th>
      <th>FLAG_DOCUMENT_21</th>
      <th>AMT_REQ_CREDIT_BUREAU_HOUR</th>
      <th>AMT_REQ_CREDIT_BUREAU_DAY</th>
      <th>AMT_REQ_CREDIT_BUREAU_WEEK</th>
      <th>AMT_REQ_CREDIT_BUREAU_MON</th>
      <th>AMT_REQ_CREDIT_BUREAU_QRT</th>
      <th>AMT_REQ_CREDIT_BUREAU_YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
      <td>307499.000000</td>
      <td>3.072330e+05</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>...</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>265992.000000</td>
      <td>265992.000000</td>
      <td>265992.000000</td>
      <td>265992.000000</td>
      <td>265992.000000</td>
      <td>265992.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>278180.518577</td>
      <td>0.080729</td>
      <td>0.417052</td>
      <td>1.687979e+05</td>
      <td>5.990260e+05</td>
      <td>27108.573909</td>
      <td>5.383962e+05</td>
      <td>0.020868</td>
      <td>-16036.995067</td>
      <td>63815.045904</td>
      <td>...</td>
      <td>0.008130</td>
      <td>0.000595</td>
      <td>0.000507</td>
      <td>0.000335</td>
      <td>0.006402</td>
      <td>0.007000</td>
      <td>0.034362</td>
      <td>0.267395</td>
      <td>0.265474</td>
      <td>1.899974</td>
    </tr>
    <tr>
      <th>std</th>
      <td>102790.175348</td>
      <td>0.272419</td>
      <td>0.722121</td>
      <td>2.371231e+05</td>
      <td>4.024908e+05</td>
      <td>14493.737315</td>
      <td>3.694465e+05</td>
      <td>0.013831</td>
      <td>4363.988632</td>
      <td>141275.766519</td>
      <td>...</td>
      <td>0.089798</td>
      <td>0.024387</td>
      <td>0.022518</td>
      <td>0.018299</td>
      <td>0.083849</td>
      <td>0.110757</td>
      <td>0.204685</td>
      <td>0.916002</td>
      <td>0.794056</td>
      <td>1.869295</td>
    </tr>
    <tr>
      <th>min</th>
      <td>100002.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.565000e+04</td>
      <td>4.500000e+04</td>
      <td>1615.500000</td>
      <td>4.050000e+04</td>
      <td>0.000290</td>
      <td>-25229.000000</td>
      <td>-17912.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>189145.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.125000e+05</td>
      <td>2.700000e+05</td>
      <td>16524.000000</td>
      <td>2.385000e+05</td>
      <td>0.010006</td>
      <td>-19682.000000</td>
      <td>-2760.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>278202.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.471500e+05</td>
      <td>5.135310e+05</td>
      <td>24903.000000</td>
      <td>4.500000e+05</td>
      <td>0.018850</td>
      <td>-15750.000000</td>
      <td>-1213.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>367142.500000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.025000e+05</td>
      <td>8.086500e+05</td>
      <td>34596.000000</td>
      <td>6.795000e+05</td>
      <td>0.028663</td>
      <td>-12413.000000</td>
      <td>-289.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>456255.000000</td>
      <td>1.000000</td>
      <td>19.000000</td>
      <td>1.170000e+08</td>
      <td>4.050000e+06</td>
      <td>258025.500000</td>
      <td>4.050000e+06</td>
      <td>0.072508</td>
      <td>-7489.000000</td>
      <td>365243.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>4.000000</td>
      <td>9.000000</td>
      <td>8.000000</td>
      <td>27.000000</td>
      <td>261.000000</td>
      <td>25.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 106 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-24b192ff-33ce-412e-b70d-a52f91e9a982')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-24b192ff-33ce-412e-b70d-a52f91e9a982 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-24b192ff-33ce-412e-b70d-a52f91e9a982');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
application_data.shape
```




    (307511, 122)



### as there are 122 columns we can use meaningful columns for our calculation


```python
list(application_data.columns)
```




    ['SK_ID_CURR',
     'TARGET',
     'NAME_CONTRACT_TYPE',
     'CODE_GENDER',
     'FLAG_OWN_CAR',
     'FLAG_OWN_REALTY',
     'CNT_CHILDREN',
     'AMT_INCOME_TOTAL',
     'AMT_CREDIT',
     'AMT_ANNUITY',
     'AMT_GOODS_PRICE',
     'NAME_TYPE_SUITE',
     'NAME_INCOME_TYPE',
     'NAME_EDUCATION_TYPE',
     'NAME_FAMILY_STATUS',
     'NAME_HOUSING_TYPE',
     'REGION_POPULATION_RELATIVE',
     'DAYS_BIRTH',
     'DAYS_EMPLOYED',
     'DAYS_REGISTRATION',
     'DAYS_ID_PUBLISH',
     'OWN_CAR_AGE',
     'FLAG_MOBIL',
     'FLAG_EMP_PHONE',
     'FLAG_WORK_PHONE',
     'FLAG_CONT_MOBILE',
     'FLAG_PHONE',
     'FLAG_EMAIL',
     'OCCUPATION_TYPE',
     'CNT_FAM_MEMBERS',
     'REGION_RATING_CLIENT',
     'REGION_RATING_CLIENT_W_CITY',
     'WEEKDAY_APPR_PROCESS_START',
     'HOUR_APPR_PROCESS_START',
     'REG_REGION_NOT_LIVE_REGION',
     'REG_REGION_NOT_WORK_REGION',
     'LIVE_REGION_NOT_WORK_REGION',
     'REG_CITY_NOT_LIVE_CITY',
     'REG_CITY_NOT_WORK_CITY',
     'LIVE_CITY_NOT_WORK_CITY',
     'ORGANIZATION_TYPE',
     'EXT_SOURCE_1',
     'EXT_SOURCE_2',
     'EXT_SOURCE_3',
     'APARTMENTS_AVG',
     'BASEMENTAREA_AVG',
     'YEARS_BEGINEXPLUATATION_AVG',
     'YEARS_BUILD_AVG',
     'COMMONAREA_AVG',
     'ELEVATORS_AVG',
     'ENTRANCES_AVG',
     'FLOORSMAX_AVG',
     'FLOORSMIN_AVG',
     'LANDAREA_AVG',
     'LIVINGAPARTMENTS_AVG',
     'LIVINGAREA_AVG',
     'NONLIVINGAPARTMENTS_AVG',
     'NONLIVINGAREA_AVG',
     'APARTMENTS_MODE',
     'BASEMENTAREA_MODE',
     'YEARS_BEGINEXPLUATATION_MODE',
     'YEARS_BUILD_MODE',
     'COMMONAREA_MODE',
     'ELEVATORS_MODE',
     'ENTRANCES_MODE',
     'FLOORSMAX_MODE',
     'FLOORSMIN_MODE',
     'LANDAREA_MODE',
     'LIVINGAPARTMENTS_MODE',
     'LIVINGAREA_MODE',
     'NONLIVINGAPARTMENTS_MODE',
     'NONLIVINGAREA_MODE',
     'APARTMENTS_MEDI',
     'BASEMENTAREA_MEDI',
     'YEARS_BEGINEXPLUATATION_MEDI',
     'YEARS_BUILD_MEDI',
     'COMMONAREA_MEDI',
     'ELEVATORS_MEDI',
     'ENTRANCES_MEDI',
     'FLOORSMAX_MEDI',
     'FLOORSMIN_MEDI',
     'LANDAREA_MEDI',
     'LIVINGAPARTMENTS_MEDI',
     'LIVINGAREA_MEDI',
     'NONLIVINGAPARTMENTS_MEDI',
     'NONLIVINGAREA_MEDI',
     'FONDKAPREMONT_MODE',
     'HOUSETYPE_MODE',
     'TOTALAREA_MODE',
     'WALLSMATERIAL_MODE',
     'EMERGENCYSTATE_MODE',
     'OBS_30_CNT_SOCIAL_CIRCLE',
     'DEF_30_CNT_SOCIAL_CIRCLE',
     'OBS_60_CNT_SOCIAL_CIRCLE',
     'DEF_60_CNT_SOCIAL_CIRCLE',
     'DAYS_LAST_PHONE_CHANGE',
     'FLAG_DOCUMENT_2',
     'FLAG_DOCUMENT_3',
     'FLAG_DOCUMENT_4',
     'FLAG_DOCUMENT_5',
     'FLAG_DOCUMENT_6',
     'FLAG_DOCUMENT_7',
     'FLAG_DOCUMENT_8',
     'FLAG_DOCUMENT_9',
     'FLAG_DOCUMENT_10',
     'FLAG_DOCUMENT_11',
     'FLAG_DOCUMENT_12',
     'FLAG_DOCUMENT_13',
     'FLAG_DOCUMENT_14',
     'FLAG_DOCUMENT_15',
     'FLAG_DOCUMENT_16',
     'FLAG_DOCUMENT_17',
     'FLAG_DOCUMENT_18',
     'FLAG_DOCUMENT_19',
     'FLAG_DOCUMENT_20',
     'FLAG_DOCUMENT_21',
     'AMT_REQ_CREDIT_BUREAU_HOUR',
     'AMT_REQ_CREDIT_BUREAU_DAY',
     'AMT_REQ_CREDIT_BUREAU_WEEK',
     'AMT_REQ_CREDIT_BUREAU_MON',
     'AMT_REQ_CREDIT_BUREAU_QRT',
     'AMT_REQ_CREDIT_BUREAU_YEAR']




```python
application_data = application_data.filter(
  [
    'SK_ID_CURR',
    'TARGET',
    'NAME_CONTRACT_TYPE',
    'CODE_GENDER',
    'FLAG_OWN_CAR',
    'FLAG_OWN_REALTY',
    'CNT_CHILDREN',
    'AMT_INCOME_TOTAL',
    'AMT_CREDIT',
    'AMT_ANNUITY',
    'AMT_GOODS_PRICE',
    'NAME_TYPE_SUITE',
    'NAME_INCOME_TYPE',
    'NAME_EDUCATION_TYPE',
    'NAME_FAMILY_STATUS',
    'NAME_HOUSING_TYPE',
    'REGION_POPULATION_RELATIVE',
    'DAYS_BIRTH',
    'DAYS_EMPLOYED',
    'DAYS_REGISTRATION',
    'DAYS_ID_PUBLISH',
    'OCCUPATION_TYPE',
    'CNT_FAM_MEMBERS',
    'FLAG_MOBIL',
    'FLAG_EMP_PHONE',
    'FLAG_WORK_PHONE',
    'FLAG_CONT_MOBILE',
    'FLAG_EMAIL',                                         
    'REGION_RATING_CLIENT',
    'REGION_RATING_CLIENT_W_CITY',
    'WEEKDAY_APPR_PROCESS_START',
    'HOUR_APPR_PROCESS_START',
    'REG_REGION_NOT_LIVE_REGION',
    'REG_REGION_NOT_WORK_REGION',
    'REG_CITY_NOT_LIVE_CITY',
    'REG_CITY_NOT_WORK_CITY',
    'ORGANIZATION_TYPE',
    'EXT_SOURCE_1',
    'EXT_SOURCE_2',
    'EXT_SOURCE_3',
    'DAYS_LAST_PHONE_CHANGE'
  ]
)
```


```python
len(application_data.columns)
```




    41




```python
application_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 307511 entries, 0 to 307510
    Data columns (total 41 columns):
     #   Column                       Non-Null Count   Dtype  
    ---  ------                       --------------   -----  
     0   SK_ID_CURR                   307511 non-null  int64  
     1   TARGET                       307511 non-null  int64  
     2   NAME_CONTRACT_TYPE           307511 non-null  object 
     3   CODE_GENDER                  307511 non-null  object 
     4   FLAG_OWN_CAR                 307511 non-null  object 
     5   FLAG_OWN_REALTY              307511 non-null  object 
     6   CNT_CHILDREN                 307511 non-null  int64  
     7   AMT_INCOME_TOTAL             307511 non-null  float64
     8   AMT_CREDIT                   307511 non-null  float64
     9   AMT_ANNUITY                  307499 non-null  float64
     10  AMT_GOODS_PRICE              307233 non-null  float64
     11  NAME_TYPE_SUITE              306219 non-null  object 
     12  NAME_INCOME_TYPE             307511 non-null  object 
     13  NAME_EDUCATION_TYPE          307511 non-null  object 
     14  NAME_FAMILY_STATUS           307511 non-null  object 
     15  NAME_HOUSING_TYPE            307511 non-null  object 
     16  REGION_POPULATION_RELATIVE   307511 non-null  float64
     17  DAYS_BIRTH                   307511 non-null  int64  
     18  DAYS_EMPLOYED                307511 non-null  int64  
     19  DAYS_REGISTRATION            307511 non-null  float64
     20  DAYS_ID_PUBLISH              307511 non-null  int64  
     21  OCCUPATION_TYPE              211120 non-null  object 
     22  CNT_FAM_MEMBERS              307509 non-null  float64
     23  FLAG_MOBIL                   307511 non-null  int64  
     24  FLAG_EMP_PHONE               307511 non-null  int64  
     25  FLAG_WORK_PHONE              307511 non-null  int64  
     26  FLAG_CONT_MOBILE             307511 non-null  int64  
     27  FLAG_EMAIL                   307511 non-null  int64  
     28  REGION_RATING_CLIENT         307511 non-null  int64  
     29  REGION_RATING_CLIENT_W_CITY  307511 non-null  int64  
     30  WEEKDAY_APPR_PROCESS_START   307511 non-null  object 
     31  HOUR_APPR_PROCESS_START      307511 non-null  int64  
     32  REG_REGION_NOT_LIVE_REGION   307511 non-null  int64  
     33  REG_REGION_NOT_WORK_REGION   307511 non-null  int64  
     34  REG_CITY_NOT_LIVE_CITY       307511 non-null  int64  
     35  REG_CITY_NOT_WORK_CITY       307511 non-null  int64  
     36  ORGANIZATION_TYPE            307511 non-null  object 
     37  EXT_SOURCE_1                 134133 non-null  float64
     38  EXT_SOURCE_2                 306851 non-null  float64
     39  EXT_SOURCE_3                 246546 non-null  float64
     40  DAYS_LAST_PHONE_CHANGE       307510 non-null  float64
    dtypes: float64(11), int64(18), object(12)
    memory usage: 96.2+ MB


### finding the percentage of NULL values in every column, for further cleaning


```python
application_data.isnull().sum() * 100 / application_data.shape[0]
```




    SK_ID_CURR                      0.000000
    TARGET                          0.000000
    NAME_CONTRACT_TYPE              0.000000
    CODE_GENDER                     0.000000
    FLAG_OWN_CAR                    0.000000
    FLAG_OWN_REALTY                 0.000000
    CNT_CHILDREN                    0.000000
    AMT_INCOME_TOTAL                0.000000
    AMT_CREDIT                      0.000000
    AMT_ANNUITY                     0.003902
    AMT_GOODS_PRICE                 0.090403
    NAME_TYPE_SUITE                 0.420148
    NAME_INCOME_TYPE                0.000000
    NAME_EDUCATION_TYPE             0.000000
    NAME_FAMILY_STATUS              0.000000
    NAME_HOUSING_TYPE               0.000000
    REGION_POPULATION_RELATIVE      0.000000
    DAYS_BIRTH                      0.000000
    DAYS_EMPLOYED                   0.000000
    DAYS_REGISTRATION               0.000000
    DAYS_ID_PUBLISH                 0.000000
    OCCUPATION_TYPE                31.345545
    CNT_FAM_MEMBERS                 0.000650
    FLAG_MOBIL                      0.000000
    FLAG_EMP_PHONE                  0.000000
    FLAG_WORK_PHONE                 0.000000
    FLAG_CONT_MOBILE                0.000000
    FLAG_EMAIL                      0.000000
    REGION_RATING_CLIENT            0.000000
    REGION_RATING_CLIENT_W_CITY     0.000000
    WEEKDAY_APPR_PROCESS_START      0.000000
    HOUR_APPR_PROCESS_START         0.000000
    REG_REGION_NOT_LIVE_REGION      0.000000
    REG_REGION_NOT_WORK_REGION      0.000000
    REG_CITY_NOT_LIVE_CITY          0.000000
    REG_CITY_NOT_WORK_CITY          0.000000
    ORGANIZATION_TYPE               0.000000
    EXT_SOURCE_1                   56.381073
    EXT_SOURCE_2                    0.214626
    EXT_SOURCE_3                   19.825307
    DAYS_LAST_PHONE_CHANGE          0.000325
    dtype: float64



### defining function for calculating percentage of NULL values in dataframe


```python
calc_per_missing_values = lambda x: 100 * (x.isnull().sum() / x.shape[0])
calc_per_missing_values(application_data)
```




    SK_ID_CURR                      0.000000
    TARGET                          0.000000
    NAME_CONTRACT_TYPE              0.000000
    CODE_GENDER                     0.000000
    FLAG_OWN_CAR                    0.000000
    FLAG_OWN_REALTY                 0.000000
    CNT_CHILDREN                    0.000000
    AMT_INCOME_TOTAL                0.000000
    AMT_CREDIT                      0.000000
    AMT_ANNUITY                     0.003902
    AMT_GOODS_PRICE                 0.090403
    NAME_TYPE_SUITE                 0.420148
    NAME_INCOME_TYPE                0.000000
    NAME_EDUCATION_TYPE             0.000000
    NAME_FAMILY_STATUS              0.000000
    NAME_HOUSING_TYPE               0.000000
    REGION_POPULATION_RELATIVE      0.000000
    DAYS_BIRTH                      0.000000
    DAYS_EMPLOYED                   0.000000
    DAYS_REGISTRATION               0.000000
    DAYS_ID_PUBLISH                 0.000000
    OCCUPATION_TYPE                31.345545
    CNT_FAM_MEMBERS                 0.000650
    FLAG_MOBIL                      0.000000
    FLAG_EMP_PHONE                  0.000000
    FLAG_WORK_PHONE                 0.000000
    FLAG_CONT_MOBILE                0.000000
    FLAG_EMAIL                      0.000000
    REGION_RATING_CLIENT            0.000000
    REGION_RATING_CLIENT_W_CITY     0.000000
    WEEKDAY_APPR_PROCESS_START      0.000000
    HOUR_APPR_PROCESS_START         0.000000
    REG_REGION_NOT_LIVE_REGION      0.000000
    REG_REGION_NOT_WORK_REGION      0.000000
    REG_CITY_NOT_LIVE_CITY          0.000000
    REG_CITY_NOT_WORK_CITY          0.000000
    ORGANIZATION_TYPE               0.000000
    EXT_SOURCE_1                   56.381073
    EXT_SOURCE_2                    0.214626
    EXT_SOURCE_3                   19.825307
    DAYS_LAST_PHONE_CHANGE          0.000325
    dtype: float64



### analysing in loops over columns in dataframe, dropping columns where more than 30% of the values are NULL


```python
for col in application_data:
  if calc_per_missing_values(application_data[col]) > 30:
    application_data.drop(col, axis=1, inplace=True)

application_data.head()
```





  <div id="df-cb8d3d63-bc10-43ed-b396-11be6f4fa846">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>CODE_GENDER</th>
      <th>FLAG_OWN_CAR</th>
      <th>FLAG_OWN_REALTY</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>...</th>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>ORGANIZATION_TYPE</th>
      <th>EXT_SOURCE_2</th>
      <th>EXT_SOURCE_3</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100002</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>202500.0</td>
      <td>406597.5</td>
      <td>24700.5</td>
      <td>...</td>
      <td>WEDNESDAY</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.262949</td>
      <td>0.139376</td>
      <td>-1134.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100003</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>N</td>
      <td>0</td>
      <td>270000.0</td>
      <td>1293502.5</td>
      <td>35698.5</td>
      <td>...</td>
      <td>MONDAY</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>School</td>
      <td>0.622246</td>
      <td>NaN</td>
      <td>-828.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100004</td>
      <td>0</td>
      <td>Revolving loans</td>
      <td>M</td>
      <td>Y</td>
      <td>Y</td>
      <td>0</td>
      <td>67500.0</td>
      <td>135000.0</td>
      <td>6750.0</td>
      <td>...</td>
      <td>MONDAY</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Government</td>
      <td>0.555912</td>
      <td>0.729567</td>
      <td>-815.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100006</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>135000.0</td>
      <td>312682.5</td>
      <td>29686.5</td>
      <td>...</td>
      <td>WEDNESDAY</td>
      <td>17</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.650442</td>
      <td>NaN</td>
      <td>-617.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100007</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0</td>
      <td>121500.0</td>
      <td>513000.0</td>
      <td>21865.5</td>
      <td>...</td>
      <td>THURSDAY</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>Religion</td>
      <td>0.322738</td>
      <td>NaN</td>
      <td>-1106.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 39 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-cb8d3d63-bc10-43ed-b396-11be6f4fa846')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-cb8d3d63-bc10-43ed-b396-11be6f4fa846 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-cb8d3d63-bc10-43ed-b396-11be6f4fa846');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
application_data.shape
```




    (307511, 39)



### calculating percentage of NULL values in every column, for further cleaning


```python
check_nulls = calc_per_missing_values(application_data)
check_nulls
```




    SK_ID_CURR                      0.000000
    TARGET                          0.000000
    NAME_CONTRACT_TYPE              0.000000
    CODE_GENDER                     0.000000
    FLAG_OWN_CAR                    0.000000
    FLAG_OWN_REALTY                 0.000000
    CNT_CHILDREN                    0.000000
    AMT_INCOME_TOTAL                0.000000
    AMT_CREDIT                      0.000000
    AMT_ANNUITY                     0.003902
    AMT_GOODS_PRICE                 0.090403
    NAME_TYPE_SUITE                 0.420148
    NAME_INCOME_TYPE                0.000000
    NAME_EDUCATION_TYPE             0.000000
    NAME_FAMILY_STATUS              0.000000
    NAME_HOUSING_TYPE               0.000000
    REGION_POPULATION_RELATIVE      0.000000
    DAYS_BIRTH                      0.000000
    DAYS_EMPLOYED                   0.000000
    DAYS_REGISTRATION               0.000000
    DAYS_ID_PUBLISH                 0.000000
    CNT_FAM_MEMBERS                 0.000650
    FLAG_MOBIL                      0.000000
    FLAG_EMP_PHONE                  0.000000
    FLAG_WORK_PHONE                 0.000000
    FLAG_CONT_MOBILE                0.000000
    FLAG_EMAIL                      0.000000
    REGION_RATING_CLIENT            0.000000
    REGION_RATING_CLIENT_W_CITY     0.000000
    WEEKDAY_APPR_PROCESS_START      0.000000
    HOUR_APPR_PROCESS_START         0.000000
    REG_REGION_NOT_LIVE_REGION      0.000000
    REG_REGION_NOT_WORK_REGION      0.000000
    REG_CITY_NOT_LIVE_CITY          0.000000
    REG_CITY_NOT_WORK_CITY          0.000000
    ORGANIZATION_TYPE               0.000000
    EXT_SOURCE_2                    0.214626
    EXT_SOURCE_3                   19.825307
    DAYS_LAST_PHONE_CHANGE          0.000325
    dtype: float64




```python
check_nulls[check_nulls == max(check_nulls)]
```




    EXT_SOURCE_3    19.825307
    dtype: float64



### dropping `External_Source_3` column as it contains around 20% missing values


```python
application_data.drop("EXT_SOURCE_3", axis=1, inplace=True)
```


```python
application_data.describe()
```





  <div id="df-daf41954-2846-42eb-a439-ef679b9b8733">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
      <td>307499.000000</td>
      <td>3.072330e+05</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>...</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.068510e+05</td>
      <td>307510.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>278180.518577</td>
      <td>0.080729</td>
      <td>0.417052</td>
      <td>1.687979e+05</td>
      <td>5.990260e+05</td>
      <td>27108.573909</td>
      <td>5.383962e+05</td>
      <td>0.020868</td>
      <td>-16036.995067</td>
      <td>63815.045904</td>
      <td>...</td>
      <td>0.056720</td>
      <td>2.052463</td>
      <td>2.031521</td>
      <td>12.063419</td>
      <td>0.015144</td>
      <td>0.050769</td>
      <td>0.078173</td>
      <td>0.230454</td>
      <td>5.143927e-01</td>
      <td>-962.858788</td>
    </tr>
    <tr>
      <th>std</th>
      <td>102790.175348</td>
      <td>0.272419</td>
      <td>0.722121</td>
      <td>2.371231e+05</td>
      <td>4.024908e+05</td>
      <td>14493.737315</td>
      <td>3.694465e+05</td>
      <td>0.013831</td>
      <td>4363.988632</td>
      <td>141275.766519</td>
      <td>...</td>
      <td>0.231307</td>
      <td>0.509034</td>
      <td>0.502737</td>
      <td>3.265832</td>
      <td>0.122126</td>
      <td>0.219526</td>
      <td>0.268444</td>
      <td>0.421124</td>
      <td>1.910602e-01</td>
      <td>826.808487</td>
    </tr>
    <tr>
      <th>min</th>
      <td>100002.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.565000e+04</td>
      <td>4.500000e+04</td>
      <td>1615.500000</td>
      <td>4.050000e+04</td>
      <td>0.000290</td>
      <td>-25229.000000</td>
      <td>-17912.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.173617e-08</td>
      <td>-4292.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>189145.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.125000e+05</td>
      <td>2.700000e+05</td>
      <td>16524.000000</td>
      <td>2.385000e+05</td>
      <td>0.010006</td>
      <td>-19682.000000</td>
      <td>-2760.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.924574e-01</td>
      <td>-1570.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>278202.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.471500e+05</td>
      <td>5.135310e+05</td>
      <td>24903.000000</td>
      <td>4.500000e+05</td>
      <td>0.018850</td>
      <td>-15750.000000</td>
      <td>-1213.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.659614e-01</td>
      <td>-757.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>367142.500000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.025000e+05</td>
      <td>8.086500e+05</td>
      <td>34596.000000</td>
      <td>6.795000e+05</td>
      <td>0.028663</td>
      <td>-12413.000000</td>
      <td>-289.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>14.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.636171e-01</td>
      <td>-274.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>456255.000000</td>
      <td>1.000000</td>
      <td>19.000000</td>
      <td>1.170000e+08</td>
      <td>4.050000e+06</td>
      <td>258025.500000</td>
      <td>4.050000e+06</td>
      <td>0.072508</td>
      <td>-7489.000000</td>
      <td>365243.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>23.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>8.549997e-01</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 27 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-daf41954-2846-42eb-a439-ef679b9b8733')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-daf41954-2846-42eb-a439-ef679b9b8733 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-daf41954-2846-42eb-a439-ef679b9b8733');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
df={}

for col in application_data:
  x = calc_per_missing_values(application_data[col])

  if x < 1:
      df.update({col : x})

pd.DataFrame.from_dict(df, orient='index')
```





  <div id="df-f0e2373c-6887-4551-b9f9-8c3215bde516">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>SK_ID_CURR</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>TARGET</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>NAME_CONTRACT_TYPE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>CODE_GENDER</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_OWN_CAR</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_OWN_REALTY</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>CNT_CHILDREN</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>AMT_INCOME_TOTAL</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>AMT_CREDIT</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>AMT_ANNUITY</th>
      <td>0.003902</td>
    </tr>
    <tr>
      <th>AMT_GOODS_PRICE</th>
      <td>0.090403</td>
    </tr>
    <tr>
      <th>NAME_TYPE_SUITE</th>
      <td>0.420148</td>
    </tr>
    <tr>
      <th>NAME_INCOME_TYPE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>NAME_EDUCATION_TYPE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>NAME_FAMILY_STATUS</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>NAME_HOUSING_TYPE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REGION_POPULATION_RELATIVE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>DAYS_BIRTH</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>DAYS_EMPLOYED</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>DAYS_REGISTRATION</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>DAYS_ID_PUBLISH</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>CNT_FAM_MEMBERS</th>
      <td>0.000650</td>
    </tr>
    <tr>
      <th>FLAG_MOBIL</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_EMP_PHONE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_WORK_PHONE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_CONT_MOBILE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>FLAG_EMAIL</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REGION_RATING_CLIENT</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>HOUR_APPR_PROCESS_START</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>ORGANIZATION_TYPE</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>EXT_SOURCE_2</th>
      <td>0.214626</td>
    </tr>
    <tr>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <td>0.000325</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f0e2373c-6887-4551-b9f9-8c3215bde516')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f0e2373c-6887-4551-b9f9-8c3215bde516 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f0e2373c-6887-4551-b9f9-8c3215bde516');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
application_data.shape
```




    (307511, 38)



### as `AMT_GOODS_PRICE` and `EXT_SOURCE_2,` has very low missing values and we can fill those columns with mean values


```python
AMT_GOODS_PRICE_mean = application_data['AMT_GOODS_PRICE'].mean()
AMT_GOODS_PRICE_mean
```




    538396.2074288895




```python
application_data['AMT_GOODS_PRICE'].fillna(AMT_GOODS_PRICE_mean, inplace=True)
```


```python
EXT_SOURCE_2_mean = application_data['EXT_SOURCE_2'].mean()
EXT_SOURCE_2_mean
```




    0.5143926741308462




```python
application_data['EXT_SOURCE_2'].fillna(EXT_SOURCE_2_mean, inplace=True)
```


```python
application_data[["AMT_GOODS_PRICE", "EXT_SOURCE_2"]].describe()
```





  <div id="df-7b6c5a75-d95a-405f-9387-64560374774b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AMT_GOODS_PRICE</th>
      <th>EXT_SOURCE_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5.383962e+05</td>
      <td>5.143927e-01</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.692794e+05</td>
      <td>1.908550e-01</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.050000e+04</td>
      <td>8.173617e-08</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2.385000e+05</td>
      <td>3.929737e-01</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4.500000e+05</td>
      <td>5.654672e-01</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.795000e+05</td>
      <td>6.634218e-01</td>
    </tr>
    <tr>
      <th>max</th>
      <td>4.050000e+06</td>
      <td>8.549997e-01</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7b6c5a75-d95a-405f-9387-64560374774b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7b6c5a75-d95a-405f-9387-64560374774b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7b6c5a75-d95a-405f-9387-64560374774b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
application_data['NAME_TYPE_SUITE'].value_counts()
```




    Unaccompanied      248526
    Family              40149
    Spouse, partner     11370
    Children             3267
    Other_B              1770
    Other_A               866
    Group of people       271
    Name: NAME_TYPE_SUITE, dtype: int64




```python
mod = application_data["NAME_TYPE_SUITE"].mode()
mod
```




    0    Unaccompanied
    Name: NAME_TYPE_SUITE, dtype: object



### as `Unaccompanied` data has the highest mode, we can fill missing values  with `Unaccompanied`



```python
application_data["NAME_TYPE_SUITE"].fillna(mod[0],inplace=True)
```

### Finding Outliers


```python
application_data.describe()
```





  <div id="df-b799bea0-00f3-4034-a224-21b69ffd17db">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
      <td>307499.000000</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>...</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>307510.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>278180.518577</td>
      <td>0.080729</td>
      <td>0.417052</td>
      <td>1.687979e+05</td>
      <td>5.990260e+05</td>
      <td>27108.573909</td>
      <td>5.383962e+05</td>
      <td>0.020868</td>
      <td>-16036.995067</td>
      <td>63815.045904</td>
      <td>...</td>
      <td>0.056720</td>
      <td>2.052463</td>
      <td>2.031521</td>
      <td>12.063419</td>
      <td>0.015144</td>
      <td>0.050769</td>
      <td>0.078173</td>
      <td>0.230454</td>
      <td>5.143927e-01</td>
      <td>-962.858788</td>
    </tr>
    <tr>
      <th>std</th>
      <td>102790.175348</td>
      <td>0.272419</td>
      <td>0.722121</td>
      <td>2.371231e+05</td>
      <td>4.024908e+05</td>
      <td>14493.737315</td>
      <td>3.692794e+05</td>
      <td>0.013831</td>
      <td>4363.988632</td>
      <td>141275.766519</td>
      <td>...</td>
      <td>0.231307</td>
      <td>0.509034</td>
      <td>0.502737</td>
      <td>3.265832</td>
      <td>0.122126</td>
      <td>0.219526</td>
      <td>0.268444</td>
      <td>0.421124</td>
      <td>1.908550e-01</td>
      <td>826.808487</td>
    </tr>
    <tr>
      <th>min</th>
      <td>100002.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.565000e+04</td>
      <td>4.500000e+04</td>
      <td>1615.500000</td>
      <td>4.050000e+04</td>
      <td>0.000290</td>
      <td>-25229.000000</td>
      <td>-17912.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.173617e-08</td>
      <td>-4292.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>189145.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.125000e+05</td>
      <td>2.700000e+05</td>
      <td>16524.000000</td>
      <td>2.385000e+05</td>
      <td>0.010006</td>
      <td>-19682.000000</td>
      <td>-2760.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.929737e-01</td>
      <td>-1570.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>278202.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.471500e+05</td>
      <td>5.135310e+05</td>
      <td>24903.000000</td>
      <td>4.500000e+05</td>
      <td>0.018850</td>
      <td>-15750.000000</td>
      <td>-1213.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.654672e-01</td>
      <td>-757.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>367142.500000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.025000e+05</td>
      <td>8.086500e+05</td>
      <td>34596.000000</td>
      <td>6.795000e+05</td>
      <td>0.028663</td>
      <td>-12413.000000</td>
      <td>-289.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>14.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.634218e-01</td>
      <td>-274.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>456255.000000</td>
      <td>1.000000</td>
      <td>19.000000</td>
      <td>1.170000e+08</td>
      <td>4.050000e+06</td>
      <td>258025.500000</td>
      <td>4.050000e+06</td>
      <td>0.072508</td>
      <td>-7489.000000</td>
      <td>365243.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>23.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>8.549997e-01</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 27 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b799bea0-00f3-4034-a224-21b69ffd17db')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b799bea0-00f3-4034-a224-21b69ffd17db button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b799bea0-00f3-4034-a224-21b69ffd17db');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
a = application_data['AMT_ANNUITY'].isnull().sum() * 100 / application_data['AMT_ANNUITY'].shape[0]
b = application_data['CNT_FAM_MEMBERS'].isnull().sum() * 100 / application_data['CNT_FAM_MEMBERS'].shape[0]
c = application_data['DAYS_LAST_PHONE_CHANGE'].isnull().sum() * 100 / application_data['DAYS_LAST_PHONE_CHANGE'].shape[0]

a,b,c
```




    (0.0039022994299390914, 0.000650383238323182, 0.000325191619161591)



### as `AMT_ANNUITY`, `CNT_FAM_MEMBERS` and `DAYS_LAST_PHONE_CHANGE` columns has very few NaN values, we can fill it with mean value



```python
AMT_ANNUITY_mean = application_data['AMT_ANNUITY'].mean()
AMT_ANNUITY_mean
```




    27108.573909183444




```python
CNT_FAM_MEMBERS_mean = application_data['CNT_FAM_MEMBERS'].mean()
CNT_FAM_MEMBERS_mean
```




    2.152665450442101




```python
DAYS_LAST_PHONE_CHANGE_mean = application_data['DAYS_LAST_PHONE_CHANGE'].mean()
DAYS_LAST_PHONE_CHANGE_mean
```




    -962.8587883320868




```python
application_data['AMT_ANNUITY'].fillna(AMT_ANNUITY_mean, inplace=True)
application_data['CNT_FAM_MEMBERS'].fillna(CNT_FAM_MEMBERS_mean, inplace=True)
application_data['DAYS_LAST_PHONE_CHANGE'].fillna(DAYS_LAST_PHONE_CHANGE_mean, inplace=True)
```


```python
application_data.describe()
```





  <div id="df-34468bf8-a045-4d8c-b6dc-1b60e3fb075a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>...</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>278180.518577</td>
      <td>0.080729</td>
      <td>0.417052</td>
      <td>1.687979e+05</td>
      <td>5.990260e+05</td>
      <td>27108.573909</td>
      <td>5.383962e+05</td>
      <td>0.020868</td>
      <td>-16036.995067</td>
      <td>63815.045904</td>
      <td>...</td>
      <td>0.056720</td>
      <td>2.052463</td>
      <td>2.031521</td>
      <td>12.063419</td>
      <td>0.015144</td>
      <td>0.050769</td>
      <td>0.078173</td>
      <td>0.230454</td>
      <td>5.143927e-01</td>
      <td>-962.858788</td>
    </tr>
    <tr>
      <th>std</th>
      <td>102790.175348</td>
      <td>0.272419</td>
      <td>0.722121</td>
      <td>2.371231e+05</td>
      <td>4.024908e+05</td>
      <td>14493.454517</td>
      <td>3.692794e+05</td>
      <td>0.013831</td>
      <td>4363.988632</td>
      <td>141275.766519</td>
      <td>...</td>
      <td>0.231307</td>
      <td>0.509034</td>
      <td>0.502737</td>
      <td>3.265832</td>
      <td>0.122126</td>
      <td>0.219526</td>
      <td>0.268444</td>
      <td>0.421124</td>
      <td>1.908550e-01</td>
      <td>826.807143</td>
    </tr>
    <tr>
      <th>min</th>
      <td>100002.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.565000e+04</td>
      <td>4.500000e+04</td>
      <td>1615.500000</td>
      <td>4.050000e+04</td>
      <td>0.000290</td>
      <td>-25229.000000</td>
      <td>-17912.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.173617e-08</td>
      <td>-4292.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>189145.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.125000e+05</td>
      <td>2.700000e+05</td>
      <td>16524.000000</td>
      <td>2.385000e+05</td>
      <td>0.010006</td>
      <td>-19682.000000</td>
      <td>-2760.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.929737e-01</td>
      <td>-1570.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>278202.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.471500e+05</td>
      <td>5.135310e+05</td>
      <td>24903.000000</td>
      <td>4.500000e+05</td>
      <td>0.018850</td>
      <td>-15750.000000</td>
      <td>-1213.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.654672e-01</td>
      <td>-757.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>367142.500000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.025000e+05</td>
      <td>8.086500e+05</td>
      <td>34596.000000</td>
      <td>6.795000e+05</td>
      <td>0.028663</td>
      <td>-12413.000000</td>
      <td>-289.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>14.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.634218e-01</td>
      <td>-274.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>456255.000000</td>
      <td>1.000000</td>
      <td>19.000000</td>
      <td>1.170000e+08</td>
      <td>4.050000e+06</td>
      <td>258025.500000</td>
      <td>4.050000e+06</td>
      <td>0.072508</td>
      <td>-7489.000000</td>
      <td>365243.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>23.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>8.549997e-01</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 27 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-34468bf8-a045-4d8c-b6dc-1b60e3fb075a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-34468bf8-a045-4d8c-b6dc-1b60e3fb075a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-34468bf8-a045-4d8c-b6dc-1b60e3fb075a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### selecting numeric type columns like `int16`, `int32`, `int64`, `float16`, `float32`, `float64`


```python
numerics = [np.number]
application_data.select_dtypes(include=numerics)
```





  <div id="df-095daab2-6466-4dae-a546-3788eee96c21">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100002</td>
      <td>1</td>
      <td>0</td>
      <td>202500.0</td>
      <td>406597.5</td>
      <td>24700.5</td>
      <td>351000.0</td>
      <td>0.018801</td>
      <td>-9461</td>
      <td>-637</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.262949</td>
      <td>-1134.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100003</td>
      <td>0</td>
      <td>0</td>
      <td>270000.0</td>
      <td>1293502.5</td>
      <td>35698.5</td>
      <td>1129500.0</td>
      <td>0.003541</td>
      <td>-16765</td>
      <td>-1188</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.622246</td>
      <td>-828.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100004</td>
      <td>0</td>
      <td>0</td>
      <td>67500.0</td>
      <td>135000.0</td>
      <td>6750.0</td>
      <td>135000.0</td>
      <td>0.010032</td>
      <td>-19046</td>
      <td>-225</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.555912</td>
      <td>-815.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100006</td>
      <td>0</td>
      <td>0</td>
      <td>135000.0</td>
      <td>312682.5</td>
      <td>29686.5</td>
      <td>297000.0</td>
      <td>0.008019</td>
      <td>-19005</td>
      <td>-3039</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>17</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.650442</td>
      <td>-617.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100007</td>
      <td>0</td>
      <td>0</td>
      <td>121500.0</td>
      <td>513000.0</td>
      <td>21865.5</td>
      <td>513000.0</td>
      <td>0.028663</td>
      <td>-19932</td>
      <td>-3038</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0.322738</td>
      <td>-1106.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>307506</th>
      <td>456251</td>
      <td>0</td>
      <td>0</td>
      <td>157500.0</td>
      <td>254700.0</td>
      <td>27558.0</td>
      <td>225000.0</td>
      <td>0.032561</td>
      <td>-9327</td>
      <td>-236</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.681632</td>
      <td>-273.0</td>
    </tr>
    <tr>
      <th>307507</th>
      <td>456252</td>
      <td>0</td>
      <td>0</td>
      <td>72000.0</td>
      <td>269550.0</td>
      <td>12001.5</td>
      <td>225000.0</td>
      <td>0.025164</td>
      <td>-20775</td>
      <td>365243</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.115992</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>307508</th>
      <td>456253</td>
      <td>0</td>
      <td>0</td>
      <td>153000.0</td>
      <td>677664.0</td>
      <td>29979.0</td>
      <td>585000.0</td>
      <td>0.005002</td>
      <td>-14966</td>
      <td>-7921</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0.535722</td>
      <td>-1909.0</td>
    </tr>
    <tr>
      <th>307509</th>
      <td>456254</td>
      <td>1</td>
      <td>0</td>
      <td>171000.0</td>
      <td>370107.0</td>
      <td>20205.0</td>
      <td>319500.0</td>
      <td>0.005313</td>
      <td>-11961</td>
      <td>-4786</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0.514163</td>
      <td>-322.0</td>
    </tr>
    <tr>
      <th>307510</th>
      <td>456255</td>
      <td>0</td>
      <td>0</td>
      <td>157500.0</td>
      <td>675000.0</td>
      <td>49117.5</td>
      <td>675000.0</td>
      <td>0.046220</td>
      <td>-16856</td>
      <td>-1262</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>20</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0.708569</td>
      <td>-787.0</td>
    </tr>
  </tbody>
</table>
<p>307511 rows × 27 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-095daab2-6466-4dae-a546-3788eee96c21')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-095daab2-6466-4dae-a546-3788eee96c21 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-095daab2-6466-4dae-a546-3788eee96c21');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### assigning into new variable


```python
outlier_df = application_data.select_dtypes(include=numerics)
```


```python
len(outlier_df.columns)
```




    27




```python
outlier_df.describe()
```





  <div id="df-0d75d35f-409c-4ebc-b7aa-f02f3da7744e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_INCOME_TOTAL</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_BIRTH</th>
      <th>DAYS_EMPLOYED</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>...</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
      <td>307511.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>278180.518577</td>
      <td>0.080729</td>
      <td>0.417052</td>
      <td>1.687979e+05</td>
      <td>5.990260e+05</td>
      <td>27108.573909</td>
      <td>5.383962e+05</td>
      <td>0.020868</td>
      <td>-16036.995067</td>
      <td>63815.045904</td>
      <td>...</td>
      <td>0.056720</td>
      <td>2.052463</td>
      <td>2.031521</td>
      <td>12.063419</td>
      <td>0.015144</td>
      <td>0.050769</td>
      <td>0.078173</td>
      <td>0.230454</td>
      <td>5.143927e-01</td>
      <td>-962.858788</td>
    </tr>
    <tr>
      <th>std</th>
      <td>102790.175348</td>
      <td>0.272419</td>
      <td>0.722121</td>
      <td>2.371231e+05</td>
      <td>4.024908e+05</td>
      <td>14493.454517</td>
      <td>3.692794e+05</td>
      <td>0.013831</td>
      <td>4363.988632</td>
      <td>141275.766519</td>
      <td>...</td>
      <td>0.231307</td>
      <td>0.509034</td>
      <td>0.502737</td>
      <td>3.265832</td>
      <td>0.122126</td>
      <td>0.219526</td>
      <td>0.268444</td>
      <td>0.421124</td>
      <td>1.908550e-01</td>
      <td>826.807143</td>
    </tr>
    <tr>
      <th>min</th>
      <td>100002.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.565000e+04</td>
      <td>4.500000e+04</td>
      <td>1615.500000</td>
      <td>4.050000e+04</td>
      <td>0.000290</td>
      <td>-25229.000000</td>
      <td>-17912.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.173617e-08</td>
      <td>-4292.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>189145.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.125000e+05</td>
      <td>2.700000e+05</td>
      <td>16524.000000</td>
      <td>2.385000e+05</td>
      <td>0.010006</td>
      <td>-19682.000000</td>
      <td>-2760.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.929737e-01</td>
      <td>-1570.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>278202.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.471500e+05</td>
      <td>5.135310e+05</td>
      <td>24903.000000</td>
      <td>4.500000e+05</td>
      <td>0.018850</td>
      <td>-15750.000000</td>
      <td>-1213.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.654672e-01</td>
      <td>-757.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>367142.500000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.025000e+05</td>
      <td>8.086500e+05</td>
      <td>34596.000000</td>
      <td>6.795000e+05</td>
      <td>0.028663</td>
      <td>-12413.000000</td>
      <td>-289.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>14.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.634218e-01</td>
      <td>-274.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>456255.000000</td>
      <td>1.000000</td>
      <td>19.000000</td>
      <td>1.170000e+08</td>
      <td>4.050000e+06</td>
      <td>258025.500000</td>
      <td>4.050000e+06</td>
      <td>0.072508</td>
      <td>-7489.000000</td>
      <td>365243.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>23.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>8.549997e-01</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 27 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0d75d35f-409c-4ebc-b7aa-f02f3da7744e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0d75d35f-409c-4ebc-b7aa-f02f3da7744e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0d75d35f-409c-4ebc-b7aa-f02f3da7744e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
import warnings
warnings.filterwarnings("ignore")

for cols in outlier_df:
    f, ax = plt.subplots(1,1,figsize=(8,8))
    f.suptitle(cols, fontsize=16)
    outlier_plot = sns.distplot(outlier_df[cols])
```


    
![png](README_files/README_53_0.png)
    



    
![png](README_files/README_53_1.png)
    



    
![png](README_files/README_53_2.png)
    



    
![png](README_files/README_53_3.png)
    



    
![png](README_files/README_53_4.png)
    



    
![png](README_files/README_53_5.png)
    



    
![png](README_files/README_53_6.png)
    



    
![png](README_files/README_53_7.png)
    



    
![png](README_files/README_53_8.png)
    



    
![png](README_files/README_53_9.png)
    



    
![png](README_files/README_53_10.png)
    



    
![png](README_files/README_53_11.png)
    



    
![png](README_files/README_53_12.png)
    



    
![png](README_files/README_53_13.png)
    



    
![png](README_files/README_53_14.png)
    



    
![png](README_files/README_53_15.png)
    



    
![png](README_files/README_53_16.png)
    



    
![png](README_files/README_53_17.png)
    



    
![png](README_files/README_53_18.png)
    



    
![png](README_files/README_53_19.png)
    



    
![png](README_files/README_53_20.png)
    



    
![png](README_files/README_53_21.png)
    



    
![png](README_files/README_53_22.png)
    



    
![png](README_files/README_53_23.png)
    



    
![png](README_files/README_53_24.png)
    



    
![png](README_files/README_53_25.png)
    



    
![png](README_files/README_53_26.png)
    


> In the plot `DAYS_EMPLOYED` there is a value present at 36k range, which is impossible.
>
> In the plot `CNT_CHILDREN`, we can see a point at high value of outlier, i.e., 19. It's very rare for a family to have `19 children`.
>
> In the plot `AMT_INCOME_TOTAL`, we can see that the highest value is way larger than other points.


```python
application_data[["CNT_CHILDREN", "DAYS_EMPLOYED", "AMT_INCOME_TOTAL"]].describe()
```





  <div id="df-d99a599a-619a-4703-b9e8-93d2d00f904e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CNT_CHILDREN</th>
      <th>DAYS_EMPLOYED</th>
      <th>AMT_INCOME_TOTAL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>307511.000000</td>
      <td>307511.000000</td>
      <td>3.075110e+05</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.417052</td>
      <td>63815.045904</td>
      <td>1.687979e+05</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.722121</td>
      <td>141275.766519</td>
      <td>2.371231e+05</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>-17912.000000</td>
      <td>2.565000e+04</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>-2760.000000</td>
      <td>1.125000e+05</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>-1213.000000</td>
      <td>1.471500e+05</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>-289.000000</td>
      <td>2.025000e+05</td>
    </tr>
    <tr>
      <th>max</th>
      <td>19.000000</td>
      <td>365243.000000</td>
      <td>1.170000e+08</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d99a599a-619a-4703-b9e8-93d2d00f904e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d99a599a-619a-4703-b9e8-93d2d00f904e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d99a599a-619a-4703-b9e8-93d2d00f904e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
q1 = application_data["CNT_CHILDREN"].quantile(0.99)
q1
```




    3.0




```python
CNT_CHILDREN_vcn = application_data['CNT_CHILDREN'].value_counts()
CNT_CHILDREN_vcn
```




    0     215371
    1      61119
    2      26749
    3       3717
    4        429
    5         84
    6         21
    7          7
    14         3
    8          2
    9          2
    12         2
    10         2
    19         2
    11         1
    Name: CNT_CHILDREN, dtype: int64




```python
CNT_CHILDREN_vcn.plot.bar()
plt.show()
```


    
![png](README_files/README_58_0.png)
    



```python
q1 = application_data["CNT_CHILDREN"].quantile(0.99)
application_data["CNT_CHILDREN"] = application_data['CNT_CHILDREN'].apply(lambda x: q1 if x > q1 else x)

f, ax = plt.subplots(figsize = (10,6))
sns.distplot(application_data["CNT_CHILDREN"])
plt.show()
```


    
![png](README_files/README_59_0.png)
    



```python
q2 = application_data["DAYS_EMPLOYED"].quantile(0.80)
application_data["DAYS_EMPLOYED"] = application_data.DAYS_EMPLOYED.apply(lambda x: q2 if x>q2 else x)

f, ax = plt.subplots(figsize = (10,6))
sns.distplot(application_data["DAYS_EMPLOYED"])
plt.show()
```


    
![png](README_files/README_60_0.png)
    



```python
q3 = application_data["AMT_INCOME_TOTAL"].quantile(0.95)
application_data["AMT_INCOME_TOTAL"] = application_data.AMT_INCOME_TOTAL.apply(lambda x: q3 if x>q3 else x)

f, ax = plt.subplots(figsize = (10,6))
sns.distplot(application_data["AMT_INCOME_TOTAL"])
plt.show()
```


    
![png](README_files/README_61_0.png)
    


### converting `DAYS_BIRTH` to `AGE`


```python
application_data[['DAYS_BIRTH']].head()
```





  <div id="df-f1bd6144-2744-498c-bd79-59ac48411396">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DAYS_BIRTH</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-9461</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-16765</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-19046</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-19005</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-19932</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f1bd6144-2744-498c-bd79-59ac48411396')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f1bd6144-2744-498c-bd79-59ac48411396 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f1bd6144-2744-498c-bd79-59ac48411396');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
y = lambda x : int(abs(x) / 365)
application_data["AGE"] = application_data['DAYS_BIRTH'].apply(y) 
application_data["AGE"].dtypes
```




    dtype('int64')




```python
application_data[["AGE"]]
```





  <div id="df-cc8beb99-546b-4951-aa6f-158e1bd7df3c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>52</td>
    </tr>
    <tr>
      <th>4</th>
      <td>54</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>307506</th>
      <td>25</td>
    </tr>
    <tr>
      <th>307507</th>
      <td>56</td>
    </tr>
    <tr>
      <th>307508</th>
      <td>41</td>
    </tr>
    <tr>
      <th>307509</th>
      <td>32</td>
    </tr>
    <tr>
      <th>307510</th>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>307511 rows × 1 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-cc8beb99-546b-4951-aa6f-158e1bd7df3c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-cc8beb99-546b-4951-aa6f-158e1bd7df3c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-cc8beb99-546b-4951-aa6f-158e1bd7df3c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### dropping `DAYS_BIRTH` column, as we have already converted the `DAYS_BIRTH` to `AGE`


```python
application_data.drop("DAYS_BIRTH", axis = 1, inplace = True)
```


```python
application_data['AMT_INCOME_TOTAL'].quantile([0.25,0.5,0.85,1])
```




    0.25    112500.0
    0.50    147150.0
    0.85    234000.0
    1.00    337500.0
    Name: AMT_INCOME_TOTAL, dtype: float64




```python
application_data['CNT_FAM_MEMBERS'].unique()
```




    array([ 1.        ,  2.        ,  3.        ,  4.        ,  5.        ,
            6.        ,  9.        ,  7.        ,  8.        , 10.        ,
           13.        ,  2.15266545, 14.        , 12.        , 20.        ,
           15.        , 16.        , 11.        ])



### as `2.15266545 family member` can't be present, let's round off this values


```python
application_data['CNT_FAM_MEMBERS'] = application_data['CNT_FAM_MEMBERS'].apply(lambda x : round(x,0))
```


```python
application_data['CNT_FAM_MEMBERS'].unique()
```




    array([ 1.,  2.,  3.,  4.,  5.,  6.,  9.,  7.,  8., 10., 13., 14., 12.,
           20., 15., 16., 11.])



### Binning Salary Amount into Categories

### classifying `SALARY_CATEGORY` into their respective categories based on Quantile Values.


```python
def classify_salary_category(x):
    if x < 337500 and x >= 234000:
        return('HIGH')
    elif x < 234000 and x >= 147150:
        return('MODERATE')
    elif x < 147150 and x >= 112500:
        return('LOW')
    else:
        return("EXTREMLY LOW")
```


```python
application_data["SALARY_CATEGORY"] = application_data['AMT_INCOME_TOTAL'].apply(classify_salary_category)    
application_data["SALARY_CATEGORY"]
```




    0             MODERATE
    1                 HIGH
    2         EXTREMLY LOW
    3                  LOW
    4                  LOW
                  ...     
    307506        MODERATE
    307507    EXTREMLY LOW
    307508        MODERATE
    307509        MODERATE
    307510        MODERATE
    Name: SALARY_CATEGORY, Length: 307511, dtype: object




```python
application_data['SALARY_CATEGORY'].value_counts()
```




    MODERATE        106966
    EXTREMLY LOW     85384
    LOW              84194
    HIGH             30967
    Name: SALARY_CATEGORY, dtype: int64



### dropping `AMT_INCOME_TOTAL` Column, as it has already categorized into `SALARY_CATEGORY`


```python
application_data.drop("AMT_INCOME_TOTAL", axis = 1, inplace = True)
```

### analysing the count of `Target` variables


```python
sns.countplot(x = "TARGET", data = application_data)
plt.show()
```


    
![png](README_files/README_81_0.png)
    


> There is a `noticeable imbalance` in our target variable
>
> Therefore, we can split the `Target` variable into two separate dataframes.

## By splitting the `application_data` based on the `Target` variable, we can create two separate dataframes


```python
non_defaulter_client = application_data[application_data['TARGET'] == 0]
non_defaulter_client.head()
```





  <div id="df-126448b7-27e6-4e87-9101-c25baaed3867">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>CODE_GENDER</th>
      <th>FLAG_OWN_CAR</th>
      <th>FLAG_OWN_REALTY</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>...</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>ORGANIZATION_TYPE</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <th>AGE</th>
      <th>SALARY_CATEGORY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>100003</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>N</td>
      <td>0.0</td>
      <td>1293502.5</td>
      <td>35698.5</td>
      <td>1129500.0</td>
      <td>...</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>School</td>
      <td>0.622246</td>
      <td>-828.0</td>
      <td>45</td>
      <td>HIGH</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100004</td>
      <td>0</td>
      <td>Revolving loans</td>
      <td>M</td>
      <td>Y</td>
      <td>Y</td>
      <td>0.0</td>
      <td>135000.0</td>
      <td>6750.0</td>
      <td>135000.0</td>
      <td>...</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Government</td>
      <td>0.555912</td>
      <td>-815.0</td>
      <td>52</td>
      <td>EXTREMLY LOW</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100006</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>312682.5</td>
      <td>29686.5</td>
      <td>297000.0</td>
      <td>...</td>
      <td>17</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.650442</td>
      <td>-617.0</td>
      <td>52</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100007</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>513000.0</td>
      <td>21865.5</td>
      <td>513000.0</td>
      <td>...</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>Religion</td>
      <td>0.322738</td>
      <td>-1106.0</td>
      <td>54</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>5</th>
      <td>100008</td>
      <td>0</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>490495.5</td>
      <td>27517.5</td>
      <td>454500.0</td>
      <td>...</td>
      <td>16</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Other</td>
      <td>0.354225</td>
      <td>-2536.0</td>
      <td>46</td>
      <td>EXTREMLY LOW</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 38 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-126448b7-27e6-4e87-9101-c25baaed3867')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-126448b7-27e6-4e87-9101-c25baaed3867 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-126448b7-27e6-4e87-9101-c25baaed3867');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
non_defaulter_client.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 282686 entries, 1 to 307510
    Data columns (total 38 columns):
     #   Column                       Non-Null Count   Dtype  
    ---  ------                       --------------   -----  
     0   SK_ID_CURR                   282686 non-null  int64  
     1   TARGET                       282686 non-null  int64  
     2   NAME_CONTRACT_TYPE           282686 non-null  object 
     3   CODE_GENDER                  282686 non-null  object 
     4   FLAG_OWN_CAR                 282686 non-null  object 
     5   FLAG_OWN_REALTY              282686 non-null  object 
     6   CNT_CHILDREN                 282686 non-null  float64
     7   AMT_CREDIT                   282686 non-null  float64
     8   AMT_ANNUITY                  282686 non-null  float64
     9   AMT_GOODS_PRICE              282686 non-null  float64
     10  NAME_TYPE_SUITE              282686 non-null  object 
     11  NAME_INCOME_TYPE             282686 non-null  object 
     12  NAME_EDUCATION_TYPE          282686 non-null  object 
     13  NAME_FAMILY_STATUS           282686 non-null  object 
     14  NAME_HOUSING_TYPE            282686 non-null  object 
     15  REGION_POPULATION_RELATIVE   282686 non-null  float64
     16  DAYS_EMPLOYED                282686 non-null  float64
     17  DAYS_REGISTRATION            282686 non-null  float64
     18  DAYS_ID_PUBLISH              282686 non-null  int64  
     19  CNT_FAM_MEMBERS              282686 non-null  float64
     20  FLAG_MOBIL                   282686 non-null  int64  
     21  FLAG_EMP_PHONE               282686 non-null  int64  
     22  FLAG_WORK_PHONE              282686 non-null  int64  
     23  FLAG_CONT_MOBILE             282686 non-null  int64  
     24  FLAG_EMAIL                   282686 non-null  int64  
     25  REGION_RATING_CLIENT         282686 non-null  int64  
     26  REGION_RATING_CLIENT_W_CITY  282686 non-null  int64  
     27  WEEKDAY_APPR_PROCESS_START   282686 non-null  object 
     28  HOUR_APPR_PROCESS_START      282686 non-null  int64  
     29  REG_REGION_NOT_LIVE_REGION   282686 non-null  int64  
     30  REG_REGION_NOT_WORK_REGION   282686 non-null  int64  
     31  REG_CITY_NOT_LIVE_CITY       282686 non-null  int64  
     32  REG_CITY_NOT_WORK_CITY       282686 non-null  int64  
     33  ORGANIZATION_TYPE            282686 non-null  object 
     34  EXT_SOURCE_2                 282686 non-null  float64
     35  DAYS_LAST_PHONE_CHANGE       282686 non-null  float64
     36  AGE                          282686 non-null  int64  
     37  SALARY_CATEGORY              282686 non-null  object 
    dtypes: float64(10), int64(16), object(12)
    memory usage: 84.1+ MB



```python
defaulter_client = application_data[application_data['TARGET'] == 1]
defaulter_client.head()
```





  <div id="df-3aa59159-745a-4de9-99c5-c3f62b6ad893">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>CODE_GENDER</th>
      <th>FLAG_OWN_CAR</th>
      <th>FLAG_OWN_REALTY</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>...</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>ORGANIZATION_TYPE</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <th>AGE</th>
      <th>SALARY_CATEGORY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100002</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>406597.5</td>
      <td>24700.5</td>
      <td>351000.0</td>
      <td>...</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.262949</td>
      <td>-1134.0</td>
      <td>25</td>
      <td>MODERATE</td>
    </tr>
    <tr>
      <th>26</th>
      <td>100031</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>979992.0</td>
      <td>27076.5</td>
      <td>702000.0</td>
      <td>...</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.548477</td>
      <td>-161.0</td>
      <td>51</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>40</th>
      <td>100047</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>1193580.0</td>
      <td>35028.0</td>
      <td>855000.0</td>
      <td>...</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Business Entity Type 3</td>
      <td>0.306841</td>
      <td>-1075.0</td>
      <td>47</td>
      <td>MODERATE</td>
    </tr>
    <tr>
      <th>42</th>
      <td>100049</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>N</td>
      <td>0.0</td>
      <td>288873.0</td>
      <td>16258.5</td>
      <td>238500.0</td>
      <td>...</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Self-employed</td>
      <td>0.674203</td>
      <td>-1480.0</td>
      <td>36</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>81</th>
      <td>100096</td>
      <td>1</td>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>0.0</td>
      <td>252000.0</td>
      <td>14593.5</td>
      <td>252000.0</td>
      <td>...</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>XNA</td>
      <td>0.023952</td>
      <td>0.0</td>
      <td>67</td>
      <td>EXTREMLY LOW</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 38 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3aa59159-745a-4de9-99c5-c3f62b6ad893')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-3aa59159-745a-4de9-99c5-c3f62b6ad893 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3aa59159-745a-4de9-99c5-c3f62b6ad893');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
defaulter_client.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 24825 entries, 0 to 307509
    Data columns (total 38 columns):
     #   Column                       Non-Null Count  Dtype  
    ---  ------                       --------------  -----  
     0   SK_ID_CURR                   24825 non-null  int64  
     1   TARGET                       24825 non-null  int64  
     2   NAME_CONTRACT_TYPE           24825 non-null  object 
     3   CODE_GENDER                  24825 non-null  object 
     4   FLAG_OWN_CAR                 24825 non-null  object 
     5   FLAG_OWN_REALTY              24825 non-null  object 
     6   CNT_CHILDREN                 24825 non-null  float64
     7   AMT_CREDIT                   24825 non-null  float64
     8   AMT_ANNUITY                  24825 non-null  float64
     9   AMT_GOODS_PRICE              24825 non-null  float64
     10  NAME_TYPE_SUITE              24825 non-null  object 
     11  NAME_INCOME_TYPE             24825 non-null  object 
     12  NAME_EDUCATION_TYPE          24825 non-null  object 
     13  NAME_FAMILY_STATUS           24825 non-null  object 
     14  NAME_HOUSING_TYPE            24825 non-null  object 
     15  REGION_POPULATION_RELATIVE   24825 non-null  float64
     16  DAYS_EMPLOYED                24825 non-null  float64
     17  DAYS_REGISTRATION            24825 non-null  float64
     18  DAYS_ID_PUBLISH              24825 non-null  int64  
     19  CNT_FAM_MEMBERS              24825 non-null  float64
     20  FLAG_MOBIL                   24825 non-null  int64  
     21  FLAG_EMP_PHONE               24825 non-null  int64  
     22  FLAG_WORK_PHONE              24825 non-null  int64  
     23  FLAG_CONT_MOBILE             24825 non-null  int64  
     24  FLAG_EMAIL                   24825 non-null  int64  
     25  REGION_RATING_CLIENT         24825 non-null  int64  
     26  REGION_RATING_CLIENT_W_CITY  24825 non-null  int64  
     27  WEEKDAY_APPR_PROCESS_START   24825 non-null  object 
     28  HOUR_APPR_PROCESS_START      24825 non-null  int64  
     29  REG_REGION_NOT_LIVE_REGION   24825 non-null  int64  
     30  REG_REGION_NOT_WORK_REGION   24825 non-null  int64  
     31  REG_CITY_NOT_LIVE_CITY       24825 non-null  int64  
     32  REG_CITY_NOT_WORK_CITY       24825 non-null  int64  
     33  ORGANIZATION_TYPE            24825 non-null  object 
     34  EXT_SOURCE_2                 24825 non-null  float64
     35  DAYS_LAST_PHONE_CHANGE       24825 non-null  float64
     36  AGE                          24825 non-null  int64  
     37  SALARY_CATEGORY              24825 non-null  object 
    dtypes: float64(10), int64(16), object(12)
    memory usage: 7.4+ MB


## Identifying clients who are deemed unlikely to repay their loans


```python
Univariate_defaulter_Num_1_df = defaulter_client.select_dtypes(include = [np.number])
Univariate_defaulter_Num_1_df.head()
```





  <div id="df-72cb5e01-0afa-4271-8128-37b7dbf4f9d0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_EMPLOYED</th>
      <th>DAYS_REGISTRATION</th>
      <th>DAYS_ID_PUBLISH</th>
      <th>...</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <th>AGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100002</td>
      <td>1</td>
      <td>0.0</td>
      <td>406597.5</td>
      <td>24700.5</td>
      <td>351000.0</td>
      <td>0.018801</td>
      <td>-637.0</td>
      <td>-3648.0</td>
      <td>-2120</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.262949</td>
      <td>-1134.0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>26</th>
      <td>100031</td>
      <td>1</td>
      <td>0.0</td>
      <td>979992.0</td>
      <td>27076.5</td>
      <td>702000.0</td>
      <td>0.018029</td>
      <td>-2628.0</td>
      <td>-6573.0</td>
      <td>-1827</td>
      <td>...</td>
      <td>3</td>
      <td>2</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.548477</td>
      <td>-161.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>40</th>
      <td>100047</td>
      <td>1</td>
      <td>0.0</td>
      <td>1193580.0</td>
      <td>35028.0</td>
      <td>855000.0</td>
      <td>0.025164</td>
      <td>-1262.0</td>
      <td>-1182.0</td>
      <td>-1029</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.306841</td>
      <td>-1075.0</td>
      <td>47</td>
    </tr>
    <tr>
      <th>42</th>
      <td>100049</td>
      <td>1</td>
      <td>0.0</td>
      <td>288873.0</td>
      <td>16258.5</td>
      <td>238500.0</td>
      <td>0.007305</td>
      <td>-3597.0</td>
      <td>-45.0</td>
      <td>-4409</td>
      <td>...</td>
      <td>3</td>
      <td>3</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.674203</td>
      <td>-1480.0</td>
      <td>36</td>
    </tr>
    <tr>
      <th>81</th>
      <td>100096</td>
      <td>1</td>
      <td>0.0</td>
      <td>252000.0</td>
      <td>14593.5</td>
      <td>252000.0</td>
      <td>0.028663</td>
      <td>-144.0</td>
      <td>-5391.0</td>
      <td>-4199</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.023952</td>
      <td>0.0</td>
      <td>67</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-72cb5e01-0afa-4271-8128-37b7dbf4f9d0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-72cb5e01-0afa-4271-8128-37b7dbf4f9d0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-72cb5e01-0afa-4271-8128-37b7dbf4f9d0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
Univariate_defaulter_Cat_1_df = defaulter_client.select_dtypes(include = ["object"])
Univariate_defaulter_Cat_1_df.head()
```





  <div id="df-d0c5af76-ab15-47fa-9b2e-48bf6d4ad14d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>CODE_GENDER</th>
      <th>FLAG_OWN_CAR</th>
      <th>FLAG_OWN_REALTY</th>
      <th>NAME_TYPE_SUITE</th>
      <th>NAME_INCOME_TYPE</th>
      <th>NAME_EDUCATION_TYPE</th>
      <th>NAME_FAMILY_STATUS</th>
      <th>NAME_HOUSING_TYPE</th>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <th>ORGANIZATION_TYPE</th>
      <th>SALARY_CATEGORY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>Unaccompanied</td>
      <td>Working</td>
      <td>Secondary / secondary special</td>
      <td>Single / not married</td>
      <td>House / apartment</td>
      <td>WEDNESDAY</td>
      <td>Business Entity Type 3</td>
      <td>MODERATE</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>Unaccompanied</td>
      <td>Working</td>
      <td>Secondary / secondary special</td>
      <td>Widow</td>
      <td>House / apartment</td>
      <td>MONDAY</td>
      <td>Business Entity Type 3</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Cash loans</td>
      <td>M</td>
      <td>N</td>
      <td>Y</td>
      <td>Unaccompanied</td>
      <td>Commercial associate</td>
      <td>Secondary / secondary special</td>
      <td>Married</td>
      <td>House / apartment</td>
      <td>TUESDAY</td>
      <td>Business Entity Type 3</td>
      <td>MODERATE</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>N</td>
      <td>Unaccompanied</td>
      <td>Working</td>
      <td>Secondary / secondary special</td>
      <td>Civil marriage</td>
      <td>House / apartment</td>
      <td>THURSDAY</td>
      <td>Self-employed</td>
      <td>LOW</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Cash loans</td>
      <td>F</td>
      <td>N</td>
      <td>Y</td>
      <td>Unaccompanied</td>
      <td>Pensioner</td>
      <td>Secondary / secondary special</td>
      <td>Married</td>
      <td>House / apartment</td>
      <td>THURSDAY</td>
      <td>XNA</td>
      <td>EXTREMLY LOW</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d0c5af76-ab15-47fa-9b2e-48bf6d4ad14d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d0c5af76-ab15-47fa-9b2e-48bf6d4ad14d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d0c5af76-ab15-47fa-9b2e-48bf6d4ad14d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




**_FLAG_OWN_REALTY_**

### Let's analyze and assess the impact of property ownership on loan repayment.

creating a graph to display the count of property owners and non-property owners within the entire population



```python
sns.countplot(x = "FLAG_OWN_REALTY", data = application_data)
plt.show()
```


    
![png](README_files/README_93_0.png)
    


### based on the above plot, it is evident that clients with some form of real estate holdings outnumber those who do not have any property.

calculating the percentage of property and non-property owners in the defaulter list


```python
df_FLAG_OWN_REALTY_vc = Univariate_defaulter_Cat_1_df["FLAG_OWN_REALTY"].value_counts()
df_FLAG_OWN_REALTY_vc
```




    Y    16983
    N     7842
    Name: FLAG_OWN_REALTY, dtype: int64




```python
app_FLAG_OWN_REALTY_vc = application_data["FLAG_OWN_REALTY"].value_counts()
app_FLAG_OWN_REALTY_vc
```




    Y    213312
    N     94199
    Name: FLAG_OWN_REALTY, dtype: int64




```python
FLAG_OWN_REALTY_vc = 100 * (df_FLAG_OWN_REALTY_vc / app_FLAG_OWN_REALTY_vc)
test_df1 = round(FLAG_OWN_REALTY_vc, 2)
test_df1
```




    Y    7.96
    N    8.32
    Name: FLAG_OWN_REALTY, dtype: float64




```python
test_df1 = pd.DataFrame(test_df1)
test_df1.reset_index(level = 0, inplace = True)
test_df1
```





  <div id="df-45ccdd13-071a-4e24-a4de-ad0a6972d5c3">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>FLAG_OWN_REALTY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Y</td>
      <td>7.96</td>
    </tr>
    <tr>
      <th>1</th>
      <td>N</td>
      <td>8.32</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-45ccdd13-071a-4e24-a4de-ad0a6972d5c3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-45ccdd13-071a-4e24-a4de-ad0a6972d5c3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-45ccdd13-071a-4e24-a4de-ad0a6972d5c3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
test_df1.rename(columns =  {
    "index" : "FLAG_OWN_REALTY", 
    "FLAG_OWN_REALTY" : "Default_Percentage"
  }, inplace = True,
)

test_df1
```





  <div id="df-474f3603-cf72-4e3b-9b1c-45a035d203a4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FLAG_OWN_REALTY</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Y</td>
      <td>7.96</td>
    </tr>
    <tr>
      <th>1</th>
      <td>N</td>
      <td>8.32</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-474f3603-cf72-4e3b-9b1c-45a035d203a4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-474f3603-cf72-4e3b-9b1c-45a035d203a4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-474f3603-cf72-4e3b-9b1c-45a035d203a4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### creating a plot illustrating the number of property owners and non-property owners based on the target variable, specifically when the target variable is equal to 1.


```python
sns.barplot(x = "FLAG_OWN_REALTY", y = "Default_Percentage", data = test_df1)
plt.show()
```


    
![png](README_files/README_101_0.png)
    


Based on the above graph, it is evident that the number of loan defaulters, represented by non-payers of the loan, is approximately 9% and is closely comparable to the other category. Therefore, using this metric alone makes it challenging to determine a clear target.

**_CODE_GENDER_**

### Let's analyze and assess how the gender of the client impacts loan repayment.

Create a graph to display the distribution of males and females in the entire population.


```python
sns.countplot(x = "CODE_GENDER", data = application_data)
plt.show()
```


    
![png](README_files/README_105_0.png)
    


### Calculating the percentage of males and females within the list of individuals who have defaulted on their loans


```python
test_df2 = round((Univariate_defaulter_Cat_1_df["CODE_GENDER"].value_counts() / application_data["CODE_GENDER"].value_counts()) * 100, 2)
test_df2 = pd.DataFrame(test_df2)
test_df2.reset_index(level=0, inplace=True)

test_df2.rename(columns = {
    "index" : "CODE_GENDER", 
    "CODE_GENDER" : "Default_Percentage"
  }, inplace = True
) 

test_df2
```





  <div id="df-fc03f14a-1c37-423f-a204-b0ebda46f94f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CODE_GENDER</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>10.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>XNA</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fc03f14a-1c37-423f-a204-b0ebda46f94f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fc03f14a-1c37-423f-a204-b0ebda46f94f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fc03f14a-1c37-423f-a204-b0ebda46f94f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### creating a plot illustrating the number of male and female clients based on the target variable, specifically when the target variable is equal to 1


```python
sns.barplot(x = "CODE_GENDER", y = "Default_Percentage", data = test_df2)
plt.show()
```


    
![png](README_files/README_109_0.png)
    


Based on the above plots and data, it is evident that female clients are more likely to be a better target compared to male clients. 

The percentage of defaulted credits is higher for male clients (10.14%) compared to female clients (7%). 

This indicates that male clients have a higher likelihood of not repaying their loans.

**_FLAG_OWN_CAR_**

### Let's analyze and assess the differences in loan repayment between car owners and non-car owners.

creating a graph to display the distribution of car owners and non-car owners within the entire population.


```python
sns.countplot(x = "FLAG_OWN_CAR", data = application_data)
plt.show()
```


    
![png](README_files/README_113_0.png)
    


The given population predominantly consists of clients who do not own cars or vehicles.

### Calculate the percentage of car owners and non-car owners within the list of individuals who have defaulted on their loans.


```python
test_df3 = round((Univariate_defaulter_Cat_1_df["FLAG_OWN_CAR"].value_counts() / application_data["FLAG_OWN_CAR"].value_counts()) * 100, 2)
test_df3 = pd.DataFrame(test_df3)
test_df3.reset_index(level=0, inplace = True)

test_df3.rename(columns = {
    "index" : "FLAG_OWN_CAR", 
    "FLAG_OWN_CAR" : "Default_Percentage"
  }, inplace = True
) 

test_df3
```





  <div id="df-ebf0bf63-d0b1-4832-af55-8656d126d88e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FLAG_OWN_CAR</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>N</td>
      <td>8.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Y</td>
      <td>7.24</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ebf0bf63-d0b1-4832-af55-8656d126d88e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ebf0bf63-d0b1-4832-af55-8656d126d88e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ebf0bf63-d0b1-4832-af55-8656d126d88e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




creating a plot to illustrate the distribution of car owners and non-car owners based on the target variable, specifically when the target variable is equal to 1.


```python
sns.barplot(x = "FLAG_OWN_CAR", y = "Default_Percentage", data = test_df3)
plt.show()
```


    
![png](README_files/README_118_0.png)
    


Based on the above graph, it is apparent that clients who own a car are less likely to default on their loans compared to those who do not own a car. The rates of loan non-repayment are similar for both car owners and non-car owners. This finding is intriguing and suggests that using car ownership as a metric may not be suitable when targeting clients.

**_NAME_FAMILY_STATUS_**

Let's analyze and assess how the family status of clients impacts their loan repayment.


```python
x = application_data['NAME_FAMILY_STATUS'].value_counts()
x = pd.DataFrame(x)
x.reset_index(level=0, inplace=True)

x.rename(columns = {
    "index" : "NAME_FAMILY_STATUS", 
    "NAME_FAMILY_STATUS" : "number"
  }, inplace = True
) 

x
```





  <div id="df-e4fceade-36d5-466a-b4b8-27fc5417cf79">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_FAMILY_STATUS</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Married</td>
      <td>196432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Single / not married</td>
      <td>45444</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Civil marriage</td>
      <td>29775</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Separated</td>
      <td>19770</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Widow</td>
      <td>16088</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Unknown</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e4fceade-36d5-466a-b4b8-27fc5417cf79')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e4fceade-36d5-466a-b4b8-27fc5417cf79 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e4fceade-36d5-466a-b4b8-27fc5417cf79');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### create a graph to display the distribution of family statuses among the clients in the entire population


```python
FamilyStatus_vs_Total = sns.barplot(x = "NAME_FAMILY_STATUS", y = "number", data = x)
FamilyStatus_vs_Total.set_xticklabels(FamilyStatus_vs_Total.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_124_0.png)
    


The majority of clients in the population are married, followed by those who are single and in civil marriages.

### calculating the percentage of clients categorized by family status within the list of individuals who have defaulted on their loans


```python
test_df4 = round((Univariate_defaulter_Cat_1_df["NAME_FAMILY_STATUS"].value_counts() / application_data["NAME_FAMILY_STATUS"].value_counts()) * 100, 2)
test_df4 = pd.DataFrame(test_df4)
test_df4.reset_index(level = 0, inplace = True)

test_df4.rename(columns = {
    "index" : "NAME_FAMILY_STATUS", 
    "NAME_FAMILY_STATUS" : "Default_Percentage"
  }, inplace = True
) 

test_df4.sort_values(by = 'Default_Percentage', inplace = True)
test_df4
```





  <div id="df-5e944422-30a6-482a-87e3-82855ed4baaa">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_FAMILY_STATUS</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>Widow</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Married</td>
      <td>7.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Separated</td>
      <td>8.19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Single / not married</td>
      <td>9.81</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Civil marriage</td>
      <td>9.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Unknown</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5e944422-30a6-482a-87e3-82855ed4baaa')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5e944422-30a6-482a-87e3-82855ed4baaa button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5e944422-30a6-482a-87e3-82855ed4baaa');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### creating a plot to illustrate the relationship between the family status of clients and the target variable, specifically when the target variable is equal to 1.


```python
FamilyStatus_vs_Target = sns.barplot(x = "NAME_FAMILY_STATUS", y = "Default_Percentage", data = test_df4)
FamilyStatus_vs_Target.set_xticklabels(FamilyStatus_vs_Target.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_129_0.png)
    


Based on the above graph, we can observe that the percentage of loan non-repayment is highest for clients with a civil marriage status and lowest for widows. This finding is intriguing because typically one might expect widows to have difficulty in loan repayment, but the data suggests the opposite trend.

**_CNT_CHILDREN_**

Now, let's analyze and compare how the number of children in a family impacts the likelihood of loan non-repayment.

### Create a graph to display the distribution of the number of children per client in the entire population.


```python
sns.countplot(x = "CNT_CHILDREN", data = application_data)
plt.show()
```


    
![png](README_files/README_134_0.png)
    


### Calculate the percentage of the number of children per client within the list of individuals who have defaulted on their loans.


```python
test_df5 = round((Univariate_defaulter_Num_1_df["CNT_CHILDREN"].value_counts() / application_data["CNT_CHILDREN"].value_counts()) * 100, 2)
test_df5 = pd.DataFrame(test_df5)
test_df5.reset_index(level = 0, inplace = True)

test_df5.rename(columns = {
    "index" : "CNT_CHILDREN", 
    "CNT_CHILDREN" : "Default_Percentage"
  }, inplace = True
)

test_df5.sort_values(by = ["Default_Percentage"], ascending = False, inplace = True)
test_df5
```





  <div id="df-8d0036e6-6571-4a45-9f1c-07011104fbed">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CNT_CHILDREN</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>10.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>8.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>8.72</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>7.71</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-8d0036e6-6571-4a45-9f1c-07011104fbed')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-8d0036e6-6571-4a45-9f1c-07011104fbed button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-8d0036e6-6571-4a45-9f1c-07011104fbed');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Create a plot illustrating the relationship between the number of children per client and the target variable, specifically when the target variable is equal to 1.


```python
sns.distplot(test_df5["Default_Percentage"])
plt.show()
```


    
![png](README_files/README_138_0.png)
    


Clients with a higher number of children are more likely to face difficulties in repaying their loans. 

This could be attributed to the increased financial responsibilities and liabilities associated with having more children. 

The greater number of dependents makes it more challenging for the client to allocate funds for loan repayment, as they have additional personal expenditures to manage.

**_CNT_FAM_MEMBERS_**


```python
y = application_data.CNT_FAM_MEMBERS.value_counts()
y = pd.DataFrame(y)
y.reset_index(level = 0, inplace = True)

y.rename(columns = {
    "index" : "CNT_FAM_MEMBERS", 
    "CNT_FAM_MEMBERS" : "number"
  }, inplace = True
) 

y
```





  <div id="df-11b69157-5029-4d7a-b7fb-3b05cdd5bedf">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CNT_FAM_MEMBERS</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.0</td>
      <td>158359</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>67847</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>52601</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>24697</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3478</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>408</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>81</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>13</th>
      <td>16.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>13.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>11.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-11b69157-5029-4d7a-b7fb-3b05cdd5bedf')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-11b69157-5029-4d7a-b7fb-3b05cdd5bedf button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-11b69157-5029-4d7a-b7fb-3b05cdd5bedf');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Create a graph to display the distribution of the number of family members per client in the entire population.


```python
NoOfFamilyMembers_vs_Total = sns.barplot(x = "CNT_FAM_MEMBERS", y = "number", data = y)
NoOfFamilyMembers_vs_Total.set_xticklabels(NoOfFamilyMembers_vs_Total.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_143_0.png)
    


### Calculate the percentage of the number of family members per client within the list of individuals who have defaulted on their loans.


```python
test_df6 = round((Univariate_defaulter_Num_1_df["CNT_FAM_MEMBERS"].value_counts() / application_data["CNT_FAM_MEMBERS"].value_counts()) * 100, 2)
test_df6 = pd.DataFrame(test_df6)
test_df6.reset_index(level = 0, inplace = True)

test_df6.rename(columns = {
    "index" : "CNT_FAM_MEMBERS", 
    "CNT_FAM_MEMBERS" : "Default_Percentage"
  }, inplace = True
)
 
test_df6.sort_values(by = ["Default_Percentage"], ascending = False, inplace = True)
test_df6
```





  <div id="df-f04ac5b6-9d4f-4f36-b1f2-c9f1493f8943">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CNT_FAM_MEMBERS</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>11.0</td>
      <td>100.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13.0</td>
      <td>100.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10.0</td>
      <td>33.33</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.0</td>
      <td>30.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>13.48</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>9.40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>8.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>8.65</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>8.36</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f04ac5b6-9d4f-4f36-b1f2-c9f1493f8943')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f04ac5b6-9d4f-4f36-b1f2-c9f1493f8943 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f04ac5b6-9d4f-4f36-b1f2-c9f1493f8943');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Calculate the percentage of the number of family members per client within the list of individuals who have defaulted on their loans.


```python
NoOfFamilyMembers_vs_Target = sns.barplot(x = "CNT_FAM_MEMBERS", y = "Default_Percentage", data = test_df6)
NoOfFamilyMembers_vs_Target.set_xticklabels(NoOfFamilyMembers_vs_Target.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_147_0.png)
    


> While it is evident that families with `11 and 13` members have the highest default rate, it is important to note that the number of such families is quite low, with only `two` in the dataset.

_NAME_EDUCATION_TYPE_

### Create a graph to display the distribution of education types within the entire population.


```python
EducationType_vs_Total = sns.countplot(x = "NAME_EDUCATION_TYPE", data = application_data)
EducationType_vs_Total.set_xticklabels(EducationType_vs_Total.get_xticklabels(),rotation = 90)
plt.show()
```


    
![png](README_files/README_151_0.png)
    


### Calculate the percentage of clients' education levels within the list of individuals who have defaulted on their loans.


```python
test_df7 = round((Univariate_defaulter_Cat_1_df["NAME_EDUCATION_TYPE"].value_counts() / application_data["NAME_EDUCATION_TYPE"].value_counts()) * 100, 2)
test_df7 = pd.DataFrame(test_df7)
test_df7.reset_index(level = 0, inplace = True)
test_df7.sort_values(by = ["NAME_EDUCATION_TYPE"], ascending = False, inplace = True)

test_df7.rename(columns = {
    "index" : "NAME_EDUCATION_TYPE", 
    "NAME_EDUCATION_TYPE" : "Default_Percentage"
  }, inplace = True
) 

test_df7
```





  <div id="df-f758b1e8-f9a0-41d1-8107-0417b9346b75">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_EDUCATION_TYPE</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Lower secondary</td>
      <td>10.93</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Secondary / secondary special</td>
      <td>8.94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Incomplete higher</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Higher education</td>
      <td>5.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Academic degree</td>
      <td>1.83</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f758b1e8-f9a0-41d1-8107-0417b9346b75')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f758b1e8-f9a0-41d1-8107-0417b9346b75 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f758b1e8-f9a0-41d1-8107-0417b9346b75');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Create a plot illustrating the relationship between the education type of each client and the target variable, specifically when the target variable is equal to 1.


```python
f, ax = plt.subplots(figsize=(8,6))
EducationType_vs_Target = sns.barplot(
  x = "NAME_EDUCATION_TYPE",
  y = "Default_Percentage", 
  data = test_df7, 
  order = test_df7['NAME_EDUCATION_TYPE']
)

EducationType_vs_Target.set_xticklabels(EducationType_vs_Target.get_xticklabels(), rotation = 45)
plt.show()
```


    
![png](README_files/README_155_0.png)
    


The above graph indicates that clients with higher education levels are more likely to repay their loans. 

This observation can be attributed to the likelihood of such clients having more stable jobs and a consistent monthly income.

**_NAME_TYPE_SUITE_**


```python
TypeSuite_vs_Total = sns.countplot(x = "NAME_TYPE_SUITE", data = application_data)
TypeSuite_vs_Total.set_xticklabels(TypeSuite_vs_Total.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_158_0.png)
    



```python
test_df8 = round((Univariate_defaulter_Cat_1_df["NAME_TYPE_SUITE"].value_counts() / application_data["NAME_TYPE_SUITE"].value_counts()) * 100, 2)
test_df8 = pd.DataFrame(test_df8)
test_df8.reset_index(level = 0, inplace = True)
test_df8.sort_values(by = ["NAME_TYPE_SUITE"], ascending = False, inplace = True)

test_df8.rename(columns = {
    "index" : "NAME_TYPE_SUITE", 
    "NAME_TYPE_SUITE" : "Default_Percentage"
  }, inplace = True
) 

test_df8
```





  <div id="df-2fb782ce-645b-4077-ade9-088535a7c2b2">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_TYPE_SUITE</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Other_B</td>
      <td>9.83</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Other_A</td>
      <td>8.78</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Group of people</td>
      <td>8.49</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Unaccompanied</td>
      <td>8.17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spouse, partner</td>
      <td>7.87</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Family</td>
      <td>7.49</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Children</td>
      <td>7.38</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-2fb782ce-645b-4077-ade9-088535a7c2b2')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-2fb782ce-645b-4077-ade9-088535a7c2b2 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-2fb782ce-645b-4077-ade9-088535a7c2b2');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (8,6))
TypeSuite_vs_Target= sns.barplot(
  x = "NAME_TYPE_SUITE", 
  y = "Default_Percentage", 
  data = test_df8, 
  order = test_df8['NAME_TYPE_SUITE']
)

TypeSuite_vs_Target.set_xticklabels(TypeSuite_vs_Target.get_xticklabels(), rotation = 45)
plt.show()
```


    
![png](README_files/README_160_0.png)
    


**_ORGANISATION_TYPE_**


```python
test_df9 = round((Univariate_defaulter_Cat_1_df["ORGANIZATION_TYPE"].value_counts() / application_data["ORGANIZATION_TYPE"].value_counts()) * 100, 2)
test_df9 = pd.DataFrame(test_df9)
test_df9.reset_index(level = 0, inplace = True)

test_df9.sort_values(by = ["ORGANIZATION_TYPE"], ascending = False, inplace = True)
test_df9.rename(columns = {
    "index" : "ORGANIZATION_TYPE", 
    "ORGANIZATION_TYPE" : "Default_Percentage"
  }, inplace = True
) 

test_df9
```





  <div id="df-c03c0caf-4bb7-4193-9ddd-4b6f2ae718e5">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ORGANIZATION_TYPE</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>Transport: type 3</td>
      <td>15.75</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Industry: type 13</td>
      <td>13.43</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Industry: type 8</td>
      <td>12.50</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Restaurant</td>
      <td>11.71</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Construction</td>
      <td>11.68</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cleaning</td>
      <td>11.15</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Industry: type 1</td>
      <td>11.07</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Industry: type 3</td>
      <td>10.62</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Realtor</td>
      <td>10.61</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Agriculture</td>
      <td>10.47</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Trade: type 3</td>
      <td>10.34</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Self-employed</td>
      <td>10.17</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Industry: type 4</td>
      <td>10.15</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Security</td>
      <td>9.98</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Trade: type 7</td>
      <td>9.45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Business Entity Type 3</td>
      <td>9.30</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Transport: type 4</td>
      <td>9.28</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Mobile</td>
      <td>9.15</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Trade: type 1</td>
      <td>8.91</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Industry: type 11</td>
      <td>8.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Business Entity Type 2</td>
      <td>8.53</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Postal</td>
      <td>8.44</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Advertising</td>
      <td>8.16</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Business Entity Type 1</td>
      <td>8.14</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Industry: type 7</td>
      <td>8.03</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Housing</td>
      <td>7.94</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Legal Services</td>
      <td>7.87</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Transport: type 2</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Other</td>
      <td>7.64</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Telecom</td>
      <td>7.63</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Industry: type 2</td>
      <td>7.21</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Industry: type 6</td>
      <td>7.14</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Emergency</td>
      <td>7.14</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Kindergarten</td>
      <td>7.03</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Trade: type 2</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Government</td>
      <td>6.98</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Industry: type 5</td>
      <td>6.84</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Industry: type 9</td>
      <td>6.68</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Electricity</td>
      <td>6.63</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Services</td>
      <td>6.60</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Medicine</td>
      <td>6.58</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Industry: type 10</td>
      <td>6.42</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Hotel</td>
      <td>6.42</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Trade: type 5</td>
      <td>6.12</td>
    </tr>
    <tr>
      <th>39</th>
      <td>School</td>
      <td>5.91</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Religion</td>
      <td>5.88</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Insurance</td>
      <td>5.70</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Culture</td>
      <td>5.54</td>
    </tr>
    <tr>
      <th>57</th>
      <td>XNA</td>
      <td>5.40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bank</td>
      <td>5.19</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Military</td>
      <td>5.13</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Police</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>56</th>
      <td>University</td>
      <td>4.90</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Security Ministries</td>
      <td>4.86</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Trade: type 6</td>
      <td>4.60</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Transport: type 1</td>
      <td>4.48</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Industry: type 12</td>
      <td>3.79</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Trade: type 4</td>
      <td>3.12</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c03c0caf-4bb7-4193-9ddd-4b6f2ae718e5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c03c0caf-4bb7-4193-9ddd-4b6f2ae718e5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c03c0caf-4bb7-4193-9ddd-4b6f2ae718e5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (22, 6))
OrganizationType_vs_Target = sns.barplot(
  x = "ORGANIZATION_TYPE", 
  y = "Default_Percentage", 
  data=test_df9,
  order=test_df9['ORGANIZATION_TYPE']
)

OrganizationType_vs_Target.set_xticklabels(OrganizationType_vs_Target.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_163_0.png)
    


Based on the above graph, the highest number of loan non-repayments can be observed among applicants working in Transport Type3.

_NAME_HOUSING_TYPE_

### Create a graph to display the distribution of housing types among each client in the entire population.


```python
HousingType_vs_Total = sns.countplot(x = "NAME_HOUSING_TYPE", data = application_data)
HousingType_vs_Total.set_xticklabels(HousingType_vs_Total.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_167_0.png)
    


### Calculate the percentage of each housing type among the clients in the defaulter list.


```python
test_df10 = round((Univariate_defaulter_Cat_1_df["NAME_HOUSING_TYPE"].value_counts() / application_data["NAME_HOUSING_TYPE"].value_counts()) * 100, 2)
test_df10 = pd.DataFrame(test_df10)
test_df10.reset_index(level = 0, inplace = True)

test_df10.rename(columns = {
    "index" : "NAME_HOUSING_TYPE", 
    "NAME_HOUSING_TYPE" : "Default_Percentage"
  }, inplace = True
) 

test_df10.sort_values(by = 'Default_Percentage' , inplace = True, ascending = False)
test_df10
```





  <div id="df-81e18fae-1f1b-41bf-bbbf-9778fd19267b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_HOUSING_TYPE</th>
      <th>Default_Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Rented apartment</td>
      <td>12.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>With parents</td>
      <td>11.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Municipal apartment</td>
      <td>8.54</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Co-op apartment</td>
      <td>7.93</td>
    </tr>
    <tr>
      <th>0</th>
      <td>House / apartment</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Office apartment</td>
      <td>6.57</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-81e18fae-1f1b-41bf-bbbf-9778fd19267b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-81e18fae-1f1b-41bf-bbbf-9778fd19267b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-81e18fae-1f1b-41bf-bbbf-9778fd19267b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Create a plot illustrating the relationship between the housing type of each client and the target variable, specifically when the target variable is equal to 1.


```python
HousingType_vs_Target = sns.barplot(x = "NAME_HOUSING_TYPE", y = "Default_Percentage", data = test_df10)
HousingType_vs_Target.set_xticklabels(HousingType_vs_Target.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_171_0.png)
    


Based on the above graph, it is evident that individuals with rented apartments are less likely to repay their loans. 

This could be attributed to the fact that they already have additional liabilities, which may impact their ability to fulfill loan repayment obligations compared to individuals who do not have this specific liability.

## **BIVARIATE ANALYSIS**


```python
f, ax = plt.subplots(figsize = (15, 10))
sns.scatterplot(x = "AMT_CREDIT", y = "AMT_GOODS_PRICE", data = application_data, hue="TARGET")
plt.show()
```


    
![png](README_files/README_174_0.png)
    


### Comparing the salary category with clients who provided their home number.


```python
f, ax = plt.subplots(figsize = (10, 9))
sns.barplot(x = "SALARY_CATEGORY", y = "FLAG_WORK_PHONE", data = application_data, hue = "TARGET")
plt.show()
```


    
![png](README_files/README_176_0.png)
    


Clients with an extremely low salary are more likely to be defaulters, particularly when they did not provide a home phone number. 

It is worth noting that only approximately 30% of people provided their phone numbers.

### Comparing the salary of clients whose permanent address does not match their contact address at the region level.


```python
f, ax = plt.subplots(figsize = (10, 9))
sns.barplot(x = "SALARY_CATEGORY", y="REG_REGION_NOT_LIVE_REGION", data = application_data, hue = "TARGET")
plt.show()
```


    
![png](README_files/README_179_0.png)
    


When a client receives an extremely low salary and their address does not match, there is a higher likelihood for them to be a defaulter.

### Analyzing the relationship between salary and clients whose permanent address does not match their work address at the region level.


```python
f, ax = plt.subplots(figsize = (10, 9))
sns.barplot(x = "SALARY_CATEGORY", y = "REG_REGION_NOT_WORK_REGION", data = application_data, hue = "TARGET")
plt.show()
```


    
![png](README_files/README_182_0.png)
    


When a client receives an extremely low salary and their work address does not match, there is a higher likelihood for them to be a defaulter.

### Examining the correlation between salary and clients whose permanent address does not match their contact address at the city level.


```python
f, ax = plt.subplots(figsize = (10, 9))
sns.barplot(x = "SALARY_CATEGORY", y = "REG_CITY_NOT_LIVE_CITY", data = application_data, hue = "TARGET")
plt.show()
```


    
![png](README_files/README_185_0.png)
    


When a client receives a lower salary and their CONTACT address (CITY LEVEL) does not match, there is a higher probability of them being a defaulter.

### Analyzing the relationship between salary and clients whose permanent address does not match their work address at the city level.


```python
f, ax = plt.subplots(figsize = (10, 9))
sns.barplot(x = "SALARY_CATEGORY", y = "REG_REGION_NOT_WORK_REGION", data = application_data, hue = "TARGET")
plt.show()
```


    
![png](README_files/README_188_0.png)
    


When a client receives a lower salary and their work address (city level) does not match, there is a higher probability of them being a defaulter.

## INCOME TYPE

### Income vs Children count


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_INCOME_TYPE", y = "CNT_CHILDREN", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_192_0.png)
    


Individuals who receive income through maternity leave are more likely to be defaulters, especially when they have more children.

### Analyzing the relationship between income and the number of family members.


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_INCOME_TYPE", y = "CNT_FAM_MEMBERS", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_195_0.png)
    


Individuals who receive income through maternity leave tend to have a higher likelihood of being defaulters when they have a greater number of family members.

### Analyzing the relationship between income type and clients whose permanent address does not match their contact address at the region level.


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_INCOME_TYPE", y = "REG_REGION_NOT_LIVE_REGION", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_198_0.png)
    


Clients who are unemployed have a higher chance of being defaulters when their permanent address does not match their contact address at the regional level.

# FAMILY STATUS

### Examining the relationship between family status and the count of children.


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_FAMILY_STATUS", y = "CNT_CHILDREN", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_202_0.png)
    


Clients who are married and have a higher count of children (5 or more) have a higher likelihood of being defaulters. 

This observation may be attributed to the economic situation of their family, as having more children can potentially impose financial strain and impact their ability to repay loans.

### Analyzing the relationship between family status and the count of family members.


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_FAMILY_STATUS", y = "CNT_FAM_MEMBERS", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_205_0.png)
    


Clients who are married and have a higher count of family members, particularly with more than five children, have a higher probability of being defaulters. 

This trend could be attributed to the economic situation of their family, as having more children often leads to increased financial responsibilities and potential difficulties in meeting loan repayment obligations.


```python
f, ax = plt.subplots(figsize = (10, 5))
plot_1 = sns.barplot(x = "NAME_FAMILY_STATUS", y = "AGE", data = application_data, hue = "TARGET")
plot_1.set_xticklabels(plot_1.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_207_0.png)
    


Based on the bivariate analyses, certain columns have been identified as being irrelevant or providing no useful information. 

Therefore, we have decided to drop those columns from the dataset.


```python
application_data.drop(["HOUR_APPR_PROCESS_START", "FLAG_MOBIL"], axis = 1, inplace = True)
```

## Analyzing the correlation between the target variable and other variables.


```python
Correlation = application_data.corr()
Correlation.sort_values(by = ["TARGET"], ascending = False, inplace = True)
Correlation
```





  <div id="df-b26ad06d-87c0-4713-b796-a23f0c2b0b35">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_CURR</th>
      <th>TARGET</th>
      <th>CNT_CHILDREN</th>
      <th>AMT_CREDIT</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_GOODS_PRICE</th>
      <th>REGION_POPULATION_RELATIVE</th>
      <th>DAYS_EMPLOYED</th>
      <th>DAYS_REGISTRATION</th>
      <th>DAYS_ID_PUBLISH</th>
      <th>...</th>
      <th>FLAG_EMAIL</th>
      <th>REGION_RATING_CLIENT</th>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <th>EXT_SOURCE_2</th>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <th>AGE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>TARGET</th>
      <td>-0.002108</td>
      <td>1.000000</td>
      <td>0.018899</td>
      <td>-0.030369</td>
      <td>-0.012817</td>
      <td>-0.039628</td>
      <td>-0.037227</td>
      <td>0.047579</td>
      <td>0.041975</td>
      <td>0.051457</td>
      <td>...</td>
      <td>-0.001758</td>
      <td>0.058899</td>
      <td>0.060893</td>
      <td>0.005576</td>
      <td>0.006942</td>
      <td>0.044395</td>
      <td>0.050994</td>
      <td>-0.160303</td>
      <td>0.055218</td>
      <td>-0.078234</td>
    </tr>
    <tr>
      <th>REGION_RATING_CLIENT_W_CITY</th>
      <td>-0.001138</td>
      <td>0.060893</td>
      <td>0.024838</td>
      <td>-0.110915</td>
      <td>-0.141678</td>
      <td>-0.112170</td>
      <td>-0.531535</td>
      <td>0.005257</td>
      <td>0.074038</td>
      <td>-0.007737</td>
      <td>...</td>
      <td>-0.050778</td>
      <td>0.950842</td>
      <td>1.000000</td>
      <td>-0.041143</td>
      <td>-0.133423</td>
      <td>0.045669</td>
      <td>0.028081</td>
      <td>-0.288015</td>
      <td>0.025717</td>
      <td>-0.008122</td>
    </tr>
    <tr>
      <th>REGION_RATING_CLIENT</th>
      <td>-0.001075</td>
      <td>0.058899</td>
      <td>0.025626</td>
      <td>-0.101776</td>
      <td>-0.128521</td>
      <td>-0.103751</td>
      <td>-0.532877</td>
      <td>0.003343</td>
      <td>0.080210</td>
      <td>-0.005103</td>
      <td>...</td>
      <td>-0.052063</td>
      <td>1.000000</td>
      <td>0.950842</td>
      <td>-0.044166</td>
      <td>-0.139890</td>
      <td>0.035741</td>
      <td>0.008360</td>
      <td>-0.292610</td>
      <td>0.026022</td>
      <td>-0.009414</td>
    </tr>
    <tr>
      <th>DAYS_LAST_PHONE_CHANGE</th>
      <td>-0.000858</td>
      <td>0.055218</td>
      <td>-0.006147</td>
      <td>-0.073701</td>
      <td>-0.063746</td>
      <td>-0.076289</td>
      <td>-0.044013</td>
      <td>0.126866</td>
      <td>0.056983</td>
      <td>0.088576</td>
      <td>...</td>
      <td>-0.019472</td>
      <td>0.026022</td>
      <td>0.025717</td>
      <td>0.037881</td>
      <td>0.036389</td>
      <td>0.054183</td>
      <td>0.046788</td>
      <td>-0.195569</td>
      <td>1.000000</td>
      <td>-0.082864</td>
    </tr>
    <tr>
      <th>DAYS_ID_PUBLISH</th>
      <td>-0.000384</td>
      <td>0.051457</td>
      <td>-0.028442</td>
      <td>-0.006575</td>
      <td>0.011268</td>
      <td>-0.009262</td>
      <td>-0.003993</td>
      <td>-0.027435</td>
      <td>0.101896</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.027505</td>
      <td>-0.005103</td>
      <td>-0.007737</td>
      <td>0.034757</td>
      <td>0.048071</td>
      <td>0.076326</td>
      <td>0.099354</td>
      <td>-0.050901</td>
      <td>0.088576</td>
      <td>-0.272175</td>
    </tr>
    <tr>
      <th>REG_CITY_NOT_WORK_CITY</th>
      <td>-0.001582</td>
      <td>0.050994</td>
      <td>0.071351</td>
      <td>-0.018856</td>
      <td>0.000896</td>
      <td>-0.020322</td>
      <td>-0.044057</td>
      <td>0.018670</td>
      <td>0.099874</td>
      <td>0.099354</td>
      <td>...</td>
      <td>0.004154</td>
      <td>0.008360</td>
      <td>0.028081</td>
      <td>0.143075</td>
      <td>0.239765</td>
      <td>0.440409</td>
      <td>1.000000</td>
      <td>-0.075887</td>
      <td>0.046788</td>
      <td>-0.242346</td>
    </tr>
    <tr>
      <th>DAYS_EMPLOYED</th>
      <td>0.000450</td>
      <td>0.047579</td>
      <td>-0.036930</td>
      <td>-0.102038</td>
      <td>-0.084454</td>
      <td>-0.103017</td>
      <td>0.001960</td>
      <td>1.000000</td>
      <td>0.052964</td>
      <td>-0.027435</td>
      <td>...</td>
      <td>0.003606</td>
      <td>0.003343</td>
      <td>0.005257</td>
      <td>0.037042</td>
      <td>0.034366</td>
      <td>0.067164</td>
      <td>0.018670</td>
      <td>-0.085191</td>
      <td>0.126866</td>
      <td>-0.014304</td>
    </tr>
    <tr>
      <th>FLAG_EMP_PHONE</th>
      <td>-0.001337</td>
      <td>0.045982</td>
      <td>0.244523</td>
      <td>0.065519</td>
      <td>0.103533</td>
      <td>0.063471</td>
      <td>0.004045</td>
      <td>-0.376736</td>
      <td>0.212361</td>
      <td>0.273611</td>
      <td>...</td>
      <td>0.062542</td>
      <td>-0.032871</td>
      <td>-0.034712</td>
      <td>0.036640</td>
      <td>0.108355</td>
      <td>0.092166</td>
      <td>0.256427</td>
      <td>0.019433</td>
      <td>-0.021103</td>
      <td>-0.619828</td>
    </tr>
    <tr>
      <th>REG_CITY_NOT_LIVE_CITY</th>
      <td>-0.001885</td>
      <td>0.044395</td>
      <td>0.020527</td>
      <td>-0.026886</td>
      <td>-0.006213</td>
      <td>-0.027198</td>
      <td>-0.050499</td>
      <td>0.067164</td>
      <td>0.064334</td>
      <td>0.076326</td>
      <td>...</td>
      <td>0.014272</td>
      <td>0.035741</td>
      <td>0.045669</td>
      <td>0.339232</td>
      <td>0.151397</td>
      <td>1.000000</td>
      <td>0.440409</td>
      <td>-0.043220</td>
      <td>0.054183</td>
      <td>-0.180376</td>
    </tr>
    <tr>
      <th>DAYS_REGISTRATION</th>
      <td>-0.000973</td>
      <td>0.041975</td>
      <td>0.185929</td>
      <td>0.009621</td>
      <td>0.038513</td>
      <td>0.011561</td>
      <td>-0.053820</td>
      <td>0.052964</td>
      <td>1.000000</td>
      <td>0.101896</td>
      <td>...</td>
      <td>0.034388</td>
      <td>0.080210</td>
      <td>0.074038</td>
      <td>0.028213</td>
      <td>0.036787</td>
      <td>0.064334</td>
      <td>0.099874</td>
      <td>-0.059836</td>
      <td>0.056983</td>
      <td>-0.331796</td>
    </tr>
    <tr>
      <th>FLAG_WORK_PHONE</th>
      <td>-0.000415</td>
      <td>0.028524</td>
      <td>0.055666</td>
      <td>-0.021085</td>
      <td>-0.024803</td>
      <td>0.001085</td>
      <td>-0.015628</td>
      <td>-0.098272</td>
      <td>0.058283</td>
      <td>0.045964</td>
      <td>...</td>
      <td>-0.011520</td>
      <td>0.007349</td>
      <td>0.013414</td>
      <td>0.064484</td>
      <td>0.068202</td>
      <td>0.045948</td>
      <td>0.121000</td>
      <td>-0.018823</td>
      <td>-0.041537</td>
      <td>-0.172467</td>
    </tr>
    <tr>
      <th>CNT_CHILDREN</th>
      <td>-0.000953</td>
      <td>0.018899</td>
      <td>1.000000</td>
      <td>0.002387</td>
      <td>0.021780</td>
      <td>-0.001596</td>
      <td>-0.025740</td>
      <td>-0.036930</td>
      <td>0.185929</td>
      <td>-0.028442</td>
      <td>...</td>
      <td>0.023402</td>
      <td>0.025626</td>
      <td>0.024838</td>
      <td>-0.013363</td>
      <td>0.008702</td>
      <td>0.020527</td>
      <td>0.071351</td>
      <td>-0.018004</td>
      <td>-0.006147</td>
      <td>-0.336435</td>
    </tr>
    <tr>
      <th>CNT_FAM_MEMBERS</th>
      <td>-0.002895</td>
      <td>0.009308</td>
      <td>0.874536</td>
      <td>0.063160</td>
      <td>0.075538</td>
      <td>0.061153</td>
      <td>-0.024209</td>
      <td>-0.063099</td>
      <td>0.173415</td>
      <td>-0.020912</td>
      <td>...</td>
      <td>0.018081</td>
      <td>0.029688</td>
      <td>0.030778</td>
      <td>-0.017133</td>
      <td>0.003133</td>
      <td>0.012253</td>
      <td>0.070719</td>
      <td>-0.001822</td>
      <td>-0.027109</td>
      <td>-0.278886</td>
    </tr>
    <tr>
      <th>REG_REGION_NOT_WORK_REGION</th>
      <td>0.001097</td>
      <td>0.006942</td>
      <td>0.008702</td>
      <td>0.051929</td>
      <td>0.079411</td>
      <td>0.053147</td>
      <td>0.056944</td>
      <td>0.034366</td>
      <td>0.036787</td>
      <td>0.048071</td>
      <td>...</td>
      <td>0.031092</td>
      <td>-0.139890</td>
      <td>-0.133423</td>
      <td>0.450804</td>
      <td>1.000000</td>
      <td>0.151397</td>
      <td>0.239765</td>
      <td>0.029477</td>
      <td>0.036389</td>
      <td>-0.095787</td>
    </tr>
    <tr>
      <th>REG_REGION_NOT_LIVE_REGION</th>
      <td>-0.000283</td>
      <td>0.005576</td>
      <td>-0.013363</td>
      <td>0.024010</td>
      <td>0.041295</td>
      <td>0.026105</td>
      <td>0.002118</td>
      <td>0.037042</td>
      <td>0.028213</td>
      <td>0.034757</td>
      <td>...</td>
      <td>0.018632</td>
      <td>-0.044166</td>
      <td>-0.041143</td>
      <td>1.000000</td>
      <td>0.450804</td>
      <td>0.339232</td>
      <td>0.143075</td>
      <td>0.015550</td>
      <td>0.037881</td>
      <td>-0.065519</td>
    </tr>
    <tr>
      <th>FLAG_CONT_MOBILE</th>
      <td>0.002815</td>
      <td>0.000370</td>
      <td>-0.000654</td>
      <td>0.023653</td>
      <td>0.022350</td>
      <td>0.020706</td>
      <td>-0.012478</td>
      <td>0.000588</td>
      <td>-0.003848</td>
      <td>-0.000802</td>
      <td>...</td>
      <td>-0.005356</td>
      <td>0.013041</td>
      <td>0.013651</td>
      <td>0.001044</td>
      <td>-0.001324</td>
      <td>-0.000878</td>
      <td>0.003270</td>
      <td>-0.003540</td>
      <td>-0.028951</td>
      <td>0.014925</td>
    </tr>
    <tr>
      <th>FLAG_EMAIL</th>
      <td>0.000281</td>
      <td>-0.001758</td>
      <td>0.023402</td>
      <td>0.016632</td>
      <td>0.071707</td>
      <td>0.017039</td>
      <td>0.040012</td>
      <td>0.003606</td>
      <td>0.034388</td>
      <td>0.027505</td>
      <td>...</td>
      <td>1.000000</td>
      <td>-0.052063</td>
      <td>-0.050778</td>
      <td>0.018632</td>
      <td>0.031092</td>
      <td>0.014272</td>
      <td>0.004154</td>
      <td>0.023724</td>
      <td>-0.019472</td>
      <td>-0.088167</td>
    </tr>
    <tr>
      <th>SK_ID_CURR</th>
      <td>1.000000</td>
      <td>-0.002108</td>
      <td>-0.000953</td>
      <td>-0.000343</td>
      <td>-0.000433</td>
      <td>-0.000232</td>
      <td>0.000849</td>
      <td>0.000450</td>
      <td>-0.000973</td>
      <td>-0.000384</td>
      <td>...</td>
      <td>0.000281</td>
      <td>-0.001075</td>
      <td>-0.001138</td>
      <td>-0.000283</td>
      <td>0.001097</td>
      <td>-0.001885</td>
      <td>-0.001582</td>
      <td>0.002339</td>
      <td>-0.000858</td>
      <td>0.001467</td>
    </tr>
    <tr>
      <th>AMT_ANNUITY</th>
      <td>-0.000433</td>
      <td>-0.012817</td>
      <td>0.021780</td>
      <td>0.770127</td>
      <td>1.000000</td>
      <td>0.774661</td>
      <td>0.118424</td>
      <td>-0.084454</td>
      <td>0.038513</td>
      <td>0.011268</td>
      <td>...</td>
      <td>0.071707</td>
      <td>-0.128521</td>
      <td>-0.141678</td>
      <td>0.041295</td>
      <td>0.079411</td>
      <td>-0.006213</td>
      <td>0.000896</td>
      <td>0.125702</td>
      <td>-0.063746</td>
      <td>-0.009455</td>
    </tr>
    <tr>
      <th>AMT_CREDIT</th>
      <td>-0.000343</td>
      <td>-0.030369</td>
      <td>0.002387</td>
      <td>1.000000</td>
      <td>0.770127</td>
      <td>0.986588</td>
      <td>0.099738</td>
      <td>-0.102038</td>
      <td>0.009621</td>
      <td>-0.006575</td>
      <td>...</td>
      <td>0.016632</td>
      <td>-0.101776</td>
      <td>-0.110915</td>
      <td>0.024010</td>
      <td>0.051929</td>
      <td>-0.026886</td>
      <td>-0.018856</td>
      <td>0.131129</td>
      <td>-0.073701</td>
      <td>0.055408</td>
    </tr>
    <tr>
      <th>REGION_POPULATION_RELATIVE</th>
      <td>0.000849</td>
      <td>-0.037227</td>
      <td>-0.025740</td>
      <td>0.099738</td>
      <td>0.118424</td>
      <td>0.103482</td>
      <td>1.000000</td>
      <td>0.001960</td>
      <td>-0.053820</td>
      <td>-0.003993</td>
      <td>...</td>
      <td>0.040012</td>
      <td>-0.532877</td>
      <td>-0.531535</td>
      <td>0.002118</td>
      <td>0.056944</td>
      <td>-0.050499</td>
      <td>-0.044057</td>
      <td>0.198706</td>
      <td>-0.044013</td>
      <td>0.029648</td>
    </tr>
    <tr>
      <th>AMT_GOODS_PRICE</th>
      <td>-0.000232</td>
      <td>-0.039628</td>
      <td>-0.001596</td>
      <td>0.986588</td>
      <td>0.774661</td>
      <td>1.000000</td>
      <td>0.103482</td>
      <td>-0.103017</td>
      <td>0.011561</td>
      <td>-0.009262</td>
      <td>...</td>
      <td>0.017039</td>
      <td>-0.103751</td>
      <td>-0.112170</td>
      <td>0.026105</td>
      <td>0.053147</td>
      <td>-0.027198</td>
      <td>-0.020322</td>
      <td>0.139209</td>
      <td>-0.076289</td>
      <td>0.053391</td>
    </tr>
    <tr>
      <th>AGE</th>
      <td>0.001467</td>
      <td>-0.078234</td>
      <td>-0.336435</td>
      <td>0.055408</td>
      <td>-0.009455</td>
      <td>0.053391</td>
      <td>0.029648</td>
      <td>-0.014304</td>
      <td>-0.331796</td>
      <td>-0.272175</td>
      <td>...</td>
      <td>-0.088167</td>
      <td>-0.009414</td>
      <td>-0.008122</td>
      <td>-0.065519</td>
      <td>-0.095787</td>
      <td>-0.180376</td>
      <td>-0.242346</td>
      <td>0.091791</td>
      <td>-0.082864</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>EXT_SOURCE_2</th>
      <td>0.002339</td>
      <td>-0.160303</td>
      <td>-0.018004</td>
      <td>0.131129</td>
      <td>0.125702</td>
      <td>0.139209</td>
      <td>0.198706</td>
      <td>-0.085191</td>
      <td>-0.059836</td>
      <td>-0.050901</td>
      <td>...</td>
      <td>0.023724</td>
      <td>-0.292610</td>
      <td>-0.288015</td>
      <td>0.015550</td>
      <td>0.029477</td>
      <td>-0.043220</td>
      <td>-0.075887</td>
      <td>1.000000</td>
      <td>-0.195569</td>
      <td>0.091791</td>
    </tr>
  </tbody>
</table>
<p>24 rows × 24 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b26ad06d-87c0-4713-b796-a23f0c2b0b35')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b26ad06d-87c0-4713-b796-a23f0c2b0b35 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b26ad06d-87c0-4713-b796-a23f0c2b0b35');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (20, 12))
sns.heatmap(Correlation, annot = True)
plt.show()
```


    
![png](README_files/README_212_0.png)
    



```python
Correlation.head()["TARGET"][1:]
```




    REGION_RATING_CLIENT_W_CITY    0.060893
    REGION_RATING_CLIENT           0.058899
    DAYS_LAST_PHONE_CHANGE         0.055218
    DAYS_ID_PUBLISH                0.051457
    Name: TARGET, dtype: float64




```python
Correlation.tail()["TARGET"]
```




    AMT_CREDIT                   -0.030369
    REGION_POPULATION_RELATIVE   -0.037227
    AMT_GOODS_PRICE              -0.039628
    AGE                          -0.078234
    EXT_SOURCE_2                 -0.160303
    Name: TARGET, dtype: float64



## Identifying highly correlated variables:

- AMT_CREDIT and AMT_GOODS_PRICE exhibit a correlation coefficient of 0.99.
- REGION_RATING_CLIENT_W_CITY and REGION_RATING_CLIENT show a correlation coefficient of 0.95.
- CNT_FAM_MEMBERS and CNT_CHILDREN display a correlation coefficient of 0.87.
- AMT_ANNUITY and AMT_CREDIT demonstrate a correlation coefficient of 0.77.

# Analyzing the data from the previous loan applications.


```python
# reading previous.csv data

previous_data = pd.read_csv('previous_application.csv')
previous_data
```





  <div id="df-856aa3fd-136c-4b51-b3ae-0c48ad33446f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_PREV</th>
      <th>SK_ID_CURR</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>AMT_ANNUITY</th>
      <th>AMT_APPLICATION</th>
      <th>AMT_CREDIT</th>
      <th>AMT_DOWN_PAYMENT</th>
      <th>AMT_GOODS_PRICE</th>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>...</th>
      <th>NAME_SELLER_INDUSTRY</th>
      <th>CNT_PAYMENT</th>
      <th>NAME_YIELD_GROUP</th>
      <th>PRODUCT_COMBINATION</th>
      <th>DAYS_FIRST_DRAWING</th>
      <th>DAYS_FIRST_DUE</th>
      <th>DAYS_LAST_DUE_1ST_VERSION</th>
      <th>DAYS_LAST_DUE</th>
      <th>DAYS_TERMINATION</th>
      <th>NFLAG_INSURED_ON_APPROVAL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2030495</td>
      <td>271877</td>
      <td>Consumer loans</td>
      <td>1730.430</td>
      <td>17145.0</td>
      <td>17145.0</td>
      <td>0.0</td>
      <td>17145.0</td>
      <td>SATURDAY</td>
      <td>15</td>
      <td>...</td>
      <td>Connectivity</td>
      <td>12.0</td>
      <td>middle</td>
      <td>POS mobile with interest</td>
      <td>365243.0</td>
      <td>-42.0</td>
      <td>300.0</td>
      <td>-42.0</td>
      <td>-37.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2802425</td>
      <td>108129</td>
      <td>Cash loans</td>
      <td>25188.615</td>
      <td>607500.0</td>
      <td>679671.0</td>
      <td>NaN</td>
      <td>607500.0</td>
      <td>THURSDAY</td>
      <td>11</td>
      <td>...</td>
      <td>XNA</td>
      <td>36.0</td>
      <td>low_action</td>
      <td>Cash X-Sell: low</td>
      <td>365243.0</td>
      <td>-134.0</td>
      <td>916.0</td>
      <td>365243.0</td>
      <td>365243.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2523466</td>
      <td>122040</td>
      <td>Cash loans</td>
      <td>15060.735</td>
      <td>112500.0</td>
      <td>136444.5</td>
      <td>NaN</td>
      <td>112500.0</td>
      <td>TUESDAY</td>
      <td>11</td>
      <td>...</td>
      <td>XNA</td>
      <td>12.0</td>
      <td>high</td>
      <td>Cash X-Sell: high</td>
      <td>365243.0</td>
      <td>-271.0</td>
      <td>59.0</td>
      <td>365243.0</td>
      <td>365243.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2819243</td>
      <td>176158</td>
      <td>Cash loans</td>
      <td>47041.335</td>
      <td>450000.0</td>
      <td>470790.0</td>
      <td>NaN</td>
      <td>450000.0</td>
      <td>MONDAY</td>
      <td>7</td>
      <td>...</td>
      <td>XNA</td>
      <td>12.0</td>
      <td>middle</td>
      <td>Cash X-Sell: middle</td>
      <td>365243.0</td>
      <td>-482.0</td>
      <td>-152.0</td>
      <td>-182.0</td>
      <td>-177.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1784265</td>
      <td>202054</td>
      <td>Cash loans</td>
      <td>31924.395</td>
      <td>337500.0</td>
      <td>404055.0</td>
      <td>NaN</td>
      <td>337500.0</td>
      <td>THURSDAY</td>
      <td>9</td>
      <td>...</td>
      <td>XNA</td>
      <td>24.0</td>
      <td>high</td>
      <td>Cash Street: high</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1670209</th>
      <td>2300464</td>
      <td>352015</td>
      <td>Consumer loans</td>
      <td>14704.290</td>
      <td>267295.5</td>
      <td>311400.0</td>
      <td>0.0</td>
      <td>267295.5</td>
      <td>WEDNESDAY</td>
      <td>12</td>
      <td>...</td>
      <td>Furniture</td>
      <td>30.0</td>
      <td>low_normal</td>
      <td>POS industry with interest</td>
      <td>365243.0</td>
      <td>-508.0</td>
      <td>362.0</td>
      <td>-358.0</td>
      <td>-351.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1670210</th>
      <td>2357031</td>
      <td>334635</td>
      <td>Consumer loans</td>
      <td>6622.020</td>
      <td>87750.0</td>
      <td>64291.5</td>
      <td>29250.0</td>
      <td>87750.0</td>
      <td>TUESDAY</td>
      <td>15</td>
      <td>...</td>
      <td>Furniture</td>
      <td>12.0</td>
      <td>middle</td>
      <td>POS industry with interest</td>
      <td>365243.0</td>
      <td>-1604.0</td>
      <td>-1274.0</td>
      <td>-1304.0</td>
      <td>-1297.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1670211</th>
      <td>2659632</td>
      <td>249544</td>
      <td>Consumer loans</td>
      <td>11520.855</td>
      <td>105237.0</td>
      <td>102523.5</td>
      <td>10525.5</td>
      <td>105237.0</td>
      <td>MONDAY</td>
      <td>12</td>
      <td>...</td>
      <td>Consumer electronics</td>
      <td>10.0</td>
      <td>low_normal</td>
      <td>POS household with interest</td>
      <td>365243.0</td>
      <td>-1457.0</td>
      <td>-1187.0</td>
      <td>-1187.0</td>
      <td>-1181.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1670212</th>
      <td>2785582</td>
      <td>400317</td>
      <td>Cash loans</td>
      <td>18821.520</td>
      <td>180000.0</td>
      <td>191880.0</td>
      <td>NaN</td>
      <td>180000.0</td>
      <td>WEDNESDAY</td>
      <td>9</td>
      <td>...</td>
      <td>XNA</td>
      <td>12.0</td>
      <td>low_normal</td>
      <td>Cash X-Sell: low</td>
      <td>365243.0</td>
      <td>-1155.0</td>
      <td>-825.0</td>
      <td>-825.0</td>
      <td>-817.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1670213</th>
      <td>2418762</td>
      <td>261212</td>
      <td>Cash loans</td>
      <td>16431.300</td>
      <td>360000.0</td>
      <td>360000.0</td>
      <td>NaN</td>
      <td>360000.0</td>
      <td>SUNDAY</td>
      <td>10</td>
      <td>...</td>
      <td>XNA</td>
      <td>48.0</td>
      <td>middle</td>
      <td>Cash X-Sell: middle</td>
      <td>365243.0</td>
      <td>-1163.0</td>
      <td>247.0</td>
      <td>-443.0</td>
      <td>-423.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>1670214 rows × 37 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-856aa3fd-136c-4b51-b3ae-0c48ad33446f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-856aa3fd-136c-4b51-b3ae-0c48ad33446f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-856aa3fd-136c-4b51-b3ae-0c48ad33446f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
previous_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1670214 entries, 0 to 1670213
    Data columns (total 37 columns):
     #   Column                       Non-Null Count    Dtype  
    ---  ------                       --------------    -----  
     0   SK_ID_PREV                   1670214 non-null  int64  
     1   SK_ID_CURR                   1670214 non-null  int64  
     2   NAME_CONTRACT_TYPE           1670214 non-null  object 
     3   AMT_ANNUITY                  1297979 non-null  float64
     4   AMT_APPLICATION              1670214 non-null  float64
     5   AMT_CREDIT                   1670213 non-null  float64
     6   AMT_DOWN_PAYMENT             774370 non-null   float64
     7   AMT_GOODS_PRICE              1284699 non-null  float64
     8   WEEKDAY_APPR_PROCESS_START   1670214 non-null  object 
     9   HOUR_APPR_PROCESS_START      1670214 non-null  int64  
     10  FLAG_LAST_APPL_PER_CONTRACT  1670214 non-null  object 
     11  NFLAG_LAST_APPL_IN_DAY       1670214 non-null  int64  
     12  RATE_DOWN_PAYMENT            774370 non-null   float64
     13  RATE_INTEREST_PRIMARY        5951 non-null     float64
     14  RATE_INTEREST_PRIVILEGED     5951 non-null     float64
     15  NAME_CASH_LOAN_PURPOSE       1670214 non-null  object 
     16  NAME_CONTRACT_STATUS         1670214 non-null  object 
     17  DAYS_DECISION                1670214 non-null  int64  
     18  NAME_PAYMENT_TYPE            1670214 non-null  object 
     19  CODE_REJECT_REASON           1670214 non-null  object 
     20  NAME_TYPE_SUITE              849809 non-null   object 
     21  NAME_CLIENT_TYPE             1670214 non-null  object 
     22  NAME_GOODS_CATEGORY          1670214 non-null  object 
     23  NAME_PORTFOLIO               1670214 non-null  object 
     24  NAME_PRODUCT_TYPE            1670214 non-null  object 
     25  CHANNEL_TYPE                 1670214 non-null  object 
     26  SELLERPLACE_AREA             1670214 non-null  int64  
     27  NAME_SELLER_INDUSTRY         1670214 non-null  object 
     28  CNT_PAYMENT                  1297984 non-null  float64
     29  NAME_YIELD_GROUP             1670214 non-null  object 
     30  PRODUCT_COMBINATION          1669868 non-null  object 
     31  DAYS_FIRST_DRAWING           997149 non-null   float64
     32  DAYS_FIRST_DUE               997149 non-null   float64
     33  DAYS_LAST_DUE_1ST_VERSION    997149 non-null   float64
     34  DAYS_LAST_DUE                997149 non-null   float64
     35  DAYS_TERMINATION             997149 non-null   float64
     36  NFLAG_INSURED_ON_APPROVAL    997149 non-null   float64
    dtypes: float64(15), int64(6), object(16)
    memory usage: 471.5+ MB


### Determine the percentage of missing values in each column to assess the necessary steps for data cleaning.


```python
(previous_data.isnull().sum() * 100 / previous_data.shape[0]).round(2)
```




    SK_ID_PREV                      0.00
    SK_ID_CURR                      0.00
    NAME_CONTRACT_TYPE              0.00
    AMT_ANNUITY                    22.29
    AMT_APPLICATION                 0.00
    AMT_CREDIT                      0.00
    AMT_DOWN_PAYMENT               53.64
    AMT_GOODS_PRICE                23.08
    WEEKDAY_APPR_PROCESS_START      0.00
    HOUR_APPR_PROCESS_START         0.00
    FLAG_LAST_APPL_PER_CONTRACT     0.00
    NFLAG_LAST_APPL_IN_DAY          0.00
    RATE_DOWN_PAYMENT              53.64
    RATE_INTEREST_PRIMARY          99.64
    RATE_INTEREST_PRIVILEGED       99.64
    NAME_CASH_LOAN_PURPOSE          0.00
    NAME_CONTRACT_STATUS            0.00
    DAYS_DECISION                   0.00
    NAME_PAYMENT_TYPE               0.00
    CODE_REJECT_REASON              0.00
    NAME_TYPE_SUITE                49.12
    NAME_CLIENT_TYPE                0.00
    NAME_GOODS_CATEGORY             0.00
    NAME_PORTFOLIO                  0.00
    NAME_PRODUCT_TYPE               0.00
    CHANNEL_TYPE                    0.00
    SELLERPLACE_AREA                0.00
    NAME_SELLER_INDUSTRY            0.00
    CNT_PAYMENT                    22.29
    NAME_YIELD_GROUP                0.00
    PRODUCT_COMBINATION             0.02
    DAYS_FIRST_DRAWING             40.30
    DAYS_FIRST_DUE                 40.30
    DAYS_LAST_DUE_1ST_VERSION      40.30
    DAYS_LAST_DUE                  40.30
    DAYS_TERMINATION               40.30
    NFLAG_INSURED_ON_APPROVAL      40.30
    dtype: float64



### function to calculate percentage of NULL values in dataFrame


```python
calc_perc_of_missing_values = lambda x: 100 * round(x.isnull().sum()/x.shape[0], 3)    
calc_perc_of_missing_values(previous_data)
```




    SK_ID_PREV                      0.0
    SK_ID_CURR                      0.0
    NAME_CONTRACT_TYPE              0.0
    AMT_ANNUITY                    22.3
    AMT_APPLICATION                 0.0
    AMT_CREDIT                      0.0
    AMT_DOWN_PAYMENT               53.6
    AMT_GOODS_PRICE                23.1
    WEEKDAY_APPR_PROCESS_START      0.0
    HOUR_APPR_PROCESS_START         0.0
    FLAG_LAST_APPL_PER_CONTRACT     0.0
    NFLAG_LAST_APPL_IN_DAY          0.0
    RATE_DOWN_PAYMENT              53.6
    RATE_INTEREST_PRIMARY          99.6
    RATE_INTEREST_PRIVILEGED       99.6
    NAME_CASH_LOAN_PURPOSE          0.0
    NAME_CONTRACT_STATUS            0.0
    DAYS_DECISION                   0.0
    NAME_PAYMENT_TYPE               0.0
    CODE_REJECT_REASON              0.0
    NAME_TYPE_SUITE                49.1
    NAME_CLIENT_TYPE                0.0
    NAME_GOODS_CATEGORY             0.0
    NAME_PORTFOLIO                  0.0
    NAME_PRODUCT_TYPE               0.0
    CHANNEL_TYPE                    0.0
    SELLERPLACE_AREA                0.0
    NAME_SELLER_INDUSTRY            0.0
    CNT_PAYMENT                    22.3
    NAME_YIELD_GROUP                0.0
    PRODUCT_COMBINATION             0.0
    DAYS_FIRST_DRAWING             40.3
    DAYS_FIRST_DUE                 40.3
    DAYS_LAST_DUE_1ST_VERSION      40.3
    DAYS_LAST_DUE                  40.3
    DAYS_TERMINATION               40.3
    NFLAG_INSURED_ON_APPROVAL      40.3
    dtype: float64



### Iterate through the columns in the DataFrame and remove those where more than 20% of the values are missing.


```python
for col in previous_data:
  if calc_perc_of_missing_values(previous_data[col]) > 20:
    previous_data.drop(col, axis = 1, inplace = True)

previous_data
```





  <div id="df-72a3e12d-0c2d-43c7-9b9a-508ebbaee23a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SK_ID_PREV</th>
      <th>SK_ID_CURR</th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>AMT_APPLICATION</th>
      <th>AMT_CREDIT</th>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <th>HOUR_APPR_PROCESS_START</th>
      <th>FLAG_LAST_APPL_PER_CONTRACT</th>
      <th>NFLAG_LAST_APPL_IN_DAY</th>
      <th>NAME_CASH_LOAN_PURPOSE</th>
      <th>...</th>
      <th>CODE_REJECT_REASON</th>
      <th>NAME_CLIENT_TYPE</th>
      <th>NAME_GOODS_CATEGORY</th>
      <th>NAME_PORTFOLIO</th>
      <th>NAME_PRODUCT_TYPE</th>
      <th>CHANNEL_TYPE</th>
      <th>SELLERPLACE_AREA</th>
      <th>NAME_SELLER_INDUSTRY</th>
      <th>NAME_YIELD_GROUP</th>
      <th>PRODUCT_COMBINATION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2030495</td>
      <td>271877</td>
      <td>Consumer loans</td>
      <td>17145.0</td>
      <td>17145.0</td>
      <td>SATURDAY</td>
      <td>15</td>
      <td>Y</td>
      <td>1</td>
      <td>XAP</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>Mobile</td>
      <td>POS</td>
      <td>XNA</td>
      <td>Country-wide</td>
      <td>35</td>
      <td>Connectivity</td>
      <td>middle</td>
      <td>POS mobile with interest</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2802425</td>
      <td>108129</td>
      <td>Cash loans</td>
      <td>607500.0</td>
      <td>679671.0</td>
      <td>THURSDAY</td>
      <td>11</td>
      <td>Y</td>
      <td>1</td>
      <td>XNA</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>x-sell</td>
      <td>Contact center</td>
      <td>-1</td>
      <td>XNA</td>
      <td>low_action</td>
      <td>Cash X-Sell: low</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2523466</td>
      <td>122040</td>
      <td>Cash loans</td>
      <td>112500.0</td>
      <td>136444.5</td>
      <td>TUESDAY</td>
      <td>11</td>
      <td>Y</td>
      <td>1</td>
      <td>XNA</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>x-sell</td>
      <td>Credit and cash offices</td>
      <td>-1</td>
      <td>XNA</td>
      <td>high</td>
      <td>Cash X-Sell: high</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2819243</td>
      <td>176158</td>
      <td>Cash loans</td>
      <td>450000.0</td>
      <td>470790.0</td>
      <td>MONDAY</td>
      <td>7</td>
      <td>Y</td>
      <td>1</td>
      <td>XNA</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>x-sell</td>
      <td>Credit and cash offices</td>
      <td>-1</td>
      <td>XNA</td>
      <td>middle</td>
      <td>Cash X-Sell: middle</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1784265</td>
      <td>202054</td>
      <td>Cash loans</td>
      <td>337500.0</td>
      <td>404055.0</td>
      <td>THURSDAY</td>
      <td>9</td>
      <td>Y</td>
      <td>1</td>
      <td>Repairs</td>
      <td>...</td>
      <td>HC</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>walk-in</td>
      <td>Credit and cash offices</td>
      <td>-1</td>
      <td>XNA</td>
      <td>high</td>
      <td>Cash Street: high</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1670209</th>
      <td>2300464</td>
      <td>352015</td>
      <td>Consumer loans</td>
      <td>267295.5</td>
      <td>311400.0</td>
      <td>WEDNESDAY</td>
      <td>12</td>
      <td>Y</td>
      <td>1</td>
      <td>XAP</td>
      <td>...</td>
      <td>XAP</td>
      <td>Refreshed</td>
      <td>Furniture</td>
      <td>POS</td>
      <td>XNA</td>
      <td>Stone</td>
      <td>43</td>
      <td>Furniture</td>
      <td>low_normal</td>
      <td>POS industry with interest</td>
    </tr>
    <tr>
      <th>1670210</th>
      <td>2357031</td>
      <td>334635</td>
      <td>Consumer loans</td>
      <td>87750.0</td>
      <td>64291.5</td>
      <td>TUESDAY</td>
      <td>15</td>
      <td>Y</td>
      <td>1</td>
      <td>XAP</td>
      <td>...</td>
      <td>XAP</td>
      <td>New</td>
      <td>Furniture</td>
      <td>POS</td>
      <td>XNA</td>
      <td>Stone</td>
      <td>43</td>
      <td>Furniture</td>
      <td>middle</td>
      <td>POS industry with interest</td>
    </tr>
    <tr>
      <th>1670211</th>
      <td>2659632</td>
      <td>249544</td>
      <td>Consumer loans</td>
      <td>105237.0</td>
      <td>102523.5</td>
      <td>MONDAY</td>
      <td>12</td>
      <td>Y</td>
      <td>1</td>
      <td>XAP</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>Consumer Electronics</td>
      <td>POS</td>
      <td>XNA</td>
      <td>Country-wide</td>
      <td>1370</td>
      <td>Consumer electronics</td>
      <td>low_normal</td>
      <td>POS household with interest</td>
    </tr>
    <tr>
      <th>1670212</th>
      <td>2785582</td>
      <td>400317</td>
      <td>Cash loans</td>
      <td>180000.0</td>
      <td>191880.0</td>
      <td>WEDNESDAY</td>
      <td>9</td>
      <td>Y</td>
      <td>1</td>
      <td>XNA</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>x-sell</td>
      <td>AP+ (Cash loan)</td>
      <td>-1</td>
      <td>XNA</td>
      <td>low_normal</td>
      <td>Cash X-Sell: low</td>
    </tr>
    <tr>
      <th>1670213</th>
      <td>2418762</td>
      <td>261212</td>
      <td>Cash loans</td>
      <td>360000.0</td>
      <td>360000.0</td>
      <td>SUNDAY</td>
      <td>10</td>
      <td>Y</td>
      <td>1</td>
      <td>XNA</td>
      <td>...</td>
      <td>XAP</td>
      <td>Repeater</td>
      <td>XNA</td>
      <td>Cash</td>
      <td>x-sell</td>
      <td>AP+ (Cash loan)</td>
      <td>-1</td>
      <td>XNA</td>
      <td>middle</td>
      <td>Cash X-Sell: middle</td>
    </tr>
  </tbody>
</table>
<p>1670214 rows × 23 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-72a3e12d-0c2d-43c7-9b9a-508ebbaee23a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-72a3e12d-0c2d-43c7-9b9a-508ebbaee23a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-72a3e12d-0c2d-43c7-9b9a-508ebbaee23a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Calculate the percentage of null values in each column to determine the necessary cleaning steps to be taken.


```python
(previous_data.isnull().sum() * 100 / previous_data.shape[0]).round(2)
```




    SK_ID_PREV                     0.00
    SK_ID_CURR                     0.00
    NAME_CONTRACT_TYPE             0.00
    AMT_APPLICATION                0.00
    AMT_CREDIT                     0.00
    WEEKDAY_APPR_PROCESS_START     0.00
    HOUR_APPR_PROCESS_START        0.00
    FLAG_LAST_APPL_PER_CONTRACT    0.00
    NFLAG_LAST_APPL_IN_DAY         0.00
    NAME_CASH_LOAN_PURPOSE         0.00
    NAME_CONTRACT_STATUS           0.00
    DAYS_DECISION                  0.00
    NAME_PAYMENT_TYPE              0.00
    CODE_REJECT_REASON             0.00
    NAME_CLIENT_TYPE               0.00
    NAME_GOODS_CATEGORY            0.00
    NAME_PORTFOLIO                 0.00
    NAME_PRODUCT_TYPE              0.00
    CHANNEL_TYPE                   0.00
    SELLERPLACE_AREA               0.00
    NAME_SELLER_INDUSTRY           0.00
    NAME_YIELD_GROUP               0.00
    PRODUCT_COMBINATION            0.02
    dtype: float64




```python
previous_data.shape
```




    (1670214, 23)




```python
PRODUCT_COMBINATION_vc = previous_data["PRODUCT_COMBINATION"].value_counts()
PRODUCT_COMBINATION_vc
```




    Cash                              285990
    POS household with interest       263622
    POS mobile with interest          220670
    Cash X-Sell: middle               143883
    Cash X-Sell: low                  130248
    Card Street                       112582
    POS industry with interest         98833
    POS household without interest     82908
    Card X-Sell                        80582
    Cash Street: high                  59639
    Cash X-Sell: high                  59301
    Cash Street: middle                34658
    Cash Street: low                   33834
    POS mobile without interest        24082
    POS other with interest            23879
    POS industry without interest      12602
    POS others without interest         2555
    Name: PRODUCT_COMBINATION, dtype: int64




```python
PRODUCT_COMBINATION_vc.plot.barh()
plt.show()
```


    
![png](README_files/README_229_0.png)
    



```python
PRODUCT_COMBINATIO_mode = previous_data["PRODUCT_COMBINATION"].mode()
PRODUCT_COMBINATIO_mode
```




    0    Cash
    Name: PRODUCT_COMBINATION, dtype: object



### Fill the 2% of missing values in the `PRODUCT_COMBINATION` column with the highest mode value.


```python
previous_data["PRODUCT_COMBINATION"].fillna(PRODUCT_COMBINATIO_mode[0], inplace = True)
```

### Let's begin the process of visualization to gain meaningful insights.

### **_Contract Status_**


```python
Contract_Status = previous_data['NAME_CONTRACT_STATUS']
Contract_Status
```




    0          Approved
    1          Approved
    2          Approved
    3          Approved
    4           Refused
                 ...   
    1670209    Approved
    1670210    Approved
    1670211    Approved
    1670212    Approved
    1670213    Approved
    Name: NAME_CONTRACT_STATUS, Length: 1670214, dtype: object



### Calculate the percentage of contract status in the dataset.


```python
df_1 = round((Contract_Status.value_counts() / previous_data["NAME_CONTRACT_STATUS"].count()) * 100, 2)
df_1 = pd.DataFrame(df_1)
df_1.reset_index(level = 0, inplace = True)

df_1.rename(columns = {
    "index" : "NAME_CONTRACT_STATUS", 
    "NAME_CONTRACT_STATUS" : "Percentage_of_Values"
  }, inplace = True
) 

df_1.sort_values(by = 'Percentage_of_Values' , inplace = True, ascending = False)
df_1
```





  <div id="df-896b3624-24fd-4337-be65-0b7aeda23c5f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_CONTRACT_STATUS</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Approved</td>
      <td>62.07</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Canceled</td>
      <td>18.94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Refused</td>
      <td>17.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Unused offer</td>
      <td>1.58</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-896b3624-24fd-4337-be65-0b7aeda23c5f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-896b3624-24fd-4337-be65-0b7aeda23c5f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-896b3624-24fd-4337-be65-0b7aeda23c5f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = ['Approved', 'Canceled', 'Refused', 'Unused offer']
sizes = df_1['Percentage_of_Values']

colors = ['gold', 'yellowgreen', 'lightcoral', 'lightskyblue']
explode = (0.1, 0.1, 0.1, 0.1)

plt.pie(sizes,
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle = 140
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_238_0.png)
    


### **_Client Type_**


```python
Client_Type = previous_data['NAME_CLIENT_TYPE']
Client_Type
```




    0           Repeater
    1           Repeater
    2           Repeater
    3           Repeater
    4           Repeater
                 ...    
    1670209    Refreshed
    1670210          New
    1670211     Repeater
    1670212     Repeater
    1670213     Repeater
    Name: NAME_CLIENT_TYPE, Length: 1670214, dtype: object



### Determine the percentage distribution of contract status in the dataset.


```python
df_2 = round((Client_Type.value_counts() / previous_data["NAME_CLIENT_TYPE"].count()) * 100, 2)
df_2 = pd.DataFrame(df_2)
df_2.reset_index(level = 0, inplace = True)

df_2.rename(columns = {
    "index" : "NAME_CLIENT_TYPE", 
    "NAME_CLIENT_TYPE" : "Percentage_of_Values"
  }, inplace = True
) 

df_2.sort_values(by = 'Percentage_of_Values' , inplace = True, ascending = False)
df_2
```





  <div id="df-5c6228f2-dffd-4fc4-9157-864fcba62622">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_CLIENT_TYPE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Repeater</td>
      <td>73.72</td>
    </tr>
    <tr>
      <th>1</th>
      <td>New</td>
      <td>18.04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Refreshed</td>
      <td>8.12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>XNA</td>
      <td>0.12</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5c6228f2-dffd-4fc4-9157-864fcba62622')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5c6228f2-dffd-4fc4-9157-864fcba62622 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5c6228f2-dffd-4fc4-9157-864fcba62622');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = ['Repeater', 'New', 'Refreshed', 'XNA']
sizes = df_2['Percentage_of_Values']

colors = ['lightcoral', 'lightskyblue', 'gold', 'yellowgreen']
explode = (0.1, 0.1, 0.1, 0.1)

plt.pie(sizes, 
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle = 140
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_243_0.png)
    


Based on the analysis, 73.4% of the applicants are repeat clients, while only 18.4% are new clients.


```python
Contract_Type = previous_data['NAME_CONTRACT_TYPE']
Contract_Type
```




    0          Consumer loans
    1              Cash loans
    2              Cash loans
    3              Cash loans
    4              Cash loans
                    ...      
    1670209    Consumer loans
    1670210    Consumer loans
    1670211    Consumer loans
    1670212        Cash loans
    1670213        Cash loans
    Name: NAME_CONTRACT_TYPE, Length: 1670214, dtype: object



### Calculate the percentage of contract statuses in the dataset.


```python
df_3 = round((Contract_Type.value_counts() / previous_data["NAME_CONTRACT_TYPE"].count()) * 100, 2)
df_3 = pd.DataFrame(df_3)
df_3.reset_index(level = 0, inplace = True)

df_3.rename(columns = {
    "index" : "NAME_CONTRACT_TYPE", 
    "NAME_CONTRACT_TYPE" : "Percentage_of_Values"
  }, inplace = True
)
 
df_3.sort_values(by = 'Percentage_of_Values' , inplace = True, ascending = False)
df_3
```





  <div id="df-9a396cd7-59cb-4179-bb3c-a3cedfd4f1cb">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_CONTRACT_TYPE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cash loans</td>
      <td>44.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Consumer loans</td>
      <td>43.66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Revolving loans</td>
      <td>11.57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>XNA</td>
      <td>0.02</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-9a396cd7-59cb-4179-bb3c-a3cedfd4f1cb')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-9a396cd7-59cb-4179-bb3c-a3cedfd4f1cb button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-9a396cd7-59cb-4179-bb3c-a3cedfd4f1cb');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = ['Cash loans', 'Consumer loans', 'Revolving loans', 'XNA']
sizes = df_3['Percentage_of_Values']

colors = ['yellowgreen', 'lightcoral', 'gold', 'lightskyblue']
explode = (0.1, 0.1, 0.1, 0.1)

plt.pie(sizes, 
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle = 140
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_248_0.png)
    


**Days of approval - WEEKDAY_APPR_PROCESS_START**


```python
Approval_days = previous_data['WEEKDAY_APPR_PROCESS_START']
Approval_days
```




    0           SATURDAY
    1           THURSDAY
    2            TUESDAY
    3             MONDAY
    4           THURSDAY
                 ...    
    1670209    WEDNESDAY
    1670210      TUESDAY
    1670211       MONDAY
    1670212    WEDNESDAY
    1670213       SUNDAY
    Name: WEEKDAY_APPR_PROCESS_START, Length: 1670214, dtype: object



### Determine the percentage distribution of contract statuses within the dataset.


```python
df_4 = round((Approval_days.value_counts() / previous_data["WEEKDAY_APPR_PROCESS_START"].count()) * 100, 2)
df_4 = pd.DataFrame(df_4)
df_4.reset_index(level = 0, inplace = True)

df_4.rename(columns = {
    "index" : "WEEKDAY_APPR_PROCESS_START", 
    "WEEKDAY_APPR_PROCESS_START" : "Percentage_of_Values"
  }, inplace = True
)
 
df_4.sort_values(by = 'Percentage_of_Values' , inplace = True, ascending = False)
df_4
```





  <div id="df-df1b693f-ea7a-4f46-b39a-e5c51627d162">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>WEEKDAY_APPR_PROCESS_START</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>TUESDAY</td>
      <td>15.27</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WEDNESDAY</td>
      <td>15.27</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MONDAY</td>
      <td>15.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FRIDAY</td>
      <td>15.09</td>
    </tr>
    <tr>
      <th>4</th>
      <td>THURSDAY</td>
      <td>14.91</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SATURDAY</td>
      <td>14.41</td>
    </tr>
    <tr>
      <th>6</th>
      <td>SUNDAY</td>
      <td>9.86</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-df1b693f-ea7a-4f46-b39a-e5c51627d162')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-df1b693f-ea7a-4f46-b39a-e5c51627d162 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-df1b693f-ea7a-4f46-b39a-e5c51627d162');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = ['TUESDAY', 'WEDNESDAY', 'MONDAY', 'THURSDAY' , 'FRIDAY' , 'SATURDAY' , 'SUNDAY']
sizes = df_4['Percentage_of_Values']

colors = ['gold', 'yellowgreen', 'lightcoral', 'lightskyblue' , '#44FF07' ,'Red','Fuchsia']
explode = (0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1)

plt.pie(sizes, 
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle = 30
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_253_0.png)
    


The majority of clients choose to apply for loans on Tuesdays, which is intriguing considering the relatively low number of applicants on weekends. 

It is unexpected, as one would assume that applicants would prefer weekends for the loan application process.

### **_Purpose of loan  - NAME_CASH_LOAN_PURPOSE_**


```python
Loan_Purpose = previous_data['NAME_CASH_LOAN_PURPOSE']
Loan_Purpose
```




    0              XAP
    1              XNA
    2              XNA
    3              XNA
    4          Repairs
                ...   
    1670209        XAP
    1670210        XAP
    1670211        XAP
    1670212        XNA
    1670213        XNA
    Name: NAME_CASH_LOAN_PURPOSE, Length: 1670214, dtype: object



### Calculate the percentage distribution of loan purposes in the dataset.


```python
df_5 = round((Loan_Purpose.value_counts() / previous_data["NAME_CASH_LOAN_PURPOSE"].count()) * 100, 2)
df_5 = pd.DataFrame(df_5)
df_5.reset_index(level = 0, inplace = True)

df_5.rename(columns = {
    "index" : "NAME_CASH_LOAN_PURPOSE", 
    "NAME_CASH_LOAN_PURPOSE" : "Percentage_of_Values"
  }, inplace = True
)
 
df_5.sort_values(by ='Percentage_of_Values', inplace = True, ascending = False)
df_5
```





  <div id="df-62f1ef5d-3403-4184-9a2b-53b03f3a1926">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_CASH_LOAN_PURPOSE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XAP</td>
      <td>55.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XNA</td>
      <td>40.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Repairs</td>
      <td>1.42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Other</td>
      <td>0.93</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Urgent needs</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Buying a used car</td>
      <td>0.17</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Building a house or an annex</td>
      <td>0.16</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Everyday expenses</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Medicine</td>
      <td>0.13</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Payments on other loans</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Education</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Journey</td>
      <td>0.07</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wedding / gift / holiday</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Purchase of electronic equipment</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Buying a new car</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Buying a home</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Car repairs</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Furniture</td>
      <td>0.04</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Buying a holiday home / land</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Business development</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Gasification / water supply</td>
      <td>0.02</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Buying a garage</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Hobby</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Money for a third person</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Refusal to name the goal</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-62f1ef5d-3403-4184-9a2b-53b03f3a1926')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-62f1ef5d-3403-4184-9a2b-53b03f3a1926 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-62f1ef5d-3403-4184-9a2b-53b03f3a1926');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (10, 4))
plot_2 = sns.barplot(x = "NAME_CASH_LOAN_PURPOSE", y = "Percentage_of_Values", data = df_5)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_259_0.png)
    


> The majority of loan purposes were not recorded, with the highest values being assigned to `XAP` and `XNA`

### **_Payment type - NAME_PAYMENT_TYPE_**

### Calculate the percentage distribution of payment types in the dataset.


```python
Payment_Type = previous_data['NAME_PAYMENT_TYPE']
df_6 = round((Payment_Type.value_counts() / previous_data["NAME_PAYMENT_TYPE"].count()) * 100, 2)

df_6 = pd.DataFrame(df_6)
df_6.reset_index(level = 0, inplace = True)

df_6.rename(columns = {
    "index" : "NAME_PAYMENT_TYPE", 
    "NAME_PAYMENT_TYPE" : "Percentage_of_Values"
  }, inplace = True
) 

df_6.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_6
```





  <div id="df-3244c71f-ada1-454f-9d03-f75005555ad4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_PAYMENT_TYPE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cash through the bank</td>
      <td>61.88</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XNA</td>
      <td>37.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Non-cash from your account</td>
      <td>0.49</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cashless from the account of the employer</td>
      <td>0.06</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3244c71f-ada1-454f-9d03-f75005555ad4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-3244c71f-ada1-454f-9d03-f75005555ad4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3244c71f-ada1-454f-9d03-f75005555ad4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "NAME_PAYMENT_TYPE", y = "Percentage_of_Values", data = df_6)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_264_0.png)
    


The majority of individuals (62.44%) opted for cash as their preferred payment method.

**Analyzing the reasons for loan rejection - CODE_REJECT_REASON.**

### Calculate the percentage distribution of payment types in the dataset.


```python
Code_Rejection = previous_data['CODE_REJECT_REASON']
df_7 = round((Code_Rejection.value_counts() / previous_data["CODE_REJECT_REASON"].count()) * 100, 2)
df_7 = pd.DataFrame(df_7)
df_7.reset_index(level = 0, inplace = True)

df_7.rename(columns = {
    "index" : "CODE_REJECT_REASON", 
    "CODE_REJECT_REASON" : "Percentage_of_Values"
  }, inplace = True
)
 
df_7.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_7
```





  <div id="df-d012508b-afdc-4a47-91f6-76eca73f9cee">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CODE_REJECT_REASON</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XAP</td>
      <td>81.01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>HC</td>
      <td>10.49</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LIMIT</td>
      <td>3.33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SCO</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CLIENT</td>
      <td>1.58</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SCOFR</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>6</th>
      <td>XNA</td>
      <td>0.31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>VERIF</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>8</th>
      <td>SYSTEM</td>
      <td>0.04</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d012508b-afdc-4a47-91f6-76eca73f9cee')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d012508b-afdc-4a47-91f6-76eca73f9cee button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d012508b-afdc-4a47-91f6-76eca73f9cee');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "CODE_REJECT_REASON", y = "Percentage_of_Values", data = df_7)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_269_0.png)
    


The primary reason for loan rejections is not recorded (**XAP (81%)**) followed by **HC**.

**Analyzing the types of goods for which clients applied in the previous application - NAME_GOODS_CATEGORY**

### Calculate the percentage of the goods that clients applied for in the previous application


```python
Goods_Category = previous_data['NAME_GOODS_CATEGORY']
df_8 = round((Goods_Category.value_counts() / previous_data["NAME_GOODS_CATEGORY"].count()) * 100, 2)
df_8 = pd.DataFrame(df_8)
df_8.reset_index(level = 0, inplace = True)

df_8.rename(columns = {
    "index" : "NAME_GOODS_CATEGORY", 
    "NAME_GOODS_CATEGORY" : "Percentage_of_Values"
  }, inplace = True
)
 
df_8.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_8
```





  <div id="df-7167d939-fbd1-4c61-b9e4-9feb838ef7ed">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_GOODS_CATEGORY</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XNA</td>
      <td>56.93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mobile</td>
      <td>13.45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Consumer Electronics</td>
      <td>7.28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Computers</td>
      <td>6.33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Audio/Video</td>
      <td>5.95</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Furniture</td>
      <td>3.21</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Photo / Cinema Equipment</td>
      <td>1.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Construction Materials</td>
      <td>1.50</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Clothing and Accessories</td>
      <td>1.41</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Auto Accessories</td>
      <td>0.44</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Jewelry</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Homewares</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Medical Supplies</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Vehicles</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Sport and Leisure</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Gardening</td>
      <td>0.16</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Other</td>
      <td>0.15</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Office Appliances</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Tourism</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Medicine</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Direct Sales</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Fitness</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Additional Service</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Education</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Weapon</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Insurance</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Animals</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>House Construction</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7167d939-fbd1-4c61-b9e4-9feb838ef7ed')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7167d939-fbd1-4c61-b9e4-9feb838ef7ed button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7167d939-fbd1-4c61-b9e4-9feb838ef7ed');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (10, 5))
plot_2 = sns.barplot(x = "NAME_GOODS_CATEGORY", y = "Percentage_of_Values", data = df_8)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_274_0.png)
    


The majority of clients applied for mobile goods, while `53.96%` of the data is not recorded (represented as `XNA`).

**Was the previous application for CASH, POS, CAR, … - NAME_PORTFOLIO**

### Calculate the percentage distribution of portfolios in the dataset.


```python
Portfolio= previous_data['NAME_PORTFOLIO']
df_9 = round((Portfolio.value_counts() / previous_data["NAME_PORTFOLIO"].count()) * 100, 2)
df_9 = pd.DataFrame(df_9)
df_9.reset_index(level = 0, inplace = True)

df_9.rename(columns = {
    "index" : "NAME_PORTFOLIO", 
    "NAME_PORTFOLIO" : "Percentage_of_Values"
  }, inplace = True
)

df_9.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_9
```





  <div id="df-6f0265fa-1a55-4275-b486-50359d87f4eb">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_PORTFOLIO</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>POS</td>
      <td>41.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cash</td>
      <td>27.63</td>
    </tr>
    <tr>
      <th>2</th>
      <td>XNA</td>
      <td>22.29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cards</td>
      <td>8.68</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cars</td>
      <td>0.03</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6f0265fa-1a55-4275-b486-50359d87f4eb')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6f0265fa-1a55-4275-b486-50359d87f4eb button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6f0265fa-1a55-4275-b486-50359d87f4eb');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = df_9.NAME_PORTFOLIO
sizes = df_9.Percentage_of_Values
colors = ['gold', 'yellowgreen', 'lightcoral', 'lightskyblue','Fuchsia']
explode = (0.1, 0.1, 0.1, 0.1, 0.1)

plt.pie(sizes, 
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle=140
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_278_0.png)
    


POS accounted for 41.4% of the applications.

**Analyzing the types of previous application methods - NAME_PRODUCT_TYPE (X-Sell or Walk-in).**

### Calculate the percentage distribution of product types in the dataset.


```python
Product_Type = previous_data['NAME_PRODUCT_TYPE']
df_10 = round((Product_Type.value_counts() / previous_data["NAME_PRODUCT_TYPE"].count()) * 100, 2)
df_10 = pd.DataFrame(df_10)
df_10.reset_index(level = 0, inplace = True)

df_10.rename(columns = {
    "index" : "NAME_PRODUCT_TYPE", 
    "NAME_PRODUCT_TYPE" : "Percentage_of_Values"
  }, inplace = True
)
 
df_10.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_10
```





  <div id="df-fd3c9940-23b7-4526-92cf-39ca91cd7cb1">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_PRODUCT_TYPE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XNA</td>
      <td>63.68</td>
    </tr>
    <tr>
      <th>1</th>
      <td>x-sell</td>
      <td>27.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>walk-in</td>
      <td>9.00</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fd3c9940-23b7-4526-92cf-39ca91cd7cb1')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fd3c9940-23b7-4526-92cf-39ca91cd7cb1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fd3c9940-23b7-4526-92cf-39ca91cd7cb1');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
labels = df_10.NAME_PRODUCT_TYPE
sizes = df_10.Percentage_of_Values
colors = ['gold', 'yellowgreen', 'lightcoral']
explode = (0.1, 0.1, 0.1)  

plt.pie(sizes,
  explode = explode, 
  labels = labels, 
  colors = colors,
  autopct = '%1.1f%%', 
  shadow = True, 
  startangle = 140
)

plt.axis('equal')
plt.show()
```


    
![png](README_files/README_282_0.png)
    


X-sell applications accounted for a higher percentage compared to walk-in applications.

**Analyzing the channels through which clients were acquired in the previous application - CHANNEL_TYPE.**

### Calculate the percentage distribution of channels through which clients applied for a loan.


```python
Channel_Type = previous_data['CHANNEL_TYPE']
df_11 = round((Channel_Type.value_counts() / previous_data["CHANNEL_TYPE"].count()) * 100, 2)
df_11 = pd.DataFrame(df_11)
df_11.reset_index(level = 0, inplace = True)

df_11.rename(columns = {
    "index" : "CHANNEL_TYPE", 
    "CHANNEL_TYPE" : "Percentage_of_Values"
  }, inplace = True
)
 
df_11.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_11
```





  <div id="df-f0839272-8512-4dbc-8b4a-7dc8684656a2">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CHANNEL_TYPE</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Credit and cash offices</td>
      <td>43.11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Country-wide</td>
      <td>29.62</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Stone</td>
      <td>12.70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Regional / Local</td>
      <td>6.50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Contact center</td>
      <td>4.27</td>
    </tr>
    <tr>
      <th>5</th>
      <td>AP+ (Cash loan)</td>
      <td>3.42</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Channel of corporate sales</td>
      <td>0.37</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Car dealer</td>
      <td>0.03</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f0839272-8512-4dbc-8b4a-7dc8684656a2')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f0839272-8512-4dbc-8b4a-7dc8684656a2 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f0839272-8512-4dbc-8b4a-7dc8684656a2');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "CHANNEL_TYPE", y = "Percentage_of_Values", data = df_11)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_287_0.png)
    


The majority of clients were acquired through Credit and Cash Offices.

**Analyzing the industry of the seller in the previous application - NAME_SELLER_INDUSTRY**

### Determining the percentage of goods that clients applied for


```python
Seller_Industry = previous_data['NAME_SELLER_INDUSTRY']
df_12 = round((Seller_Industry.value_counts() / previous_data["NAME_SELLER_INDUSTRY"].count()) * 100, 2)
df_12 = pd.DataFrame(df_12)
df_12.reset_index(level = 0, inplace = True)

df_12.rename(columns = {
    "index" : "NAME_SELLER_INDUSTRY", 
    "NAME_SELLER_INDUSTRY" : "Percentage_of_Values"
  }, inplace = True
)
 
df_12.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_12
```





  <div id="df-60ae656b-31a6-4cfc-b9e2-7fcbe0c3b0e7">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_SELLER_INDUSTRY</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XNA</td>
      <td>51.23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Consumer electronics</td>
      <td>23.85</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Connectivity</td>
      <td>16.53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furniture</td>
      <td>3.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Construction</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Clothing</td>
      <td>1.43</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Industry</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Auto technology</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Jewelry</td>
      <td>0.16</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MLM partners</td>
      <td>0.07</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Tourism</td>
      <td>0.03</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-60ae656b-31a6-4cfc-b9e2-7fcbe0c3b0e7')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-60ae656b-31a6-4cfc-b9e2-7fcbe0c3b0e7 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-60ae656b-31a6-4cfc-b9e2-7fcbe0c3b0e7');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "NAME_SELLER_INDUSTRY", y = "Percentage_of_Values", data = df_12)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_292_0.png)
    


The majority of sellers belong to the **Consumer Electronics** industry.

**Grouped interest rate into small medium and high of the previous application - NAME_YIELD_GROUP**

### find the percentage of Interest rate into small medium and high


```python
Yield_Groups = previous_data['NAME_YIELD_GROUP']
df_13 = round((Yield_Groups.value_counts() / previous_data["NAME_YIELD_GROUP"].count()) * 100, 2)
df_13 = pd.DataFrame(df_13)
df_13.reset_index(level = 0, inplace = True)

df_13.rename(columns = {
    "index" : "NAME_YIELD_GROUP", 
    "NAME_YIELD_GROUP" : "Percentage_of_Values"
  }, inplace = True
)
 
df_13.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_13
```





  <div id="df-b46cc69b-e81e-43e5-9fa1-1c5bd0d5191e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME_YIELD_GROUP</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>XNA</td>
      <td>30.97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>middle</td>
      <td>23.08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>high</td>
      <td>21.15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>low_normal</td>
      <td>19.28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>low_action</td>
      <td>5.51</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b46cc69b-e81e-43e5-9fa1-1c5bd0d5191e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b46cc69b-e81e-43e5-9fa1-1c5bd0d5191e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b46cc69b-e81e-43e5-9fa1-1c5bd0d5191e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "NAME_YIELD_GROUP", y = "Percentage_of_Values", data = df_13)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_296_0.png)
    


The majority of the interest rates fall within the medium range

**Detailed information about the product combinations in the previous application - PRODUCT_COMBINATION**

### Calculate the percentage of different product combinations


```python
Product_Combination = previous_data['PRODUCT_COMBINATION']
df_14 = round((Product_Combination.value_counts() / previous_data["PRODUCT_COMBINATION"].count()) * 100, 2)
df_14 = pd.DataFrame(df_14)
df_14.reset_index(level = 0, inplace = True)

df_14.rename(columns = {
    "index" : "PRODUCT_COMBINATION", 
    "PRODUCT_COMBINATION" : "Percentage_of_Values"
  }, inplace = True
)
 
df_14.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_14
```





  <div id="df-bd63d51a-b500-4269-a1d0-ee8f2398ca34">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PRODUCT_COMBINATION</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cash</td>
      <td>17.14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>POS household with interest</td>
      <td>15.78</td>
    </tr>
    <tr>
      <th>2</th>
      <td>POS mobile with interest</td>
      <td>13.21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cash X-Sell: middle</td>
      <td>8.61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cash X-Sell: low</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Card Street</td>
      <td>6.74</td>
    </tr>
    <tr>
      <th>6</th>
      <td>POS industry with interest</td>
      <td>5.92</td>
    </tr>
    <tr>
      <th>7</th>
      <td>POS household without interest</td>
      <td>4.96</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Card X-Sell</td>
      <td>4.82</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Cash Street: high</td>
      <td>3.57</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Cash X-Sell: high</td>
      <td>3.55</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Cash Street: middle</td>
      <td>2.08</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Cash Street: low</td>
      <td>2.03</td>
    </tr>
    <tr>
      <th>13</th>
      <td>POS mobile without interest</td>
      <td>1.44</td>
    </tr>
    <tr>
      <th>14</th>
      <td>POS other with interest</td>
      <td>1.43</td>
    </tr>
    <tr>
      <th>15</th>
      <td>POS industry without interest</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>16</th>
      <td>POS others without interest</td>
      <td>0.15</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-bd63d51a-b500-4269-a1d0-ee8f2398ca34')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-bd63d51a-b500-4269-a1d0-ee8f2398ca34 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-bd63d51a-b500-4269-a1d0-ee8f2398ca34');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (15, 4))
plot_2 = sns.barplot(x = "PRODUCT_COMBINATION", y = "Percentage_of_Values", data = df_14)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_300_0.png)
    


The most common product combination is **Cash**, followed by **POS household** with interest.

**Flag if the application was the last application per day of the client - NFLAG_LAST_APPL_IN_DAY**

### Determine the percentage of clients who requested insurance


```python
Insurance = previous_data['NFLAG_LAST_APPL_IN_DAY']
df_15 = round((Insurance.value_counts() / previous_data["NFLAG_LAST_APPL_IN_DAY"].count()) * 100, 2)
df_15 = pd.DataFrame(df_15)
df_15.reset_index(level = 0, inplace = True)

df_15.rename(columns = {
    "index" : "INSURANCE_FLAG", 
    "NFLAG_LAST_APPL_IN_DAY" : "Percentage_of_Values"
  }, inplace = True
)
 
df_15.sort_values(by = 'Percentage_of_Values', inplace = True, ascending = False)
df_15
```





  <div id="df-7d514bef-5fc0-4997-84fe-4f1d5a92cdb4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>INSURANCE_FLAG</th>
      <th>Percentage_of_Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>99.65</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7d514bef-5fc0-4997-84fe-4f1d5a92cdb4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7d514bef-5fc0-4997-84fe-4f1d5a92cdb4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7d514bef-5fc0-4997-84fe-4f1d5a92cdb4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
f, ax = plt.subplots(figsize = (5, 4))
plot_2 = sns.barplot(x = "INSURANCE_FLAG", y = "Percentage_of_Values", data = df_15)
plot_2.set_xticklabels(plot_2.get_xticklabels(), rotation = 90)
plt.show()
```


    
![png](README_files/README_304_0.png)
    


The majority of clients made their last application of the day


```python
previous_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1670214 entries, 0 to 1670213
    Data columns (total 23 columns):
     #   Column                       Non-Null Count    Dtype  
    ---  ------                       --------------    -----  
     0   SK_ID_PREV                   1670214 non-null  int64  
     1   SK_ID_CURR                   1670214 non-null  int64  
     2   NAME_CONTRACT_TYPE           1670214 non-null  object 
     3   AMT_APPLICATION              1670214 non-null  float64
     4   AMT_CREDIT                   1670213 non-null  float64
     5   WEEKDAY_APPR_PROCESS_START   1670214 non-null  object 
     6   HOUR_APPR_PROCESS_START      1670214 non-null  int64  
     7   FLAG_LAST_APPL_PER_CONTRACT  1670214 non-null  object 
     8   NFLAG_LAST_APPL_IN_DAY       1670214 non-null  int64  
     9   NAME_CASH_LOAN_PURPOSE       1670214 non-null  object 
     10  NAME_CONTRACT_STATUS         1670214 non-null  object 
     11  DAYS_DECISION                1670214 non-null  int64  
     12  NAME_PAYMENT_TYPE            1670214 non-null  object 
     13  CODE_REJECT_REASON           1670214 non-null  object 
     14  NAME_CLIENT_TYPE             1670214 non-null  object 
     15  NAME_GOODS_CATEGORY          1670214 non-null  object 
     16  NAME_PORTFOLIO               1670214 non-null  object 
     17  NAME_PRODUCT_TYPE            1670214 non-null  object 
     18  CHANNEL_TYPE                 1670214 non-null  object 
     19  SELLERPLACE_AREA             1670214 non-null  int64  
     20  NAME_SELLER_INDUSTRY         1670214 non-null  object 
     21  NAME_YIELD_GROUP             1670214 non-null  object 
     22  PRODUCT_COMBINATION          1670214 non-null  object 
    dtypes: float64(2), int64(6), object(15)
    memory usage: 293.1+ MB


**Correlation in previous_data df**


```python
Correlation = previous_data.corr()
f, ax = plt.subplots(figsize = (20, 12))
sns.heatmap(Correlation,annot = True)
plt.show()
```


    
![png](README_files/README_308_0.png)
    


The above plot illustrates the correlation between variables in the previous application.


```python
prev_app_df = pd.merge(
                previous_data, 
                application_data,
                how = "inner",
                on = "SK_ID_CURR"
              )

prev_app_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 1413701 entries, 0 to 1413700
    Data columns (total 58 columns):
     #   Column                        Non-Null Count    Dtype  
    ---  ------                        --------------    -----  
     0   SK_ID_PREV                    1413701 non-null  int64  
     1   SK_ID_CURR                    1413701 non-null  int64  
     2   NAME_CONTRACT_TYPE_x          1413701 non-null  object 
     3   AMT_APPLICATION               1413701 non-null  float64
     4   AMT_CREDIT_x                  1413700 non-null  float64
     5   WEEKDAY_APPR_PROCESS_START_x  1413701 non-null  object 
     6   HOUR_APPR_PROCESS_START       1413701 non-null  int64  
     7   FLAG_LAST_APPL_PER_CONTRACT   1413701 non-null  object 
     8   NFLAG_LAST_APPL_IN_DAY        1413701 non-null  int64  
     9   NAME_CASH_LOAN_PURPOSE        1413701 non-null  object 
     10  NAME_CONTRACT_STATUS          1413701 non-null  object 
     11  DAYS_DECISION                 1413701 non-null  int64  
     12  NAME_PAYMENT_TYPE             1413701 non-null  object 
     13  CODE_REJECT_REASON            1413701 non-null  object 
     14  NAME_CLIENT_TYPE              1413701 non-null  object 
     15  NAME_GOODS_CATEGORY           1413701 non-null  object 
     16  NAME_PORTFOLIO                1413701 non-null  object 
     17  NAME_PRODUCT_TYPE             1413701 non-null  object 
     18  CHANNEL_TYPE                  1413701 non-null  object 
     19  SELLERPLACE_AREA              1413701 non-null  int64  
     20  NAME_SELLER_INDUSTRY          1413701 non-null  object 
     21  NAME_YIELD_GROUP              1413701 non-null  object 
     22  PRODUCT_COMBINATION           1413701 non-null  object 
     23  TARGET                        1413701 non-null  int64  
     24  NAME_CONTRACT_TYPE_y          1413701 non-null  object 
     25  CODE_GENDER                   1413701 non-null  object 
     26  FLAG_OWN_CAR                  1413701 non-null  object 
     27  FLAG_OWN_REALTY               1413701 non-null  object 
     28  CNT_CHILDREN                  1413701 non-null  float64
     29  AMT_CREDIT_y                  1413701 non-null  float64
     30  AMT_ANNUITY                   1413701 non-null  float64
     31  AMT_GOODS_PRICE               1413701 non-null  float64
     32  NAME_TYPE_SUITE               1413701 non-null  object 
     33  NAME_INCOME_TYPE              1413701 non-null  object 
     34  NAME_EDUCATION_TYPE           1413701 non-null  object 
     35  NAME_FAMILY_STATUS            1413701 non-null  object 
     36  NAME_HOUSING_TYPE             1413701 non-null  object 
     37  REGION_POPULATION_RELATIVE    1413701 non-null  float64
     38  DAYS_EMPLOYED                 1413701 non-null  float64
     39  DAYS_REGISTRATION             1413701 non-null  float64
     40  DAYS_ID_PUBLISH               1413701 non-null  int64  
     41  CNT_FAM_MEMBERS               1413701 non-null  float64
     42  FLAG_EMP_PHONE                1413701 non-null  int64  
     43  FLAG_WORK_PHONE               1413701 non-null  int64  
     44  FLAG_CONT_MOBILE              1413701 non-null  int64  
     45  FLAG_EMAIL                    1413701 non-null  int64  
     46  REGION_RATING_CLIENT          1413701 non-null  int64  
     47  REGION_RATING_CLIENT_W_CITY   1413701 non-null  int64  
     48  WEEKDAY_APPR_PROCESS_START_y  1413701 non-null  object 
     49  REG_REGION_NOT_LIVE_REGION    1413701 non-null  int64  
     50  REG_REGION_NOT_WORK_REGION    1413701 non-null  int64  
     51  REG_CITY_NOT_LIVE_CITY        1413701 non-null  int64  
     52  REG_CITY_NOT_WORK_CITY        1413701 non-null  int64  
     53  ORGANIZATION_TYPE             1413701 non-null  object 
     54  EXT_SOURCE_2                  1413701 non-null  float64
     55  DAYS_LAST_PHONE_CHANGE        1413701 non-null  float64
     56  AGE                           1413701 non-null  int64  
     57  SALARY_CATEGORY               1413701 non-null  object 
    dtypes: float64(12), int64(19), object(27)
    memory usage: 636.4+ MB


### Calculate the percentage of null values in each column to determine the required cleaning actions


```python
prev_app_df.isnull().sum() * 100 / len(prev_app_df)
```




    SK_ID_PREV                      0.000000
    SK_ID_CURR                      0.000000
    NAME_CONTRACT_TYPE_x            0.000000
    AMT_APPLICATION                 0.000000
    AMT_CREDIT_x                    0.000071
    WEEKDAY_APPR_PROCESS_START_x    0.000000
    HOUR_APPR_PROCESS_START         0.000000
    FLAG_LAST_APPL_PER_CONTRACT     0.000000
    NFLAG_LAST_APPL_IN_DAY          0.000000
    NAME_CASH_LOAN_PURPOSE          0.000000
    NAME_CONTRACT_STATUS            0.000000
    DAYS_DECISION                   0.000000
    NAME_PAYMENT_TYPE               0.000000
    CODE_REJECT_REASON              0.000000
    NAME_CLIENT_TYPE                0.000000
    NAME_GOODS_CATEGORY             0.000000
    NAME_PORTFOLIO                  0.000000
    NAME_PRODUCT_TYPE               0.000000
    CHANNEL_TYPE                    0.000000
    SELLERPLACE_AREA                0.000000
    NAME_SELLER_INDUSTRY            0.000000
    NAME_YIELD_GROUP                0.000000
    PRODUCT_COMBINATION             0.000000
    TARGET                          0.000000
    NAME_CONTRACT_TYPE_y            0.000000
    CODE_GENDER                     0.000000
    FLAG_OWN_CAR                    0.000000
    FLAG_OWN_REALTY                 0.000000
    CNT_CHILDREN                    0.000000
    AMT_CREDIT_y                    0.000000
    AMT_ANNUITY                     0.000000
    AMT_GOODS_PRICE                 0.000000
    NAME_TYPE_SUITE                 0.000000
    NAME_INCOME_TYPE                0.000000
    NAME_EDUCATION_TYPE             0.000000
    NAME_FAMILY_STATUS              0.000000
    NAME_HOUSING_TYPE               0.000000
    REGION_POPULATION_RELATIVE      0.000000
    DAYS_EMPLOYED                   0.000000
    DAYS_REGISTRATION               0.000000
    DAYS_ID_PUBLISH                 0.000000
    CNT_FAM_MEMBERS                 0.000000
    FLAG_EMP_PHONE                  0.000000
    FLAG_WORK_PHONE                 0.000000
    FLAG_CONT_MOBILE                0.000000
    FLAG_EMAIL                      0.000000
    REGION_RATING_CLIENT            0.000000
    REGION_RATING_CLIENT_W_CITY     0.000000
    WEEKDAY_APPR_PROCESS_START_y    0.000000
    REG_REGION_NOT_LIVE_REGION      0.000000
    REG_REGION_NOT_WORK_REGION      0.000000
    REG_CITY_NOT_LIVE_CITY          0.000000
    REG_CITY_NOT_WORK_CITY          0.000000
    ORGANIZATION_TYPE               0.000000
    EXT_SOURCE_2                    0.000000
    DAYS_LAST_PHONE_CHANGE          0.000000
    AGE                             0.000000
    SALARY_CATEGORY                 0.000000
    dtype: float64



**Correlation between previous_data and application_data dataframes**


```python
Correlation = prev_app_df.corr()
Correlation.sort_values(by = ["TARGET"], ascending = False, inplace = True)

f, ax = plt.subplots(figsize = (20, 12))
sns.heatmap(Correlation, annot = True)
plt.show()
```


    
![png](README_files/README_314_0.png)
    


The above plot represents the correlation between the `previous_data` and `application_data` dataframes.


```python
Correlation.head()["TARGET"][1:]
```




    DAYS_LAST_PHONE_CHANGE         0.059721
    REGION_RATING_CLIENT_W_CITY    0.059700
    REGION_RATING_CLIENT           0.056932
    DAYS_ID_PUBLISH                0.051037
    Name: TARGET, dtype: float64




```python
Correlation.tail()["TARGET"][1:]
```




    AMT_GOODS_PRICE              -0.032550
    REGION_POPULATION_RELATIVE   -0.035028
    AGE                          -0.074810
    EXT_SOURCE_2                 -0.154919
    Name: TARGET, dtype: float64



#### Similarly, in this case as well, we can observe that the same variables that we identified in the application data are also playing a significant role in identifying the defaulters.


```python

```
