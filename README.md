# [Projeto 1: HeartFailure](https://github.com/leoprasel/Portfolio)
## Resumo:
* Projeto de análise de dados e machine learning utilizando banco de dados do Kaggle, com dados sobre pacientes que tiveram ataques cardíacos e suas características físicas 


{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt\n",
    "\n",
    "database_url = 'https://raw.githubusercontent.com/leoprasel/Portfolio/main/heart_failure_clinical_records_dataset.csv'\n",
    "\n",
    "df = pd.read_csv(database_url)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Understanding the data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>age</th>\n",
       "      <th>anaemia</th>\n",
       "      <th>creatinine_phosphokinase</th>\n",
       "      <th>diabetes</th>\n",
       "      <th>ejection_fraction</th>\n",
       "      <th>high_blood_pressure</th>\n",
       "      <th>platelets</th>\n",
       "      <th>serum_creatinine</th>\n",
       "      <th>serum_sodium</th>\n",
       "      <th>sex</th>\n",
       "      <th>smoking</th>\n",
       "      <th>DEATH_EVENT</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>75.0</td>\n",
       "      <td>0</td>\n",
       "      <td>582</td>\n",
       "      <td>0</td>\n",
       "      <td>20</td>\n",
       "      <td>1</td>\n",
       "      <td>265000.00</td>\n",
       "      <td>1.9</td>\n",
       "      <td>130</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>55.0</td>\n",
       "      <td>0</td>\n",
       "      <td>7861</td>\n",
       "      <td>0</td>\n",
       "      <td>38</td>\n",
       "      <td>0</td>\n",
       "      <td>263358.03</td>\n",
       "      <td>1.1</td>\n",
       "      <td>136</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>65.0</td>\n",
       "      <td>0</td>\n",
       "      <td>146</td>\n",
       "      <td>0</td>\n",
       "      <td>20</td>\n",
       "      <td>0</td>\n",
       "      <td>162000.00</td>\n",
       "      <td>1.3</td>\n",
       "      <td>129</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>50.0</td>\n",
       "      <td>1</td>\n",
       "      <td>111</td>\n",
       "      <td>0</td>\n",
       "      <td>20</td>\n",
       "      <td>0</td>\n",
       "      <td>210000.00</td>\n",
       "      <td>1.9</td>\n",
       "      <td>137</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>65.0</td>\n",
       "      <td>1</td>\n",
       "      <td>160</td>\n",
       "      <td>1</td>\n",
       "      <td>20</td>\n",
       "      <td>0</td>\n",
       "      <td>327000.00</td>\n",
       "      <td>2.7</td>\n",
       "      <td>116</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    age  anaemia  creatinine_phosphokinase  diabetes  ejection_fraction  \\\n",
       "0  75.0        0                       582         0                 20   \n",
       "1  55.0        0                      7861         0                 38   \n",
       "2  65.0        0                       146         0                 20   \n",
       "3  50.0        1                       111         0                 20   \n",
       "4  65.0        1                       160         1                 20   \n",
       "\n",
       "   high_blood_pressure  platelets  serum_creatinine  serum_sodium  sex  \\\n",
       "0                    1  265000.00               1.9           130    1   \n",
       "1                    0  263358.03               1.1           136    1   \n",
       "2                    0  162000.00               1.3           129    1   \n",
       "3                    0  210000.00               1.9           137    1   \n",
       "4                    0  327000.00               2.7           116    0   \n",
       "\n",
       "   smoking  DEATH_EVENT  \n",
       "0        0            1  \n",
       "1        0            1  \n",
       "2        1            1  \n",
       "3        0            1  \n",
       "4        0            1  "
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = df.drop('time', axis = 1)\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Data cleaning"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [],
   "source": [
    "#change datatypes\n",
    "\n",
    "DataTypes = {\n",
    "    #quantitative\n",
    "    'age': int,\n",
    "    'creatinine_phosphokinase': int,\n",
    "    'ejection_fraction': int,\n",
    "    'platelets': float,\n",
    "    'serum_creatinine': float,\n",
    "    'serum_sodium': int,\n",
    "    #categorical\n",
    "    'anaemia': int,\n",
    "    'diabetes': int,\n",
    "    'high_blood_pressure': int,\n",
    "    'sex': int,\n",
    "    'smoking': int,\n",
    "    'DEATH_EVENT': int,\n",
    "}\n",
    "df = df.astype(DataTypes)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Value count 299\n",
      "\n",
      "Null values \n",
      "\n",
      "age                         0\n",
      "anaemia                     0\n",
      "creatinine_phosphokinase    0\n",
      "diabetes                    0\n",
      "ejection_fraction           0\n",
      "high_blood_pressure         0\n",
      "platelets                   0\n",
      "serum_creatinine            0\n",
      "serum_sodium                0\n",
      "sex                         0\n",
      "smoking                     0\n",
      "DEATH_EVENT                 0\n",
      "dtype: int64\n",
      "\n",
      "NA values \n",
      "\n",
      "age                         0\n",
      "anaemia                     0\n",
      "creatinine_phosphokinase    0\n",
      "diabetes                    0\n",
      "ejection_fraction           0\n",
      "high_blood_pressure         0\n",
      "platelets                   0\n",
      "serum_creatinine            0\n",
      "serum_sodium                0\n",
      "sex                         0\n",
      "smoking                     0\n",
      "DEATH_EVENT                 0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "#check null and na values\n",
    "\n",
    "print('Value count', df.age.count())\n",
    "print('\\nNull values \\n')\n",
    "print(df.isnull().sum())\n",
    "print('\\nNA values \\n')\n",
    "print(df.isna().sum())"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Insights"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Average survival age: 60.82943143812709\n",
      "Average death age: 65.20833333333333\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x26eed9ee5f8>"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "print('Average survival age:', df.age.mean())\n",
    "print('Average death age:', df[df['DEATH_EVENT'] == 1].age.mean())\n",
    "\n",
    "sns.distplot( df.age , color = \"skyblue\", label = \"Survived Patients\")\n",
    "sns.distplot( df[df['DEATH_EVENT'] == 1].age , color = \"orange\", label = \"Deceased Patients\")\n",
    "plt.legend()\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### There is small difference between the distribution of the age of both alive and dead patients"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x26efca95c18>"
      ]
     },
     "execution_count": 49,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.countplot(data = df, x = df.DEATH_EVENT, hue = 'anaemia')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Both in alive and dead patients, there were more people without anaemia than with it, showing no correlation between the feature and the effect"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x26efe4a1c18>"
      ]
     },
     "execution_count": 70,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(x = df.sex.replace({0:'Female',1:\"Male\"}), y = df.serum_creatinine, hue = df.DEATH_EVENT, palette = 'Set2')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### The low creatinine in the blood seems to be a very important factor in the survival of the patient"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x177cf91c6d8>"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "gender_type_list = ['Male Smokers','Male non-Smoker','Female Smoker','Female non-Smoker'] \n",
    "gender_type_count = [df[(df.smoking == 1)&(df.sex == 1)].sex.count(),\n",
    "                         df[(df.smoking == 0)&(df.sex == 1)].sex.count(),\n",
    "                         df[(df.smoking == 1)&(df.sex == 0)].sex.count(),\n",
    "                         df[(df.smoking == 0)&(df.sex == 0)].sex.count()]\n",
    "gender_type_percentile = [df[(df.smoking == 1)&(df.sex == 1)].sex.count()/df.sex.count(),\n",
    "                         df[(df.smoking == 0)&(df.sex == 1)].sex.count()/df.sex.count(),\n",
    "                         df[(df.smoking == 1)&(df.sex == 0)].sex.count()/df.sex.count(),\n",
    "                         df[(df.smoking == 0)&(df.sex == 0)].sex.count()/df.sex.count()]\n",
    "\n",
    "\n",
    "gender_type = pd.DataFrame(data = {'Gender Type': gender_type_list, \n",
    "                                   'Count': gender_type_count,\n",
    "                                   'Percentile': gender_type_percentile}).sort_values('Count', ascending=False)\n",
    "\n",
    "sns.barplot(data=gender_type, x = 'Count', y = 'Gender Type', palette = 'Paired')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x26efe504a90>"
      ]
     },
     "execution_count": 71,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAYUAAAEHCAYAAABBW1qbAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4xLjAsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+17YcXAAAV3UlEQVR4nO3df5TV9X3n8ecbQanVxF+jKIMZMJqoUKudYGKi+WEblRDERruyzQYjOawnWm26En9ko0m2OcfG7KZpzJrDqkF7sogHzaJGaZQNVSL+ANSCkFarWR0lMGKwTVprwPf+cb/z9Xa8wHWYe+/M3OfjnDlzv5/vr/flcOZ1Pp/v9/v5RmYiSRLAqFYXIEkaOgwFSVLJUJAklQwFSVLJUJAklUa3uoDdcdBBB2VXV1ery5CkYWX16tUvZ2ZHrXXDOhS6urpYtWpVq8uQpGElIv7fjtY5fCRJKjUsFCLipojYHBHraqy7NCIyIg4qliMi/ioinomIv4uIExpVlyRpxxrZU1gAnN6/MSImAH8APF/VfAZwZPEzF7i+gXVJknagYdcUMvOBiOiqsepbwBeBJVVtZwK3ZGXOjYcjYr+IODQzNzaqPknamd/85jf09PTw2muvtbqUARs7diydnZ2MGTOm7n2aeqE5ImYAL2bmkxFRvWo88ELVck/R9pZQiIi5VHoTHH744Y0rVlJb6+npYd9996Wrq4t+f6+Ghcxky5Yt9PT0MHHixLr3a9qF5ojYG/gScFWt1TXaas7Ul5nzM7M7M7s7OmreUSVJu+21117jwAMPHJaBABARHHjggW+7p9PMnsIRwESgr5fQCayJiKlUegYTqrbtBF5qYm2S9BbDNRD6DKT+pvUUMnNtZh6cmV2Z2UUlCE7IzF8AdwKfKe5Cej/wqtcTJKn5GnlL6kJgJfCeiOiJiDk72fwe4FngGeB/AZ9vVF2SNBQsX76c6dOnv6X9zjvv5JprrmlBRRWNvPto1i7Wd1V9TuDCRtWyM78375ZWnHZIWn3tZ1pdgtT2ZsyYwYwZM1p2fp9olqQ6/PrXv+YTn/gExx13HJMnT2bRokV0dXVx5ZVX8oEPfIDu7m7WrFnDaaedxhFHHMH3vvc9oHIX0Lx585g8eTJTpkxh0aJFbzn2Y489xvHHH8+zzz7LggULuOiiiwA477zzuPjiiznppJOYNGkSixcvBuCNN97g85//PMceeyzTp09n2rRp5brdZShIUh2WLl3KYYcdxpNPPsm6des4/fTKs7kTJkxg5cqVnHzyyZx33nksXryYhx9+mKuuqtxoeccdd/DEE0/w5JNPcv/99zNv3jw2bnzzkulDDz3EBRdcwJIlS5g0adJbzrtx40ZWrFjB3XffzeWXX14e8+c//zlr167lhhtuYOXKlYP2PQ0FSarDlClTuP/++7nssst48MEHeec73wlQDvVMmTKFE088kX333ZeOjg7Gjh3L1q1bWbFiBbNmzWKPPfbgkEMO4cMf/jCPPfYYABs2bGDu3LncddddO3zuaubMmYwaNYpjjjmGTZs2AbBixQrOOeccRo0axbhx4/joRz86aN9zWM+SKknNctRRR7F69WruuecerrjiCj7+8Y8DsNdeewEwatSo8nPf8rZt26hcMq3t0EMP5bXXXuPxxx/nsMMOq7lN9TH7jrWzY+4uewqSVIeXXnqJvffem09/+tNceumlrFmzpq79TjnlFBYtWsT27dvp7e3lgQceYOrUqQDst99+/OhHP+LKK69k+fLlddfyoQ99iNtvv5033niDTZs2va19d8WegiTVYe3atcybN49Ro0YxZswYrr/+es4+++xd7nfWWWexcuVKjjvuOCKCb3zjG4wbN46f/exnABxyyCHcddddnHHGGdx000111fKpT32KZcuWMXnyZI466ihOPPHEcjhrd0UjuyGN1t3dnbv7kh1vSX2Tt6RKb9qwYQNHH310q8vYoV/96lfss88+bNmyhalTp/LTn/6UcePGvWW7Wt8jIlZnZnet49pTkKRhaPr06WzdupXXX3+dL3/5yzUDYSAMBUkahgbzOkI1LzRLkkqGgiSpZChIkkqGgiSp5IVmSRqAwb6dvZ5bwpcuXcoll1zC9u3b+dznPlfOhTSY7ClI0jCwfft2LrzwQu69917Wr1/PwoULWb9+/aCfx1CQpGHg0Ucf5d3vfjeTJk1izz335Nxzz2XJkiWDfh5DQZKGgRdffJEJE958lX1nZycvvvjioJ/HUJCkYaDWlEQRMejnMRQkaRjo7OzkhRdeKJd7enp2ON327jAUJGkYeN/73sfTTz/Nc889x+uvv86tt97akHc5e0uqJA1As2cVHj16NNdddx2nnXYa27dv5/zzz+fYY48d/PMM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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.countplot(data = df, x = df.DEATH_EVENT, hue = 'smoking')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### There isn't much data from female smokers, and there is no relevant information between the correlation of smoking and heart attacks"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Machine learning model"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## First test"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.ensemble import RandomForestClassifier\n",
    "from sklearn.model_selection import train_test_split\n",
    "from sklearn.metrics import confusion_matrix\n",
    "from sklearn.metrics import classification_report"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [],
   "source": [
    "x = df.drop('DEATH_EVENT',axis=1) #features\n",
    "y = df.DEATH_EVENT #target\n",
    "x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.3, random_state = 100)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini',\n",
       "                       max_depth=None, max_features='auto', max_leaf_nodes=None,\n",
       "                       min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "                       min_samples_leaf=1, min_samples_split=2,\n",
       "                       min_weight_fraction_leaf=0.0, n_estimators=10,\n",
       "                       n_jobs=None, oob_score=False, random_state=100,\n",
       "                       verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rfc = RandomForestClassifier(n_estimators = 10, random_state = 100)\n",
    "rfc.fit(x_train,y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Confusion Matrix\n",
      "[[54  5]\n",
      " [23  8]]\n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.70      0.92      0.79        59\n",
      "           1       0.62      0.26      0.36        31\n",
      "\n",
      "    accuracy                           0.69        90\n",
      "   macro avg       0.66      0.59      0.58        90\n",
      "weighted avg       0.67      0.69      0.65        90\n",
      "\n"
     ]
    }
   ],
   "source": [
    "prediction = rfc.predict(x_test)\n",
    "print('Confusion Matrix')\n",
    "print(confusion_matrix(y_test,prediction))\n",
    "print('\\n')\n",
    "print(classification_report(y_test,prediction))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Hyperparameters tuning"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Leo\\Anaconda3\\lib\\site-packages\\sklearn\\model_selection\\_split.py:1978: FutureWarning: The default value of cv will change from 3 to 5 in version 0.22. Specify it explicitly to silence this warning.\n",
      "  warnings.warn(CV_WARNING, FutureWarning)\n",
      "C:\\Users\\Leo\\Anaconda3\\lib\\site-packages\\sklearn\\model_selection\\_search.py:813: DeprecationWarning: The default of the `iid` parameter will change from True to False in version 0.22 and will be removed in 0.24. This will change numeric results when test-set sizes are unequal.\n",
      "  DeprecationWarning)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "GridSearchCV(cv='warn', error_score='raise-deprecating',\n",
       "             estimator=RandomForestClassifier(bootstrap=True, class_weight=None,\n",
       "                                              criterion='gini', max_depth=None,\n",
       "                                              max_features='auto',\n",
       "                                              max_leaf_nodes=None,\n",
       "                                              min_impurity_decrease=0.0,\n",
       "                                              min_impurity_split=None,\n",
       "                                              min_samples_leaf=1,\n",
       "                                              min_samples_split=2,\n",
       "                                              min_weight_fraction_leaf=0.0,\n",
       "                                              n_estimators=10, n_jobs=None,\n",
       "                                              oob_score=False, random_state=100,\n",
       "                                              verbose=0, warm_start=False),\n",
       "             iid='warn', n_jobs=None,\n",
       "             param_grid={'bootstrap': [True, False],\n",
       "                         'max_depth': [10, 25, 50, 75, 100, None],\n",
       "                         'max_features': ['auto', 'sqrt'],\n",
       "                         'min_samples_leaf': [1, 2, 4],\n",
       "                         'min_samples_split': [2, 5, 10],\n",
       "                         'n_estimators': [30, 40, 50, 60]},\n",
       "             pre_dispatch='2*n_jobs', refit=True, return_train_score=False,\n",
       "             scoring=None, verbose=0)"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "parameters = {\n",
    "    'bootstrap': [True, False],\n",
    "    'max_depth': [10, 25, 50, 75, 100, None],\n",
    "    'max_features': ['auto', 'sqrt'],\n",
    "    'min_samples_leaf': [1, 2, 4],\n",
    "    'min_samples_split': [2, 5, 10],\n",
    "    'n_estimators': [30, 40, 50, 60]\n",
    "}\n",
    "grid_rfc = GridSearchCV(estimator = rfc, param_grid = parameters)\n",
    "grid_rfc.fit(x_train,y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini',\n",
       "                       max_depth=10, max_features='auto', max_leaf_nodes=None,\n",
       "                       min_impurity_decrease=0.0, min_impurity_split=None,\n",
       "                       min_samples_leaf=4, min_samples_split=10,\n",
       "                       min_weight_fraction_leaf=0.0, n_estimators=60,\n",
       "                       n_jobs=None, oob_score=False, random_state=100,\n",
       "                       verbose=0, warm_start=False)"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "grid_rfc.best_estimator_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Confusion Matrix\n",
      "[[54  5]\n",
      " [19 12]]\n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.74      0.92      0.82        59\n",
      "           1       0.71      0.39      0.50        31\n",
      "\n",
      "    accuracy                           0.73        90\n",
      "   macro avg       0.72      0.65      0.66        90\n",
      "weighted avg       0.73      0.73      0.71        90\n",
      "\n"
     ]
    }
   ],
   "source": [
    "grid_prediction = grid_rfc.predict(x_test)\n",
    "print('Confusion Matrix')\n",
    "print(confusion_matrix(y_test,grid_prediction))\n",
    "print('\\n')\n",
    "print(classification_report(y_test,grid_prediction))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Even though 71% precision is better than a blind guess, it isn't the most accurate.\n",
    "### The results could be much better with more data, as 299 inputs is still a small sample size."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10]),\n",
       " <a list of 11 Text xticklabel objects>)"
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plot_df = pd.DataFrame(data = {'col': x_test.columns, \\\n",
    "                              'importance': grid_rfc.best_estimator_.feature_importances_})\\\n",
    "                                .sort_values('importance',ascending = False)\n",
    "\n",
    "sns.barplot(x = plot_df.col, y = plot_df.importance)\n",
    "plt.xticks(rotation = 90)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### The feature importance shows that the creatinine, ejection fraction and age are the most preditive features, so the research should focus on obtaining those informations"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
