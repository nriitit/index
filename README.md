
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Subjects</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      text-align: center;
      padding: 50px;
    }

    h1 {
      color: #333;
      margin-bottom: 30px;
    }

    .tab-button {
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .tab-button:hover {
      background-color: #0056b3;
    }

    .tab-content {
      display: none;
      text-align: left;
      margin-top: 30px;
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
      overflow-x: auto;
    }

    pre {
      white-space: pre-wrap;
      word-wrap: break-word;
    }
  </style>
</head>
<body>

  <h1>Welcome to My Subject Portal</h1>

  <!-- Buttons for each tab -->
  <button class="tab-button" onclick="showTab('bda')">BDA LAB</button>
  <button class="tab-button" onclick="showTab('ml')">ML LAB</button>
  <button class="tab-button" onclick="showTab('ml3')">ML-3</button>
  <button class="tab-button" onclick="showTab('cns8a')">CNS8A</button>
  <button class="tab-button" onclick="showTab('cns8b')">CNS8B</button>
  <button class="tab-button" onclick="showTab('id3ml')">ID3ML</button>

  <!-- Tab contents -->
  <div id="bda" class="tab-content">
    <iframe src="https://drive.google.com/file/d/1ZLqwIfCu7R4F_RMvzbAUI0Mwc16mdwg5/preview" width="100%" height="500"></iframe>
  </div>

  <div id="ml" class="tab-content">
    <iframe src="https://drive.google.com/file/d/1YAOuKECOeBpOQeDjeZnxwybdK2dsKC3U/preview" width="100%" height="500"></iframe>
  </div>

  <div id="ml3" class="tab-content">
    <pre>
import math
import pandas as pd

def calculate_entropy(data):
    value_counts = data.value_counts()
    total_records = len(data)
    entropy = 0
    for count in value_counts:
        prob = count / total_records
        entropy -= prob * math.log2(prob)
    return entropy

def calculate_information_gain(data, attribute, target):
    total_entropy = calculate_entropy(data[target])
    unique_values = data[attribute].unique()
    weighted_entropy = 0
    for value in unique_values:
        subset = data[data[attribute] == value]
        weighted_entropy += (len(subset) / len(data)) * calculate_entropy(subset[target])
    information_gain = total_entropy - weighted_entropy
    return information_gain

def id3(data, target, attributes):
    if len(data[target].unique()) == 1:
        return data[target].iloc[0]
    if not attributes:
        return data[target].mode()[0]
    info_gains = {attr: calculate_information_gain(data, attr, target) for attr in attributes}
    best_attribute = max(info_gains, key=info_gains.get)
    tree = {best_attribute: {}}
    for value in data[best_attribute].unique():
        subset = data[data[best_attribute] == value]
        remaining_attributes = [attr for attr in attributes if attr != best_attribute]
        subtree = id3(subset, target, remaining_attributes)
        tree[best_attribute][value] = subtree
    return tree

def classify(tree, sample):
    if not isinstance(tree, dict):
        return tree
    attribute = next(iter(tree))
    attribute_value = sample[attribute]
    subtree = tree[attribute].get(attribute_value)
    return classify(subtree, sample)

data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rainy', 'Rainy', 'Rainy', 'Overcast', 'Sunny', 'Sunny', 
                'Rainy', 'Sunny', 'Overcast', 'Overcast', 'Rainy'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 
                    'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 
                 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 
             'Strong', 'Strong', 'Weak', 'Strong'],
    'PlayTennis': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})

target = 'PlayTennis'
attributes = ['Outlook', 'Temperature', 'Humidity', 'Wind']
tree = id3(data, target, attributes)

print("Decision Tree:")
print(tree)

sample = {'Outlook': 'Sunny', 'Temperature': 'Hot', 'Humidity': 'High', 'Wind': 'Weak'}
result = classify(tree, sample)
print(f"\nClassifying new sample {sample}: {result}")
    </pre>
  </div>

  <div id="cns8a" class="tab-content">
    <pre>
import java.math.BigInteger;
import java.security.SecureRandom;

public class RSA {
    public static void main(String[] args) {
        try {
            SecureRandom rand = new SecureRandom();
            BigInteger p = BigInteger.probablePrime(512, rand);
            BigInteger q = BigInteger.probablePrime(512, rand);

            BigInteger n = p.multiply(q);
            BigInteger phi = p.subtract(BigInteger.ONE).multiply(q.subtract(BigInteger.ONE));
            BigInteger e = BigInteger.valueOf(65537);
            BigInteger d = e.modInverse(phi);

            String message = "Hello, RSA!";
            BigInteger msg = new BigInteger(message.getBytes());

            BigInteger cipher = msg.modPow(e, n);
            BigInteger decrypt = cipher.modPow(d, n);
            String dec = new String(decrypt.toByteArray());

            System.out.println("Encrypted: " + cipher);
            System.out.println("Decrypted: " + dec);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
    </pre>
  </div>

  <div id="cns8b" class="tab-content">
    <pre>
#include <stdio.h>
int main()
{
    char *str = "Hello World";
    printf("Original string:%s\n", str);
    printf("After AND operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char and_result = str[i] & 127;
        printf("%c", and_result);
    }

    printf("\n");
    printf("After XOR operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char xor_result = str[i] ^ 127;
        printf("%c", xor_result);
    }

    printf("\n");
    return 0;
}
    </pre>
  </div>

  <div id="id3ml" class="tab-content">
    <pre>
import pandas as pd
import numpy as np
from math import log2

def entropy(data):
    labels = data.iloc[:, -1]
    classes = labels.unique()
    return -sum((labels == c).mean() * log2((labels == c).mean()) for c in classes)

def info_gain(data, feature):
    total_entropy = entropy(data)
    values = data[feature].unique()
    weighted_entropy = sum(
        (data[feature] == v).mean() * entropy(data[data[feature] == v])
        for v in values
    )
    return total_entropy - weighted_entropy

def id3(data, features):
    labels = data.iloc[:, -1]
    
    if len(labels.unique()) == 1:
        return labels.iloc[0]
    if not features:
        return labels.mode()[0]
    
    gains = {f: info_gain(data, f) for f in features}
    best = max(gains, key=gains.get)
    tree = {best: {}}
    
    for val in data[best].unique():
        subset = data[data[best] == val].drop(columns=best)
        if subset.empty:
            tree[best][val] = labels.mode()[0]
        else:
            tree[best][val] = id3(subset.reset_index(drop=True), [f for f in features if f != best])
    
    return tree

data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rain', 'Rain', 'Rain', 'Overcast', 'Sunny', 'Sunny', 'Rain', 'Sunny', 'Overcast', 'Overcast', 'Rain'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Strong'],
    'Play': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})

tree = id3(data, data.columns[:-1].tolist())
from pprint import pprint
pprint(tree)
    </pre>
  </div>

  <script>
    function showTab(tabId) {
      var contents = document.querySelectorAll('.tab-content');
      contents.forEach(c => c.style.display = 'none');
      document.getElementById(tabId).style.display = 'block';
    }
  </script>

</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Subjects</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      text-align: center;
      padding: 50px;
    }

    h1 {
      color: #333;
      margin-bottom: 30px;
    }

    .tab-button {
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .tab-button:hover {
      background-color: #0056b3;
    }

    .tab-content {
      display: none;
      text-align: left;
      margin-top: 30px;
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
      overflow-x: auto;
    }

    pre {
      white-space: pre-wrap;
      word-wrap: break-word;
    }
  </style>
</head>
<body>

  <h1>Welcome to My Subject Portal</h1>

  <!-- Buttons for each tab -->
  <button class="tab-button" onclick="showTab('bda')">BDA LAB</button>
  <button class="tab-button" onclick="showTab('ml')">ML LAB</button>
  <button class="tab-button" onclick="showTab('ml3')">ML-3</button>
  <button class="tab-button" onclick="showTab('cns8a')">CNS8A</button>
  <button class="tab-button" onclick="showTab('cns8b')">CNS8B</button>
  <button class="tab-button" onclick="showTab('id3ml')">ID3ML</button>

  <!-- Tab contents -->
  <div id="bda" class="tab-content">
    <iframe src="https://drive.google.com/file/d/1ZLqwIfCu7R4F_RMvzbAUI0Mwc16mdwg5/preview" width="100%" height="500"></iframe>
  </div>

  <div id="ml" class="tab-content">
    <iframe src="https://drive.google.com/file/d/1YAOuKECOeBpOQeDjeZnxwybdK2dsKC3U/preview" width="100%" height="500"></iframe>
  </div>

  <div id="ml3" class="tab-content">
    <pre>
import math
import pandas as pd

def calculate_entropy(data):
    value_counts = data.value_counts()
    total_records = len(data)
    entropy = 0
    for count in value_counts:
        prob = count / total_records
        entropy -= prob * math.log2(prob)
    return entropy

def calculate_information_gain(data, attribute, target):
    total_entropy = calculate_entropy(data[target])
    unique_values = data[attribute].unique()
    weighted_entropy = 0
    for value in unique_values:
        subset = data[data[attribute] == value]
        weighted_entropy += (len(subset) / len(data)) * calculate_entropy(subset[target])
    information_gain = total_entropy - weighted_entropy
    return information_gain

def id3(data, target, attributes):
    if len(data[target].unique()) == 1:
        return data[target].iloc[0]
    if not attributes:
        return data[target].mode()[0]
    info_gains = {attr: calculate_information_gain(data, attr, target) for attr in attributes}
    best_attribute = max(info_gains, key=info_gains.get)
    tree = {best_attribute: {}}
    for value in data[best_attribute].unique():
        subset = data[data[best_attribute] == value]
        remaining_attributes = [attr for attr in attributes if attr != best_attribute]
        subtree = id3(subset, target, remaining_attributes)
        tree[best_attribute][value] = subtree
    return tree

def classify(tree, sample):
    if not isinstance(tree, dict):
        return tree
    attribute = next(iter(tree))
    attribute_value = sample[attribute]
    subtree = tree[attribute].get(attribute_value)
    return classify(subtree, sample)

data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rainy', 'Rainy', 'Rainy', 'Overcast', 'Sunny', 'Sunny', 
                'Rainy', 'Sunny', 'Overcast', 'Overcast', 'Rainy'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 
                    'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 
                 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 
             'Strong', 'Strong', 'Weak', 'Strong'],
    'PlayTennis': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})

target = 'PlayTennis'
attributes = ['Outlook', 'Temperature', 'Humidity', 'Wind']
tree = id3(data, target, attributes)

print("Decision Tree:")
print(tree)

sample = {'Outlook': 'Sunny', 'Temperature': 'Hot', 'Humidity': 'High', 'Wind': 'Weak'}
result = classify(tree, sample)
print(f"\nClassifying new sample {sample}: {result}")
    </pre>
  </div>

  <div id="cns8a" class="tab-content">
    <pre>
import java.math.BigInteger;
import java.security.SecureRandom;

public class RSA {
    public static void main(String[] args) {
        try {
            SecureRandom rand = new SecureRandom();
            BigInteger p = BigInteger.probablePrime(512, rand);
            BigInteger q = BigInteger.probablePrime(512, rand);

            BigInteger n = p.multiply(q);
            BigInteger phi = p.subtract(BigInteger.ONE).multiply(q.subtract(BigInteger.ONE));
            BigInteger e = BigInteger.valueOf(65537);
            BigInteger d = e.modInverse(phi);

            String message = "Hello, RSA!";
            BigInteger msg = new BigInteger(message.getBytes());

            BigInteger cipher = msg.modPow(e, n);
            BigInteger decrypt = cipher.modPow(d, n);
            String dec = new String(decrypt.toByteArray());

            System.out.println("Encrypted: " + cipher);
            System.out.println("Decrypted: " + dec);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
    </pre>
  </div>

  <div id="cns8b" class="tab-content">
    <pre>
#include <stdio.h>
int main()
{
    char *str = "Hello World";
    printf("Original string:%s\n", str);
    printf("After AND operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char and_result = str[i] & 127;
        printf("%c", and_result);
    }

    printf("\n");
    printf("After XOR operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char xor_result = str[i] ^ 127;
        printf("%c", xor_result);
    }

    printf("\n");
    return 0;
}
    </pre>
  </div>

  <div id="id3ml" class="tab-content">
    <pre>
import pandas as pd
import numpy as np
from math import log2

def entropy(data):
    labels = data.iloc[:, -1]
    classes = labels.unique()
    return -sum((labels == c).mean() * log2((labels == c).mean()) for c in classes)

def info_gain(data, feature):
    total_entropy = entropy(data)
    values = data[feature].unique()
    weighted_entropy = sum(
        (data[feature] == v).mean() * entropy(data[data[feature] == v])
        for v in values
    )
    return total_entropy - weighted_entropy

def id3(data, features):
    labels = data.iloc[:, -1]
    
    if len(labels.unique()) == 1:
        return labels.iloc[0]
    if not features:
        return labels.mode()[0]
    
    gains = {f: info_gain(data, f) for f in features}
    best = max(gains, key=gains.get)
    tree = {best: {}}
    
    for val in data[best].unique():
        subset = data[data[best] == val].drop(columns=best)
        if subset.empty:
            tree[best][val] = labels.mode()[0]
        else:
            tree[best][val] = id3(subset.reset_index(drop=True), [f for f in features if f != best])
    
    return tree

data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rain', 'Rain', 'Rain', 'Overcast', 'Sunny', 'Sunny', 'Rain', 'Sunny', 'Overcast', 'Overcast', 'Rain'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Strong'],
    'Play': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})

tree = id3(data, data.columns[:-1].tolist())
from pprint import pprint
pprint(tree)
    </pre>
  </div>

  <script>
    function showTab(tabId) {
      var contents = document.querySelectorAll('.tab-content');
      contents.forEach(c => c.style.display = 'none');
      document.getElementById(tabId).style.display = 'block';
    }
  </script>

</body>
</html>

