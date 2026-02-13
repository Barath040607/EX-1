import numpy as np
import pandas as pd

# Create training dataset directly (No CSV file needed)
data = pd.DataFrame({
    'Sky': ['Sunny', 'Sunny', 'Rainy', 'Sunny'],
    'AirTemp': ['Warm', 'Warm', 'Cold', 'Warm'],
    'Humidity': ['Normal', 'High', 'High', 'High'],
    'Wind': ['Strong', 'Strong', 'Strong', 'Strong'],
    'Water': ['Warm', 'Warm', 'Warm', 'Cool'],
    'Forecast': ['Same', 'Same', 'Change', 'Change'],
    'EnjoySport': ['Yes', 'Yes', 'No', 'Yes']
})

print("Training Data:\n")
print(data)

# Separate features and target
concepts = np.array(data.iloc[:, :-1])
target = np.array(data.iloc[:, -1])

print("\nConcepts:\n", concepts)
print("\nTarget:\n", target)


# Candidate Elimination Algorithm
def learn(concepts, target):

    specific_h = concepts[0].copy()
    print("\nInitial Specific Hypothesis:")
    print(specific_h)

    general_h = [["?" for _ in range(len(specific_h))]
                 for _ in range(len(specific_h))]

    print("\nInitial General Hypothesis:")
    print(general_h)

    for i, h in enumerate(concepts):

        if target[i] == "Yes":  # Positive example
            for x in range(len(specific_h)):
                if h[x] != specific_h[x]:
                    specific_h[x] = "?"
                    general_h[x][x] = "?"

        if target[i] == "No":  # Negative example
            for x in range(len(specific_h)):
                if h[x] != specific_h[x]:
                    general_h[x][x] = specific_h[x]
                else:
                    general_h[x][x] = "?"

        print("\nStep", i + 1)
        print("Specific Hypothesis:", specific_h)
        print("General Hypothesis:", general_h)

    # Remove all '?' rows from general hypothesis
    general_h = [g for g in general_h if g != ["?" for _ in range(len(specific_h))]]

    return specific_h, general_h


# Run algorithm
s_final, g_final = learn(concepts, target)

print("\nFinal Specific Hypothesis:")
print(s_final)

print("\nFinal General Hypothesis:")
print(g_final)
