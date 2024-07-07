# Breast Audit Data Processing

This project provides a script to read a .xlsx file containing breast audit data, process the data, and write it to a .csv file. Additionally, the script performs various data transformations and visualisations.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Data Processing Steps](#data-processing-steps)
- [Visualisations](#visualisations)
- [Contributing](#contributing)
- [License](#license)

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/breast-audit-data-processing.git
    ```
2. Navigate to the project directory:
    ```bash
    cd breast-audit-data-processing
    ```
3. Install the required Python packages:
    ```bash
    pip install pandas matplotlib
    ```

## Usage

1. Update the `input_file` and `output_file` paths in the script to match your file locations:
    ```python
    input_file = "/path/to/your/input.xlsx"
    output_file = "/path/to/your/output.csv"
    ```

2. Run the script:
    ```bash
    python process_data.py
    ```

## Data Processing Steps

The script performs the following steps:

1. **Read the .xlsx file:**
    ```python
    df = pd.read_excel(input_file, skiprows=5)
    ```

2. **Write the data to a .csv file:**
    ```python
    df.to_csv(output_file, index=False)
    ```

3. **Initial Data Exploration:**
    - Print the first 5 rows.
    - Print the shape of the dataframe.
    - Print the column names.
    - Print the data types of the columns.

4. **Data Cleaning and Transformation:**
    - Remove the `Number` column.
    - Rename columns to remove spaces and provide meaningful names.
    - Replace NaN values in specific columns.
    - Map categorical values to numerical values.
    - Handle NaN values row by row for specific columns.

5. **Data Visualisations:**
    - Bar chart for the distribution of `UssType`.
    - Pie chart for `Further Annotations`.

## Visualisations

The script includes code to visualise the data using `matplotlib`.

1. **Bar Chart for UssType:**
    ```python
    ax = df['UssType'].value_counts().plot(kind='bar')
    for i in ax.patches:
        ax.text(i.get_x() + i.get_width() / 2, i.get_height() + 0.5,
                f'{(i.get_height() / df.shape[0] * 100):.2f}%', ha='center')
    plt.xlabel('UssType')
    plt.ylabel('Frequency')
    plt.title('Type of Breast Ultrasound Scan')
    plt.show()
    ```

2. **Pie Chart for Further Annotations:**
    ```python
    values = [df['Further_Annotations'].value_counts()[0.0], df['Further_Annotations'].value_counts()[1.0],
              df[(df['Further_Annotations'] == 1.0) & (df['Defined_Zone'] == 1.0)].shape[0]]
    labels = ['No Further Annotations', 'Further Annotations', 'Further Annotations with Defined Zone']
    plt.pie(values, labels=labels, autopct='%1.1f%%')
    plt.title('Further Annotations')
    plt.show()
    ```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
