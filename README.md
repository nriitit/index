
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
  <button class="tab-button" onclick="showTab('ml8')">ML8</button>

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

# Example usage with Play Tennis dataset
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

  <div id="ml8" class="tab-content">
    <pre>
import numpy as np
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.decomposition import PCA
from sklearn.svm import SVC
from sklearn.model_selection import train_test_split

# Load data and apply PCA
X, y = datasets.load_iris(return_X_y=True)
X_pca = PCA(n_components=2).fit_transform(X)

# Train SVM on PCA-reduced data
X_train, X_test, y_train, y_test = train_test_split(X_pca, y, test_size=0.3, random_state=42)
svm = SVC(kernel='linear').fit(X_train, y_train)

# Plot decision boundary and data points
xx, yy = np.meshgrid(np.linspace(X_pca[:, 0].min() - 1, X_pca[:, 0].max() + 1, 500),
                     np.linspace(X_pca[:, 1].min() - 1, X_pca[:, 1].max() + 1, 500))
Z = svm.predict(np.c_[xx.ravel(), yy.ravel()]).reshape(xx.shape)

plt.figure(figsize=(8, 6))
plt.contourf(xx, yy, Z, alpha=0.3, cmap=plt.cm.coolwarm)
plt.scatter(X_test[:, 0], X_test[:, 1], c=y_test, edgecolors='k', marker='x', cmap=plt.cm.coolwarm)
plt.title('SVM with PCA (Iris Dataset)')
plt.xlabel('PCA Component 1')
plt.ylabel('PCA Component 2')
plt.grid(True)
plt.tight_layout()
plt.show()
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

