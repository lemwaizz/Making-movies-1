# Making-movies-1

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Importing Relevant Libraries"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "import pandas as pd\n",
    "import sqlite3\n",
    "#importing the relevant data visualization libraries\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "from glob import glob"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Loading Data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['./zippedData\\\\bom.movie_gross.csv.gz',\n",
       " './zippedData\\\\tmdb.movies.csv.gz',\n",
       " './zippedData\\\\tn.movie_budgets.csv.gz']"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "csv_files = glob(\"./zippedData/*.csv.gz\")\n",
    "csv_files"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "bom_df=pd.read_csv('./zippedData\\\\bom.movie_gross.csv.gz')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "budgets_df=pd.read_csv('./zippedData\\\\tn.movie_budgets.csv.gz')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Understanding(budgets)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>$425,000,000</td>\n",
       "      <td>$760,507,625</td>\n",
       "      <td>$2,776,345,279</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>$410,600,000</td>\n",
       "      <td>$241,063,875</td>\n",
       "      <td>$1,045,663,875</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>$350,000,000</td>\n",
       "      <td>$42,762,350</td>\n",
       "      <td>$149,762,350</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>$330,600,000</td>\n",
       "      <td>$459,005,868</td>\n",
       "      <td>$1,403,013,963</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>$317,000,000</td>\n",
       "      <td>$620,181,382</td>\n",
       "      <td>$1,316,721,747</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   id  release_date                                        movie  \\\n",
       "0   1  Dec 18, 2009                                       Avatar   \n",
       "1   2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3   4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4   5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "  production_budget domestic_gross worldwide_gross  \n",
       "0      $425,000,000   $760,507,625  $2,776,345,279  \n",
       "1      $410,600,000   $241,063,875  $1,045,663,875  \n",
       "2      $350,000,000    $42,762,350    $149,762,350  \n",
       "3      $330,600,000   $459,005,868  $1,403,013,963  \n",
       "4      $317,000,000   $620,181,382  $1,316,721,747  "
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>5777</th>\n",
       "      <td>78</td>\n",
       "      <td>Dec 31, 2018</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>$7,000</td>\n",
       "      <td>$0</td>\n",
       "      <td>$0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5778</th>\n",
       "      <td>79</td>\n",
       "      <td>Apr 2, 1999</td>\n",
       "      <td>Following</td>\n",
       "      <td>$6,000</td>\n",
       "      <td>$48,482</td>\n",
       "      <td>$240,495</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5779</th>\n",
       "      <td>80</td>\n",
       "      <td>Jul 13, 2005</td>\n",
       "      <td>Return to the Land of Wonders</td>\n",
       "      <td>$5,000</td>\n",
       "      <td>$1,338</td>\n",
       "      <td>$1,338</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5780</th>\n",
       "      <td>81</td>\n",
       "      <td>Sep 29, 2015</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>$1,400</td>\n",
       "      <td>$0</td>\n",
       "      <td>$0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5781</th>\n",
       "      <td>82</td>\n",
       "      <td>Aug 5, 2005</td>\n",
       "      <td>My Date With Drew</td>\n",
       "      <td>$1,100</td>\n",
       "      <td>$181,041</td>\n",
       "      <td>$181,041</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  release_date                          movie production_budget  \\\n",
       "5777  78  Dec 31, 2018                         Red 11            $7,000   \n",
       "5778  79   Apr 2, 1999                      Following            $6,000   \n",
       "5779  80  Jul 13, 2005  Return to the Land of Wonders            $5,000   \n",
       "5780  81  Sep 29, 2015           A Plague So Pleasant            $1,400   \n",
       "5781  82   Aug 5, 2005              My Date With Drew            $1,100   \n",
       "\n",
       "     domestic_gross worldwide_gross  \n",
       "5777             $0              $0  \n",
       "5778        $48,482        $240,495  \n",
       "5779         $1,338          $1,338  \n",
       "5780             $0              $0  \n",
       "5781       $181,041        $181,041  "
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 5782 entries, 0 to 5781\n",
      "Data columns (total 6 columns):\n",
      " #   Column             Non-Null Count  Dtype \n",
      "---  ------             --------------  ----- \n",
      " 0   id                 5782 non-null   int64 \n",
      " 1   release_date       5782 non-null   object\n",
      " 2   movie              5782 non-null   object\n",
      " 3   production_budget  5782 non-null   object\n",
      " 4   domestic_gross     5782 non-null   object\n",
      " 5   worldwide_gross    5782 non-null   object\n",
      "dtypes: int64(1), object(5)\n",
      "memory usage: 271.2+ KB\n"
     ]
    }
   ],
   "source": [
    "budgets_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
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
       "      <th>id</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>5782.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>50.372363</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>28.821076</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>25.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>50.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>75.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>100.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                id\n",
       "count  5782.000000\n",
       "mean     50.372363\n",
       "std      28.821076\n",
       "min       1.000000\n",
       "25%      25.000000\n",
       "50%      50.000000\n",
       "75%      75.000000\n",
       "max     100.000000"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There are no null values."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Cleaning(budgets)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "False"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#checking for duplicates\n",
    "budgets_df.duplicated().any()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'$410,600,000'"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df['production_budget'][1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5777</th>\n",
       "      <td>78</td>\n",
       "      <td>Dec 31, 2018</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>7000.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5778</th>\n",
       "      <td>79</td>\n",
       "      <td>Apr 2, 1999</td>\n",
       "      <td>Following</td>\n",
       "      <td>6000.0</td>\n",
       "      <td>48482.0</td>\n",
       "      <td>2.404950e+05</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5779</th>\n",
       "      <td>80</td>\n",
       "      <td>Jul 13, 2005</td>\n",
       "      <td>Return to the Land of Wonders</td>\n",
       "      <td>5000.0</td>\n",
       "      <td>1338.0</td>\n",
       "      <td>1.338000e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5780</th>\n",
       "      <td>81</td>\n",
       "      <td>Sep 29, 2015</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>1400.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5781</th>\n",
       "      <td>82</td>\n",
       "      <td>Aug 5, 2005</td>\n",
       "      <td>My Date With Drew</td>\n",
       "      <td>1100.0</td>\n",
       "      <td>181041.0</td>\n",
       "      <td>1.810410e+05</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5782 rows × 6 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  release_date                                        movie  \\\n",
       "0      1  Dec 18, 2009                                       Avatar   \n",
       "1      2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2      3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3      4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4      5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "...   ..           ...                                          ...   \n",
       "5777  78  Dec 31, 2018                                       Red 11   \n",
       "5778  79   Apr 2, 1999                                    Following   \n",
       "5779  80  Jul 13, 2005                Return to the Land of Wonders   \n",
       "5780  81  Sep 29, 2015                         A Plague So Pleasant   \n",
       "5781  82   Aug 5, 2005                            My Date With Drew   \n",
       "\n",
       "      production_budget  domestic_gross  worldwide_gross  \n",
       "0           425000000.0     760507625.0     2.776345e+09  \n",
       "1           410600000.0     241063875.0     1.045664e+09  \n",
       "2           350000000.0      42762350.0     1.497624e+08  \n",
       "3           330600000.0     459005868.0     1.403014e+09  \n",
       "4           317000000.0     620181382.0     1.316722e+09  \n",
       "...                 ...             ...              ...  \n",
       "5777             7000.0             0.0     0.000000e+00  \n",
       "5778             6000.0         48482.0     2.404950e+05  \n",
       "5779             5000.0          1338.0     1.338000e+03  \n",
       "5780             1400.0             0.0     0.000000e+00  \n",
       "5781             1100.0        181041.0     1.810410e+05  \n",
       "\n",
       "[5782 rows x 6 columns]"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#converting to a numeric data type\n",
    "def numclean(df,col):\n",
    "    df[col]=df[col].str.replace(\"$\",\"\").str.replace(\",\",\"\").astype(float)\n",
    "    return df\n",
    "numclean(budgets_df,'production_budget')\n",
    "numclean(budgets_df,'domestic_gross')\n",
    "numclean(budgets_df,'worldwide_gross')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   id  release_date                                        movie  \\\n",
       "0   1  Dec 18, 2009                                       Avatar   \n",
       "1   2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3   4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4   5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "   production_budget  domestic_gross  worldwide_gross  \n",
       "0        425000000.0     760507625.0     2.776345e+09  \n",
       "1        410600000.0     241063875.0     1.045664e+09  \n",
       "2        350000000.0      42762350.0     1.497624e+08  \n",
       "3        330600000.0     459005868.0     1.403014e+09  \n",
       "4        317000000.0     620181382.0     1.316722e+09  "
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>5777</th>\n",
       "      <td>78</td>\n",
       "      <td>Dec 31, 2018</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>7000.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5778</th>\n",
       "      <td>79</td>\n",
       "      <td>Apr 2, 1999</td>\n",
       "      <td>Following</td>\n",
       "      <td>6000.0</td>\n",
       "      <td>48482.0</td>\n",
       "      <td>240495.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5779</th>\n",
       "      <td>80</td>\n",
       "      <td>Jul 13, 2005</td>\n",
       "      <td>Return to the Land of Wonders</td>\n",
       "      <td>5000.0</td>\n",
       "      <td>1338.0</td>\n",
       "      <td>1338.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5780</th>\n",
       "      <td>81</td>\n",
       "      <td>Sep 29, 2015</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>1400.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5781</th>\n",
       "      <td>82</td>\n",
       "      <td>Aug 5, 2005</td>\n",
       "      <td>My Date With Drew</td>\n",
       "      <td>1100.0</td>\n",
       "      <td>181041.0</td>\n",
       "      <td>181041.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  release_date                          movie  production_budget  \\\n",
       "5777  78  Dec 31, 2018                         Red 11             7000.0   \n",
       "5778  79   Apr 2, 1999                      Following             6000.0   \n",
       "5779  80  Jul 13, 2005  Return to the Land of Wonders             5000.0   \n",
       "5780  81  Sep 29, 2015           A Plague So Pleasant             1400.0   \n",
       "5781  82   Aug 5, 2005              My Date With Drew             1100.0   \n",
       "\n",
       "      domestic_gross  worldwide_gross  \n",
       "5777             0.0              0.0  \n",
       "5778         48482.0         240495.0  \n",
       "5779          1338.0           1338.0  \n",
       "5780             0.0              0.0  \n",
       "5781        181041.0         181041.0  "
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
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
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   release_date                                        movie  \\\n",
       "0  Dec 18, 2009                                       Avatar   \n",
       "1  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   Jun 7, 2019                                 Dark Phoenix   \n",
       "3   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "   production_budget  domestic_gross  worldwide_gross  \n",
       "0        425000000.0     760507625.0     2.776345e+09  \n",
       "1        410600000.0     241063875.0     1.045664e+09  \n",
       "2        350000000.0      42762350.0     1.497624e+08  \n",
       "3        330600000.0     459005868.0     1.403014e+09  \n",
       "4        317000000.0     620181382.0     1.316722e+09  "
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_cleaned=budgets_df.drop('id',axis=1)\n",
    "budgets_cleaned.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
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
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2009-12-18</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2011-05-20</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2019-06-07</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2015-05-01</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2017-12-15</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  release_date                                        movie  \\\n",
       "0   2009-12-18                                       Avatar   \n",
       "1   2011-05-20  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   2019-06-07                                 Dark Phoenix   \n",
       "3   2015-05-01                      Avengers: Age of Ultron   \n",
       "4   2017-12-15            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "   production_budget  domestic_gross  worldwide_gross  \n",
       "0        425000000.0     760507625.0     2.776345e+09  \n",
       "1        410600000.0     241063875.0     1.045664e+09  \n",
       "2        350000000.0      42762350.0     1.497624e+08  \n",
       "3        330600000.0     459005868.0     1.403014e+09  \n",
       "4        317000000.0     620181382.0     1.316722e+09  "
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#convert release date to date_time format\n",
    "budgets_cleaned['release_date'] = pd.to_datetime(budgets_cleaned['release_date'])\n",
    "budgets_cleaned.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Understanding(Box office)"
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
       "      <th>title</th>\n",
       "      <th>studio</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Toy Story 3</td>\n",
       "      <td>BV</td>\n",
       "      <td>415000000.0</td>\n",
       "      <td>652000000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Alice in Wonderland (2010)</td>\n",
       "      <td>BV</td>\n",
       "      <td>334200000.0</td>\n",
       "      <td>691300000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Harry Potter and the Deathly Hallows Part 1</td>\n",
       "      <td>WB</td>\n",
       "      <td>296000000.0</td>\n",
       "      <td>664300000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Inception</td>\n",
       "      <td>WB</td>\n",
       "      <td>292600000.0</td>\n",
       "      <td>535700000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Shrek Forever After</td>\n",
       "      <td>P/DW</td>\n",
       "      <td>238700000.0</td>\n",
       "      <td>513900000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                         title studio  domestic_gross  \\\n",
       "0                                  Toy Story 3     BV     415000000.0   \n",
       "1                   Alice in Wonderland (2010)     BV     334200000.0   \n",
       "2  Harry Potter and the Deathly Hallows Part 1     WB     296000000.0   \n",
       "3                                    Inception     WB     292600000.0   \n",
       "4                          Shrek Forever After   P/DW     238700000.0   \n",
       "\n",
       "  foreign_gross  year  \n",
       "0     652000000  2010  \n",
       "1     691300000  2010  \n",
       "2     664300000  2010  \n",
       "3     535700000  2010  \n",
       "4     513900000  2010  "
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
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
       "      <th>title</th>\n",
       "      <th>studio</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>3382</th>\n",
       "      <td>The Quake</td>\n",
       "      <td>Magn.</td>\n",
       "      <td>6200.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3383</th>\n",
       "      <td>Edward II (2018 re-release)</td>\n",
       "      <td>FM</td>\n",
       "      <td>4800.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3384</th>\n",
       "      <td>El Pacto</td>\n",
       "      <td>Sony</td>\n",
       "      <td>2500.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3385</th>\n",
       "      <td>The Swan</td>\n",
       "      <td>Synergetic</td>\n",
       "      <td>2400.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3386</th>\n",
       "      <td>An Actor Prepares</td>\n",
       "      <td>Grav.</td>\n",
       "      <td>1700.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                            title      studio  domestic_gross foreign_gross  \\\n",
       "3382                    The Quake       Magn.          6200.0           NaN   \n",
       "3383  Edward II (2018 re-release)          FM          4800.0           NaN   \n",
       "3384                     El Pacto        Sony          2500.0           NaN   \n",
       "3385                     The Swan  Synergetic          2400.0           NaN   \n",
       "3386            An Actor Prepares       Grav.          1700.0           NaN   \n",
       "\n",
       "      year  \n",
       "3382  2018  \n",
       "3383  2018  \n",
       "3384  2018  \n",
       "3385  2018  \n",
       "3386  2018  "
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(3387, 5)"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>domestic_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>3.359000e+03</td>\n",
       "      <td>3387.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2.874585e+07</td>\n",
       "      <td>2013.958075</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>6.698250e+07</td>\n",
       "      <td>2.478141</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000e+02</td>\n",
       "      <td>2010.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1.200000e+05</td>\n",
       "      <td>2012.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1.400000e+06</td>\n",
       "      <td>2014.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.790000e+07</td>\n",
       "      <td>2016.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>9.367000e+08</td>\n",
       "      <td>2018.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       domestic_gross         year\n",
       "count    3.359000e+03  3387.000000\n",
       "mean     2.874585e+07  2013.958075\n",
       "std      6.698250e+07     2.478141\n",
       "min      1.000000e+02  2010.000000\n",
       "25%      1.200000e+05  2012.000000\n",
       "50%      1.400000e+06  2014.000000\n",
       "75%      2.790000e+07  2016.000000\n",
       "max      9.367000e+08  2018.000000"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 3387 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   title           3387 non-null   object \n",
      " 1   studio          3382 non-null   object \n",
      " 2   domestic_gross  3359 non-null   float64\n",
      " 3   foreign_gross   2037 non-null   object \n",
      " 4   year            3387 non-null   int64  \n",
      "dtypes: float64(1), int64(1), object(3)\n",
      "memory usage: 132.4+ KB\n"
     ]
    }
   ],
   "source": [
    "bom_df.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There are null values in the following columns:\n",
    "studio  \n",
    "domestic_gross\n",
    "foreign_gross"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Cleaning(Box Office)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "title                0\n",
       "studio               5\n",
       "domestic_gross      28\n",
       "foreign_gross     1350\n",
       "year                 0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# number of rows with null values\n",
    "bom_df.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
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
       "      <th>title</th>\n",
       "      <th>studio</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>571</th>\n",
       "      <td>Poetry</td>\n",
       "      <td>Kino</td>\n",
       "      <td>356000.0</td>\n",
       "      <td>1900000</td>\n",
       "      <td>2011</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3343</th>\n",
       "      <td>The Third Murder</td>\n",
       "      <td>FM</td>\n",
       "      <td>89300.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1850</th>\n",
       "      <td>Camp X-Ray</td>\n",
       "      <td>IFC</td>\n",
       "      <td>13300.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2014</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3257</th>\n",
       "      <td>Don't Worry He Won't Get Far on Foot</td>\n",
       "      <td>Amazon</td>\n",
       "      <td>1400000.0</td>\n",
       "      <td>2500000</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1512</th>\n",
       "      <td>Non-Stop</td>\n",
       "      <td>Uni.</td>\n",
       "      <td>92200000.0</td>\n",
       "      <td>130600000</td>\n",
       "      <td>2014</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                     title  studio  domestic_gross  \\\n",
       "571                                 Poetry    Kino        356000.0   \n",
       "3343                      The Third Murder      FM         89300.0   \n",
       "1850                            Camp X-Ray     IFC         13300.0   \n",
       "3257  Don't Worry He Won't Get Far on Foot  Amazon       1400000.0   \n",
       "1512                              Non-Stop    Uni.      92200000.0   \n",
       "\n",
       "     foreign_gross  year  \n",
       "571        1900000  2011  \n",
       "3343           NaN  2018  \n",
       "1850           NaN  2014  \n",
       "3257       2500000  2018  \n",
       "1512     130600000  2014  "
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# sample rows where foreign_gross has no missing values\n",
    "bom_df[bom_df[\"studio\"].notna()].sample(5, random_state = 1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
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
       "      <th>title</th>\n",
       "      <th>studio</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>210</th>\n",
       "      <td>Outside the Law (Hors-la-loi)</td>\n",
       "      <td>NaN</td>\n",
       "      <td>96900.0</td>\n",
       "      <td>3300000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>555</th>\n",
       "      <td>Fireflies in the Garden</td>\n",
       "      <td>NaN</td>\n",
       "      <td>70600.0</td>\n",
       "      <td>3300000</td>\n",
       "      <td>2011</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>933</th>\n",
       "      <td>Keith Lemon: The Film</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>4000000</td>\n",
       "      <td>2012</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1862</th>\n",
       "      <td>Plot for Peace</td>\n",
       "      <td>NaN</td>\n",
       "      <td>7100.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2014</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2825</th>\n",
       "      <td>Secret Superstar</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>122000000</td>\n",
       "      <td>2017</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                              title studio  domestic_gross foreign_gross  year\n",
       "210   Outside the Law (Hors-la-loi)    NaN         96900.0       3300000  2010\n",
       "555         Fireflies in the Garden    NaN         70600.0       3300000  2011\n",
       "933           Keith Lemon: The Film    NaN             NaN       4000000  2012\n",
       "1862                 Plot for Peace    NaN          7100.0           NaN  2014\n",
       "2825               Secret Superstar    NaN             NaN     122000000  2017"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# sample rows where foreign_gross has missing values\n",
    "bom_df[bom_df[\"studio\"].isna()]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [],
   "source": [
    "bom_df.dropna(subset = [\"studio\"], inplace = True)"
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
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 3382 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   title           3382 non-null   object \n",
      " 1   studio          3382 non-null   object \n",
      " 2   domestic_gross  3356 non-null   float64\n",
      " 3   foreign_gross   2033 non-null   object \n",
      " 4   year            3382 non-null   int64  \n",
      "dtypes: float64(1), int64(1), object(3)\n",
      "memory usage: 158.5+ KB\n"
     ]
    }
   ],
   "source": [
    "bom_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.768775872264932"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# percentage of missing values in domestic_gross\n",
    "bom_df[\"domestic_gross\"].isnull().sum()/len(bom_df)*100"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Since the percentage is quite small, we can drop the rows."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 3356 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   title           3356 non-null   object \n",
      " 1   studio          3356 non-null   object \n",
      " 2   domestic_gross  3356 non-null   float64\n",
      " 3   foreign_gross   2007 non-null   object \n",
      " 4   year            3356 non-null   int64  \n",
      "dtypes: float64(1), int64(1), object(3)\n",
      "memory usage: 157.3+ KB\n"
     ]
    }
   ],
   "source": [
    "bom_df.dropna(subset = [\"domestic_gross\"], inplace = True)\n",
    "bom_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "40.19666269368295"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# percentage of missing values in foreign gross\n",
    "bom_df[\"foreign_gross\"].isnull().sum()/len(bom_df)*100"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Not droppable as it is too large. We shall replace the values with either the mean or median depending on our investigation."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    652000000\n",
       "1    691300000\n",
       "2    664300000\n",
       "3    535700000\n",
       "4    513900000\n",
       "Name: foreign_gross, dtype: object"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# preview of foreign gross column\n",
    "bom_df[\"foreign_gross\"].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 3356 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   title           3356 non-null   object \n",
      " 1   studio          3356 non-null   object \n",
      " 2   domestic_gross  3356 non-null   float64\n",
      " 3   foreign_gross   2007 non-null   float64\n",
      " 4   year            3356 non-null   int64  \n",
      "dtypes: float64(2), int64(1), object(2)\n",
      "memory usage: 157.3+ KB\n"
     ]
    }
   ],
   "source": [
    "#converting to numerical values\n",
    "bom_df[\"foreign_gross\"] = [float(str(i).replace(\",\", \"\")) for i in bom_df[\"foreign_gross\"]]\n",
    "bom_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "75790384.84130543"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df[\"foreign_gross\"].mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "19400000.0"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df[\"foreign_gross\"].median()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "75790384.84130543"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#replacing with mean as replacing with the median affects mean\n",
    "bom_df[\"foreign_gross\"].fillna(bom_df[\"foreign_gross\"].mean(), inplace=True)\n",
    "bom_df[\"foreign_gross\"].mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 3356 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   title           3356 non-null   object \n",
      " 1   studio          3356 non-null   object \n",
      " 2   domestic_gross  3356 non-null   float64\n",
      " 3   foreign_gross   3356 non-null   float64\n",
      " 4   year            3356 non-null   int64  \n",
      "dtypes: float64(2), int64(1), object(2)\n",
      "memory usage: 157.3+ KB\n"
     ]
    }
   ],
   "source": [
    "bom_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "False"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.duplicated().any()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
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
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>3.356000e+03</td>\n",
       "      <td>3.356000e+03</td>\n",
       "      <td>3356.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2.877149e+07</td>\n",
       "      <td>7.579038e+07</td>\n",
       "      <td>2013.970203</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>6.700694e+07</td>\n",
       "      <td>1.068472e+08</td>\n",
       "      <td>2.479064</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000e+02</td>\n",
       "      <td>6.000000e+02</td>\n",
       "      <td>2010.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1.200000e+05</td>\n",
       "      <td>1.220000e+07</td>\n",
       "      <td>2012.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1.400000e+06</td>\n",
       "      <td>7.579038e+07</td>\n",
       "      <td>2014.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.795000e+07</td>\n",
       "      <td>7.579038e+07</td>\n",
       "      <td>2016.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>9.367000e+08</td>\n",
       "      <td>9.605000e+08</td>\n",
       "      <td>2018.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       domestic_gross  foreign_gross         year\n",
       "count    3.356000e+03   3.356000e+03  3356.000000\n",
       "mean     2.877149e+07   7.579038e+07  2013.970203\n",
       "std      6.700694e+07   1.068472e+08     2.479064\n",
       "min      1.000000e+02   6.000000e+02  2010.000000\n",
       "25%      1.200000e+05   1.220000e+07  2012.000000\n",
       "50%      1.400000e+06   7.579038e+07  2014.000000\n",
       "75%      2.795000e+07   7.579038e+07  2016.000000\n",
       "max      9.367000e+08   9.605000e+08  2018.000000"
      ]
     },
     "execution_count": 36,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bom_df.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Understanding(imdb)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "metadata": {},
   "outputs": [],
   "source": [
    "conn= sqlite3.connect(\"./zippedData/im.db_1/im.db\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {},
   "outputs": [],
   "source": [
    "cur=conn.cursor()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[('movie_basics',),\n",
       " ('directors',),\n",
       " ('known_for',),\n",
       " ('movie_akas',),\n",
       " ('movie_ratings',),\n",
       " ('persons',),\n",
       " ('principals',),\n",
       " ('writers',)]"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "cur.execute(\"\"\"SELECT name FROM sqlite_master WHERE type = 'table';\"\"\")\n",
    "table_names = cur.fetchall()\n",
    "table_names"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "metadata": {},
   "outputs": [],
   "source": [
    "moviebasics_df=pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_basics;\n",
    "\"\"\", conn)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {},
   "outputs": [],
   "source": [
    "movieratings_df=pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_ratings;\n",
    "\"\"\", conn)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Cleaning(movie_basics)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
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
       "      <th>movie_id</th>\n",
       "      <th>primary_title</th>\n",
       "      <th>original_title</th>\n",
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>tt0063540</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>2013</td>\n",
       "      <td>175.0</td>\n",
       "      <td>Action,Crime,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>tt0066787</td>\n",
       "      <td>One Day Before the Rainy Season</td>\n",
       "      <td>Ashad Ka Ek Din</td>\n",
       "      <td>2019</td>\n",
       "      <td>114.0</td>\n",
       "      <td>Biography,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>tt0069049</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>2018</td>\n",
       "      <td>122.0</td>\n",
       "      <td>Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>tt0069204</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>2018</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Comedy,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>tt0100275</td>\n",
       "      <td>The Wandering Soap Opera</td>\n",
       "      <td>La Telenovela Errante</td>\n",
       "      <td>2017</td>\n",
       "      <td>80.0</td>\n",
       "      <td>Comedy,Drama,Fantasy</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    movie_id                    primary_title              original_title  \\\n",
       "0  tt0063540                        Sunghursh                   Sunghursh   \n",
       "1  tt0066787  One Day Before the Rainy Season             Ashad Ka Ek Din   \n",
       "2  tt0069049       The Other Side of the Wind  The Other Side of the Wind   \n",
       "3  tt0069204                  Sabse Bada Sukh             Sabse Bada Sukh   \n",
       "4  tt0100275         The Wandering Soap Opera       La Telenovela Errante   \n",
       "\n",
       "   start_year  runtime_minutes                genres  \n",
       "0        2013            175.0    Action,Crime,Drama  \n",
       "1        2019            114.0       Biography,Drama  \n",
       "2        2018            122.0                 Drama  \n",
       "3        2018              NaN          Comedy,Drama  \n",
       "4        2017             80.0  Comedy,Drama,Fantasy  "
      ]
     },
     "execution_count": 42,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_basics;\n",
    "\"\"\", conn).head().head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>movie_id</th>\n",
       "      <th>primary_title</th>\n",
       "      <th>original_title</th>\n",
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>tt0063540</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>2013</td>\n",
       "      <td>175.0</td>\n",
       "      <td>Action,Crime,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>tt0066787</td>\n",
       "      <td>One Day Before the Rainy Season</td>\n",
       "      <td>Ashad Ka Ek Din</td>\n",
       "      <td>2019</td>\n",
       "      <td>114.0</td>\n",
       "      <td>Biography,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>tt0069049</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>2018</td>\n",
       "      <td>122.0</td>\n",
       "      <td>Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>tt0069204</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>2018</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Comedy,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>tt0100275</td>\n",
       "      <td>The Wandering Soap Opera</td>\n",
       "      <td>La Telenovela Errante</td>\n",
       "      <td>2017</td>\n",
       "      <td>80.0</td>\n",
       "      <td>Comedy,Drama,Fantasy</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    movie_id                    primary_title              original_title  \\\n",
       "0  tt0063540                        Sunghursh                   Sunghursh   \n",
       "1  tt0066787  One Day Before the Rainy Season             Ashad Ka Ek Din   \n",
       "2  tt0069049       The Other Side of the Wind  The Other Side of the Wind   \n",
       "3  tt0069204                  Sabse Bada Sukh             Sabse Bada Sukh   \n",
       "4  tt0100275         The Wandering Soap Opera       La Telenovela Errante   \n",
       "\n",
       "   start_year  runtime_minutes                genres  \n",
       "0        2013            175.0    Action,Crime,Drama  \n",
       "1        2019            114.0       Biography,Drama  \n",
       "2        2018            122.0                 Drama  \n",
       "3        2018              NaN          Comedy,Drama  \n",
       "4        2017             80.0  Comedy,Drama,Fantasy  "
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_basics;\n",
    "\"\"\", conn).head().tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 146144 entries, 0 to 146143\n",
      "Data columns (total 6 columns):\n",
      " #   Column           Non-Null Count   Dtype  \n",
      "---  ------           --------------   -----  \n",
      " 0   movie_id         146144 non-null  object \n",
      " 1   primary_title    146144 non-null  object \n",
      " 2   original_title   146123 non-null  object \n",
      " 3   start_year       146144 non-null  int64  \n",
      " 4   runtime_minutes  114405 non-null  float64\n",
      " 5   genres           140736 non-null  object \n",
      "dtypes: float64(1), int64(1), object(4)\n",
      "memory usage: 6.7+ MB\n"
     ]
    }
   ],
   "source": [
    "pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_basics;\n",
    "\"\"\", conn).info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Discrepancies in entries indicate existence of null values."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
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
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>146144.000000</td>\n",
       "      <td>114405.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2014.621798</td>\n",
       "      <td>86.187247</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>2.733583</td>\n",
       "      <td>166.360590</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>2010.000000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>2012.000000</td>\n",
       "      <td>70.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2015.000000</td>\n",
       "      <td>87.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2017.000000</td>\n",
       "      <td>99.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2115.000000</td>\n",
       "      <td>51420.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          start_year  runtime_minutes\n",
       "count  146144.000000    114405.000000\n",
       "mean     2014.621798        86.187247\n",
       "std         2.733583       166.360590\n",
       "min      2010.000000         1.000000\n",
       "25%      2012.000000        70.000000\n",
       "50%      2015.000000        87.000000\n",
       "75%      2017.000000        99.000000\n",
       "max      2115.000000     51420.000000"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.read_sql(\"\"\"\n",
    "SELECT * FROM movie_basics;\n",
    "\"\"\", conn).describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "movie_id               0\n",
       "primary_title          0\n",
       "original_title        21\n",
       "start_year             0\n",
       "runtime_minutes    31739\n",
       "genres              5408\n",
       "dtype: int64"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df.isna().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.014369389095686446"
      ]
     },
     "execution_count": 47,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "((moviebasics_df[\"original_title\"].isna().sum()/len(moviebasics_df)) * 100)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {},
   "outputs": [],
   "source": [
    "#Drop as percentage is insignificant\n",
    "moviebasics_df.dropna(subset = [\"original_title\"], inplace = True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 146123 entries, 0 to 146143\n",
      "Data columns (total 6 columns):\n",
      " #   Column           Non-Null Count   Dtype  \n",
      "---  ------           --------------   -----  \n",
      " 0   movie_id         146123 non-null  object \n",
      " 1   primary_title    146123 non-null  object \n",
      " 2   original_title   146123 non-null  object \n",
      " 3   start_year       146123 non-null  int64  \n",
      " 4   runtime_minutes  114401 non-null  float64\n",
      " 5   genres           140734 non-null  object \n",
      "dtypes: float64(1), int64(1), object(4)\n",
      "memory usage: 7.8+ MB\n"
     ]
    }
   ],
   "source": [
    "moviebasics_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "21.709108080179025"
      ]
     },
     "execution_count": 50,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "((moviebasics_df[\"runtime_minutes\"].isna().sum()/len(moviebasics_df)) * 100)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "replacing with either mean or median as it is a substantial percentage\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "86.18612599540214"
      ]
     },
     "execution_count": 51,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df[\"runtime_minutes\"].mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "87.0"
      ]
     },
     "execution_count": 52,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df[\"runtime_minutes\"].median()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "metadata": {},
   "outputs": [],
   "source": [
    "moviebasics_df[\"runtime_minutes\"].fillna(moviebasics_df[\"runtime_minutes\"].mean(),inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "86.18612599540215"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#investigating effect on mean\n",
    "moviebasics_df[\"runtime_minutes\"].mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 146123 entries, 0 to 146143\n",
      "Data columns (total 6 columns):\n",
      " #   Column           Non-Null Count   Dtype  \n",
      "---  ------           --------------   -----  \n",
      " 0   movie_id         146123 non-null  object \n",
      " 1   primary_title    146123 non-null  object \n",
      " 2   original_title   146123 non-null  object \n",
      " 3   start_year       146123 non-null  int64  \n",
      " 4   runtime_minutes  146123 non-null  float64\n",
      " 5   genres           140734 non-null  object \n",
      "dtypes: float64(1), int64(1), object(4)\n",
      "memory usage: 7.8+ MB\n"
     ]
    }
   ],
   "source": [
    "moviebasics_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "3.6879888860754293"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "((moviebasics_df[\"genres\"].isna().sum()/len(moviebasics_df)) * 100)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 140734 entries, 0 to 146143\n",
      "Data columns (total 6 columns):\n",
      " #   Column           Non-Null Count   Dtype  \n",
      "---  ------           --------------   -----  \n",
      " 0   movie_id         140734 non-null  object \n",
      " 1   primary_title    140734 non-null  object \n",
      " 2   original_title   140734 non-null  object \n",
      " 3   start_year       140734 non-null  int64  \n",
      " 4   runtime_minutes  140734 non-null  float64\n",
      " 5   genres           140734 non-null  object \n",
      "dtypes: float64(1), int64(1), object(4)\n",
      "memory usage: 7.5+ MB\n"
     ]
    }
   ],
   "source": [
    "#Dropping as value is insignificant\n",
    "moviebasics_df.dropna(subset = [\"genres\"], inplace = True)\n",
    "moviebasics_df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "movie_id           0\n",
       "primary_title      0\n",
       "original_title     0\n",
       "start_year         0\n",
       "runtime_minutes    0\n",
       "genres             0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 58,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df.isna().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "False"
      ]
     },
     "execution_count": 59,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df.duplicated().any()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Cleaning(movie_ratings)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
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
       "      <th>movie_id</th>\n",
       "      <th>averagerating</th>\n",
       "      <th>numvotes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>tt10356526</td>\n",
       "      <td>8.3</td>\n",
       "      <td>31</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>tt10384606</td>\n",
       "      <td>8.9</td>\n",
       "      <td>559</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>tt1042974</td>\n",
       "      <td>6.4</td>\n",
       "      <td>20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>tt1043726</td>\n",
       "      <td>4.2</td>\n",
       "      <td>50352</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>tt1060240</td>\n",
       "      <td>6.5</td>\n",
       "      <td>21</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     movie_id  averagerating  numvotes\n",
       "0  tt10356526            8.3        31\n",
       "1  tt10384606            8.9       559\n",
       "2   tt1042974            6.4        20\n",
       "3   tt1043726            4.2     50352\n",
       "4   tt1060240            6.5        21"
      ]
     },
     "execution_count": 60,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movieratings_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
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
       "      <th>movie_id</th>\n",
       "      <th>averagerating</th>\n",
       "      <th>numvotes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>73851</th>\n",
       "      <td>tt9805820</td>\n",
       "      <td>8.1</td>\n",
       "      <td>25</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>73852</th>\n",
       "      <td>tt9844256</td>\n",
       "      <td>7.5</td>\n",
       "      <td>24</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>73853</th>\n",
       "      <td>tt9851050</td>\n",
       "      <td>4.7</td>\n",
       "      <td>14</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>73854</th>\n",
       "      <td>tt9886934</td>\n",
       "      <td>7.0</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>73855</th>\n",
       "      <td>tt9894098</td>\n",
       "      <td>6.3</td>\n",
       "      <td>128</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        movie_id  averagerating  numvotes\n",
       "73851  tt9805820            8.1        25\n",
       "73852  tt9844256            7.5        24\n",
       "73853  tt9851050            4.7        14\n",
       "73854  tt9886934            7.0         5\n",
       "73855  tt9894098            6.3       128"
      ]
     },
     "execution_count": 61,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movieratings_df.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(73856, 3)"
      ]
     },
     "execution_count": 62,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movieratings_df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
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
       "      <th>averagerating</th>\n",
       "      <th>numvotes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>73856.000000</td>\n",
       "      <td>7.385600e+04</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>6.332729</td>\n",
       "      <td>3.523662e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>1.474978</td>\n",
       "      <td>3.029402e+04</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>5.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>5.500000</td>\n",
       "      <td>1.400000e+01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>6.500000</td>\n",
       "      <td>4.900000e+01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>7.400000</td>\n",
       "      <td>2.820000e+02</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>10.000000</td>\n",
       "      <td>1.841066e+06</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       averagerating      numvotes\n",
       "count   73856.000000  7.385600e+04\n",
       "mean        6.332729  3.523662e+03\n",
       "std         1.474978  3.029402e+04\n",
       "min         1.000000  5.000000e+00\n",
       "25%         5.500000  1.400000e+01\n",
       "50%         6.500000  4.900000e+01\n",
       "75%         7.400000  2.820000e+02\n",
       "max        10.000000  1.841066e+06"
      ]
     },
     "execution_count": 63,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movieratings_df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 73856 entries, 0 to 73855\n",
      "Data columns (total 3 columns):\n",
      " #   Column         Non-Null Count  Dtype  \n",
      "---  ------         --------------  -----  \n",
      " 0   movie_id       73856 non-null  object \n",
      " 1   averagerating  73856 non-null  float64\n",
      " 2   numvotes       73856 non-null  int64  \n",
      "dtypes: float64(1), int64(1), object(1)\n",
      "memory usage: 1.7+ MB\n"
     ]
    }
   ],
   "source": [
    "movieratings_df.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There are no null values."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "False"
      ]
     },
     "execution_count": 65,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movieratings_df.duplicated().any()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #DATA ANALYSIS"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Budgets"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   id  release_date                                        movie  \\\n",
       "0   1  Dec 18, 2009                                       Avatar   \n",
       "1   2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3   4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4   5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "   production_budget  domestic_gross  worldwide_gross  \n",
       "0        425000000.0     760507625.0     2.776345e+09  \n",
       "1        410600000.0     241063875.0     1.045664e+09  \n",
       "2        350000000.0      42762350.0     1.497624e+08  \n",
       "3        330600000.0     459005868.0     1.403014e+09  \n",
       "4        317000000.0     620181382.0     1.316722e+09  "
      ]
     },
     "execution_count": 66,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 67,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    5.782000e+03\n",
       "mean     3.158776e+07\n",
       "std      4.181208e+07\n",
       "min      1.100000e+03\n",
       "25%      5.000000e+06\n",
       "50%      1.700000e+07\n",
       "75%      4.000000e+07\n",
       "max      4.250000e+08\n",
       "Name: production_budget, dtype: float64"
      ]
     },
     "execution_count": 67,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Plot release day for all movies\n",
    "budgets_df['production_budget'].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
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
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5777</th>\n",
       "      <td>Red 11</td>\n",
       "      <td>7000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5778</th>\n",
       "      <td>Following</td>\n",
       "      <td>6000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5779</th>\n",
       "      <td>Return to the Land of Wonders</td>\n",
       "      <td>5000.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5780</th>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>1400.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5781</th>\n",
       "      <td>My Date With Drew</td>\n",
       "      <td>1100.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5782 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                            movie  production_budget\n",
       "0                                          Avatar        425000000.0\n",
       "1     Pirates of the Caribbean: On Stranger Tides        410600000.0\n",
       "2                                    Dark Phoenix        350000000.0\n",
       "3                         Avengers: Age of Ultron        330600000.0\n",
       "4               Star Wars Ep. VIII: The Last Jedi        317000000.0\n",
       "...                                           ...                ...\n",
       "5777                                       Red 11             7000.0\n",
       "5778                                    Following             6000.0\n",
       "5779                Return to the Land of Wonders             5000.0\n",
       "5780                         A Plague So Pleasant             1400.0\n",
       "5781                            My Date With Drew             1100.0\n",
       "\n",
       "[5782 rows x 2 columns]"
      ]
     },
     "execution_count": 68,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df[['movie', 'production_budget']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 69,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count         5782.000000\n",
       "mean      31587757.096506\n",
       "std       41812076.826943\n",
       "min           1100.000000\n",
       "25%        5000000.000000\n",
       "50%       17000000.000000\n",
       "75%       40000000.000000\n",
       "max      425000000.000000\n",
       "Name: production_budget, dtype: object"
      ]
     },
     "execution_count": 69,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df['production_budget'].describe().apply(lambda x: format(x, 'f'))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "metadata": {},
   "outputs": [],
   "source": [
    "bins = [0, 7000000, 20000000, 50000000, np.inf]\n",
    "names = ['<7m', '7-20m', '20-50m', '>50m']\n",
    "budgets_df['budget_range'] = pd.cut(budgets_df['production_budget'], bins, labels=names)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 540x360 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#plotting to see the budget range\n",
    "sns.catplot(x = 'budget_range', y = 'worldwide_gross', aspect = 1.5, kind = 'box', \n",
    "            palette=\"Blues\", data = budgets_df)\n",
    "plt.title('Impact of Budget on Worldwide Gross')\n",
    "plt.xlabel('Budget in USD Millions')\n",
    "plt.ylabel('Worldwide Gross in USD Billions')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Recommendation based on budgets"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "A budget of above $50 million leads to a greater worldwide gross thus higher profits"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Release Month"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 72,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Create month column \n",
    "budgets_df['release_month'] = pd.DatetimeIndex(budgets_df['release_date']).month"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 73,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "      <th>budget_range</th>\n",
       "      <th>release_month</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>12</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>317000000.0</td>\n",
       "      <td>620181382.0</td>\n",
       "      <td>1.316722e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>12</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   id  release_date                                        movie  \\\n",
       "0   1  Dec 18, 2009                                       Avatar   \n",
       "1   2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2   3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3   4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4   5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "\n",
       "   production_budget  domestic_gross  worldwide_gross budget_range  \\\n",
       "0        425000000.0     760507625.0     2.776345e+09         >50m   \n",
       "1        410600000.0     241063875.0     1.045664e+09         >50m   \n",
       "2        350000000.0      42762350.0     1.497624e+08         >50m   \n",
       "3        330600000.0     459005868.0     1.403014e+09         >50m   \n",
       "4        317000000.0     620181382.0     1.316722e+09         >50m   \n",
       "\n",
       "   release_month  \n",
       "0             12  \n",
       "1              5  \n",
       "2              6  \n",
       "3              5  \n",
       "4             12  "
      ]
     },
     "execution_count": 73,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "budgets_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 74,
   "metadata": {},
   "outputs": [],
   "source": [
    "def releasemonthplot(df):\n",
    "    fig, ax = plt.subplots(ncols = 2, nrows = 1, figsize = (12,5))\n",
    "    sns.barplot( x = 'release_month', color = '#9ecae1',data = df, ax = ax[0])\n",
    "    ax[0].set_xlabel('Release Month')\n",
    "    ax[0].set_ylabel('Number of Movies')\n",
    "    ax[0].set_title('Number of Movies released per Month')\n",
    "    sns.barplot( x = 'release_month', y = 'worldwide_gross', color = '#3182bd', \n",
    "                data = df, ax = ax[1])\n",
    "    ax[1].set_xlabel('Release Month')\n",
    "    ax[1].set_ylabel('Worldwide Gross in USD billions')\n",
    "    ax[1].set_title('Worldwide Gross per Release Month')\n",
    "    plt.close(2)\n",
    "    plt.close(3)\n",
    "    return plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 75,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 864x360 with 2 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#Running function for dataframe\n",
    "releasemonthplot(budgets_df)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Recommendation(Release month)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There is generally a higher worldwide gross in June and July thus one should aim to release movies then"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Data Analysis(Runtime)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 76,
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
       "      <th>movie_id</th>\n",
       "      <th>primary_title</th>\n",
       "      <th>original_title</th>\n",
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>tt0063540</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>2013</td>\n",
       "      <td>175.000000</td>\n",
       "      <td>Action,Crime,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>tt0066787</td>\n",
       "      <td>One Day Before the Rainy Season</td>\n",
       "      <td>Ashad Ka Ek Din</td>\n",
       "      <td>2019</td>\n",
       "      <td>114.000000</td>\n",
       "      <td>Biography,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>tt0069049</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>2018</td>\n",
       "      <td>122.000000</td>\n",
       "      <td>Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>tt0069204</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>2018</td>\n",
       "      <td>86.186126</td>\n",
       "      <td>Comedy,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>tt0100275</td>\n",
       "      <td>The Wandering Soap Opera</td>\n",
       "      <td>La Telenovela Errante</td>\n",
       "      <td>2017</td>\n",
       "      <td>80.000000</td>\n",
       "      <td>Comedy,Drama,Fantasy</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    movie_id                    primary_title              original_title  \\\n",
       "0  tt0063540                        Sunghursh                   Sunghursh   \n",
       "1  tt0066787  One Day Before the Rainy Season             Ashad Ka Ek Din   \n",
       "2  tt0069049       The Other Side of the Wind  The Other Side of the Wind   \n",
       "3  tt0069204                  Sabse Bada Sukh             Sabse Bada Sukh   \n",
       "4  tt0100275         The Wandering Soap Opera       La Telenovela Errante   \n",
       "\n",
       "   start_year  runtime_minutes                genres  \n",
       "0        2013       175.000000    Action,Crime,Drama  \n",
       "1        2019       114.000000       Biography,Drama  \n",
       "2        2018       122.000000                 Drama  \n",
       "3        2018        86.186126          Comedy,Drama  \n",
       "4        2017        80.000000  Comedy,Drama,Fantasy  "
      ]
     },
     "execution_count": 76,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 77,
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
       "      <th>primary_title</th>\n",
       "      <th>runtime_minutes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>175.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>One Day Before the Rainy Season</td>\n",
       "      <td>114.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>122.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>86.186126</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>The Wandering Soap Opera</td>\n",
       "      <td>80.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>146138</th>\n",
       "      <td>The Secret of China</td>\n",
       "      <td>86.186126</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>146139</th>\n",
       "      <td>Kuambil Lagi Hatiku</td>\n",
       "      <td>123.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>146140</th>\n",
       "      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>\n",
       "      <td>86.186126</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>146141</th>\n",
       "      <td>Dankyavar Danka</td>\n",
       "      <td>86.186126</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>146143</th>\n",
       "      <td>Chico Albuquerque - Revelações</td>\n",
       "      <td>86.186126</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>140734 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                      primary_title  runtime_minutes\n",
       "0                                         Sunghursh       175.000000\n",
       "1                   One Day Before the Rainy Season       114.000000\n",
       "2                        The Other Side of the Wind       122.000000\n",
       "3                                   Sabse Bada Sukh        86.186126\n",
       "4                          The Wandering Soap Opera        80.000000\n",
       "...                                             ...              ...\n",
       "146138                          The Secret of China        86.186126\n",
       "146139                          Kuambil Lagi Hatiku       123.000000\n",
       "146140  Rodolpho Teóphilo - O Legado de um Pioneiro        86.186126\n",
       "146141                              Dankyavar Danka        86.186126\n",
       "146143               Chico Albuquerque - Revelações        86.186126\n",
       "\n",
       "[140734 rows x 2 columns]"
      ]
     },
     "execution_count": 77,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df[['primary_title', 'runtime_minutes']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 78,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    140734.000000\n",
       "mean         86.246280\n",
       "std         149.934119\n",
       "min           1.000000\n",
       "25%          75.000000\n",
       "50%          86.186126\n",
       "75%          95.000000\n",
       "max       51420.000000\n",
       "Name: runtime_minutes, dtype: float64"
      ]
     },
     "execution_count": 78,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df['runtime_minutes'].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 79,
   "metadata": {},
   "outputs": [],
   "source": [
    "moviebasics_df.rename(columns = {'primary_title':'movie'}, inplace = True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 80,
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
       "      <th>movie_id</th>\n",
       "      <th>movie</th>\n",
       "      <th>original_title</th>\n",
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>tt0063540</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>Sunghursh</td>\n",
       "      <td>2013</td>\n",
       "      <td>175.000000</td>\n",
       "      <td>Action,Crime,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>tt0066787</td>\n",
       "      <td>One Day Before the Rainy Season</td>\n",
       "      <td>Ashad Ka Ek Din</td>\n",
       "      <td>2019</td>\n",
       "      <td>114.000000</td>\n",
       "      <td>Biography,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>tt0069049</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>The Other Side of the Wind</td>\n",
       "      <td>2018</td>\n",
       "      <td>122.000000</td>\n",
       "      <td>Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>tt0069204</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>Sabse Bada Sukh</td>\n",
       "      <td>2018</td>\n",
       "      <td>86.186126</td>\n",
       "      <td>Comedy,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>tt0100275</td>\n",
       "      <td>The Wandering Soap Opera</td>\n",
       "      <td>La Telenovela Errante</td>\n",
       "      <td>2017</td>\n",
       "      <td>80.000000</td>\n",
       "      <td>Comedy,Drama,Fantasy</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    movie_id                            movie              original_title  \\\n",
       "0  tt0063540                        Sunghursh                   Sunghursh   \n",
       "1  tt0066787  One Day Before the Rainy Season             Ashad Ka Ek Din   \n",
       "2  tt0069049       The Other Side of the Wind  The Other Side of the Wind   \n",
       "3  tt0069204                  Sabse Bada Sukh             Sabse Bada Sukh   \n",
       "4  tt0100275         The Wandering Soap Opera       La Telenovela Errante   \n",
       "\n",
       "   start_year  runtime_minutes                genres  \n",
       "0        2013       175.000000    Action,Crime,Drama  \n",
       "1        2019       114.000000       Biography,Drama  \n",
       "2        2018       122.000000                 Drama  \n",
       "3        2018        86.186126          Comedy,Drama  \n",
       "4        2017        80.000000  Comedy,Drama,Fantasy  "
      ]
     },
     "execution_count": 80,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "moviebasics_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 81,
   "metadata": {},
   "outputs": [],
   "source": [
    "movies_and_budgets = budgets_df.merge(moviebasics_df, on = \"movie\", how = \"inner\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 83,
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
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "      <th>budget_range</th>\n",
       "      <th>release_month</th>\n",
       "      <th>movie_id</th>\n",
       "      <th>original_title</th>\n",
       "      <th>start_year</th>\n",
       "      <th>runtime_minutes</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>425000000.0</td>\n",
       "      <td>760507625.0</td>\n",
       "      <td>2.776345e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>12</td>\n",
       "      <td>tt1775309</td>\n",
       "      <td>Abatâ</td>\n",
       "      <td>2011</td>\n",
       "      <td>93.0</td>\n",
       "      <td>Horror</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>410600000.0</td>\n",
       "      <td>241063875.0</td>\n",
       "      <td>1.045664e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>5</td>\n",
       "      <td>tt1298650</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>2011</td>\n",
       "      <td>136.0</td>\n",
       "      <td>Action,Adventure,Fantasy</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>350000000.0</td>\n",
       "      <td>42762350.0</td>\n",
       "      <td>1.497624e+08</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>6</td>\n",
       "      <td>tt6565702</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>2019</td>\n",
       "      <td>113.0</td>\n",
       "      <td>Action,Adventure,Sci-Fi</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>330600000.0</td>\n",
       "      <td>459005868.0</td>\n",
       "      <td>1.403014e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>5</td>\n",
       "      <td>tt2395427</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>2015</td>\n",
       "      <td>141.0</td>\n",
       "      <td>Action,Adventure,Sci-Fi</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>7</td>\n",
       "      <td>Apr 27, 2018</td>\n",
       "      <td>Avengers: Infinity War</td>\n",
       "      <td>300000000.0</td>\n",
       "      <td>678815482.0</td>\n",
       "      <td>2.048134e+09</td>\n",
       "      <td>&gt;50m</td>\n",
       "      <td>4</td>\n",
       "      <td>tt4154756</td>\n",
       "      <td>Avengers: Infinity War</td>\n",
       "      <td>2018</td>\n",
       "      <td>149.0</td>\n",
       "      <td>Action,Adventure,Sci-Fi</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3738</th>\n",
       "      <td>67</td>\n",
       "      <td>Apr 28, 2006</td>\n",
       "      <td>Clean</td>\n",
       "      <td>10000.0</td>\n",
       "      <td>138711.0</td>\n",
       "      <td>1.387110e+05</td>\n",
       "      <td>&lt;7m</td>\n",
       "      <td>4</td>\n",
       "      <td>tt6619196</td>\n",
       "      <td>Clean</td>\n",
       "      <td>2017</td>\n",
       "      <td>70.0</td>\n",
       "      <td>Comedy,Drama,Horror</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3739</th>\n",
       "      <td>68</td>\n",
       "      <td>Jul 6, 2001</td>\n",
       "      <td>Cure</td>\n",
       "      <td>10000.0</td>\n",
       "      <td>94596.0</td>\n",
       "      <td>9.459600e+04</td>\n",
       "      <td>&lt;7m</td>\n",
       "      <td>7</td>\n",
       "      <td>tt1872026</td>\n",
       "      <td>Cure</td>\n",
       "      <td>2011</td>\n",
       "      <td>93.0</td>\n",
       "      <td>Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3740</th>\n",
       "      <td>73</td>\n",
       "      <td>Jan 13, 2012</td>\n",
       "      <td>Newlyweds</td>\n",
       "      <td>9000.0</td>\n",
       "      <td>4584.0</td>\n",
       "      <td>4.584000e+03</td>\n",
       "      <td>&lt;7m</td>\n",
       "      <td>1</td>\n",
       "      <td>tt1880418</td>\n",
       "      <td>Newlyweds</td>\n",
       "      <td>2011</td>\n",
       "      <td>95.0</td>\n",
       "      <td>Comedy,Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3741</th>\n",
       "      <td>78</td>\n",
       "      <td>Dec 31, 2018</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>7000.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>&lt;7m</td>\n",
       "      <td>12</td>\n",
       "      <td>tt7837402</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>2019</td>\n",
       "      <td>77.0</td>\n",
       "      <td>Horror,Sci-Fi,Thriller</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3742</th>\n",
       "      <td>81</td>\n",
       "      <td>Sep 29, 2015</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>1400.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>&lt;7m</td>\n",
       "      <td>9</td>\n",
       "      <td>tt2107644</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>2013</td>\n",
       "      <td>76.0</td>\n",
       "      <td>Drama,Horror,Thriller</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3743 rows × 13 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  release_date                                        movie  \\\n",
       "0      1  Dec 18, 2009                                       Avatar   \n",
       "1      2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2      3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3      4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4      7  Apr 27, 2018                       Avengers: Infinity War   \n",
       "...   ..           ...                                          ...   \n",
       "3738  67  Apr 28, 2006                                        Clean   \n",
       "3739  68   Jul 6, 2001                                         Cure   \n",
       "3740  73  Jan 13, 2012                                    Newlyweds   \n",
       "3741  78  Dec 31, 2018                                       Red 11   \n",
       "3742  81  Sep 29, 2015                         A Plague So Pleasant   \n",
       "\n",
       "      production_budget  domestic_gross  worldwide_gross budget_range  \\\n",
       "0           425000000.0     760507625.0     2.776345e+09         >50m   \n",
       "1           410600000.0     241063875.0     1.045664e+09         >50m   \n",
       "2           350000000.0      42762350.0     1.497624e+08         >50m   \n",
       "3           330600000.0     459005868.0     1.403014e+09         >50m   \n",
       "4           300000000.0     678815482.0     2.048134e+09         >50m   \n",
       "...                 ...             ...              ...          ...   \n",
       "3738            10000.0        138711.0     1.387110e+05          <7m   \n",
       "3739            10000.0         94596.0     9.459600e+04          <7m   \n",
       "3740             9000.0          4584.0     4.584000e+03          <7m   \n",
       "3741             7000.0             0.0     0.000000e+00          <7m   \n",
       "3742             1400.0             0.0     0.000000e+00          <7m   \n",
       "\n",
       "      release_month   movie_id                               original_title  \\\n",
       "0                12  tt1775309                                        Abatâ   \n",
       "1                 5  tt1298650  Pirates of the Caribbean: On Stranger Tides   \n",
       "2                 6  tt6565702                                 Dark Phoenix   \n",
       "3                 5  tt2395427                      Avengers: Age of Ultron   \n",
       "4                 4  tt4154756                       Avengers: Infinity War   \n",
       "...             ...        ...                                          ...   \n",
       "3738              4  tt6619196                                        Clean   \n",
       "3739              7  tt1872026                                         Cure   \n",
       "3740              1  tt1880418                                    Newlyweds   \n",
       "3741             12  tt7837402                                       Red 11   \n",
       "3742              9  tt2107644                         A Plague So Pleasant   \n",
       "\n",
       "      start_year  runtime_minutes                    genres  \n",
       "0           2011             93.0                    Horror  \n",
       "1           2011            136.0  Action,Adventure,Fantasy  \n",
       "2           2019            113.0   Action,Adventure,Sci-Fi  \n",
       "3           2015            141.0   Action,Adventure,Sci-Fi  \n",
       "4           2018            149.0   Action,Adventure,Sci-Fi  \n",
       "...          ...              ...                       ...  \n",
       "3738        2017             70.0       Comedy,Drama,Horror  \n",
       "3739        2011             93.0                     Drama  \n",
       "3740        2011             95.0              Comedy,Drama  \n",
       "3741        2019             77.0    Horror,Sci-Fi,Thriller  \n",
       "3742        2013             76.0     Drama,Horror,Thriller  \n",
       "\n",
       "[3743 rows x 13 columns]"
      ]
     },
     "execution_count": 83,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movies_and_budgets"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 84,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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/TRFMIe5ZlMHsYjQGI8i4v7HIsI1mzqmWzTDMKYQUwRzmF09CRpikRFlDbEIu3sS0ySRYUwPP/3pTxERtm7dmi/buXMnL33pSwHYuHEjb3rTm0Ydt3HjRkSE66+/Pl/24IMPIiJ89atfnZAsF154IU888cTYO1YRUwRzmOULGhlKj0xwNJTOsmxBY4kjDOPgZMOGDZx22mnceOON4z72ZS97GTfddFP+84033siJJ544YVmuu+46jjvuuAkfPxFMEcxh1q9dRTqrJFIZVN3/dFZZv7ZamRYNo7ps3NrJBddu5rQr7uSCazdXZT5rYGCA3/72t1x//fUTUgQrVqxgeHiYPXv2oKrcdtttnHHGgaR9Dz30EKeccgonnHACb3nLW+jp6eHJJ5/kVa86kA10586dnHDCCQCsW7cuH0bnV7/6Faeeeionn3wyb3vb2xgYGADgkksu4bjjjuOEE07gU58qlhRxfJgimMOsW93OZWcdT3tLPfuH0rS31HPZWcfbqiFjRlKrxQ0/+9nPOP300znmmGNYuHAhW7ZsGXcd5557Lv/5n//Jvffey8knn0xd3YEsqu9+97u54ooreOSRR3jZy17G5z//eY499lhSqRQdHW4+7qabbuLtb3/7iDq7urr44he/yB133MGWLVtYs2YNX/va19i3bx8//elPefzxx3nkkUf4zGc+M6nrB1s+OudZt7rdGn5jVhBe3ADQGI+SSGW4ZlPHpJ7hDRs28PGPfxyA888/nw0bNnDyySePq463v/3tnHfeeWzdupULLriAe+916Yr3799Pb28vr3vd6wB4z3vew9ve9rb8MT/+8Y+55JJLuOmmm0aYlwA2b97ME088wWtf+1oAUqkUp556KvPmzaO+vp4LL7yQN77xjUXnLsaLKQLDMGYFu3oStDaM9Jad7OKG7u5u7rzzTh577DFEhGw2i4jw5S9/eVz1LFmyhFgsxu23386VV16ZVwTlOO+883jb297GOeecg4hw9NFHj9iuqvz5n/85GzZsGHXs73//e379619z44038s1vfpM777xzXPIWYqYhwzBmBbVY3HDzzTfz7ne/m2eeeYadO3eya9cuVq5cyT333DPuui677DKuuOIKIpEDK/Hmz5/PggULuPvuuwH4wQ9+kB8dHHnkkUQiEb7whS9w3nnnjarvlFNO4be//S3bt28HIJFI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\n",
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
    "#analysing the joined dataframe\n",
    "sns.regplot(x = 'runtime_minutes', y = 'worldwide_gross', \n",
    "            label = 'All Movies', data = movies_and_budgets)\n",
    "plt.xlabel('Runtime in Minutes')\n",
    "plt.ylabel('Worldwide Gross in USD Billions')\n",
    "plt.title('Relationship between Runtime and Worldwide Gross')\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "96.00528417900202"
      ]
     },
     "execution_count": 86,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movies_and_budgets['runtime_minutes'].mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 87,
   "metadata": {},
   "outputs": [
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
    "movies_and_budgets[\"runtime_minutes\"].hist(bins = 30);"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# #Recommendation(Runtime)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "There does not seem to be any correlation between runtime and worldwide gross.The safer option would be to aim for the average runtime which is 100 minutes"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python (learn-env)",
   "language": "python",
   "name": "learn-env"
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
   "version": "3.8.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
