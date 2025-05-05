# histogram-for-marks-data
import pandas as pd
import matplotlib.pyplot as plt

# Replace 'your_excel_file.xlsx' with the actual file path
file_path = 'your_excel_file.xlsx'

try:
    # Read the Excel file into a Pandas DataFrame
    df = pd.read_excel(file_path)

    # Ensure there's a 'Marks' column
    if 'Marks' not in df.columns:
        raise ValueError("The Excel file must contain a column named 'Marks'")

    # Calculate percentages
    df['Percentage'] = (df['Marks'] / 15) * 100

    # Categorize students
    high_achievers = df[df['Percentage'] > 75]
    good_achievers = df[(df['Percentage'] >= 60) & (df['Percentage'] <= 75)]
    below_average = df[df['Percentage'] < 60]

    # Print the categorized data
    print("High Achievers (75% +):\n", high_achievers)
    print("\nGood Achievers (60% - 75%):\n", good_achievers)
    print("\nBelow Average (Under 60%):\n", below_average)

    # --- Histogram Plot ---
    # Prepare data for histogram
    histogram_data = []
    histogram_labels = []
    if not high_achievers.empty:
        histogram_data.append(len(high_achievers))
        histogram_labels.append('75%+')
    if not good_achievers.empty:
        histogram_data.append(len(good_achievers))
        histogram_labels.append('60%-75%')
    if not below_average.empty:
        histogram_data.append(len(below_average))
        histogram_labels.append('Under 60%')

    # Plot the histogram
    plt.figure(figsize=(8, 6))
    plt.bar(histogram_labels, histogram_data, color='blue', edgecolor='black', width=0.5)
    plt.xlabel('Percentage')
    plt.ylabel('Number of Students')
    plt.title('Histogram Plot')
    plt.grid(True)
    plt.show()

    # --- Scatter Plot ---
    # Prepare data for scatter plot
    student_names = df['Student'].tolist()  # Assuming there's a 'Student' column
    percentages = df['Percentage'].tolist()

    # Plot the scatter plot
    plt.figure(figsize=(8, 6))
    plt.scatter(student_names, percentages, color='blue', marker='o')
    plt.xlabel('Students')
    plt.ylabel('Percentage')
    plt.title('Scatter Plot')
    plt.grid(True)
    plt.show()


except FileNotFoundError:
    print(f"Error: File not found at {file_path}. Please check the file path.")
except ValueError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
