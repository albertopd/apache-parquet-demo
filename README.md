# Apache Parquet vs CSV Benchmarking Demo

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![Python](https://img.shields.io/badge/Python-3.13-blue.svg)](https://www.python.org/) [![pandas](https://img.shields.io/badge/pandas-2.2-blue.svg)](https://pandas.pydata.org/) [![fastparquet](https://img.shields.io/badge/fastparquet-2024.5.0-blue.svg)](https://fastparquet.readthedocs.io/) [![matplotlib](https://img.shields.io/badge/matplotlib-3.9-blue.svg)](https://matplotlib.org/) 

This project demonstrates the performance advantages of Apache Parquet over CSV format for data storage and processing. Using the "Best Books Ever" dataset, it compares file sizes, read performance, and advanced features like column selection, predicate pushdown, and partition pruning.

## ✨ Features

- **File Size Comparison**: Compare storage efficiency between CSV and different Parquet formats
- **Performance Benchmarking**: Measure read times for various data access patterns
- **Column Selection**: Demonstrate columnar storage advantages for partial data reads
- **Predicate Pushdown**: Show how Parquet can filter data during read operations
- **Partition Pruning**: Illustrate performance benefits of partitioned datasets
- **Compression Analysis**: Compare default vs compressed Parquet formats
- **Visualizations**: Generate charts showing performance differences

## 📂 Project Structure

```
apache-parquet-demo/
├── data/
│   ├── books.csv                    # Source CSV dataset (must be downloaded)
│   ├── books_default.parquet        # Default Parquet format (generated)
│   ├── books_compressed.parquet     # Snappy-compressed Parquet (generated)
│   ├── books_partitioned/           # Language-partitioned dataset (generated)
│   └── README.md                    # Data source information
├── parquet_vs_csv_benchmark.ipynb   # Main benchmarking notebook
├── requirements.txt                 # Python dependencies
├── LICENSE                          # MIT License
└── README.md                        # This file
```

## 📋 Requirements

- Python 3.13 or later
- Required Python packages listed in [requirements.txt](requirements.txt)
- Dataset: Books CSV file from [Zenodo - Best Books Ever Dataset](https://zenodo.org/records/4265096)

## 📦 Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/albertopd/apache-parquet-demo.git
   cd apache-parquet-demo
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the dataset**:
   - Visit [Zenodo - Best Books Ever Dataset](https://zenodo.org/records/4265096)
   - Download the `books.csv` file
   - Place it in the `data/` directory

## 🚀 Usage

1. **Start Jupyter Notebook**:
   ```bash
   jupyter notebook parquet_vs_csv_benchmark.ipynb
   ```

2. **Run the benchmark**:
   - Execute all cells in order to see the complete analysis
   - The notebook will automatically create Parquet files in different formats
   - View performance comparisons and file size charts

### What the Benchmark Tests

#### File Size Comparison

- **CSV**: Original format
- **Parquet (default)**: Uncompressed Parquet
- **Parquet (compressed)**: GZip compression
- **Parquet (partitioned)**: Partitioned by language (and GZip compressed)

#### Performance Tests

1. **Full dataset loading**: Complete file read performance
2. **Column selection**: Reading only specific columns (title, author, rating)
3. **Predicate pushdown**: Filtering books with rating > 4.5
4. **Partition pruning**: Reading only English books from partitioned dataset

## 📝 Example Output

### File Size Reduction

Typical results show significant storage savings:

```
=============== File Size Comparison ==============
CSV                       70.43 MB
Parquet (default)         40.66 MB  (42.3% smaller)
Parquet (compressed)      25.36 MB  (64.0% smaller)
Parquet (comp/partioned)  23.32 MB  (66.9% smaller)
```

### Performance Improvements

Benchmark results demonstrate Parquet's advantages:

```
=================== Load Full Dataset ====================
CSV                                           Time: 1.203s
Parquet                                       Time: 0.227s

===== Load Subset of Columns (title, author, rating) =====
CSV - Column Subset                           Time: 0.520s
Parquet - Column Pruning                      Time: 0.020s

============= Load Rows Where: rating > 4.5 ==============
CSV - Filter Rows After Load                  Time: 1.220s
Parquet - Predicate Pushdown                  Time: 0.207s

========= Load Rows Where: language == 'English' =========
CSV - Filter Rows After Load                  Time: 1.245s
Parquet - Partition Pruning                   Time: 0.389s
```

### Visual Charts

![File Size Comparison](screenshots/file-size-comparison.png)

![Performance Comparison](screenshots/performance-comparison.png)

## 🎯 Key Takeaways

- **Storage**: Parquet typically reduces file size by 65-75%
- **Speed**: Column-oriented access is significantly faster
- **Features**: Parquet supports advanced query optimizations

## 📜 License

This project is licensed under the [MIT License](LICENSE).

## 👤 Author

[Alberto Pérez Dávila](https://github.com/albertopd)